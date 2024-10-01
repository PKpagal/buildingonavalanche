// SPDX-License-Identifier: MIT
pragma solidity ^0.8.18;

import "@openzeppelin/contracts/token/ERC20/ERC20.sol";
import "@openzeppelin/contracts/access/Ownable.sol";

contract DegenToken is ERC20, Ownable {

    // Constructor initializing token name, symbol, and the owner
    constructor(address initialOwner) ERC20("Degen", "DGN") Ownable(initialOwner) {
        // No need to call transferOwnership here, it's already set in Ownable
    }

    // Events to log token activities
    event TokensRedeemed(address indexed account, uint rewardTier);
    event TokensBurned(address indexed account, uint amountBurned);
    event TokensTransferred(address indexed from, address indexed to, uint amountTransferred);

    // Mint new tokens to the specified address, only callable by the contract owner
    function mint(address recipient, uint256 amountToMint) public onlyOwner {
        _mint(recipient, amountToMint);
    }
    
    // Returns the balance of the caller (msg.sender)
    function getBalance() public view returns (uint256) {
        return balanceOf(msg.sender);
    }

    // Redeem tokens based on the reward tier, requires sufficient balance
    function redeem(uint rewardTier) public {
        uint256 requiredAmount = rewardTier * 10;
        require(balanceOf(msg.sender) >= requiredAmount, "Insufficient balance to redeem tokens");
        burn(requiredAmount);
        emit TokensRedeemed(msg.sender, rewardTier);
    }

    // Burn a specified amount of tokens from the caller's balance
    function burn(uint256 amountToBurn) public {
        _burn(msg.sender, amountToBurn);
        emit TokensBurned(msg.sender, amountToBurn);
    }
}
