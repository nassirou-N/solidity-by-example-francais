# **Les tableau (Array)**

le tableau sont souvant dynamique mais on peu aussi avoir les tableaux de taille fixe.

```solidity
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.26;

contract Array {
    // Several ways to initialize an array
    uint256[] public arr;
    uint256[] public arr2 = [1, 2, 3];
    // Fixed sized array, all elements initialize to 0
    uint256[10] public myFixedSizeArr;

    function get(uint256 i) public view returns (uint256) {
        return arr[i];
    }

    // Solidity can return the entire array.
    // But this function should be avoided for
    // arrays that can grow indefinitely in length.
    function getArr() public view returns (uint256[] memory) {
        return arr;
    }

    function push(uint256 i) public {
        // Append to array
        // This will increase the array length by 1.
        arr.push(i);
    }

    function pop() public {
        // Remove last element from array
        // This will decrease the array length by 1
        arr.pop();
    }

    function getLength() public view returns (uint256) {
        return arr.length;
    }

    function remove(uint256 index) public {
        // Delete does not change the array length.
        // It resets the value at index to it's default value,
        // in this case 0
        delete arr[index];
    }

    function examples() external pure {
        // create array in memory, only fixed size can be created
        uint256[] memory a = new uint256[](5);

        // create a nested array in memory
        // b = [[1, 2, 3], [4, 5, 6]]
        uint256[][] memory b = new uint256[][](2);
        for (uint256 i = 0; i < b.length; i++) {
            b[i] = new uint256[](3);
        }
        b[0][0] = 1;
        b[0][1] = 2;
        b[0][2] = 3;
        b[1][0] = 4;
        b[1][1] = 5;
        b[1][2] = 6;
    }
}
```
### **Exemple pour supprimer les elements dans un tableau**
```solidity
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.26;

contract ArrayRemoveByShifting {
    // [1, 2, 3] -- remove(1) --> [1, 3, 3] --> [1, 3]
    // [1, 2, 3, 4, 5, 6] -- remove(2) --> [1, 2, 4, 5, 6, 6] --> [1, 2, 4, 5, 6]
    // [1, 2, 3, 4, 5, 6] -- remove(0) --> [2, 3, 4, 5, 6, 6] --> [2, 3, 4, 5, 6]
    // [1] -- remove(0) --> [1] --> []

    uint256[] public arr;

    function remove(uint256 _index) public {
        require(_index < arr.length, "index out of bounds");

        for (uint256 i = _index; i < arr.length - 1; i++) {
            arr[i] = arr[i + 1];
        }
        arr.pop();
    }

    function test() external {
        arr = [1, 2, 3, 4, 5];
        remove(2);
        // [1, 2, 4, 5]
        assert(arr[0] == 1);
        assert(arr[1] == 2);
        assert(arr[2] == 4);
        assert(arr[3] == 5);
        assert(arr.length == 4);

        arr = [1];
        remove(0);
        // []
        assert(arr.length == 0);
    }
}
```


## Execute Sur Remix

[tableau.sol](https://remix.ethereum.org/?#code=Ly8gU1BEWC1MaWNlbnNlLUlkZW50aWZpZXI6IE1JVApwcmFnbWEgc29saWRpdHkgXjAuOC4yNjsKCmNvbnRyYWN0IEFycmF5IHsKICAgIC8vIFNldmVyYWwgd2F5cyB0byBpbml0aWFsaXplIGFuIGFycmF5CiAgICB1aW50MjU2W10gcHVibGljIGFycjsKICAgIHVpbnQyNTZbXSBwdWJsaWMgYXJyMiA9IFsxLCAyLCAzXTsKICAgIC8vIEZpeGVkIHNpemVkIGFycmF5LCBhbGwgZWxlbWVudHMgaW5pdGlhbGl6ZSB0byAwCiAgICB1aW50MjU2WzEwXSBwdWJsaWMgbXlGaXhlZFNpemVBcnI7CgogICAgZnVuY3Rpb24gZ2V0KHVpbnQyNTYgaSkgcHVibGljIHZpZXcgcmV0dXJucyAodWludDI1NikgewogICAgICAgIHJldHVybiBhcnJbaV07CiAgICB9CgogICAgLy8gU29saWRpdHkgY2FuIHJldHVybiB0aGUgZW50aXJlIGFycmF5LgogICAgLy8gQnV0IHRoaXMgZnVuY3Rpb24gc2hvdWxkIGJlIGF2b2lkZWQgZm9yCiAgICAvLyBhcnJheXMgdGhhdCBjYW4gZ3JvdyBpbmRlZmluaXRlbHkgaW4gbGVuZ3RoLgogICAgZnVuY3Rpb24gZ2V0QXJyKCkgcHVibGljIHZpZXcgcmV0dXJucyAodWludDI1NltdIG1lbW9yeSkgewogICAgICAgIHJldHVybiBhcnI7CiAgICB9CgogICAgZnVuY3Rpb24gcHVzaCh1aW50MjU2IGkpIHB1YmxpYyB7CiAgICAgICAgLy8gQXBwZW5kIHRvIGFycmF5CiAgICAgICAgLy8gVGhpcyB3aWxsIGluY3JlYXNlIHRoZSBhcnJheSBsZW5ndGggYnkgMS4KICAgICAgICBhcnIucHVzaChpKTsKICAgIH0KCiAgICBmdW5jdGlvbiBwb3AoKSBwdWJsaWMgewogICAgICAgIC8vIFJlbW92ZSBsYXN0IGVsZW1lbnQgZnJvbSBhcnJheQogICAgICAgIC8vIFRoaXMgd2lsbCBkZWNyZWFzZSB0aGUgYXJyYXkgbGVuZ3RoIGJ5IDEKICAgICAgICBhcnIucG9wKCk7CiAgICB9CgogICAgZnVuY3Rpb24gZ2V0TGVuZ3RoKCkgcHVibGljIHZpZXcgcmV0dXJucyAodWludDI1NikgewogICAgICAgIHJldHVybiBhcnIubGVuZ3RoOwogICAgfQoKICAgIGZ1bmN0aW9uIHJlbW92ZSh1aW50MjU2IGluZGV4KSBwdWJsaWMgewogICAgICAgIC8vIERlbGV0ZSBkb2VzIG5vdCBjaGFuZ2UgdGhlIGFycmF5IGxlbmd0aC4KICAgICAgICAvLyBJdCByZXNldHMgdGhlIHZhbHVlIGF0IGluZGV4IHRvIGl0J3MgZGVmYXVsdCB2YWx1ZSwKICAgICAgICAvLyBpbiB0aGlzIGNhc2UgMAogICAgICAgIGRlbGV0ZSBhcnJbaW5kZXhdOwogICAgfQoKICAgIGZ1bmN0aW9uIGV4YW1wbGVzKCkgZXh0ZXJuYWwgcHVyZSB7CiAgICAgICAgLy8gY3JlYXRlIGFycmF5IGluIG1lbW9yeSwgb25seSBmaXhlZCBzaXplIGNhbiBiZSBjcmVhdGVkCiAgICAgICAgdWludDI1NltdIG1lbW9yeSBhID0gbmV3IHVpbnQyNTZbXSg1KTsKCiAgICAgICAgLy8gY3JlYXRlIGEgbmVzdGVkIGFycmF5IGluIG1lbW9yeQogICAgICAgIC8vIGIgPSBbWzEsIDIsIDNdLCBbNCwgNSwgNl1dCiAgICAgICAgdWludDI1NltdW10gbWVtb3J5IGIgPSBuZXcgdWludDI1NltdW10oMik7CiAgICAgICAgZm9yICh1aW50MjU2IGkgPSAwOyBpIDwgYi5sZW5ndGg7IGkrKykgewogICAgICAgICAgICBiW2ldID0gbmV3IHVpbnQyNTZbXSgzKTsKICAgICAgICB9CiAgICAgICAgYlswXVswXSA9IDE7CiAgICAgICAgYlswXVsxXSA9IDI7CiAgICAgICAgYlswXVsyXSA9IDM7CiAgICAgICAgYlsxXVswXSA9IDQ7CiAgICAgICAgYlsxXVsxXSA9IDU7CiAgICAgICAgYlsxXVsyXSA9IDY7CiAgICB9Cn0K&lang=fr&optimize=false&runs=200&evmVersion=null&version=soljson-v0.8.26+commit.8a97fa7a.js)
