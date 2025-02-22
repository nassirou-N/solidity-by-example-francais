# **Ercrire et Lire des variables sur solidity**

écrire ou modifie la valeur d'un variable consiste a faire une transaction qui consomme des gas

lire la valeur d'un variable ne consomme pas de gas

```solidity
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.26;

contract SimpleStorage {
    // State variable to store a number
    uint256 public num;

    // You need to send a transaction to write to a state variable.
    function set(uint256 _num) public {
        num = _num;
    }

    // You can read from a state variable without sending a transaction.
    function get() public view returns (uint256) {
        return num;
    }
}

```
## Execute sur Remix

[simpleStorage.sol](https://remix.ethereum.org/?#code=Ly8gU1BEWC1MaWNlbnNlLUlkZW50aWZpZXI6IE1JVApwcmFnbWEgc29saWRpdHkgXjAuOC4yNjsKCmNvbnRyYWN0IFNpbXBsZVN0b3JhZ2UgewogICAgLy8gU3RhdGUgdmFyaWFibGUgdG8gc3RvcmUgYSBudW1iZXIKICAgIHVpbnQyNTYgcHVibGljIG51bTsKCiAgICAvLyBZb3UgbmVlZCB0byBzZW5kIGEgdHJhbnNhY3Rpb24gdG8gd3JpdGUgdG8gYSBzdGF0ZSB2YXJpYWJsZS4KICAgIGZ1bmN0aW9uIHNldCh1aW50MjU2IF9udW0pIHB1YmxpYyB7CiAgICAgICAgbnVtID0gX251bTsKICAgIH0KCiAgICAvLyBZb3UgY2FuIHJlYWQgZnJvbSBhIHN0YXRlIHZhcmlhYmxlIHdpdGhvdXQgc2VuZGluZyBhIHRyYW5zYWN0aW9uLgogICAgZnVuY3Rpb24gZ2V0KCkgcHVibGljIHZpZXcgcmV0dXJucyAodWludDI1NikgewogICAgICAgIHJldHVybiBudW07CiAgICB9Cn0K&lang=fr&optimize=false&runs=200&evmVersion=null&version=soljson-v0.8.26+commit.8a97fa7a.js)
