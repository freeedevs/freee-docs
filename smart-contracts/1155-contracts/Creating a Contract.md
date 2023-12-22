---
description: All 1155 contracts created from Freee are deployed by calling a central factory contract.
---

# Creating a Contract

When calling this factory it will deploy a minimal proxy contract that is upgradeable.
All upgrades are opt-in and must be done manually on a per contract basis by the user.

View the list of deployed contract addresses [here](../contract-addresses.md).

## Calling the Factory Contract

The `createContract` function on the factory is responsible for deploying a new 1155 contract. 

The `setupActions` parameter allows for multiple actions to be called when deploying the contract.

Such as creating a token and sale in the same transaction as deploying the contract.

- `contractURI`: The URI for the contract metadata
- `name`: The name of the contract
- `defaultRoyaltyConfiguration`: The default royalty configuration for the contract
- `defaultAdmin`: The default admin for the contract
- `setupActions`: The actions to perform on the new contract upon initialization (optional)
  
```sol
function createContract(
    string calldata newContractURI,
    string calldata name,
    ICreatorRoyaltiesControl.RoyaltyConfiguration memory defaultRoyaltyConfiguration,
    address payable defaultAdmin,
    bytes[] calldata setupActions
) external returns (address)
```


>The contract supports multicall so multiple functions can be called to set up the contract in a single transaction.

## Royalty Configuration

The `defaultRoyaltyConfiguration` sets contract-wide royalties. 

Note, that royalties can also be set at the token level.

The parameter can be passed in with the following details: 

- `royaltyMintSchedule`: 1/N tokens are minted to the royalty recipient
- `royaltyBPS`: The royalty amount in basis points for secondary sales.
- `royaltyRecipient`: The address that will receive the royalty payments.

```sol
struct RoyaltyConfiguration {
    uint32 royaltyMintSchedule;
    uint32 royaltyBPS;
    address royaltyRecipient;
}
```

## Contract URI 
The Contract URI contains contract specific details. This metadata is stored in a JSON file on IPFS. 

The uri is retrieved via the `contractURI()` call on the contract.

```sol
type CollectionMetadata = {
  name?: string
  description?: string
  image?: string
  imageURI?: string
  animation_url?: string
  animationURI?: string
  seller_fee_basis_points?: string
  seller_fee_recipient?: string
  storefront?: {
    theme?: StorefrontTheme
  }
}
```

## Setup Actions

An optional param that is encoded function data that can be passed in and can call a separate function within the contract.
This allows creating a token and setting permissions in the same transaction of creating the contract. Actions that can be called:
- Creating a token
- Setting the salesConfig
- Granting permissions/minter role
- Admin minting tokens