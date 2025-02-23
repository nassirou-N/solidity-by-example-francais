# **Location des données: Storage, Memory et Calldata**

le variable déclare en local on different allocation soit: $\color{red}{\textsf{storage}}$ , $\color{red}{\textsf{memory}}$, ou $\color{red}{\textsf{calldata}}$

- $\color{red}{\textsf{storage}}$ toute changement des données sont sauvegarde directement dans la blockchain  
- $\color{red}{\textsf{memory}}$ les données sont temporaire et existe uniqument lors de l'execution de la fonction
- $\color{red}{\textsf{calldata}}$ specifique au argument d'une fonction.

```solidity
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.26;

contract DataLocations {
    uint256[] public arr;
    mapping(uint256 => address) map;

    struct MyStruct {
        uint256 foo;
    }

    mapping(uint256 => MyStruct) myStructs;

    function f() public {
        // call _f with state variables
        _f(arr, map, myStructs[1]);

        // get a struct from a mapping
        MyStruct storage myStruct = myStructs[1];
        // create a struct in memory
        MyStruct memory myMemStruct = MyStruct(0);
    }

    function _f(
        uint256[] storage _arr,
        mapping(uint256 => address) storage _map,
        MyStruct storage _myStruct
    ) internal {
        // do something with storage variables
    }

    // You can return memory variables
    function g(uint256[] memory _arr) public returns (uint256[] memory) {
        // do something with memory array
    }

    function h(uint256[] calldata _arr) external {
        // do something with calldata array
    }
}
```

## Execute sur Remix

[dataLocation.sol](https://remix.ethereum.org/?#code=Ly8gU1BEWC1MaWNlbnNlLUlkZW50aWZpZXI6IE1JVApwcmFnbWEgc29saWRpdHkgXjAuOC4yNjsKCmNvbnRyYWN0IERhdGFMb2NhdGlvbnMgewogICAgdWludDI1NltdIHB1YmxpYyBhcnI7CiAgICBtYXBwaW5nKHVpbnQyNTYgPT4gYWRkcmVzcykgbWFwOwoKICAgIHN0cnVjdCBNeVN0cnVjdCB7CiAgICAgICAgdWludDI1NiBmb287CiAgICB9CgogICAgbWFwcGluZyh1aW50MjU2ID0+IE15U3RydWN0KSBteVN0cnVjdHM7CgogICAgZnVuY3Rpb24gZigpIHB1YmxpYyB7CiAgICAgICAgLy8gY2FsbCBfZiB3aXRoIHN0YXRlIHZhcmlhYmxlcwogICAgICAgIF9mKGFyciwgbWFwLCBteVN0cnVjdHNbMV0pOwoKICAgICAgICAvLyBnZXQgYSBzdHJ1Y3QgZnJvbSBhIG1hcHBpbmcKICAgICAgICBNeVN0cnVjdCBzdG9yYWdlIG15U3RydWN0ID0gbXlTdHJ1Y3RzWzFdOwogICAgICAgIC8vIGNyZWF0ZSBhIHN0cnVjdCBpbiBtZW1vcnkKICAgICAgICBNeVN0cnVjdCBtZW1vcnkgbXlNZW1TdHJ1Y3QgPSBNeVN0cnVjdCgwKTsKICAgIH0KCiAgICBmdW5jdGlvbiBfZigKICAgICAgICB1aW50MjU2W10gc3RvcmFnZSBfYXJyLAogICAgICAgIG1hcHBpbmcodWludDI1NiA9PiBhZGRyZXNzKSBzdG9yYWdlIF9tYXAsCiAgICAgICAgTXlTdHJ1Y3Qgc3RvcmFnZSBfbXlTdHJ1Y3QKICAgICkgaW50ZXJuYWwgewogICAgICAgIC8vIGRvIHNvbWV0aGluZyB3aXRoIHN0b3JhZ2UgdmFyaWFibGVzCiAgICB9CgogICAgLy8gWW91IGNhbiByZXR1cm4gbWVtb3J5IHZhcmlhYmxlcwogICAgZnVuY3Rpb24gZyh1aW50MjU2W10gbWVtb3J5IF9hcnIpIHB1YmxpYyByZXR1cm5zICh1aW50MjU2W10gbWVtb3J5KSB7CiAgICAgICAgLy8gZG8gc29tZXRoaW5nIHdpdGggbWVtb3J5IGFycmF5CiAgICB9CgogICAgZnVuY3Rpb24gaCh1aW50MjU2W10gY2FsbGRhdGEgX2FycikgZXh0ZXJuYWwgewogICAgICAgIC8vIGRvIHNvbWV0aGluZyB3aXRoIGNhbGxkYXRhIGFycmF5CiAgICB9Cn0K&lang=fr&optimize=false&runs=200&evmVersion=null&version=soljson-v0.8.26+commit.8a97fa7a.js)
    