# Hello World

$\color{red}{\textsf{pragma}}$ spécifie la version de compilation de solidity.

```solidity
// SPDX-License-Identifier: MIT
//la version du compilateur qui est superier ou equal de 0.8.26 a 0.9.0
pragma solidity ^0.8.26;

contract HelloWorld {
    string public hello = "Hello World"; 

}
```



## try on Remix
[HelloWorld.sol](https://remix.ethereum.org/?#code=Ly8gU1BEWC1MaWNlbnNlLUlkZW50aWZpZXI6IE1JVAovLyBjb21waWxlciB2ZXJzaW9uIG11c3QgYmUgZ3JlYXRlciB0aGFuIG9yIGVxdWFsIHRvIDAuOC4yNiBhbmQgbGVzcyB0aGFuIDAuOS4wCnByYWdtYSBzb2xpZGl0eSBeMC44LjI2OwoKY29udHJhY3QgSGVsbG9Xb3JsZCB7CiAgICBzdHJpbmcgcHVibGljIGdyZWV0ID0gIkhlbGxvIFdvcmxkISI7Cn0K&lang=fr&optimize=false&runs=200&evmVersion=null&version=soljson-v0.8.26+commit.8a97fa7a.js)