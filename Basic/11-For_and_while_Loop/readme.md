# **les boucles pour et tantque**

solidity support les boucles pout ($\color{red}{\textsf{for}}$), tantque ($\color{red}{\textsf{while}}$) et faire... jusqu'a ($\color{red}{\textsf{do while}}$).

**attention** ne faites pas des boucles infinie car elle peux consomme plus de gas prevue ce qui peux annule la transaction.

ce pourquoi les boucle $\color{red}{\textsf{do while}}$ et ($\color{red}{\textsf{while}}$) ne sont pas trés utilises.

```solidity
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.26;

contract Loop {
    function loop() public pure {
        // for loop
        for (uint256 i = 0; i < 10; i++) {
            if (i == 3) {
                // Skip to next iteration with continue
                continue;
            }
            if (i == 5) {
                // Exit loop with break
                break;
            }
        }

        // while loop
        uint256 j;
        while (j < 10) {
            j++;
        }
    }
}
```
## Execute sur Remix

[loop.sol](https://remix.ethereum.org/?#code=Ly8gU1BEWC1MaWNlbnNlLUlkZW50aWZpZXI6IE1JVApwcmFnbWEgc29saWRpdHkgXjAuOC4yNjsKCmNvbnRyYWN0IExvb3AgewogICAgZnVuY3Rpb24gbG9vcCgpIHB1YmxpYyBwdXJlIHsKICAgICAgICAvLyBmb3IgbG9vcAogICAgICAgIGZvciAodWludDI1NiBpID0gMDsgaSA8IDEwOyBpKyspIHsKICAgICAgICAgICAgaWYgKGkgPT0gMykgewogICAgICAgICAgICAgICAgLy8gU2tpcCB0byBuZXh0IGl0ZXJhdGlvbiB3aXRoIGNvbnRpbnVlCiAgICAgICAgICAgICAgICBjb250aW51ZTsKICAgICAgICAgICAgfQogICAgICAgICAgICBpZiAoaSA9PSA1KSB7CiAgICAgICAgICAgICAgICAvLyBFeGl0IGxvb3Agd2l0aCBicmVhawogICAgICAgICAgICAgICAgYnJlYWs7CiAgICAgICAgICAgIH0KICAgICAgICB9CgogICAgICAgIC8vIHdoaWxlIGxvb3AKICAgICAgICB1aW50MjU2IGo7CiAgICAgICAgd2hpbGUgKGogPCAxMCkgewogICAgICAgICAgICBqKys7CiAgICAgICAgfQogICAgfQp9Cg&lang=fr&optimize=false&runs=200&evmVersion=null&version=soljson-v0.8.26+commit.8a97fa7a.js)