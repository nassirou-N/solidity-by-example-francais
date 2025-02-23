# **Mapping**

les Maps est un nouvel type qui est créer par le syntaxe suivante $\color{red}{\textsf{mapping(keyType => valueType)}}$.

la clé $\color{red}{\textsf{keyType}}$ est un type de donne comme bytes, int, uint, string,address ou toute contract par son address.

la valeur $\color{red}{\textsf{valueType}}$ toutes les types inclue ou un autre mapping ou tableau.

le mappings ne sont pas iterable.

```solidity
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.26;

contract Mapping {
    // Mapping from address to uint
    mapping(address => uint256) public myMap;

    function get(address _addr) public view returns (uint256) {
        // Mapping always returns a value.
        // If the value was never set, it will return the default value.
        return myMap[_addr];
    }

    function set(address _addr, uint256 _i) public {
        // Update the value at this address
        myMap[_addr] = _i;
    }

    function remove(address _addr) public {
        // Reset the value to the default value.
        delete myMap[_addr];
    }
}

contract NestedMapping {
    // Nested mapping (mapping from address to another mapping)
    mapping(address => mapping(uint256 => bool)) public nested;

    function get(address _addr1, uint256 _i) public view returns (bool) {
        // You can get values from a nested mapping
        // even when it is not initialized
        return nested[_addr1][_i];
    }

    function set(address _addr1, uint256 _i, bool _boo) public {
        nested[_addr1][_i] = _boo;
    }

    function remove(address _addr1, uint256 _i) public {
        delete nested[_addr1][_i];
    }
}
```

## Execute sur Remix

[mapping.sol](https://remix.ethereum.org/?#code=Ly8gU1BEWC1MaWNlbnNlLUlkZW50aWZpZXI6IE1JVApwcmFnbWEgc29saWRpdHkgXjAuOC4yNjsKCmNvbnRyYWN0IE1hcHBpbmcgewogICAgLy8gTWFwcGluZyBmcm9tIGFkZHJlc3MgdG8gdWludAogICAgbWFwcGluZyhhZGRyZXNzID0+IHVpbnQyNTYpIHB1YmxpYyBteU1hcDsKCiAgICBmdW5jdGlvbiBnZXQoYWRkcmVzcyBfYWRkcikgcHVibGljIHZpZXcgcmV0dXJucyAodWludDI1NikgewogICAgICAgIC8vIE1hcHBpbmcgYWx3YXlzIHJldHVybnMgYSB2YWx1ZS4KICAgICAgICAvLyBJZiB0aGUgdmFsdWUgd2FzIG5ldmVyIHNldCwgaXQgd2lsbCByZXR1cm4gdGhlIGRlZmF1bHQgdmFsdWUuCiAgICAgICAgcmV0dXJuIG15TWFwW19hZGRyXTsKICAgIH0KCiAgICBmdW5jdGlvbiBzZXQoYWRkcmVzcyBfYWRkciwgdWludDI1NiBfaSkgcHVibGljIHsKICAgICAgICAvLyBVcGRhdGUgdGhlIHZhbHVlIGF0IHRoaXMgYWRkcmVzcwogICAgICAgIG15TWFwW19hZGRyXSA9IF9pOwogICAgfQoKICAgIGZ1bmN0aW9uIHJlbW92ZShhZGRyZXNzIF9hZGRyKSBwdWJsaWMgewogICAgICAgIC8vIFJlc2V0IHRoZSB2YWx1ZSB0byB0aGUgZGVmYXVsdCB2YWx1ZS4KICAgICAgICBkZWxldGUgbXlNYXBbX2FkZHJdOwogICAgfQp9Cgpjb250cmFjdCBOZXN0ZWRNYXBwaW5nIHsKICAgIC8vIE5lc3RlZCBtYXBwaW5nIChtYXBwaW5nIGZyb20gYWRkcmVzcyB0byBhbm90aGVyIG1hcHBpbmcpCiAgICBtYXBwaW5nKGFkZHJlc3MgPT4gbWFwcGluZyh1aW50MjU2ID0+IGJvb2wpKSBwdWJsaWMgbmVzdGVkOwoKICAgIGZ1bmN0aW9uIGdldChhZGRyZXNzIF9hZGRyMSwgdWludDI1NiBfaSkgcHVibGljIHZpZXcgcmV0dXJucyAoYm9vbCkgewogICAgICAgIC8vIFlvdSBjYW4gZ2V0IHZhbHVlcyBmcm9tIGEgbmVzdGVkIG1hcHBpbmcKICAgICAgICAvLyBldmVuIHdoZW4gaXQgaXMgbm90IGluaXRpYWxpemVkCiAgICAgICAgcmV0dXJuIG5lc3RlZFtfYWRkcjFdW19pXTsKICAgIH0KCiAgICBmdW5jdGlvbiBzZXQoYWRkcmVzcyBfYWRkcjEsIHVpbnQyNTYgX2ksIGJvb2wgX2JvbykgcHVibGljIHsKICAgICAgICBuZXN0ZWRbX2FkZHIxXVtfaV0gPSBfYm9vOwogICAgfQoKICAgIGZ1bmN0aW9uIHJlbW92ZShhZGRyZXNzIF9hZGRyMSwgdWludDI1NiBfaSkgcHVibGljIHsKICAgICAgICBkZWxldGUgbmVzdGVkW19hZGRyMV1bX2ldOwogICAgfQp9Cg&lang=fr&optimize=false&runs=200&evmVersion=null&version=soljson-v0.8.26+commit.8a97fa7a.js)