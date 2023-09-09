# solidity-workshop

In this workshop, we will be using Remix, a browser based development environment for Solidity that allows you write and test smart contracts without installing a compiler or additional versions of Solidity. Let's get started!

## Intro to Solidity

Solidity is a fully open-source, statically-typed curly-braces programming language specifically designed for writing smart contracts that run on Ethereum. Using Solidity, you can write contracts for use cases such as voting, crowdfunding, multi-sig wallets, and more! Below we list some of the most popular use cases:
- DAOs
- Gaming & Metaverse
- DeFi
- NFTs & more!

If you want to get started building your own decentralised applications using Solidity, check out the [Solidity by Example](https://docs.soliditylang.org/en/latest/solidity-by-example.html) section of the official docs to see sample code of different contracts and understand the core concepts of the language.

## The Anatomy of a Solidity Smart Contract

For the purpose of learning Solidity basics, will be taking the example of a Pokémon smart contract throughout this workshop.

## Workshop Overview

This is Part I of a longer workshop that teaches you how to build a Pokémon game. In part I, we will focus on Solidity at a glance for beginners and learn the fundamentals while writing a small Random Pokémon Generator contract that allows us to generate a random Pokémon and save it to our PokéDex for our game. Our factory contract will achieve the following:

- To maintain a collection of all Pokémon in our PokéDex
- Write a function for generating new random Pokémons

## Pokémon DNA & Individual Values

The Pokémon being created depends on the individual values passed by the user to form a unique 12-digit identifier called the Pokémon DNA. For instance, a Ditto has the following individual values or IV. 

Enough of nerdy Pokémon stuff. Let's dive right into learning Solidity!

**Table of content:**
- [Intro to Smart Contracts](#1)
- [State Variables & Integers](#2)
- [Math Operations](#3)
- [Structs](#4)
- [Arrays](#5)
- [Function Declarations](#6)
- [Working With Structs and Arrays](#7)
- [Private / Public Functions](#8)
- [More on Functions](#9)
- [Public Function](#10)

<!-- headings -->
<a id="1"></a>

### Intro Smart Contracts
In the context of Solidity, a smart contract is a collection of code and data that is stored at a specific address on the Ethereum blockchain. The code inside the smart contract is its functions and the data is the state of the chain.

The following example contract that implements a basic counter and allows you to retrieve, increment, and decrement the count stored in the variable:

```
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.20;

contract Counter {
    uint public count;

    // Function to get the current count
    function get() public view returns (uint) {
        return count;
    }

    // Function to increment count by 1
    function inc() public {
        count += 1;
    }

    // Function to decrement count by 1
    function dec() public {
        // This function will fail if count = 0
        count -= 1;
    }
}
```

- SPDX-License Identifier:
- Versin Pragma: All solidity code starts with a "Version Pragma" which describes the version of the Solidity compiler that should be use. This is to prevent issues with future compiler versions potentially introducing changes that would break your code.

<a id="2"></a>
### State Variables & Integers

```
contract Example {
  // This will be stored permanently in the blockchain
  uint myUnsignedInteger = 100;
}
```

<a id="3"></a>
### Math Operations

- Addition: x + y
- Subtraction: x - y,
- Multiplication: x * y
- Division: x / y
- Modulus / remainder: x % y (for example, 13 % 5 is 3, because if you divide 5 into 13, 3 is the remainder)

```
uint x = 3 * 2; // equal to 8
```

<a id="4"></a>
### Structs

```
struct Fruit {
  string name;
  string color;
}
```

<a id="5"></a>
### Arrays

- Fixed Arrays
- Dynamic Arrays

```
// Array with a fixed length of 3 elements:
uint[3] fixedArray;
// another fixed Array with 7 strings:
string[7] stringArray;
// a dynamic Array - has no fixed size, can keep growing:
uint[] dynamicArray;
```

- Array using struct

You can also create an array using a struct:
```
Person[] people;
```

- Public Array
  
You can declare an array as public as follows and Solidity will automatically create a getter method for it.

```
Person[] public people;
```

Other contracts would then be able to read from, but not write to, this array. So this is a useful pattern for storing public data in your contract.

<a id="6"></a>
### Function Declarations

A function in Solidity looks something like this:
```
function eatHamburgers(string memory _name, uint _amount) public {
//function body
}
```

Here's how you can call this function:

<a id="7"></a>
### Working With Structs and Arrays


<a id="8"></a>
### Private / Public Functions


<a id="9"></a>
### More on Functions


<a id="10"></a>
### Public Function

## Next Steps

Voila! Your Solidity Random Pokémon Generator smart contract is ready! Now we need to write a frontend using JS that can interacts with our contract. Ethereum has a JS library called Web3.js that allows you to do this. In part II, we will learn how to deploy a contract and set up Web3.js

Stay tuned for the next meetup and come learn more about Advanced Solidity in Part II of the workshop! :)
