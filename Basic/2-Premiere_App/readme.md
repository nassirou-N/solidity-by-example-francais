# Premier Application

c'est juste un simple contract qui increment et decremante un compter enregistre par la variable

```solidity
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.26;

contract Counter {
    uint256 public count;

//fonction pour voir le count actuelle
    function get() public view returns(uint256){
        return count;
    }

    // fuonction qui incremente le count avec 1
    function inc() public {
        count += 1;
    }
     // fuonction qui decremente le count avec 1
    function dec() public {
        count -= 1;
    }
}
```
## execute sur Remix


[premierApp.sol](https://remix.ethereum.org/?#code=Ly8gU1BEWC1MaWNlbnNlLUlkZW50aWZpZXI6IE1JVApwcmFnbWEgc29saWRpdHkgXjAuOC4yNjsKCmNvbnRyYWN0IENvdW50ZXIgewogICAgdWludDI1NiBwdWJsaWMgY291bnQ7CgogICAgLy8gRnVuY3Rpb24gdG8gZ2V0IHRoZSBjdXJyZW50IGNvdW50CiAgICBmdW5jdGlvbiBnZXQoKSBwdWJsaWMgdmlldyByZXR1cm5zICh1aW50MjU2KSB7CiAgICAgICAgcmV0dXJuIGNvdW50OwogICAgfQoKICAgIC8vIEZ1bmN0aW9uIHRvIGluY3JlbWVudCBjb3VudCBieSAxCiAgICBmdW5jdGlvbiBpbmMoKSBwdWJsaWMgewogICAgICAgIGNvdW50ICs9IDE7CiAgICB9CgogICAgLy8gRnVuY3Rpb24gdG8gZGVjcmVtZW50IGNvdW50IGJ5IDEKICAgIGZ1bmN0aW9uIGRlYygpIHB1YmxpYyB7CiAgICAgICAgLy8gVGhpcyBmdW5jdGlvbiB3aWxsIGZhaWwgaWYgY291bnQgPSAwCiAgICAgICAgY291bnQgLT0gMTsKICAgIH0KfQo&lang=fr&optimize=false&runs=200&evmVersion=null&version=soljson-v0.8.26+commit.8a97fa7a.js)