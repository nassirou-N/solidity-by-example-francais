# **If / Else**

solidity support les condition $\color{red}{\textsf{if}}$,$\color{red}{\textsf{else if}}$ and $\color{red}{\textsf{else}}$.

```solidity
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.26;

contract IfElse {
    function foo(uint256 x) public pure returns (uint256) {
        if (x < 10) {
            return 0;
        } else if (x < 20) {
            return 1;
        } else {
            return 2;
        }
    }

    function ternary(uint256 _x) public pure returns (uint256) {
        // if (_x < 10) {
        //     return 1;
        // }
        // return 2;

        // shorthand way to write if / else statement
        // the "?" operator is called the ternary operator
        return _x < 10 ? 1 : 2;
    }
}

```
## Execute sur Remix

[ifElse.sol](https://remix.ethereum.org/?#code=Ly8gU1BEWC1MaWNlbnNlLUlkZW50aWZpZXI6IE1JVApwcmFnbWEgc29saWRpdHkgXjAuOC4yNjsKCmNvbnRyYWN0IElmRWxzZSB7CiAgICBmdW5jdGlvbiBmb28odWludDI1NiB4KSBwdWJsaWMgcHVyZSByZXR1cm5zICh1aW50MjU2KSB7CiAgICAgICAgaWYgKHggPCAxMCkgewogICAgICAgICAgICByZXR1cm4gMDsKICAgICAgICB9IGVsc2UgaWYgKHggPCAyMCkgewogICAgICAgICAgICByZXR1cm4gMTsKICAgICAgICB9IGVsc2UgewogICAgICAgICAgICByZXR1cm4gMjsKICAgICAgICB9CiAgICB9CgogICAgZnVuY3Rpb24gdGVybmFyeSh1aW50MjU2IF94KSBwdWJsaWMgcHVyZSByZXR1cm5zICh1aW50MjU2KSB7CiAgICAgICAgLy8gaWYgKF94IDwgMTApIHsKICAgICAgICAvLyAgICAgcmV0dXJuIDE7CiAgICAgICAgLy8gfQogICAgICAgIC8vIHJldHVybiAyOwoKICAgICAgICAvLyBzaG9ydGhhbmQgd2F5IHRvIHdyaXRlIGlmIC8gZWxzZSBzdGF0ZW1lbnQKICAgICAgICAvLyB0aGUgIj8iIG9wZXJhdG9yIGlzIGNhbGxlZCB0aGUgdGVybmFyeSBvcGVyYXRvcgogICAgICAgIHJldHVybiBfeCA8IDEwID8gMSA6IDI7CiAgICB9Cn0K&lang=fr&optimize=false&runs=200&evmVersion=null&version=soljson-v0.8.26+commit.8a97fa7a.js)