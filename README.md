
# Dynamic Fee Hook( [Atrium](https://atrium.academy/uniswap-old),  Uniswap Hook Incubator 3)
This repository contains the implementation of the `GasPriceFeeHook` contract, which introduces a dynamic gas price-based fee mechanism for the Uniswap V4 protocol.

## Dynamic Fee Concept
The `GasPriceFeeHook` contract implements a dynamic fee mechanism that adjusts the transaction fee based on the current gas price. The goal is to provide a more flexible and responsive fee structure that adapts to the network's gas price conditions.

## Key features:

 - Moving Average Gas Price: The contract maintains a moving average of the gas price, updated after each swap transaction.

 - Gas Price Tiers: The contract defines three gas price tiers:

    1. If the current gas price is more than 10% above the moving average, the fee is halved.
    2. If the current gas price is more than 10% below the moving average, the fee is doubled.
    3. Otherwise, the default base fee is applied.


 - Fee Overriding: The beforeSwap hook overrides the LP fee for each swap transaction, using the dynamic fee calculated based on the current gas price conditions.

## Installation and Testing
This project uses the Foundry development framework. To set up the project and run the tests, follow these steps:

Install Foundry:

```
curl -L https://foundry.paradigm.xyz | bash
foundryup

```

Clone this repository:

```
git clone https://github.com/ProfSaz/dynamic-fee-hook.git
cd dynamic-fee-hook

```

Install dependencies:

```
forge install
```

Run the tests:

```
forge test

```
The `TestGasPriceFeesHook` contract in the `GasPriceFeeHook.t.sol` file in the test folder contains the test case that verifies the behavior of the `GasPriceFeeHook` contract.

## Test Case
The test case covers the following scenarios:

- Swap at a gas price equal to the moving average: The default base fee is applied.
- Swap at a gas price lower than the moving average: The fee is doubled.
- Swap at a gas price higher than the moving average: The fee is halved.

The test case verifies that the dynamic fee mechanism is working as expected by checking the output amounts of the swap transactions and the updates to the moving average gas price and its count.

## Conclusion
The `GasPriceFeeHook` contract demonstrates a flexible and adaptive fee mechanism for the Uniswap V4 protocol. By dynamically adjusting the fees based on the current gas price conditions, the contract aims to provide a more optimized and consistent user experience across different network states.