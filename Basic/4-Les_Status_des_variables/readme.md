# Variable

on a 3 types the variable en solidity

- **local**
    -  déclare dans une fonction
    - elle n'est pas enregistre dans la blockchain
- **state**
    - déclare hors de la fonction
    - enregistre dans la blockchain
- **global**
    - des information provenant de la blockchain
    - elle permanente dans la blockchain

```solidity
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.26;

contract Variables {
    // State variables est enregistre dans la blockchain
    string public text = "Hello";
    uint256 public num = 123;

    function doSomething() public view {
        // Local variables n'est pas enregistre dans la blockchain
        uint256 i = 456;

        // Here are some global variables
        uint256 timestamp = block.timestamp; // Current block timestamp
        address sender = msg.sender; // address of the caller
    }
}
```
## execute sur Remix

[Variable](https://remix.ethereum.org/?#code=Ly8gU1BEWC1MaWNlbnNlLUlkZW50aWZpZXI6IE1JVApwcmFnbWEgc29saWRpdHkgXjAuOC4yNjsKCmNvbnRyYWN0IFZhcmlhYmxlcyB7CiAgICAvLyBTdGF0ZSB2YXJpYWJsZXMgYXJlIHN0b3JlZCBvbiB0aGUgYmxvY2tjaGFpbi4KICAgIHN0cmluZyBwdWJsaWMgdGV4dCA9ICJIZWxsbyI7CiAgICB1aW50MjU2IHB1YmxpYyBudW0gPSAxMjM7CgogICAgZnVuY3Rpb24gZG9Tb21ldGhpbmcoKSBwdWJsaWMgdmlldyB7CiAgICAgICAgLy8gTG9jYWwgdmFyaWFibGVzIGFyZSBub3Qgc2F2ZWQgdG8gdGhlIGJsb2NrY2hhaW4uCiAgICAgICAgdWludDI1NiBpID0gNDU2OwoKICAgICAgICAvLyBIZXJlIGFyZSBzb21lIGdsb2JhbCB2YXJpYWJsZXMKICAgICAgICB1aW50MjU2IHRpbWVzdGFtcCA9IGJsb2NrLnRpbWVzdGFtcDsgLy8gQ3VycmVudCBibG9jayB0aW1lc3RhbXAKICAgICAgICBhZGRyZXNzIHNlbmRlciA9IG1zZy5zZW5kZXI7IC8vIGFkZHJlc3Mgb2YgdGhlIGNhbGxlcgogICAgfQp9Cg&lang=fr&optimize=false&runs=200&evmVersion=null&version=soljson-v0.8.26+commit.8a97fa7a.js)
