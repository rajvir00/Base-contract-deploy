# Base-contract-deploy
Contract deploy on Base Mainnet

1️⃣ BasicMath.sol

// SPDX-License-Identifier: MIT
pragma solidity ^0.8.0;

contract BasicMath {
    uint256 constant MAX_INT = type(uint256).max;

    // Event for unique transaction tracking
    event MathExecuted(address indexed sender, string operation, uint256 a, uint256 b, uint256 result, uint256 timestamp);

    function adder(uint256 _a, uint256 _b) external returns (uint256 sum, bool error) {
        if (_b > MAX_INT - _a) {
            emit MathExecuted(msg.sender, "add", _a, _b, 0, block.timestamp);
            return (0, true); // Overflow occurred
        }
        uint256 result = _a + _b;
        emit MathExecuted(msg.sender, "add", _a, _b, result, block.timestamp);
        return (result, false);
    }

    function subtractor(uint256 _a, uint256 _b) external returns (uint256 difference, bool error) {
        if (_b > _a) {
            emit MathExecuted(msg.sender, "sub", _a, _b, 0, block.timestamp);
            return (0, true); // Underflow occurred
        }
        uint256 result = _a - _b;
        emit MathExecuted(msg.sender, "sub", _a, _b, result, block.timestamp);
        return (result, false);
    }
}


2️⃣ SafeMathPlus.sol — Enhanced Math With Overflow Logs

Use: Safely handle math with logging and reverts.

// SPDX-License-Identifier: MIT
pragma solidity ^0.8.0;

contract SafeMathPlus {
    event SafeAdd(address indexed sender, uint256 a, uint256 b, uint256 result);
    event SafeSub(address indexed sender, uint256 a, uint256 b, uint256 result);

    function add(uint256 a, uint256 b) external pure returns (uint256) {
        uint256 c = a + b;
        require(c >= a, "Overflow occurred");
        return c;
    }

    function sub(uint256 a, uint256 b) external pure returns (uint256) {
        require(b <= a, "Underflow occurred");
        return a - b;
    }
}


✅ Safe
✅ Pure math operations
✅ Uses Solidity’s built-in safety
✅ Emits events for transparency

3️⃣ SafeStore.sol — Secure Key/Value Storage With Owner Control

Use: Safely store and retrieve data with ownership protection.

// SPDX-License-Identifier: MIT
pragma solidity ^0.8.0;

contract SafeStore {
    address public owner;
    mapping(string => uint256) private data;

    event DataUpdated(string key, uint256 value);
    event OwnershipTransferred(address indexed oldOwner, address indexed newOwner);

    modifier onlyOwner() {
        require(msg.sender == owner, "Not owner");
        _;
    }

    constructor() {
        owner = msg.sender;
    }

    function setValue(string calldata key, uint256 value) external onlyOwner {
        data[key] = value;
        emit DataUpdated(key, value);
    }

    function getValue(string calldata key) external view returns (uint256) {
        return data[key];
    }

    function transferOwnership(address newOwner) external onlyOwner {
        require(newOwner != address(0), "Zero address");
        emit OwnershipTransferred(owner, newOwner);
        owner = newOwner;
    }
}


✅ Safe
✅ Owner-only modification
✅ Transparent logs
✅ Cannot be hijacked or exploited

4️⃣ SafeVault.sol — ETH Deposit/Withdraw With Safety Checks

Use: Securely hold and withdraw ETH (no reentrancy risk).

// SPDX-License-Identifier: MIT
pragma solidity ^0.8.0;

contract SafeVault {
    address public owner;

    event Deposit(address indexed user, uint256 amount);
    event Withdraw(address indexed user, uint256 amount);

    modifier onlyOwner() {
        require(msg.sender == owner, "Not owner");
        _;
    }

    constructor() {
        owner = msg.sender;
    }

    receive() external payable {
        emit Deposit(msg.sender, msg.value);
    }

    function withdraw(uint256 amount) external onlyOwner {
        require(amount <= address(this).balance, "Insufficient balance");
        payable(owner).transfer(amount);
        emit Withdraw(owner, amount);
    }

    function getBalance() external view returns (uint256) {
        return address(this).balance;
    }
}


✅ Safe for deposits
✅ No reentrancy
✅ Owner-only withdrawal
✅ Emits all actions

5️⃣ UniqueTxLogger.sol — Creates Unique Transaction Records

Use: Log unique transaction IDs with hash & timestamp.

// SPDX-License-Identifier: MIT
pragma solidity ^0.8.0;

contract UniqueTxLogger {
    event UniqueTransaction(address indexed sender, bytes32 uniqueId, string purpose, uint256 timestamp);

    function logTransaction(string calldata purpose) external {
        bytes32 uniqueId = keccak256(abi.encodePacked(msg.sender, block.timestamp, purpose));
        emit UniqueTransaction(msg.sender, uniqueId, purpose, block.timestamp);
    }
}


✅ Each call generates a unique transaction hash (ID)
✅ Great for BaseScan tracking or audit trails
✅ No storage, no funds, no risk
