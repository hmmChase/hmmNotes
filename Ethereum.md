# _Ethereum_

---

- Has a cryptocurrency similar to Bitcoin called Ether
- Its purpose is for decentralized contract development (smart contracts)
- Has a method for funding transactions depending on complexity, bandwidth use, and storage needs

---

# _DAPPS_

- Distributed Applications
- Also called smart contracts
- Data and logic is shared on the blockchain

---

# _Solidity_

- Programming language to create smart contracts
- OOP Language

## Data Types

- booleans
- strings
- integers
  - int / uint
  - The primary difference between int and uint (Unsigned Integer), is that int can hold negative numbers as values.
- address
- ufixed

## Access Modifiers

- Ensures your code can only be executed from where you expect
- Public
  - can be accessed everywhere
- Private
  - can only be accessed from this contract
- Internal
  - can be accessed by this contract and derived contracts from it
- External
  - disallows internal access and makes contract only accessible externally

## Structs

- Custom defined data types

```
struct Person
{
    unint age;
    bool isCool;
    address accountAddress;
}
```

- Structs can contain other structs

```
struct Parents
{
    Person father;
    Person mother;
}
```

## Enums

- Enumerated Types
- A List of a finite set of values
- `enum Sex {Male, Female, Non-Specified}`
- When you return an `enum`, it returns the integer value associated with it

## Arrays

- Data Structure for grouping elements
- The elements must be all the same data type
- `string[] names;`
- Can be fixed length
  - `Person[10] toTenAuthors`
- Assigned using the index of the element you want to access
  - topTenAuthors[3] = persons[5]

## Data locations

- For Structs and Arrays and Mappings
- Sets the location of the data
- Changes how assignments behave

* memory
  - Default for function and return parameters
* storage
  - Default for local variables
  - State variables are forced to storage
* calldata
  - Non-modifiable, non-persistent area where function arguments are stored
  - External functions and input parameters are forced to calldata

## Mapping Tables

- Table of values
- Hash tables with key types and value types
- Will map any type to the index of another type
- Common use is to map addresses to values
  - `mapping(address => uint) public balances`
- Access using type definition
  - `return balances[account.Address]`
- Similar to dictionaries in c#

## Selfdestruct

- Kills a contract
- The only way code is removed from the blockchain is by using selfdestruct
- `selfdestruct(msg.sender)`
- The remaining ether stored at the address is sent to the designated target and the storage code is removed from the state

## delete

- Deletes content
- `delete(objectArray);`
- A good way to clean up a contract by deleting all the stored data for a variable

## Exceptions

- Stops all operations and returns unspent ether
- If a condition check fails or something goes wrong in your code, use to stop all operations
- `throw();`

## Comments

- `// single line`
- `/* multi-line */`
- `/// @notice Natspec`

## Calling external functions

\*

## Misc

- Working with contracts should be asynchronous
- Writing data is called a transaction, whereas reading data is called a call

---

# _Gas_

- Payment model
- Protects the system from attacks
- Internal pricing for running transactions or contracts

### Effects of Startgas and Gasprice

- Too low
  - Startgas
    - Not sent to miners
  - Gasprice
    - No work done by miners
- Low
  - Startgas
    - Out-of-gas error
  - Gasprice
    - Mined slower
- Medium
  - Startgas
    - Ideal
  - Gasprice
    - Ideal
- High
  - Startgas
    - Delay in getting mined
  - Gasprice
    - Mined faster
- Too high
  - Startgas
    - Exceed block gas limit
  - Gasprice
    - Not sent to miners if sender is out funds

---

# _Transactions_

### Components

- Recipient
  - who the message is going to
- Signature
  - identifies the sender
- Value
  - the amount to send from the sender to the recipient
- Gasprice
  - the fee the sender is willing to pay for gas
  - the higher the fee, the higher miners will rank you
- Startgas
  - represents the maximum number of computational steps the transaction executed is allowed to take
  - makes sure you are not allowed to start infinite loops in your code
  - gives the miners an estimated of the amount they can earn for doing the transaction
- Message
  - Optional data field which can contain a message sent to a contract

---

# _Web3_

- Ethereum JavaScript API
- Makes RPC calls under the hood for us
- Works with Metamask, taking care of authentication

---

# _Truffle_

- Smart contract framework
- https://www.truffleframework.com/

## Features

- Compiles and builds
- Automated testing using Ganache
  - A local in-memory blockchain for testing
  - Implements ethereumJS
  - Creates 10 test accounts with private keys
- Deployment
- Console mode

## Install

- `npm install -g truffle`

## Setup

- `truffle init`
  - Creates a bare Truffle project with no smart contracts included
- `truffle develop`
  - Spawns a development blockchain locally on port `9545`
    - regardless of what your `truffle.js` configuration file calls for
  - Will create 10 accounts, 10 private keys, and a mnemonic seed
  - Enters truffle development console mode
- `truffle migrate` or `migrate` (in dev mode)
  - Runs all migrations located within your project's `migrations` directory
  - Deploys contract to test server
  - Migrations are simply a set of managed deployment scripts
  - If your migrations were previously run successfully, `truffle migrate` will start execution from the last migration that was run, running only newly created migrations
    - use `--reset` option to run all your migrations from the beginning

## _Consoles_

### Regular

### Development

- You can interact with your contract in the console using JavaScript
- The contract is referenced using the `deployed` keyword

- Create the handler

```
truffle(develop)> var hw
undefined
truffle(develop)> HelloWorld.deployed().then(function (deployed){hw=deployed;});
undefined
```

```
FoodSafe.deployed().then(function (retval){fs=retval;});
```

- Invoke the function

```
truffle(develop)> hw.SayHello.call()
'Hello World!'
```

## _Workflows_

### Webpack

- https://truffleframework.com/boxes/webpack
- `truffle unbox webpack`
- `truffle dev`
- `compile`
- `migrate`
- `ctrl+c` x 2
- `cd app`
- `npm run dev`

---
