# Minting Tokens

## Mint Fee

Freee charges a small fee for minting an NFT.

There is no charge to the creator, all the funds from the sales go to the creator.

Lastly, the mint fee doesn't apply to admin minted NFT (airdropping).

The best way to find the mint fee for a specific contract is to retrieve it from the contract by calling the `mintFee` function. You can read more about the mint fee [here](<../../FREEE Mint & Collect Fees.md>).

## Mint Function

Purchase tokens given a minter contract and minter arguments

* `minter`: The minter contract to use
* `tokenId`: The token ID to purchase
* `quantity`: The quantity of tokens to purchase
* `minterArguments`: The arguments to pass to the minter (detail in the minters section)

\*The minter arguments are different for each minter contract and are listed in the section.

```solidity
function mintWithRewards(
    IMinter1155 minter,
    uint256 tokenId,
    uint256 quantity,
    bytes calldata minterArguments,
    address mintReferral
) external payable nonReentrant 
```

## Minter Strategy Contracts

The minting logic for 1155's lives outside of the main 1155 contract.

It lives in separate contracts called minters.

To mint a token the `mint` function is called on the main 1155 contract and then minter checks if the user should be able to mint.

Then the minter tells the main 1155 contract if it should mint or not.

View the list of deployed contract addresses [here](../contract-addresses/).

\*Note, that the minter arguments are type `bytes`

### Fixed Price Strategy

Mint NFTs for a specific ETH price.

`ETH transaction value = ((price + mint fee) * amount)`

`minterArguments`: User address to mint to, in bytes

\*Note, the payment amount of ETH must be set an override if using wagmi or ethers.js.

#### Getting the Mint Price

Calling the `sale` function on the fixed-price minter will return the price for a specific token. `function sale(address tokenContract, uint256 tokenId)`

### Merkle Proof Strategy

Mints tokens based on a merkle tree.

`ETH transaction value = ((price + mint fee) * amount)`

`minterArguments`: Address to mint to, Max quantity, Price per token, Merkle proof

## Admin Minting

Admins can mint NFTs to addresses. These NFTs **do not** incur the mint fee.

```sol
function adminMint(
    address recipient, 
    uint256 tokenId, 
    uint256 quantity, 
    bytes memory data
) external onlyAdminOrRole(tokenId, PERMISSION_BIT_MINTER)
```

```sol
function adminMintBatch(
    address recipient, 
    uint256[] memory tokenIds, 
    uint256[] memory quantities, 
    bytes memory data
) public nonReentrant
```
