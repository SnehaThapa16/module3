# MelodyToken Smart Contract

This Solidity program is a simple "TOKEN CONTRACT" that represents the token called MelodyToken, abbreviated by MLDY, with functionalities for managing its total supply through mint and burn functions.

## Description

This program is a smart contract written in Solidity, a programming language used for developing smart contracts on the Ethereum blockchain. The contract represents a token named "MELODY TOKEN" with the symbol "MLDY" and includes functionalities to mint (create) and burn (destroy) tokens, which affects the total supply using the OpenZeppelin ERC20 implementation. Additionally, it uses a mapping of addresses to balances, which enables the contract to keep track of the balance of MLDY tokens held by each address. The contract also allows for token transfers between addresses.

## Getting Started

### Executing Program

To run this program, you can use Remix, an online Solidity IDE. Follow the steps below to get started:

1. Go to the [Remix Ethereum IDE](https://remix.ethereum.org/).
2. Create a new file by clicking on the "+" icon in the left-hand sidebar.
3. Save the file with a `.sol` extension (e.g., `MelodyToken.sol`).
4. Copy and paste the following code into the file:

```solidity
// SPDX-License-Identifier: MIT
pragma solidity 0.8.25;

import "@openzeppelin/contracts/token/ERC20/ERC20.sol";

contract MelodyToken is ERC20 {

    address public melodyOwner;
    uint256 private _melodyTotalSupply = 0;

    constructor() ERC20("MELODY TOKEN", "MLDY") {
        melodyOwner = msg.sender;
    }

    modifier onlyMelodyOwner() {
        require(melodyOwner == msg.sender, "Only Owner Can Access");
        _;
    }

    function mint(address _receiver, uint256 _amount) public onlyMelodyOwner {
        _mint(_receiver, _amount);
        _melodyTotalSupply += _amount;
        emit Transfer(address(0), _receiver, _amount);
    }

    function burn(uint256 _amount) public {
        require(balanceOf(msg.sender) >= _amount, "Insufficient Balance");
        _burn(msg.sender, _amount);
        _melodyTotalSupply -= _amount;
        emit Transfer(msg.sender, address(0), _amount);
    }

    function transfer(address _receiver, uint256 _amount) public override returns (bool) {
        require(msg.sender != _receiver, "You Can't Transfer To Yourself");
        require(balanceOf(msg.sender) >= _amount, "Insufficient Balance");

        _transfer(_msgSender(), _receiver, _amount);
        return true;
    }

    function totalSupply() public view override returns (uint256) {
        return _melodyTotalSupply;
    }
}
```

## Compiling the Code
1. Click on the "Solidity Compiler" tab in the left-hand sidebar.
2. Ensure the "Compiler" option is set to "0.8.25" (or another compatible version).
3. Click on the "Compile MelodyToken.sol" button.

## Deploying the Contract
1. Go to the "Deploy & Run Transactions" tab in the left-hand sidebar.
2. Select the "MelodyToken" contract from the dropdown menu.
3. Click on the "Deploy" button.

## Interacting with the Contract
### Mint Tokens
1. Select the mint function.
2. Enter the address and the number of tokens to mint.
3. Click on the "transact" button.

### Burn Tokens
1. Select the burn function.
2. Enter the number of tokens to burn.
3. Click on the "transact" button.

### Transfer Tokens
1. Select the transfer function.
2. Enter the recipient address and the number of tokens to transfer.
3. Click on the "transact" button.

### Check Balances
1. Select the balanceOf function.
2. Enter the address and click on the "call" button.
3. The balance of the entered address will be displayed.

### View Token Details
1. Retrieve the values of melodyOwner and totalSupply from the deployed contract.

## Authors
Sneha Thapa [https://www.linkedin.com/in/sneha-thapa-00a353270/]

