---
description: The NFT contracts created from the `NFTCreator` are known as an `ERC721Drop`.
---

# ERC721Drop

Each drop contract is cloned from an `implementation` address and receives its own address. 

Both `Editions` and `Drops` use the same base contract but have different metadata rendering contracts.

View the list of deployed contract addresses [here](../contract-addresses.md).

- `Edition`: A collection where all the NFTs share the same media asset.
- `Drop`: A collection where all the NFTs have individual pieces of media.

## Sales Configuration

The sales configuration is set when the contract is created.
The config holds the internal settings for all the minting/sales parameters.

*Times are Unix Timestamps
- `publicSaleStart`: Start time for public minting
- `publicSaleEnd`: End time for public minting
- `presaleStart`: Start time for private minting
- `presaleEnd`: End time for private minting
- `publicSalePrice`: Price in the ETH required to mint an NFT
- `maxSalePurchasePerAddress`: Max amount of NFTs an address can mint (only for public minting)
- `presaleMerkleRoot`: A cryptographic proof that is used for presale minting (allow list)

Note that `presaleMerkleRoot` can be set to `0x0000000000000000000000000000000000000000000000000000000000000000` if there are no plans for allow list minting.

Current values can be viewed by calling `salesConfig` on the contract and it can be updated by calling `setSalesConfig` with the new parameters.

Learn more about creating an allow list [here.](./ERC721Drop#creating-a-presale-allowlist)
```
function setSaleConfiguration(
    uint104 publicSalePrice,
    uint32 maxSalePurchasePerAddress,
    uint64 publicSaleStart,
    uint64 publicSaleEnd,
    uint64 presaleStart,
    uint64 presaleEnd,
    bytes32 presaleMerkleRoot
) 
```

## Collection Size

#### Fixed Size
A fixed-size collection is where there is a max number of NFTs that are allowed to be minted from the contract.
The max size is set when creating the contract and specifying the `editionSize`.

#### Open Edition
An open edition collection has no max amount but instead has a certain time window where minting is open. 
However, once the period is over then no one can publicly mint anymore.

Note, `finalizeOpenEdition` **must be called by an admin** once the minting window has closed to make sure that it's not possible to mint any more NFTs from the contract.

```
function finalizeOpenEdition()
```

## Minting Functions

#### adminMint
An admin can mint a certain number of the NFTs to an address without having to pay the base price or protocol rewards.

```
function adminMint(address recipient, uint256 quantity)
```

#### adminMintAirdrop 
An admin can mint a single NFT to multiple different addresses in a single transaction without having to pay the base price.
The function takes in an array of addresses to mint to.

```
function adminMintAirdrop(address[] calldata recipients)
```

#### mint
A public minting function that can be called by anyone once the public sale has started. 

```
function mint(
    address recipient, 
    uint256 quantity, 
    string calldata comment
)
```

#### purchasePresale

A private sale function for allowlist minting that requires a merkle proof.
Check out the section [here](./ERC721Drop#creating-a-presale-allow-list) for creating an allowlist.  

```
function purchasePresale(
    uint256 quantity,
    uint256 maxQuantity,
    uint256 pricePerToken,
    bytes32[] calldata merkleProof,
    string memory comment
)
```

## Collection Roles

#### Owner

The owner doesn't have access to any write functions on the contract. They are only able to set royalty and contract configurations on third-party applications that expect an owner. 

The owner address is set to the same address as the default admin argument when the contract was created but can be updated to any address by a default admin.

#### Default Admin
This admin has the most control and is set when the contract is first initialized.

It is recommended to set the deployer address to the default admin when first creating the NFT contract.

There can also be more than one default admin and can be updated to a new address.

Capabilities include: 

- Assign and revoke admin roles
- Call `adminMint`and `adminMintAirdrop` mint functions
- Change the owner Address
- Update the `salesConfig`
- Call `finalizeOpenEdition`

`bytes32 role = 0x0000000000000000000000000000000000000000000000000000000000000000`

#### Minter Role

A restricted admin that is only able to access special minting functions such as `adminMint` and `adminMintAirdrop`.

`bytes32 role = MINTER_ROLE`


#### Sales Manager Role

A restricted admin that is only able to update the `salesConfig` and call the `withdraw` function.

`bytes32 role = SALES_MANAGER_ROLE`


## Assigning and Revoking Roles

Note, admin roles can only be assigned and revoked by default admins. 

#### Checking Admin Status

`isAdmin` function checks if an address is an admin or not. 

```
function isAdmin(address user)
```

`hasRole` is more granular and checks if an address has a specific admin role.
```
function hasRole(bytes32 role, address account)
```

#### Granting a Role

`grantRole` allows for a default admin to add an admin. 
```
function grantRole(bytes32 role, address account)
```

#### Revoking a Role

`revokeRole` allows for a default admin to remove an admin. 
```
function revokeRole(bytes32 role, address account)
```

#### Changing the Owner

`setOwner` sets the owner of the contract to a new address.
```
function setOwner(address newOwner)
```

## Withdrawing Funds
Once minting has concluded, the funds can be moved out of the contract by calling the `withdraw` function.
Withdraw can be called by a default admin, the `fundsRecipient` address, a sales manager role.
```
function withdraw()
```

This will push the funds to the `fundsRecipient` address, which is set to the default admin when the contract was initialized.
However, it can be updated to any address by calling the `setFundsRecipient` function.

```
function setFundsRecipient(address payable newRecipientAddress)
```

## Creating a Presale AllowList

A Merkle root allows a large data set to be condensed and expressed in a small piece of data.

The Merkle root is used to store a list of valid preSale minting addresses, without needing to store the whole list directly in the contract.

It is possible to upload an allowlist using the manage interface on the create website.

## Updating Contract Info on OpenSea

Once the contract is deployed, the address that is set as the owner will need to log in to OpenSea to access and update the contract information. 

## Upgrading the Contract

Once deployed it is possible to upgrade the NFT contract to have new functionality.

All upgrades are opt-in and can only be initiated by a default admin.

`upgradeTo` allows the NFT contract to upgrade to a new implementation contract to make delegate calls.

```
function upgradeTo(address newImplementation)
```

Similar to `upgradeTo`, `upgradeToAndCall` allows a new implementation contract to be specified, but it also allows for call data to be passed in when updating. 

```
function upgradeToAndCall(address newImplementation, bytes data)
```