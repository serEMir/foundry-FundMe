# FundMe

FundMe is a decentralized crowdfunding smart contract built on Ethereum. It allows users to fund the contract with ETH and enables the contract owner to withdraw the funds. The project uses Chainlink's price feeds to ensure that the minimum funding amount is met in USD.

## Features

- **Funding**: Users can fund the contract with ETH.
- **Minimum USD Requirement**: Ensures that the funding amount meets a minimum value in USD using Chainlink price feeds.
- **Owner-Only Withdrawals**: Only the contract owner can withdraw the funds.
- **Cheaper Withdrawals**: Optimized withdrawal function to save gas costs.
- **Fallback and Receive Functions**: Handles direct ETH transfers to the contract.

## Prerequisites

- [Foundry](https://github.com/foundry-rs/foundry) installed
- An Ethereum wallet with test ETH (e.g., MetaMask)
- Access to an Ethereum testnet (e.g., Sepolia)

## Installation

1. Clone the repository:
```bash
git clone https://github.com/serEmir/foundry-Fundme.git
cd foundry-Fundme
```

2. Configure environment variables: Create a `.env` file and add the following:
   ```bash
   SEPOLIA_RPC_URL=<your-sepolia-rpc-url>
   ETHERSCAN_API_KEY=<your-ethers-api-key>
   ```

## Usage

**Encrypt a Private Key in a keystore**

To encrypt a private key in a keystore so you don't have your private key in plain sight, use:
```bash
cast wallet import <your-account-name> --interactive
```
follow the prompt and provide your private key and a password

**Deploy the Contract**

To deploy the `FundMe` contract, run:
```bash
forge script script/DeployFundMe.s.sol:DeployFundMe --rpc-url <RPC_URL> --account <YOUR_ACCOUNT> --broadcast
```

**Fund the Contract**

To fund the contract, use the `Interactions.s.sol` script:
```bash
forge script script/Interactions.s.sol:FundFundMe --sender <YOUR_ADDRESS> --rpc-url <RPC_URL> --account <YOUR_ACCOUNT> --broadcast
```

**Withdraw Funds**

To withdraw funds as the owner, use:
```bash
forge script script/Interactions.s.sol:WithdrawFundMe --sender <OWNER_ADDRESS> --rpc-url <RPC_URL> --account <YOUR_ACCOUNT> --broadcast
```

## Testing

Run the tests using Foundry:
```bash
forge test -vvv
```

## Gas Optimization

The `cheaperWithdraw` function is optimized for gas efficiency by reducing redundant storage reads. Use this function for withdrawals when gas costs are a concern.

## Key Contracts and Libraries

- `FundMe`: The main contract for funding and withdrawing.
- `PriceConverter`: A library for converting ETH to USD using Chainlink price feeds.
- `MockV3Aggregator`: A mock contract for testing price feeds.

## CI/CD

The project uses GitHub Actions for continuous integration. The workflow is defined in `.github/workflows/test.yml`. It runs the following steps:

1. Code formatting check (`forge fmt --check`)
2. Build the project (`forge build`)
3. Run tests (`forge test`)

## License

This project is licensed under the MIT License.

## Acknowledgments

- [Chainlink](https://chain.link/) for providing decentralized price feeds.
- [Foundry](https://github.com/foundry-rs/foundry) for the development framework.
- [Cyfrin](https://github.com/Cyfrin) for the Foundry DevOps tools.

**Contributions are welcome! Please open an issue or submit a pull request for any improvements or bug fixes.**