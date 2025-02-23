# **View et Pure Fonction**

les etats $\color{red}{\textsf{view}}$ et $\color{red}{\textsf{pure}}$ en solidity ne comsomme pas de gas

- $\color{red}{\textsf{view}}$ fonction ne change pas l'etat de la blockchain elle permet de voir les données
- $\color{red}{\textsf{pure}}$ fonction ne change pas aussi l'etat de la blockchain, en plus elle peut charge un donnée.

```solidity
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.26;

contract ViewAndPure {
    uint256 public x = 1;

    // Promise not to modify the state.
    function addToX(uint256 y) public view returns (uint256) {
        return x + y;
    }

    // Promise not to modify or read from the state.
    function add(uint256 i, uint256 j) public pure returns (uint256) {
        return i + j;
    }
}
```

## Execute sur Remix

[view_et_pure.sol](https://remix.ethereum.org/?#code=Ly8gU1BEWC1MaWNlbnNlLUlkZW50aWZpZXI6IE1JVApwcmFnbWEgc29saWRpdHkgXjAuOC4yNjsKCmNvbnRyYWN0IFZpZXdBbmRQdXJlIHsKICAgIHVpbnQyNTYgcHVibGljIHggPSAxOwoKICAgIC8vIFByb21pc2Ugbm90IHRvIG1vZGlmeSB0aGUgc3RhdGUuCiAgICBmdW5jdGlvbiBhZGRUb1godWludDI1NiB5KSBwdWJsaWMgdmlldyByZXR1cm5zICh1aW50MjU2KSB7CiAgICAgICAgcmV0dXJuIHggKyB5OwogICAgfQoKICAgIC8vIFByb21pc2Ugbm90IHRvIG1vZGlmeSBvciByZWFkIGZyb20gdGhlIHN0YXRlLgogICAgZnVuY3Rpb24gYWRkKHVpbnQyNTYgaSwgdWludDI1NiBqKSBwdWJsaWMgcHVyZSByZXR1cm5zICh1aW50MjU2KSB7CiAgICAgICAgcmV0dXJuIGkgKyBqOwogICAgfQp9Cg&lang=fr&optimize=false&runs=200&evmVersion=null&version=soljson-v0.8.26+commit.8a97fa7a.js)
    