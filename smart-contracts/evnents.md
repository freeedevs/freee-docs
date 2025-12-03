---
description: Events for Indexing and Integration Overview
---

# Smart Contracts Event-based Overview

## 1155 Contracts

### Creating a New Token

When a user creates a new token, the parameters expected are maxSupply and URI. maxSupply is the immutable maximum number of NFTs that can be made for this token and the URI is possible to change but the initial URL representing the token.

Now that we have both gasless and on-chain minting the token creation event arguments are slightly different to determine the originating user of the mint.

Creating new tokens can happen with a call to `setupNewToken()`.

Be aware that often creating a new token and minting often occur in the _same_ transaction.

It is also possible to setup a new token without a mint event.

Any time a new token is setup this event is emitted, however, the sender field is not the actual creator and is the premint executor contract in a gasless setting.

```sol
emit UpdatedToken(address sender, uint256 tokenId, TokenData {
    string uri,
    uint256 maxSupply,
})
```

The standard 1155 `URI` event is also emitted when the token is setup when provided with:

```sol
event URI(string uri, uint256 tokenId)
// Emitted in Creator1155Impl:306
```

### Setting a Price

#### Events Emitted:

Minting a token can occur via different `SalesConfiguration` contracts which are given `Minter` roles on the 1155 contracts to setup a mint.

Sales configurations are linked to contracts via `Permissions` with the `Minter` role.

You can determine which contract is a sales configuration contract by their `contractName`.

The most common `SalesConfiguration` is a `FixedPriceSaleStrategy`. The `factory` contracts include getters for `fixedPriceMinter` and `merkleMinter` which are the two sales methods but users can add their own as well.

We index known sales configuration contracts for `SaleSet` events.

```sol
event SaleSet(address indexed mediaContract, uint256 indexed tokenId, SalesConfig {
    /// @notice Unix timestamp for the sale start
    uint64 saleStart;
    /// @notice Unix timestamp for the sale end
    uint64 saleEnd;
    /// @notice Max tokens that can be minted for an address, 0 if unlimited
    uint64 maxTokensPerAddress;
    /// @notice Price per token in eth wei
    uint96 pricePerToken;
    /// @notice Funds recipient (0 if no different funds recipient than the contract global)
    address fundsRecipient;
} salesConfig);
```

#### How to call:

These settings are set via the `callSale` argument which sets the caller context for security purposes to be the calling contract and does the required permissions checks:

```sol
function callSale(uint256 tokenId, IMinter1155 minterModule, bytes calldata data);
```

For example, you would setup a fixed price nft sale in solidity for token id `1` using:

```sol
Free1155(nftContract).callSale(1, FIXED_PRICE_SALE_STRATEGY, abi.encodeWithSelector(FixedPriceSaleStrategy.setSale(1, SalesConfig({
    saleStart: 0,
    saleEnd: 1735711271, // new years 2025
    maxTokensPerAddress: 0, // unlimited
    pricePerToken: 0 ether,
    fundsRecipient: address(0) // set to contract
}))));
```

Note that the `FIXED_PRICE_SALE_STRATEGY` would need to have `Minter` permissions either on the whole contract (token id `0`) or on the individual token (token id `1`).

### Purchasing / Collecting a Token

#### Mint Events Emitted:

When a user purchases a token the primary event emitted is the `Purchased` event:

```sol
event Purchased(address sender, address minterModule, uint256 tokenId, uint256 quantity, uint256 amount);
```

The amount includes both the price and the mint fee.

The other events emitted on a purchase are the standard 1155 transfer events:

```sol
event TransferSingle(address indexed operator, address indexed from, address indexed to, uint256 id, uint256 value)
```

If the user wishes to include a `MintComment`, an MintComment event is emitted in the same transaction from the `FixedPriceSaleStrategy`.

```sol
event MintComment(address indexed sender, address indexed tokenContract, uint256 indexed tokenId, uint256 quantity, string comment);
```

#### Calling the Mint Function:

Purchasing a token should be called via:

```sol
function mint(
    IMinter1155 minter,
    uint256 tokenId,
    uint256 quantity,
    bytes calldata minterArguments
)
```

* The first argument is the minter module which can be found via looking at permissions or the subgraph.
* The second argument is the desired `tokenId` and the `quantity`.
* Sales information can be found by querying the subgraph or the fixed price minter's `function sale(address tokenContract, uint256 tokenId) returns (SalesConfig memory)`.
* MinterArguments for fixed price minter are `abi.encode(address (tokenMintRecipient))`, and `abi.encode(address (tokenMintRecipient), string (mintComment))` if you wish to add a MintComment.

### Mint Comments

Mint comments are optional strings emitted on the `FixedPriceSaleStrategy`.

```sol
event MintComment(address indexed sender, address indexed tokenContract, uint256 indexed tokenId, uint256 quantity, string comment);
```

### Permissions

When permissions are changed the `UpdatedPermissions` event is emitted.

```sol
event UpdatedPermissions(uint256 indexed tokenId, address indexed user, uint256 indexed permissions);
```

Global permissions are assigned to token id 0, and individual token permissions are assigned to the token. By default, the user that creates a token is given admin permissions on that token.

| Permission    | Bits | Numeric | Description                                                         |
| ------------- | ---- | ------- | ------------------------------------------------------------------- |
| Admin         | 2^1  | 2       | Allows for all functionality and for managing permissions           |
| Minter        | 2^2  | 4       | Allows to mint existing tokens                                      |
| Sales         | 2^3  | 8       | Allows for updating pricing and sales information                   |
| Metadata      | 2^4  | 16      | Allows for updating token metadata and information                  |
| Funds Manager | 2^5  | 32      | Allows for withdrawing funds and setting the funds withdraw address |

Permissions can be added via `addPermission(uint256 tokenId, address user, uint256 permissions)` and removed via `function removePermission(uint256 tokenId, address user, uint256 permissionBits)`.

## 721 Events

### Creating a new Token

721 Contracts share both metadata as either a series of metadata or shared edition metadata.

They also have the same sales settings across the contract unlike 1155 tokens.

New tokens are created by calling the NFTCreatorV1 proxy contract.

Once the contract is created, if the sale is active users can purchase tokens.

We also support a `multicall` pattern with the `setupCalls` argument where the factory is granted temporary admin permissions to execute multiple commands on the contract after deployment allowing for setting additional settings or minting upon deployment.

#### Creating an Edition:

```sol
function createEdition(
    string memory name,
    string memory symbol,
    address defaultAdmin,
    uint64 editionSize,
    uint16 royaltyBPS,
    address payable fundsRecipient,
    bytes[] memory setupCalls,
    IMetadataRenderer metadataRenderer,
    bytes memory metadataInitializer
)
```

**Setting a Price**

Event emitted with Sales Configuration Setup:

```sol
event SalesConfigChanged(address indexed changedBy);
```

After this event is emitted, the contract sales information can be queried and stored.

**Collecting a Token**

First, sales information can be retrieved by calling `salesConfig()` on the 721 contract which returns all of the presale (allowlist), and public sale (standard purchase) configuration.

After this call, the `function mint(address recipient, uint256 quantity, string calldata comment)` function can be called.

The mint fee can be queried from `feeForAmount(uint256 amount) returns (address, uint256 fee)` which returns the total mint fee for a given amount.

The value sent is `pricePerToken * numberOfTokens + mintFee`.
