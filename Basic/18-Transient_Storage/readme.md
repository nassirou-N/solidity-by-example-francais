# **Transient Storage**

toutes les données dans le transient storage s'efface aprés la transaction

```solidity
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.26;

// Make sure EVM version and VM set to Cancun

// Storage - data is stored on the blockchain
// Memory - data is cleared out after a function call
// Transient storage - data is cleared out after a transaction

interface ITest {
    function val() external view returns (uint256);
    function test() external;
}

// Contract for testing TestStorage and TestTransientStorage
// Shows the difference between normal storage and transient storage
contract Callback {
    uint256 public val;

    fallback() external {
        val = ITest(msg.sender).val();
    }

    function test(address target) external {
        ITest(target).test();
    }
}

contract TestStorage {
    uint256 public val;

    function test() public {
        val = 123;
        bytes memory b = "";
        msg.sender.call(b);
    }
}

contract TestTransientStorage {
    bytes32 constant SLOT = 0;

    function test() public {
        assembly {
            tstore(SLOT, 321)
        }
        bytes memory b = "";
        msg.sender.call(b);
    }

    function val() public view returns (uint256 v) {
        assembly {
            v := tload(SLOT)
        }
    }
}

// Contract for testing reentrancy protection
contract MaliciousCallback {
    uint256 public count = 0;

    // Try to reenter the target contract multiple times
    fallback() external {
        ITest(msg.sender).test();
    }

    // Test function to initiate reentrance attack
    function attack(address _target) external {
        // First call to test()
        ITest(_target).test();
    }
}

contract ReentrancyGuard {
    bool private locked;

    modifier lock() {
        require(!locked);
        locked = true;
        _;
        locked = false;
    }

    // 27587 gas
    function test() public lock {
        // Ignore call error
        bytes memory b = "";
        msg.sender.call(b);
    }
}

contract ReentrancyGuardTransient {
    bytes32 constant SLOT = 0;

    modifier lock() {
        assembly {
            if tload(SLOT) { revert(0, 0) }
            tstore(SLOT, 1)
        }
        _;
        assembly {
            tstore(SLOT, 0)
        }
    }

    // 4909 gas
    function test() external lock {
        // Ignore call error
        bytes memory b = "";
        msg.sender.call(b);
    }
}
```
## Execute sur Remix

[transient.sol](https://remix.ethereum.org/?#code=Ly8gU1BEWC1MaWNlbnNlLUlkZW50aWZpZXI6IE1JVApwcmFnbWEgc29saWRpdHkgXjAuOC4yNjsKCi8vIE1ha2Ugc3VyZSBFVk0gdmVyc2lvbiBhbmQgVk0gc2V0IHRvIENhbmN1bgoKLy8gU3RvcmFnZSAtIGRhdGEgaXMgc3RvcmVkIG9uIHRoZSBibG9ja2NoYWluCi8vIE1lbW9yeSAtIGRhdGEgaXMgY2xlYXJlZCBvdXQgYWZ0ZXIgYSBmdW5jdGlvbiBjYWxsCi8vIFRyYW5zaWVudCBzdG9yYWdlIC0gZGF0YSBpcyBjbGVhcmVkIG91dCBhZnRlciBhIHRyYW5zYWN0aW9uCgppbnRlcmZhY2UgSVRlc3QgewogICAgZnVuY3Rpb24gdmFsKCkgZXh0ZXJuYWwgdmlldyByZXR1cm5zICh1aW50MjU2KTsKICAgIGZ1bmN0aW9uIHRlc3QoKSBleHRlcm5hbDsKfQoKLy8gQ29udHJhY3QgZm9yIHRlc3RpbmcgVGVzdFN0b3JhZ2UgYW5kIFRlc3RUcmFuc2llbnRTdG9yYWdlCi8vIFNob3dzIHRoZSBkaWZmZXJlbmNlIGJldHdlZW4gbm9ybWFsIHN0b3JhZ2UgYW5kIHRyYW5zaWVudCBzdG9yYWdlCmNvbnRyYWN0IENhbGxiYWNrIHsKICAgIHVpbnQyNTYgcHVibGljIHZhbDsKCiAgICBmYWxsYmFjaygpIGV4dGVybmFsIHsKICAgICAgICB2YWwgPSBJVGVzdChtc2cuc2VuZGVyKS52YWwoKTsKICAgIH0KCiAgICBmdW5jdGlvbiB0ZXN0KGFkZHJlc3MgdGFyZ2V0KSBleHRlcm5hbCB7CiAgICAgICAgSVRlc3QodGFyZ2V0KS50ZXN0KCk7CiAgICB9Cn0KCmNvbnRyYWN0IFRlc3RTdG9yYWdlIHsKICAgIHVpbnQyNTYgcHVibGljIHZhbDsKCiAgICBmdW5jdGlvbiB0ZXN0KCkgcHVibGljIHsKICAgICAgICB2YWwgPSAxMjM7CiAgICAgICAgYnl0ZXMgbWVtb3J5IGIgPSAiIjsKICAgICAgICBtc2cuc2VuZGVyLmNhbGwoYik7CiAgICB9Cn0KCmNvbnRyYWN0IFRlc3RUcmFuc2llbnRTdG9yYWdlIHsKICAgIGJ5dGVzMzIgY29uc3RhbnQgU0xPVCA9IDA7CgogICAgZnVuY3Rpb24gdGVzdCgpIHB1YmxpYyB7CiAgICAgICAgYXNzZW1ibHkgewogICAgICAgICAgICB0c3RvcmUoU0xPVCwgMzIxKQogICAgICAgIH0KICAgICAgICBieXRlcyBtZW1vcnkgYiA9ICIiOwogICAgICAgIG1zZy5zZW5kZXIuY2FsbChiKTsKICAgIH0KCiAgICBmdW5jdGlvbiB2YWwoKSBwdWJsaWMgdmlldyByZXR1cm5zICh1aW50MjU2IHYpIHsKICAgICAgICBhc3NlbWJseSB7CiAgICAgICAgICAgIHYgOj0gdGxvYWQoU0xPVCkKICAgICAgICB9CiAgICB9Cn0KCi8vIENvbnRyYWN0IGZvciB0ZXN0aW5nIHJlZW50cmFuY3kgcHJvdGVjdGlvbgpjb250cmFjdCBNYWxpY2lvdXNDYWxsYmFjayB7CiAgICB1aW50MjU2IHB1YmxpYyBjb3VudCA9IDA7CgogICAgLy8gVHJ5IHRvIHJlZW50ZXIgdGhlIHRhcmdldCBjb250cmFjdCBtdWx0aXBsZSB0aW1lcwogICAgZmFsbGJhY2soKSBleHRlcm5hbCB7CiAgICAgICAgSVRlc3QobXNnLnNlbmRlcikudGVzdCgpOwogICAgfQoKICAgIC8vIFRlc3QgZnVuY3Rpb24gdG8gaW5pdGlhdGUgcmVlbnRyYW5jZSBhdHRhY2sKICAgIGZ1bmN0aW9uIGF0dGFjayhhZGRyZXNzIF90YXJnZXQpIGV4dGVybmFsIHsKICAgICAgICAvLyBGaXJzdCBjYWxsIHRvIHRlc3QoKQogICAgICAgIElUZXN0KF90YXJnZXQpLnRlc3QoKTsKICAgIH0KfQoKY29udHJhY3QgUmVlbnRyYW5jeUd1YXJkIHsKICAgIGJvb2wgcHJpdmF0ZSBsb2NrZWQ7CgogICAgbW9kaWZpZXIgbG9jaygpIHsKICAgICAgICByZXF1aXJlKCFsb2NrZWQpOwogICAgICAgIGxvY2tlZCA9IHRydWU7CiAgICAgICAgXzsKICAgICAgICBsb2NrZWQgPSBmYWxzZTsKICAgIH0KCiAgICAvLyAyNzU4NyBnYXMKICAgIGZ1bmN0aW9uIHRlc3QoKSBwdWJsaWMgbG9jayB7CiAgICAgICAgLy8gSWdub3JlIGNhbGwgZXJyb3IKICAgICAgICBieXRlcyBtZW1vcnkgYiA9ICIiOwogICAgICAgIG1zZy5zZW5kZXIuY2FsbChiKTsKICAgIH0KfQoKY29udHJhY3QgUmVlbnRyYW5jeUd1YXJkVHJhbnNpZW50IHsKICAgIGJ5dGVzMzIgY29uc3RhbnQgU0xPVCA9IDA7CgogICAgbW9kaWZpZXIgbG9jaygpIHsKICAgICAgICBhc3NlbWJseSB7CiAgICAgICAgICAgIGlmIHRsb2FkKFNMT1QpIHsgcmV2ZXJ0KDAsIDApIH0KICAgICAgICAgICAgdHN0b3JlKFNMT1QsIDEpCiAgICAgICAgfQogICAgICAgIF87CiAgICAgICAgYXNzZW1ibHkgewogICAgICAgICAgICB0c3RvcmUoU0xPVCwgMCkKICAgICAgICB9CiAgICB9CgogICAgLy8gNDkwOSBnYXMKICAgIGZ1bmN0aW9uIHRlc3QoKSBleHRlcm5hbCBsb2NrIHsKICAgICAgICAvLyBJZ25vcmUgY2FsbCBlcnJvcgogICAgICAgIGJ5dGVzIG1lbW9yeSBiID0gIiI7CiAgICAgICAgbXNnLnNlbmRlci5jYWxsKGIpOwogICAgfQp9Cg&lang=fr&optimize=false&runs=200&evmVersion=null&version=soljson-v0.8.26+commit.8a97fa7a.js)
