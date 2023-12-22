
# Creating a Token

Calling `setupNewTokenWithCreateReferral` on a deployed 1155 contract will create a new token.

View the list of deployed contract addresses [here](../contract-addresses.md).

All tokens start at tokenId 1 and increment up. 

tokenId 0 is reserved for the contract information.

`maxSupply` should be set to `MAX_INT` for an open edition.

```sol
function setupNewToken(
    string calldata newURI,
    uint256 maxSupply,
) public onlyAdminOrRole(CONTRACT_BASE_ID, PERMISSION_BIT_MINTER) nonReentrant returns (uint256)
```

## Updating Metadata

`updateTokenURI` updates the token URI for a token. 

Won't work for tokenId 0 since that is reserved for the contract level information.

```sol
function updateTokenURI(
    uint256 tokenId, 
    string memory _newURI
)
```

Updates the contract metadata.

```sol
function updateContractMetadata(
    string memory _newURI, 
    string memory _newName
)
```

