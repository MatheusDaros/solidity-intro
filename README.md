# How to Use Remix to Deploy Your First Smart Contract
In this article, you will learn how to use Remix, a web-based IDE for Ethereum, to create and deploy your first smart contract. You will also learn the basics of the blockchain structure, how to interact with your contract using MetaMask and read data from it using Etherscan, how to use OpenZeppelin, a library of secure and reusable smart contracts and how the Solidity language can be used for coding smart contracts.

## What is Remix?
Remix is an online IDE that allows you to write, compile, debug, test, and deploy smart contracts for Ethereum and EVM-compatible blockchains. It has a user-friendly interface, a rich set of plugins, and a visual debugger. You can use Remix directly from your browser or download the desktop app or the VSCode extension. You can also connect Remix to your local or remote node, or use the in-browser blockchain (Remix VM) for development and testing.

To start using Remix, go to <http://remix.ethereum.org/> or <https://remix-ide.readthedocs.io/en/latest/>.

## What is a Smart Contract?
A smart contract is a piece of code that runs on the blockchain and defines the rules and logic for a digital agreement. Smart contracts can store data, execute functions, interact with other contracts, and transfer funds. Smart contracts are immutable, transparent, and verifiable by anyone.

The most popular language for writing smart contracts on Ethereum is Solidity, a high-level, object-oriented language that is influenced by C++, Python, and JavaScript. Solidity has a syntax similar to JavaScript and supports common programming features such as variables, functions, operators, control structures, inheritance, and modifiers.

To learn more about Solidity, you can check the official documentation at <https://docs.soliditylang.org/>.

## What is OpenZeppelin?
OpenZeppelin is a library of secure and reusable smart contracts for Ethereum and other EVM-compatible blockchains. OpenZeppelin provides implementations of common standards such as ERC20 and ERC721 tokens, as well as utility contracts for access control, math operations, security checks, and more.

OpenZeppelin contracts are written in Solidity and follow the best practices for code quality, security, and auditability. You can import OpenZeppelin contracts in your own contracts using a simple import statement.

To learn more about OpenZeppelin, you can check the official website at <https://openzeppelin.com/> or the GitHub repository at <https://github.com/OpenZeppelin/openzeppelin-contracts>.

## How to Create an ERC20 Token using Remix and OpenZeppelin
An ERC20 token is a standard for fungible tokens on Ethereum. Fungible tokens are tokens that have the same value and can be exchanged or divided. Examples of fungible tokens are currencies, loyalty points, or utility tokens.

To create an ERC20 token using Remix and OpenZeppelin, you can follow these steps:

* Create a new workspace in Remix
* Choose a template
  * OpenZeppelin
    * ERC20
    * Mintable
    * Burnable
* Choose a workspace name
* Confirm

You should find a file inside the folder `contracts` with the name `MyToken.sol`.
The code for that contract should be similar to this:

```solidity
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.9;

import "@openzeppelin/contracts/token/ERC20/ERC20.sol";
import "@openzeppelin/contracts/token/ERC20/extensions/ERC20Burnable.sol";
import "@openzeppelin/contracts/access/Ownable.sol";

contract MyToken is ERC20, ERC20Burnable, Ownable {
    constructor() ERC20("MyToken", "MTK") {}

    function mint(address to, uint256 amount) public onlyOwner {
        _mint(to, amount);
    }
}
```

This simple solidity file is already enough to use a big set of functionalities provided by ERC20 Tokens.

## Features of the MyToken Contract

The MyToken contract is a simple ERC20 token that inherits from the OpenZeppelin contracts ERC20, ERC20Burnable, and Ownable. It has a mint function that can only be called by the owner of the contract.

### ERC20

The ERC20 contract implements the ERC20 standard, which defines a common interface for fungible tokens on Ethereum. The ERC20 contract provides basic functions for transferring tokens, allowing token holders to approve others to transfer their tokens, and querying the balance and total supply of tokens. The ERC20 contract also emits events for token transfers and approvals.

To use the ERC20 contract, you need to specify the name and symbol of your token in the constructor, and optionally the number of decimals (default is 18). You also need to implement the `_mint` function, which creates new tokens and adds them to the total supply and the recipient's balance.

You can import the ERC20 contract from OpenZeppelin using the following statement:

```solidity
import "@openzeppelin/contracts/token/ERC20/ERC20.sol";
```

You can learn more about the ERC20 contract and its functions in the [OpenZeppelin documentation](https://docs.openzeppelin.com/contracts/4.x/api/token/erc20).

### ERC20Burnable

The ERC20Burnable contract extends the ERC20 contract and adds a burn function that allows token holders to destroy their tokens, reducing the total supply and their balance. The burn function emits a Transfer event with the zero address as the recipient.

To use the ERC20Burnable contract, you need to inherit from it in your token contract. You don't need to implement any additional functions.

You can import the ERC20Burnable contract from OpenZeppelin using the following statement:

```solidity
import "@openzeppelin/contracts/token/ERC20/extensions/ERC20Burnable.sol";
```

You can learn more about the ERC20Burnable contract and its functions in the [OpenZeppelin documentation](https://docs.openzeppelin.com/contracts/4.x/api/token/erc20#ERC20Burnable).

### Ownable

The Ownable contract provides a basic access control mechanism that assigns an owner to a contract. The owner is set to the deployer of the contract by default, and can be transferred or renounced by the current owner. The Ownable contract also provides a modifier called `onlyOwner` that restricts the execution of functions to the owner only.

To use the Ownable contract, you need to inherit from it in your token contract. You don't need to implement any additional functions.

You can import the Ownable contract from OpenZeppelin using the following statement:

```solidity
import "@openzeppelin/contracts/access/Ownable.sol";
```

You can learn more about the Ownable contract and its functions in the [OpenZeppelin documentation](https://docs.openzeppelin.com/contracts/4.x/access-control#ownership-and-ownable).

### Mint Function

The mint function is a custom function that allows the owner of the contract to create new tokens and assign them to a recipient address. The mint function uses the `_mint` function inherited from the ERC20 contract, which updates the total supply and the recipient's balance, and emits a Transfer event. The mint function also uses the `onlyOwner` modifier inherited from the Ownable contract, which ensures that only the owner can call this function.

The mint function has two parameters: `to` and `amount`. The `to` parameter is an address that receives the newly created tokens. The `amount` parameter is a uint256 that specifies how many tokens to create.

The mint function has no return value.

The mint function is defined as follows:

```solidity
function mint(address to, uint256 amount) public onlyOwner {
    _mint(to, amount);
}
```

## Interacting with the smart contract

### How to Compile and Deploy in Remix using a VM

In this section, we will learn how to compile and deploy a smart contract in Remix using a virtual machine (VM) provided by Remix. This is a convenient way to test your contract without spending any real gas or connecting to any network.

- In Remix, open the `MyToken.sol` file that you created in the previous section.
- In the Solidity Compiler plugin, click on `Compile MyToken.sol`.
- In the Deploy & Run Transactions plugin, select `JavaScript VM (Shangai)` as the environment. This will create some prefunded accounts with 100 fake ETH each for testing purposes.
- Select `MyToken` as the contract to deploy.
- Press the `Deploy` button. Remix will deploy your token contract to the VM and show it under the Deployed Contracts section.
- Congratulations! You have compiled and deployed your first smart contract in Remix using a VM 🙌

## How to Connect to MetaMask Wallet and Deploy to a Testnet

In this section, we will learn how to connect Remix to your MetaMask wallet and deploy your smart contract to a public testnet. A testnet is a network that simulates the mainnet, but uses fake ETH and tokens for testing purposes. There are several testnets available for Ethereum, such as Goerli and Sepolia.

We will use the Sepolia testnet in this tutorial, but you can choose any other testnet that you prefer.

- In MetaMask, make sure you have selected the Sepolia Test Network from the network dropdown menu.
- If you don't have any Sepolia ETH in your account, you can get some from a faucet. A faucet is a website that gives you free test ETH for testing purposes.
- In Remix, in the Deploy & Run Transactions plugin, select `Injected Web3` as the environment. This will connect Remix to your MetaMask wallet and show your current account and balance.
- Select `MyToken` as the contract to deploy.
- Press the `Deploy` button and confirm the transaction on MetaMask. Remix will deploy your token contract to the Sepolia testnet and show it under the Deployed Contracts section.
- And this is it! You have connected Remix to your MetaMask wallet and deployed your smart contract to the Sepolia public testnet 👌

## How to View Transactions in Etherscan

In this section, we will learn how to view the transactions that we made on the testnets using Etherscan, a block explorer for Ethereum and its testnets. A block explorer is a website that allows you to search and browse the transactions, blocks, accounts, and smart contracts on the blockchain.

- To view the transactions that you made on the Sepolia testnet, you can go to [https://sepolia.etherscan.io/](https://sepolia.etherscan.io/) and enter your MetaMask address or the transaction hash in the search bar. You will see the details of your transactions, such as the status, amount, gas fee, and timestamp.

# Conclusion
In this article, you learned how to use Remix to deploy your first smart contract. You also learned the basics of the blockchain structure, how to interact with your contract using MetaMask and Etherscan, and how to use OpenZeppelin, a library of secure and reusable smart contracts.

You can use Remix to experiment with different types of smart contracts, such as ERC721 (non-fungible tokens) or ERC1155 (multi-token standard). You can also use OpenZeppelin templates or write your own custom logic.

We hope you enjoyed this tutorial and learned something new. If you have any questions or feedback, feel free to open an issue an I'll get to it as soon as possible. Happy coding!
