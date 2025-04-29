# **Fonction Modifier**

Modifier est un code qui est execute avant et/ou aprés un appelle fonction.

Modifier est utilise pour:

- restriction d'accéss
- valise un entrée
- protection contre l'attaque par reentrance

``` solidity
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.26;

contract FunctionModifier {
    // We will use these variables to demonstrate how to use
    // modifiers.
    address public owner;
    uint256 public x = 10;
    bool public locked;

    constructor() {
        // Set the transaction sender as the owner of the contract.
        owner = msg.sender;
    }

    // Modifier to check that the caller is the owner of
    // the contract.
    modifier onlyOwner() {
        require(msg.sender == owner, "Not owner");
        // Underscore is a special character only used inside
        // a function modifier and it tells Solidity to
        // execute the rest of the code.
        _;
    }

    // Modifiers can take inputs. This modifier checks that the
    // address passed in is not the zero address.
    modifier validAddress(address _addr) {
        require(_addr != address(0), "Not valid address");
        _;
    }

    function changeOwner(address _newOwner)
        public
        onlyOwner
        validAddress(_newOwner)
    {
        owner = _newOwner;
    }

    // Modifiers can be called before and / or after a function.
    // This modifier prevents a function from being called while
    // it is still executing.
    modifier noReentrancy() {
        require(!locked, "No reentrancy");

        locked = true;
        _;
        locked = false;
    }

    function decrement(uint256 i) public noReentrancy {
        x -= i;

        if (i > 1) {
            decrement(i - 1);
        }
    }
}

```

## execute sur remix 

[FunctionModifier.sol](https://remix.ethereum.org/?#code=Ly8gU1BEWC1MaWNlbnNlLUlkZW50aWZpZXI6IE1JVApwcmFnbWEgc29saWRpdHkgXjAuOC4yNjsKCmNvbnRyYWN0IEZ1bmN0aW9uTW9kaWZpZXIgewogICAgLy8gV2Ugd2lsbCB1c2UgdGhlc2UgdmFyaWFibGVzIHRvIGRlbW9uc3RyYXRlIGhvdyB0byB1c2UKICAgIC8vIG1vZGlmaWVycy4KICAgIGFkZHJlc3MgcHVibGljIG93bmVyOwogICAgdWludDI1NiBwdWJsaWMgeCA9IDEwOwogICAgYm9vbCBwdWJsaWMgbG9ja2VkOwoKICAgIGNvbnN0cnVjdG9yKCkgewogICAgICAgIC8vIFNldCB0aGUgdHJhbnNhY3Rpb24gc2VuZGVyIGFzIHRoZSBvd25lciBvZiB0aGUgY29udHJhY3QuCiAgICAgICAgb3duZXIgPSBtc2cuc2VuZGVyOwogICAgfQoKICAgIC8vIE1vZGlmaWVyIHRvIGNoZWNrIHRoYXQgdGhlIGNhbGxlciBpcyB0aGUgb3duZXIgb2YKICAgIC8vIHRoZSBjb250cmFjdC4KICAgIG1vZGlmaWVyIG9ubHlPd25lcigpIHsKICAgICAgICByZXF1aXJlKG1zZy5zZW5kZXIgPT0gb3duZXIsICJOb3Qgb3duZXIiKTsKICAgICAgICAvLyBVbmRlcnNjb3JlIGlzIGEgc3BlY2lhbCBjaGFyYWN0ZXIgb25seSB1c2VkIGluc2lkZQogICAgICAgIC8vIGEgZnVuY3Rpb24gbW9kaWZpZXIgYW5kIGl0IHRlbGxzIFNvbGlkaXR5IHRvCiAgICAgICAgLy8gZXhlY3V0ZSB0aGUgcmVzdCBvZiB0aGUgY29kZS4KICAgICAgICBfOwogICAgfQoKICAgIC8vIE1vZGlmaWVycyBjYW4gdGFrZSBpbnB1dHMuIFRoaXMgbW9kaWZpZXIgY2hlY2tzIHRoYXQgdGhlCiAgICAvLyBhZGRyZXNzIHBhc3NlZCBpbiBpcyBub3QgdGhlIHplcm8gYWRkcmVzcy4KICAgIG1vZGlmaWVyIHZhbGlkQWRkcmVzcyhhZGRyZXNzIF9hZGRyKSB7CiAgICAgICAgcmVxdWlyZShfYWRkciAhPSBhZGRyZXNzKDApLCAiTm90IHZhbGlkIGFkZHJlc3MiKTsKICAgICAgICBfOwogICAgfQoKICAgIGZ1bmN0aW9uIGNoYW5nZU93bmVyKGFkZHJlc3MgX25ld093bmVyKQogICAgICAgIHB1YmxpYwogICAgICAgIG9ubHlPd25lcgogICAgICAgIHZhbGlkQWRkcmVzcyhfbmV3T3duZXIpCiAgICB7CiAgICAgICAgb3duZXIgPSBfbmV3T3duZXI7CiAgICB9CgogICAgLy8gTW9kaWZpZXJzIGNhbiBiZSBjYWxsZWQgYmVmb3JlIGFuZCAvIG9yIGFmdGVyIGEgZnVuY3Rpb24uCiAgICAvLyBUaGlzIG1vZGlmaWVyIHByZXZlbnRzIGEgZnVuY3Rpb24gZnJvbSBiZWluZyBjYWxsZWQgd2hpbGUKICAgIC8vIGl0IGlzIHN0aWxsIGV4ZWN1dGluZy4KICAgIG1vZGlmaWVyIG5vUmVlbnRyYW5jeSgpIHsKICAgICAgICByZXF1aXJlKCFsb2NrZWQsICJObyByZWVudHJhbmN5Iik7CgogICAgICAgIGxvY2tlZCA9IHRydWU7CiAgICAgICAgXzsKICAgICAgICBsb2NrZWQgPSBmYWxzZTsKICAgIH0KCiAgICBmdW5jdGlvbiBkZWNyZW1lbnQodWludDI1NiBpKSBwdWJsaWMgbm9SZWVudHJhbmN5IHsKICAgICAgICB4IC09IGk7CgogICAgICAgIGlmIChpID4gMSkgewogICAgICAgICAgICBkZWNyZW1lbnQoaSAtIDEpOwogICAgICAgIH0KICAgIH0KfQo&lang=fr&optimize=false&runs=200&evmVersion=null&version=soljson-v0.8.26+commit.8a97fa7a.js)