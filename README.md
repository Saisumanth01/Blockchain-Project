

Examine the Solidity code below. Identify the vulnerability and explain how it can be exploited. Then, rewrite the function to fix the issue.

pragma solidity ^0.8.0;

contract Payment {
    mapping(address => uint) public balances;

    function deposit() public payable {
        balances[msg.sender] += msg.value;
    }

    function withdraw(uint amount) public {
        require(balances[msg.sender] >= amount, "Insufficient balance");
        (bool sent, ) = msg.sender.call{value: amount}("");
        require(sent, "Failed to send Ether");
        balances[msg.sender] -= amount;
    }
}

