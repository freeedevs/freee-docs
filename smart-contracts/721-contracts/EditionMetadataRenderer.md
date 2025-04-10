---
description: Metadata rendering contract for NFTs with all the same media assets.
---

# Edition Metadata Renderer

This contract is in charge of managing and rendering the metadata for editions. An edition is an NFT collection where all the NFTs share the same media asset (video, image, etc).

Whenever a `tokenURI` is called on the NFT contract, the call is forwarded to this contract to get metadata for a specific NFT.

View the list of deployed contract addresses [here](../contract-addresses/).

## updateMediaURIs

Updates the media asset for the edition.

* `target`: The contract address to update metadata for
* `imageURI`: The new media uri
* `animationURI`: The new animation uri

The `imageURI` is the resource for the main piece of media and `animationURI` is used for the thumbnail if a video.

```sol
function updateMediaURIs(
    address target,
    string memory imageURI,
    string memory animationURI
)
```

## updateDescription

Updates the description for the edition.

* `target`: The contract address to update the description for
* `newDescription`: The new description

```sol
function updateDescription(address target, string memory newDescription)
```
