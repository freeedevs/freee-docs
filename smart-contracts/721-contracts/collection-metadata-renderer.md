---
description: >-
  Metadata rendering contract for NFTs with individual media assets
  (Collection).
---

# Collection Metadata Renderer

This contract is in charge of managing and rendering the metadata for collection on Freee.

A collection NFTs have unique individual media assets.

Whenever a `tokenURI` is called on an NFT contract it is forwarded to this contract to get metadata for a specific NFT.

View the list of deployed contract addresses [here](../contract-addresses/).

* `baseURI`: A common base path that all the assets share and can append the tokenId to the end to get the metadata for an NFT.
* `contractURI`: A resource for getting metadata for the contract. Follows the contract-level metadata format described [here](https://docs.opensea.io/docs/contract-level-metadata).
* `provenanceHash`: A hash that is used to prove that the order of the images and metadata was set pre-mint, and was not manipulated.
* `target`: The address of the NFT contract to get data for.

## updateMetadataBase

Updates the baseURI and contractURI.

```sol
function updateMetadataBase(
    address target,
    string memory baseUri,
    string memory newContractUri
)
```

## updateMetadataBaseWithDetails

Updates the metadata base URI, extension, contract URI and freezing details.

```sol
function updateMetadataBaseWithDetails(
    address target,
    string memory metadataBase,
    string memory metadataExtension,
    string memory newContractURI,
    uint256 freezeAt
)
```

## updateProvenanceHash

Updates the provenance hash stored in the contract.

```sol
function updateProvenanceHash(address target, bytes32 provenanceHash)
```
