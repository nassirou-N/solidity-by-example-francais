# **Enum**

solidity support le type $\color{red}{\textsf{Enum}}$ utilise pour faire un model de choix avec les etats. 
le Enum sont declare en déhors du contract

```solidity
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.26;

contract Enum {
    // Enum representing shipping status
    enum Status {
        Pending,
        Shipped,
        Accepted,
        Rejected,
        Canceled
    }

    // Default value is the first element listed in
    // definition of the type, in this case "Pending"
    Status public status;

    // Returns uint
    // Pending  - 0
    // Shipped  - 1
    // Accepted - 2
    // Rejected - 3
    // Canceled - 4
    function get() public view returns (Status) {
        return status;
    }

    // Update status by passing uint into input
    function set(Status _status) public {
        status = _status;
    }

    // You can update to a specific enum like this
    function cancel() public {
        status = Status.Canceled;
    }

    // delete resets the enum to its first value, 0
    function reset() public {
        delete status;
    }
}
```
### **declare et import les Enum**
le fichier des enum
```solidity
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.26;
// This is saved 'EnumDeclaration.sol'

enum Status {
    Pending,
    Shipped,
    Accepted,
    Rejected,
    Canceled
} ```
cet file import le enum

```solidity
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.26;

import "./EnumDeclaration.sol";

contract Enum {
    Status public status;
}
```

## Execute sur Remix

[enum.sol](https://remix.ethereum.org/?#code=Ly8gU1BEWC1MaWNlbnNlLUlkZW50aWZpZXI6IE1JVApwcmFnbWEgc29saWRpdHkgXjAuOC4yNjsKCmltcG9ydCAiLi9FbnVtRGVjbGFyYXRpb24uc29sIjsKCmNvbnRyYWN0IEVudW0gewogICAgU3RhdHVzIHB1YmxpYyBzdGF0dXM7Cn0K&lang=fr&optimize=false&runs=200&evmVersion=null&version=soljson-v0.8.26+commit.8a97fa7a.js)


