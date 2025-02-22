# **Immutable**

immutable est comme une constante mais a la seul difference qu'elle est initialise dans le constructeur du contract mais ne peut plus être modiffier aprés. elle est identifier par le mot **immutable** avant le nom du variable et aussi la convention demande de mette **i_**

```solidity
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.26;

contract Immutable {
    address public immutable myAddr;
    uint256 public immutable myUint;

    constructor(uint256 _myUint) {
        myAddr = msg.sender;
        myUint = _myUint;
    }
}

```

## execute sur Remix

[immutable.sol](https://remix.ethereum.org/?#code=Ly8gU1BEWC1MaWNlbnNlLUlkZW50aWZpZXI6IE1JVApwcmFnbWEgc29saWRpdHkgXjAuOC4yNjsKCmNvbnRyYWN0IEltbXV0YWJsZSB7CiAgICBhZGRyZXNzIHB1YmxpYyBpbW11dGFibGUgbXlBZGRyOwogICAgdWludDI1NiBwdWJsaWMgaW1tdXRhYmxlIG15VWludDsKCiAgICBjb25zdHJ1Y3Rvcih1aW50MjU2IF9teVVpbnQpIHsKICAgICAgICBteUFkZHIgPSBtc2cuc2VuZGVyOwogICAgICAgIG15VWludCA9IF9teVVpbnQ7CiAgICB9Cn0K&lang=fr&optimize=false&runs=200&evmVersion=null&version=soljson-v0.8.26+commit.8a97fa7a.js)