# ServiceToken Smart Contract

## Overview


The `ServiceToken` smart contract is an ERC20 token implementation with additional functionalities that include burning tokens and redeeming them for specific services. The contract utilizes the OpenZeppelin library for secure and standardized token management. This token can be minted by the owner, transferred between addresses, and burned for predefined services such as car rentals, bike rentals, and mobile service subscriptions.

## Features

- **ERC20 Standard Compliance**: Implements the ERC20 standard for fungible tokens.
- **Ownable**: Ensures that only the owner can perform certain actions, such as minting tokens.
- **ERC20Burnable**: Adds functionality to burn tokens, reducing the total supply.
- **Service Redemption**: Allows users to redeem tokens for predefined services at specified rates.
- **Events**: Emits events for significant actions like burning tokens and redeeming services.

## Contract Details

### Enums

- **ServiceType**: An enumeration representing the different types of services available for redemption.
  - `CarRental`
  - `BikeRental`
  - `MobileServiceSubscription`

### Mappings

- **serviceRates**: Maps `ServiceType` to the rate (in tokens) required to redeem that service.
- **serviceProducts**: Maps `ServiceType` to a human-readable product name.

### Variables

- **recentlyRedeemedService**: Stores the last redeemed service type.

### Events

- **LogMessage**: Emits a log message for generic purposes.
- **ServiceRedeemed**: Emits when a service is successfully redeemed, including the player address, the amount of tokens used, and the product name.

## Functions

### Constructor

```solidity
constructor(address initialOwner)
```
Initializes the contract with the owner and sets up the service rates and product names.

### setRatesAndProducts

```solidity
function setRatesAndProducts() internal
```
Sets the rates and product names for each service type. This function is called internally by the constructor.

### mintTokens

```solidity
function mintTokens(address beneficiary, uint256 amount) external onlyOwner
```
Mints new tokens to a specified beneficiary address. Can only be called by the owner.

### burnTokens

```solidity
function burnTokens(uint256 amount) external
```
Burns a specified amount of tokens from the caller's balance.

### transferTokens

```solidity
function transferTokens(address recipient, uint256 amount) external
```
Transfers a specified amount of tokens to a recipient address.

### redeemForService

```solidity
function redeemForService(uint256 tokenAmount) external
```
Redeems tokens for a service. The amount of tokens determines which service is redeemed. If the caller does not have enough tokens, the transaction reverts.

### getRecentlyRedeemedService

```solidity
function getRecentlyRedeemedService() external view returns (string memory)
```
Returns the product name of the most recently redeemed service.

## Deployment

To deploy the `ServiceToken` contract:

1. Install the necessary dependencies:
   ```sh
   npm install @openzeppelin/contracts
   ```

2. Compile the contract:
   ```sh
   npx hardhat compile
   ```

3. Deploy the contract using your preferred method (e.g., Hardhat, Truffle, Remix).

## Usage

After deploying the contract, the owner can mint tokens to users. Users can then transfer tokens, burn them, or redeem them for services based on the predefined rates. Events will be emitted for burning tokens and redeeming services, which can be monitored to track the contract's activity.

## Example

### Minting Tokens

```solidity
serviceToken.mintTokens(beneficiaryAddress, 1000);
```

### Redeeming a Service

```solidity
serviceToken.redeemForService(1000);
```

### Checking the Recently Redeemed Service

```solidity
string memory recentService = serviceToken.getRecentlyRedeemedService();
```

## License

This project is licensed under the MIT License. See the [LICENSE](LICENSE) file for details.
