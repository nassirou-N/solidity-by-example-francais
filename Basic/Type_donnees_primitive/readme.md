# Les Types des données primitives

nous vous introduises les types de données primitives en solidity

- $\color{red}{\textsf{boolean}}$
- $\color{red}{\textsf{uint256}}$ avec different format uint4 uint8, uint16, jusqu'a uint256 
- $\color{red}{\textsf{int256}}$ même chose format que les uint
- $\color{red}{\textsf{address}}$
- $\color{red}{\textsf{string}}$

- $\color{red}{\textsf{bytes}}$ les bytes son en paire aussi mais elle s'arrête sur les bytes32



```solidity
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.26;

contract Primitives {
    bool public boo = true;

    /*
    uint stands for unsigned integer, meaning non negative integers
    different sizes are available
        uint8   ranges from 0 to 2 ** 8 - 1
        uint16  ranges from 0 to 2 ** 16 - 1
        ...
        uint256 ranges from 0 to 2 ** 256 - 1
    */
    uint8 public u8 = 1;
    uint256 public u256 = 456;
    uint256 public u = 123; // uint is an alias for uint256

    /*
    Negative numbers are allowed for int types.
    Like uint, different ranges are available from int8 to int256
    
    int256 ranges from -2 ** 255 to 2 ** 255 - 1
    int128 ranges from -2 ** 127 to 2 ** 127 - 1
    */
    int8 public i8 = -1;
    int256 public i256 = 456;
    int256 public i = -123; // int is same as int256

    // minimum and maximum of int
    int256 public minInt = type(int256).min;
    int256 public maxInt = type(int256).max;

    address public addr = 0xCA35b7d915458EF540aDe6068dFe2F44E8fa733c;

    /*
    In Solidity, the data type byte represent a sequence of bytes. 
    Solidity presents two types of bytes :

     - fixed-sized byte arrays
     - dynamically-sized byte arrays.
     
     The term bytes in Solidity represents a dynamic array of bytes. 
     It’s a shorthand for byte[] .
    */
    bytes1 a = 0xb5; //  [10110101]
    bytes1 b = 0x56; //  [01010110]
// the string 
    string public hello = "hello world"

    // Default values
    // Unassigned variables have a default value

    bool public defaultBoo; // false
    uint256 public defaultUint; // 0
    int256 public defaultInt; // 0
    address public defaultAddr; // 0x0000000000000000000000000000000000000000
}


```

[premierApp.sol](https://remix.ethereum.org/?#code=Ly8gU1BEWC1MaWNlbnNlLUlkZW50aWZpZXI6IE1JVApwcmFnbWEgc29saWRpdHkgXjAuOC4yNjsKCmNvbnRyYWN0IFByaW1pdGl2ZXMgewogICAgYm9vbCBwdWJsaWMgYm9vID0gdHJ1ZTsKCiAgICAvKgogICAgdWludCBzdGFuZHMgZm9yIHVuc2lnbmVkIGludGVnZXIsIG1lYW5pbmcgbm9uIG5lZ2F0aXZlIGludGVnZXJzCiAgICBkaWZmZXJlbnQgc2l6ZXMgYXJlIGF2YWlsYWJsZQogICAgICAgIHVpbnQ4ICAgcmFuZ2VzIGZyb20gMCB0byAyICoqIDggLSAxCiAgICAgICAgdWludDE2ICByYW5nZXMgZnJvbSAwIHRvIDIgKiogMTYgLSAxCiAgICAgICAgLi4uCiAgICAgICAgdWludDI1NiByYW5nZXMgZnJvbSAwIHRvIDIgKiogMjU2IC0gMQogICAgKi8KICAgIHVpbnQ4IHB1YmxpYyB1OCA9IDE7CiAgICB1aW50MjU2IHB1YmxpYyB1MjU2ID0gNDU2OwogICAgdWludDI1NiBwdWJsaWMgdSA9IDEyMzsgLy8gdWludCBpcyBhbiBhbGlhcyBmb3IgdWludDI1NgoKICAgIC8qCiAgICBOZWdhdGl2ZSBudW1iZXJzIGFyZSBhbGxvd2VkIGZvciBpbnQgdHlwZXMuCiAgICBMaWtlIHVpbnQsIGRpZmZlcmVudCByYW5nZXMgYXJlIGF2YWlsYWJsZSBmcm9tIGludDggdG8gaW50MjU2CiAgICAKICAgIGludDI1NiByYW5nZXMgZnJvbSAtMiAqKiAyNTUgdG8gMiAqKiAyNTUgLSAxCiAgICBpbnQxMjggcmFuZ2VzIGZyb20gLTIgKiogMTI3IHRvIDIgKiogMTI3IC0gMQogICAgKi8KICAgIGludDggcHVibGljIGk4ID0gLTE7CiAgICBpbnQyNTYgcHVibGljIGkyNTYgPSA0NTY7CiAgICBpbnQyNTYgcHVibGljIGkgPSAtMTIzOyAvLyBpbnQgaXMgc2FtZSBhcyBpbnQyNTYKCiAgICAvLyBtaW5pbXVtIGFuZCBtYXhpbXVtIG9mIGludAogICAgaW50MjU2IHB1YmxpYyBtaW5JbnQgPSB0eXBlKGludDI1NikubWluOwogICAgaW50MjU2IHB1YmxpYyBtYXhJbnQgPSB0eXBlKGludDI1NikubWF4OwoKICAgIGFkZHJlc3MgcHVibGljIGFkZHIgPSAweENBMzViN2Q5MTU0NThFRjU0MGFEZTYwNjhkRmUyRjQ0RThmYTczM2M7CgogICAgLyoKICAgIEluIFNvbGlkaXR5LCB0aGUgZGF0YSB0eXBlIGJ5dGUgcmVwcmVzZW50IGEgc2VxdWVuY2Ugb2YgYnl0ZXMuIAogICAgU29saWRpdHkgcHJlc2VudHMgdHdvIHR5cGVzIG9mIGJ5dGVzIDoKCiAgICAgLSBmaXhlZC1zaXplZCBieXRlIGFycmF5cwogICAgIC0gZHluYW1pY2FsbHktc2l6ZWQgYnl0ZSBhcnJheXMuCiAgICAgCiAgICAgVGhlIHRlcm0gYnl0ZXMgaW4gU29saWRpdHkgcmVwcmVzZW50cyBhIGR5bmFtaWMgYXJyYXkgb2YgYnl0ZXMuIAogICAgIEl04oCZcyBhIHNob3J0aGFuZCBmb3IgYnl0ZVtdIC4KICAgICovCiAgICBieXRlczEgYSA9IDB4YjU7IC8vICBbMTAxMTAxMDFdCiAgICBieXRlczEgYiA9IDB4NTY7IC8vICBbMDEwMTAxMTBdCgogICAgLy8gRGVmYXVsdCB2YWx1ZXMKICAgIC8vIFVuYXNzaWduZWQgdmFyaWFibGVzIGhhdmUgYSBkZWZhdWx0IHZhbHVlCiAgICBib29sIHB1YmxpYyBkZWZhdWx0Qm9vOyAvLyBmYWxzZQogICAgdWludDI1NiBwdWJsaWMgZGVmYXVsdFVpbnQ7IC8vIDAKICAgIGludDI1NiBwdWJsaWMgZGVmYXVsdEludDsgLy8gMAogICAgYWRkcmVzcyBwdWJsaWMgZGVmYXVsdEFkZHI7IC8vIDB4MDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMAp9Cg&lang=fr&optimize=false&runs=200&evmVersion=null&version=soljson-v0.8.26+commit.8a97fa7a.js)

