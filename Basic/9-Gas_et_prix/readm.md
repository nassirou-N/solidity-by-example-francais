# **Gas**

**combien d'ether payez-vous pour cet transaction?** t-elle est la question a chaque fois

vous paye le gas en ether qui est convertie en wei et le prix de gas d'un transaction est equal: $\color{red}{\textsf{GAS = gas spent * gas price }}$

- $\color{red}{\textsf{gas}}$ est l'unit de computation
- $\color{red}{\textsf{gas spent}}$ est la total des gas utilise pour effectue cet transaction
- $\color{red}{\textsf{gas price}}$ le prix de gas par unit

le transaction avec les frais de gas éleves sont prioritaire

```solidity
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.26;

contract Gas {
    uint256 public i = 0;

    // Using up all of the gas that you send causes your transaction to fail.
    // State changes are undone.
    // Gas spent is not refunded.
    function forever() public {
        // Here we run a loop until all of the gas are spent
        // and the transaction fails
        while (true) {
            i += 1;
        }
    }
}

```
## Excute sur Remix

[gas.sol](https://remix.ethereum.org/?#code=Ly8gU1BEWC1MaWNlbnNlLUlkZW50aWZpZXI6IE1JVApwcmFnbWEgc29saWRpdHkgXjAuOC4yNjsKCmNvbnRyYWN0IEdhcyB7CiAgICB1aW50MjU2IHB1YmxpYyBpID0gMDsKCiAgICAvLyBVc2luZyB1cCBhbGwgb2YgdGhlIGdhcyB0aGF0IHlvdSBzZW5kIGNhdXNlcyB5b3VyIHRyYW5zYWN0aW9uIHRvIGZhaWwuCiAgICAvLyBTdGF0ZSBjaGFuZ2VzIGFyZSB1bmRvbmUuCiAgICAvLyBHYXMgc3BlbnQgaXMgbm90IHJlZnVuZGVkLgogICAgZnVuY3Rpb24gZm9yZXZlcigpIHB1YmxpYyB7CiAgICAgICAgLy8gSGVyZSB3ZSBydW4gYSBsb29wIHVudGlsIGFsbCBvZiB0aGUgZ2FzIGFyZSBzcGVudAogICAgICAgIC8vIGFuZCB0aGUgdHJhbnNhY3Rpb24gZmFpbHMKICAgICAgICB3aGlsZSAodHJ1ZSkgewogICAgICAgICAgICBpICs9IDE7CiAgICAgICAgfQogICAgfQp9Cg&lang=fr&optimize=false&runs=200&evmVersion=null&version=soljson-v0.8.26+commit.8a97fa7a.js)