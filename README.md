# Token Vesting

All the contracts are taken in full from [OpenZeppelin v2.0.0](https://github.com/OpenZeppelin/openzeppelin-contracts/releases/tag/v2.0.0) implementation.

[Official PaymentSplitter](https://github.com/OpenZeppelin/openzeppelin-contracts/blob/06e265b38d3e9daeaa7b33f9035c700d6bc0c6a0/contracts/payment/PaymentSplitter.sol) has been modified in a following way:
- enable ERC20 support (original version splits native ETH)
- remove private modifiers on state vars (lowers gas fees)
- change functions visibility from public to external (lowers gas fees)
- remove fallback function

The diff can be found [here](https://www.diffchecker.com/8kDjpV0P).

## Process

For each group of investors:

1. deploy `PaymentSplitter` and initialize with list of investors and their respective shares
2. deploy `TokenVesting` and set the previously deployed splitter as beneficiary
3. transfer total amount of tokens belonging to all the investors directly to the vesting contract
4. call `release()` repeatedly - on both vesting and splitter contracts