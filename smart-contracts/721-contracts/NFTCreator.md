---
description: A factory that deploys new NFT contracts.
---

# NFT Creator Factory

The factory references an `implementation` contract and clones it to give it it's own unique address.

## Edition&#x20;

This contract can be used to create  `Editions`&#x20;

* `Editions`: All the NFTs share the same media asset.

Platforms have the ability to earn some of the protocol rewards for helping creators deploy their smart contracts.

## Global Variables

* `implementation`: An NFT contract used for cloning.
* `editionMetadataRenderer`: A contract for rendering editions metadata.

## Creating an NFT Contract

### createEdition

Creates a new edition contract with an address. Note, not all of these fields can be changed after creating the contract.

* `name`: Name of the edition contract (cannot be changed)
* `symbol`: Symbol of the edition contract (cannot be changed)
* `defaultAdmin`: Default admin address (contract sets the owner to this address by default)
* `editionSize`: Total size of the edition (number of possible editions)
* `royaltyBPS`: BPS amount of royalty (cannot be changed)
* `fundsRecipient`: Recipient for sales and royalties
* `description`: Metadata: Description of the edition entry
* `animationURI`: Metadata: Animation url (optional) of the edition entry
* `imageURI`: Metadata: Image url (semi-required) of the edition entry

```sol
function createEdition(
    string memory name,
    string memory symbol,
    uint64 editionSize,
    uint16 royaltyBPS,
    address payable fundsRecipient,
    address defaultAdmin,
    IERC721Drop.SalesConfiguration memory saleConfig,
    string memory description,
    string memory animationURI,
    string memory imageURI,
    address createReferral
) 
```
