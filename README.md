# Blockchain-Project
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.0;
contract Payment {
    mapping(address => uint) public balances;
    function deposit() public payable {
        balances[msg.sender] += msg.value;
    }
    function withdraw(uint amount) public {
        require(balances[msg.sender] >= amount, "Insufficient balance");
      
        balances[msg.sender] -= amount;
        (bool sent, ) = msg.sender.call{value: amount}("");
        require(sent, "Failed to send Ether");
    }
}
