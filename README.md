# solidity-workshop

In this workshop, we will be using Remix, a browser based development environment for Solidity that allows you write and test smart contracts without installing a compiler or additional versions of Solidity. Let's get started!

## Intro to Solidity

[Solidity](https://docs.soliditylang.org/en/v0.8.21/) is a fully open-source, statically-typed curly-braces programming language specifically designed for writing smart contracts that run on Ethereum. Using Solidity, you can write contracts for use cases such as voting, crowdfunding, multi-sig wallets, and more! Below we list some of the most popular use cases:
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

The Pokémon being created depends on the individual values passed by the user to form a unique 16-digit identifier called the Pokémon DNA.

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

- SPDX-License Identifier: This is machine-readable identifier to tell the compiler under which the source code is licensed.
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
function paint(string memory _color, uint _brush) public {
//function body
}
```
You can pass aurguments to a function in two ways:
- either by value
- or by reference

Here's how you can call this function:
```
paint("purple", 4);
```

<a id="7"></a>
### Working With Structs and Arrays

```
// create a New Person:
Person satoshi = Person(172, "Satoshi");

// Add that person to the Array:
people.push(satoshi);
```

It is also possible to do this in one line:
```
people.push(Person(16, "Vitalik"));
```

<a id="8"></a>
### Private / Public Functions

Here's how you can declare a private function:
```
uint[] numbers;

function _addToArray(uint _number) private {
  numbers.push(_number);
}
```
This means only other functions within our contract will be able to call this function and add to the numbers array.

<a id="9"></a>
### Return Values & Function Modifiers

#### Return Values
In Solidity, the function declaration contains the return type. Here's how you can declare a function to return its value:
```
string greeting = "What's up dog";

function sayHello() public returns (string memory) {
  return greeting;
}
```

#### Function Modifiers
Solidity has `view` and `pure` functions. A `view` function can only view the data but not modify it. Whereas, a `pure` function can neither access nor write data in the smart contract.

- `view` function declaration
```
function sayHello() public view returns (string memory) {
}
```

- `pure` function declaration
```
function _multiply(uint a, uint b) private pure returns (uint) {
  return a * b;
}
```

<a id="10"></a>
### Public Function

```
// SPDX-License-Identifier: GPL-3.0
pragma solidity >=0.8.2 <0.9.0;

contract RandomPokemonGenerator {

    // declare our event here

    uint dnaDigits = 16;
    uint dnaModulus = 10 ** dnaDigits;

    struct Pokemon {
        string name;
        uint dna;
    }

    Pokemon[] public pokemons;

    function _createPokemon(string memory _name, uint _dna) private {
        pokemons.push(Pokemon(_name, _dna));
        // and fire it here
    }

    function _generateRandomDna(string memory _str) private view returns (uint) {
        uint rand = uint(keccak256(abi.encodePacked(_str)));
        return rand % dnaModulus;
    }

    function createRandomPokemon(string memory _name) public {
        uint randDna = _generateRandomDna(_name);
        _createPokemon(_name, randDna);
    }

}
```

## Next Steps

Voila! Your Solidity Random Pokémon Generator smart contract is ready! Now we need to write a frontend using JS that can interacts with our contract. Ethereum has a JS library called Web3.js that allows you to do this. In part II, we will learn how to deploy a contract and set up [Web3.js](https://web3js.readthedocs.io/en/v1.3.4/).

Stay tuned for the next meetup and come learn more about Advanced Solidity in Part II of the workshop! :)
