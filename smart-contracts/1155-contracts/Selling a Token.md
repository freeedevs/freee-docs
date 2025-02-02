# Selling a Token

Once a token has been created, it can then be put up for sale.

Minter strategy contracts are separate contracts that hold minting logic, but the main 1155 is called for minting.

Check out the \[minting]\(./Minting Tokens.md) section to learn more about minters.

View the list of deployed contract addresses [here](../contract-addresses/).

To create a sale you must use the `callSale` function on the 1155 contract.

This will set the sale in the appropriate minter.

```sol
function callSale(
    uint256 tokenId,
    IMinter1155 salesConfig, // Minter Strategy Contract
    bytes memory data
) 
```

The data that is passed into the minter is used to call the `setSale` function.

Each minter has a unique salesConfig.

```sol
function setSale(uint256 tokenId, SalesConfig memory salesConfig) 
```

### Fixed Price Sale

Calling `callSale` on an 1155 contract will create a sale for an NFT, but the `FIXED_PRICE_SALE_STRATEGY` address must be specified.

The `salesConfig` for a fixed price is structured as follows:

```sol
struct SalesConfig {
    uint64 saleStart; 
    uint64 saleEnd; 
    uint64 maxTokensPerAddress; 
    uint96 pricePerToken; // Price in Wei
    address fundsRecipient; // Where to send the funds
}
```

### Merkle Sale

Create a allow list sale with a Merkle proof.

Note, the price and the max mint amount per address are specified when creating the Merkle tree.

The Merkle sales config is as follows:

```sol
struct MerkleSaleSettings {
    uint64 presaleStart;
    uint64 presaleEnd;
    address fundsRecipient;
    bytes32 merkleRoot;
}
```

## Royalty

Royalties are set on the main 1155 contract.

* `royaltyBPS`: The royalty amount in basis points for secondary sales.
* `royaltyRecipient`: The address that will receive the royalty payments.

```sol
struct RoyaltyConfiguration {
    uint32 royaltyMintSchedule;
    uint32 royaltyBPS;
    address royaltyRecipient;
}
```

This can be set at both the contract and token level.

```sol
function updateRoyaltiesForToken(
    uint256 tokenId, 
    RoyaltyConfiguration memory newConfiguration
)
```

## Withdrawing Funds

Admin can withdraw all funds to the `msg.sender`.

```sol
function withdrawAll() public onlyAdminOrRole(CONTRACT_BASE_ID, PERMISSION_BIT_FUNDS_MANAGER)
```

Admin can withdraw a certain amount to a specific address.

```sol
function withdrawCustom(
    address recipient, 
    uint256 amounts
) public onlyAdminOrRole(CONTRACT_BASE_ID, PERMISSION_BIT_FUNDS_MANAGER)
```
