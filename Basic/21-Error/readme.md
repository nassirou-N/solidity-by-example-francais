## **Error**

Une erreur annulera toutes les modifications apportées à l'état au cours d'une transaction.

on gere les erreurs avec  $\color{red}{\textsf{require}}$,  $\color{red}{\textsf{revert}}$, ou  $\color{red}{\textsf{assert}}$.

-  $\color{red}{\textsf{require}}$ utilise pour valide les entres et condition avant l'execution
- $\color{red}{\textsf{revert}}$ est simulaire a $\color{red}{\textsf{require}}$ regarde le code ci-dessous pour plus de detaille.
- $\color{red}{\textsf{assert}}$ est utilisé pour verifie un code qui ne seras jamais faux.

**use custom error to save gas.** avec  $\color{red}{\textsf{error}}$ **Nom_erreur()**

```solidity
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.26;

contract Error {
    function testRequire(uint256 _i) public pure {
        // Require should be used to validate conditions such as:
        // - inputs
        // - conditions before execution
        // - return values from calls to other functions
        require(_i > 10, "Input must be greater than 10");
    }

    function testRevert(uint256 _i) public pure {
        // Revert is useful when the condition to check is complex.
        // This code does the exact same thing as the example above
        if (_i <= 10) {
            revert("Input must be greater than 10");
        }
    }

    uint256 public num;

    function testAssert() public view {
        // Assert should only be used to test for internal errors,
        // and to check invariants.

        // Here we assert that num is always equal to 0
        // since it is impossible to update the value of num
        assert(num == 0);
    }

    // custom error
    error InsufficientBalance(uint256 balance, uint256 withdrawAmount);

    function testCustomError(uint256 _withdrawAmount) public view {
        uint256 bal = address(this).balance;
        if (bal < _withdrawAmount) {
            revert InsufficientBalance({
                balance: bal,
                withdrawAmount: _withdrawAmount
            });
        }
    }
}

```
un autre exemple pour plus d'explication

```solidity
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.26;

contract Account {
    uint256 public balance;
    uint256 public constant MAX_UINT = 2 ** 256 - 1;

    function deposit(uint256 _amount) public {
        uint256 oldBalance = balance;
        uint256 newBalance = balance + _amount;

        // balance + _amount does not overflow if balance + _amount >= balance
        require(newBalance >= oldBalance, "Overflow");

        balance = newBalance;

        assert(balance >= oldBalance);
    }

    function withdraw(uint256 _amount) public {
        uint256 oldBalance = balance;

        // balance - _amount does not underflow if balance >= _amount
        require(balance >= _amount, "Underflow");

        if (balance < _amount) {
            revert("Underflow");
        }

        balance -= _amount;

        assert(balance <= oldBalance);
    }
}

```

## Execute sur Remix

[Account.sol](https://remix.ethereum.org/?#code=Ly8gU1BEWC1MaWNlbnNlLUlkZW50aWZpZXI6IE1JVApwcmFnbWEgc29saWRpdHkgXjAuOC4yNjsKCmNvbnRyYWN0IEFjY291bnQgewogICAgdWludDI1NiBwdWJsaWMgYmFsYW5jZTsKICAgIHVpbnQyNTYgcHVibGljIGNvbnN0YW50IE1BWF9VSU5UID0gMiAqKiAyNTYgLSAxOwoKICAgIGZ1bmN0aW9uIGRlcG9zaXQodWludDI1NiBfYW1vdW50KSBwdWJsaWMgewogICAgICAgIHVpbnQyNTYgb2xkQmFsYW5jZSA9IGJhbGFuY2U7CiAgICAgICAgdWludDI1NiBuZXdCYWxhbmNlID0gYmFsYW5jZSArIF9hbW91bnQ7CgogICAgICAgIC8vIGJhbGFuY2UgKyBfYW1vdW50IGRvZXMgbm90IG92ZXJmbG93IGlmIGJhbGFuY2UgKyBfYW1vdW50ID49IGJhbGFuY2UKICAgICAgICByZXF1aXJlKG5ld0JhbGFuY2UgPj0gb2xkQmFsYW5jZSwgIk92ZXJmbG93Iik7CgogICAgICAgIGJhbGFuY2UgPSBuZXdCYWxhbmNlOwoKICAgICAgICBhc3NlcnQoYmFsYW5jZSA+PSBvbGRCYWxhbmNlKTsKICAgIH0KCiAgICBmdW5jdGlvbiB3aXRoZHJhdyh1aW50MjU2IF9hbW91bnQpIHB1YmxpYyB7CiAgICAgICAgdWludDI1NiBvbGRCYWxhbmNlID0gYmFsYW5jZTsKCiAgICAgICAgLy8gYmFsYW5jZSAtIF9hbW91bnQgZG9lcyBub3QgdW5kZXJmbG93IGlmIGJhbGFuY2UgPj0gX2Ftb3VudAogICAgICAgIHJlcXVpcmUoYmFsYW5jZSA+PSBfYW1vdW50LCAiVW5kZXJmbG93Iik7CgogICAgICAgIGlmIChiYWxhbmNlIDwgX2Ftb3VudCkgewogICAgICAgICAgICByZXZlcnQoIlVuZGVyZmxvdyIpOwogICAgICAgIH0KCiAgICAgICAgYmFsYW5jZSAtPSBfYW1vdW50OwoKICAgICAgICBhc3NlcnQoYmFsYW5jZSA8PSBvbGRCYWxhbmNlKTsKICAgIH0KfQo&lang=fr&optimize=false&runs=200&evmVersion=null&version=soljson-v0.8.26+commit.8a97fa7a.js)



