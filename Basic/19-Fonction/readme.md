# **Les Fonctions**

```solidity
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.26;

contract Function {
    // Functions can return multiple values.
    function returnMany() public pure returns (uint256, bool, uint256) {
        return (1, true, 2);
    }

    // Return values can be named.
    function named() public pure returns (uint256 x, bool b, uint256 y) {
        return (1, true, 2);
    }

    // Return values can be assigned to their name.
    // In this case the return statement can be omitted.
    function assigned() public pure returns (uint256 x, bool b, uint256 y) {
        x = 1;
        b = true;
        y = 2;
    }

    // Use destructuring assignment when calling another
    // function that returns multiple values.
    function destructuringAssignments()
        public
        pure
        returns (uint256, bool, uint256, uint256, uint256)
    {
        (uint256 i, bool b, uint256 j) = returnMany();

        // Values can be left out.
        (uint256 x,, uint256 y) = (4, 5, 6);

        return (i, b, j, x, y);
    }

    // Cannot use map for either input or output

    // Can use array for input
    function arrayInput(uint256[] memory _arr) public {}

    // Can use array for output
    uint256[] public arr;

    function arrayOutput() public view returns (uint256[] memory) {
        return arr;
    }
}

// Call function with key-value inputs
contract XYZ {
    function someFuncWithManyInputs(
        uint256 x,
        uint256 y,
        uint256 z,
        address a,
        bool b,
        string memory c
    ) public pure returns (uint256) {}

    function callFunc() external pure returns (uint256) {
        return someFuncWithManyInputs(1, 2, 3, address(0), true, "c");
    }

    function callFuncWithKeyValue() external pure returns (uint256) {
        return someFuncWithManyInputs({
            a: address(0),
            b: true,
            c: "c",
            x: 1,
            y: 2,
            z: 3
        });
    }
}
```

## Execute sur Remix

[fonction.sol](https://remix.ethereum.org/?#code=Ly8gU1BEWC1MaWNlbnNlLUlkZW50aWZpZXI6IE1JVApwcmFnbWEgc29saWRpdHkgXjAuOC4yNjsKCmNvbnRyYWN0IEZ1bmN0aW9uIHsKICAgIC8vIEZ1bmN0aW9ucyBjYW4gcmV0dXJuIG11bHRpcGxlIHZhbHVlcy4KICAgIGZ1bmN0aW9uIHJldHVybk1hbnkoKSBwdWJsaWMgcHVyZSByZXR1cm5zICh1aW50MjU2LCBib29sLCB1aW50MjU2KSB7CiAgICAgICAgcmV0dXJuICgxLCB0cnVlLCAyKTsKICAgIH0KCiAgICAvLyBSZXR1cm4gdmFsdWVzIGNhbiBiZSBuYW1lZC4KICAgIGZ1bmN0aW9uIG5hbWVkKCkgcHVibGljIHB1cmUgcmV0dXJucyAodWludDI1NiB4LCBib29sIGIsIHVpbnQyNTYgeSkgewogICAgICAgIHJldHVybiAoMSwgdHJ1ZSwgMik7CiAgICB9CgogICAgLy8gUmV0dXJuIHZhbHVlcyBjYW4gYmUgYXNzaWduZWQgdG8gdGhlaXIgbmFtZS4KICAgIC8vIEluIHRoaXMgY2FzZSB0aGUgcmV0dXJuIHN0YXRlbWVudCBjYW4gYmUgb21pdHRlZC4KICAgIGZ1bmN0aW9uIGFzc2lnbmVkKCkgcHVibGljIHB1cmUgcmV0dXJucyAodWludDI1NiB4LCBib29sIGIsIHVpbnQyNTYgeSkgewogICAgICAgIHggPSAxOwogICAgICAgIGIgPSB0cnVlOwogICAgICAgIHkgPSAyOwogICAgfQoKICAgIC8vIFVzZSBkZXN0cnVjdHVyaW5nIGFzc2lnbm1lbnQgd2hlbiBjYWxsaW5nIGFub3RoZXIKICAgIC8vIGZ1bmN0aW9uIHRoYXQgcmV0dXJucyBtdWx0aXBsZSB2YWx1ZXMuCiAgICBmdW5jdGlvbiBkZXN0cnVjdHVyaW5nQXNzaWdubWVudHMoKQogICAgICAgIHB1YmxpYwogICAgICAgIHB1cmUKICAgICAgICByZXR1cm5zICh1aW50MjU2LCBib29sLCB1aW50MjU2LCB1aW50MjU2LCB1aW50MjU2KQogICAgewogICAgICAgICh1aW50MjU2IGksIGJvb2wgYiwgdWludDI1NiBqKSA9IHJldHVybk1hbnkoKTsKCiAgICAgICAgLy8gVmFsdWVzIGNhbiBiZSBsZWZ0IG91dC4KICAgICAgICAodWludDI1NiB4LCwgdWludDI1NiB5KSA9ICg0LCA1LCA2KTsKCiAgICAgICAgcmV0dXJuIChpLCBiLCBqLCB4LCB5KTsKICAgIH0KCiAgICAvLyBDYW5ub3QgdXNlIG1hcCBmb3IgZWl0aGVyIGlucHV0IG9yIG91dHB1dAoKICAgIC8vIENhbiB1c2UgYXJyYXkgZm9yIGlucHV0CiAgICBmdW5jdGlvbiBhcnJheUlucHV0KHVpbnQyNTZbXSBtZW1vcnkgX2FycikgcHVibGljIHt9CgogICAgLy8gQ2FuIHVzZSBhcnJheSBmb3Igb3V0cHV0CiAgICB1aW50MjU2W10gcHVibGljIGFycjsKCiAgICBmdW5jdGlvbiBhcnJheU91dHB1dCgpIHB1YmxpYyB2aWV3IHJldHVybnMgKHVpbnQyNTZbXSBtZW1vcnkpIHsKICAgICAgICByZXR1cm4gYXJyOwogICAgfQp9CgovLyBDYWxsIGZ1bmN0aW9uIHdpdGgga2V5LXZhbHVlIGlucHV0cwpjb250cmFjdCBYWVogewogICAgZnVuY3Rpb24gc29tZUZ1bmNXaXRoTWFueUlucHV0cygKICAgICAgICB1aW50MjU2IHgsCiAgICAgICAgdWludDI1NiB5LAogICAgICAgIHVpbnQyNTYgeiwKICAgICAgICBhZGRyZXNzIGEsCiAgICAgICAgYm9vbCBiLAogICAgICAgIHN0cmluZyBtZW1vcnkgYwogICAgKSBwdWJsaWMgcHVyZSByZXR1cm5zICh1aW50MjU2KSB7fQoKICAgIGZ1bmN0aW9uIGNhbGxGdW5jKCkgZXh0ZXJuYWwgcHVyZSByZXR1cm5zICh1aW50MjU2KSB7CiAgICAgICAgcmV0dXJuIHNvbWVGdW5jV2l0aE1hbnlJbnB1dHMoMSwgMiwgMywgYWRkcmVzcygwKSwgdHJ1ZSwgImMiKTsKICAgIH0KCiAgICBmdW5jdGlvbiBjYWxsRnVuY1dpdGhLZXlWYWx1ZSgpIGV4dGVybmFsIHB1cmUgcmV0dXJucyAodWludDI1NikgewogICAgICAgIHJldHVybiBzb21lRnVuY1dpdGhNYW55SW5wdXRzKHsKICAgICAgICAgICAgYTogYWRkcmVzcygwKSwKICAgICAgICAgICAgYjogdHJ1ZSwKICAgICAgICAgICAgYzogImMiLAogICAgICAgICAgICB4OiAxLAogICAgICAgICAgICB5OiAyLAogICAgICAgICAgICB6OiAzCiAgICAgICAgfSk7CiAgICB9Cn0K&lang=fr&optimize=false&runs=200&evmVersion=null&version=soljson-v0.8.26+commit.8a97fa7a.js)
