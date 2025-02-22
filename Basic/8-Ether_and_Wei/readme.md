# Ether et Wei

les transaction son payes en $\color{red}{\textsf{Ether}}$.

un **Eth** est equal **$\color{red}{\textsf{10e18}}$** 

```solidity
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.26;

contract EtherUnits {
    uint256 public oneWei = 1 wei;
    // 1 wei is equal to 1
    bool public isOneWei = (oneWei == 1);

    uint256 public oneGwei = 1 gwei;
    // 1 gwei is equal to 10^9 wei
    bool public isOneGwei = (oneGwei == 1e9);

    uint256 public oneEther = 1 ether;
    // 1 ether is equal to 10^18 wei
    bool public isOneEther = (oneEther == 1e18);
}

```
## Execute sur Remix

[EtherUints.sol](https://remix.ethereum.org/?#code=Ly8gU1BEWC1MaWNlbnNlLUlkZW50aWZpZXI6IE1JVApwcmFnbWEgc29saWRpdHkgXjAuOC4yNjsKCmNvbnRyYWN0IEV0aGVyVW5pdHMgewogICAgdWludDI1NiBwdWJsaWMgb25lV2VpID0gMSB3ZWk7CiAgICAvLyAxIHdlaSBpcyBlcXVhbCB0byAxCiAgICBib29sIHB1YmxpYyBpc09uZVdlaSA9IChvbmVXZWkgPT0gMSk7CgogICAgdWludDI1NiBwdWJsaWMgb25lR3dlaSA9IDEgZ3dlaTsKICAgIC8vIDEgZ3dlaSBpcyBlcXVhbCB0byAxMF45IHdlaQogICAgYm9vbCBwdWJsaWMgaXNPbmVHd2VpID0gKG9uZUd3ZWkgPT0gMWU5KTsKCiAgICB1aW50MjU2IHB1YmxpYyBvbmVFdGhlciA9IDEgZXRoZXI7CiAgICAvLyAxIGV0aGVyIGlzIGVxdWFsIHRvIDEwXjE4IHdlaQogICAgYm9vbCBwdWJsaWMgaXNPbmVFdGhlciA9IChvbmVFdGhlciA9PSAxZTE4KTsKfQo&lang=fr&optimize=false&runs=200&evmVersion=null&version=soljson-v0.8.26+commit.8a97fa7a.js)