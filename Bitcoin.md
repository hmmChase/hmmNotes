# _Bitcoin_

- https://bitcoincore.org/bin/
- https://fermatslibrary.com/s/bitcoin

---

# _Encryption_

- https://www.youtube.com/watch?v=PdGRmshPXdo

---

# _Digital Signatures_

- Mathematical mechanism to combine a public sequence of numbers with a digital message
- Certify a record with your signature in a way that isn't forgable
- A process that binds an identity to a message

## Steps:

- Alice wants to sign a message
  - she generates two sequences of numbers that have a mathematical relationship
    - signing key (sk)
      - private
    - verification key (vk)
      - public
  - It should be hard to figure out the sk if you see the vk \*
- To sign the message:
  - The message and the sk are input together into a mathematical equation
  - The output is another sequence of numbers which is the signature
- To verify the message was signed by Alice:
  - The message, signature, and vk are input together into a mathematical equation
  - The equation verifies that the signature that corresponds with the message is one that would be produced by the sk, and the sk in turn corresponds with the vk

* Elliptic Curve Exponentiation

---

# _Merkle Tree_

- A hash of hashes
- Data is hashed, then a group of hashes are hashed, then the groups of hashes are hashed into a root hash
- If any data has changed, the root hash will change
- The chain of blocks are stored and verified using a Merkle Tree

---

# _Fees_

- https://bitcoinfees.21.co/api/v1/fees/recommended
  - The API returns a JSON object with the current fee estimate for fastest confirmation (fastestFee), confirmation within three blocks (halfHourFee) and six blocks (hourFee), in satoshi per byte.

---

# _Nodes_

- https://www.reddit.com/r/Bitcoin/comments/7zqpth/why_running_a_node_is_important/

## _Hardware_

- https://store.casa/lightning-node/
- http://bitseed.org/
- https://getbitbox.io/
- https://lightning.farm/

### M5stack

- https://www.amazon.com/dp/B07DY9VC3X/ref=twister_B077Z1KVM3?_encoding=UTF8&psc=1

### Raspberry pi

- https://github.com/Stadicus/guides/tree/master/raspibolt
- https://github.com/rootzoll/raspiblitz

* MicroPython
  - https://www.raspberrypi.org/forums/viewtopic.php?t=191744
  - https://forum.micropython.org/viewtopic.php?t=3317
  - https://github.com/boochow/micropython-raspberrypi
* Harddrives
  - https://www.raspberrypi.org/forums/viewtopic.php?t=203732

## _Software_

### BTCPay Server

- https://www.reddit.com/r/Bitcoin/comments/9ksxd4/it_is_now_possible_to_deploy_btcpay_server_full/
- https://www.reddit.com/r/Bitcoin/comments/9o3btt/getting_started_with_btcpay_server_free_and_open/

### Opennode

- https://github.com/opennodedev/opennode-node

---

# _API's_

- https://p.nomics.com/cryptocurrency-bitcoin-api/

---

# _Data_

- https://statoshi.info/
- https://www.blockchain.com/btc/strange-transactions

---

# _Tutorials_

- https://www.youtube.com/watch?time_continue=2&v=H8Tl-6VfORE&t=44s
- https://www.youtube.com/watch?v=g6BhU-K-3ts&feature=youtu.be
- https://anders.com/blockchain/
- https://github.com/Stadicus/guides/
- https://medium.com/coinmonks/guide-setup-a-lightning-network-node-on-windows-8475206807f
- https://medium.com/andreas-tries-blockchain/bitcoin-lightning-network-1-can-i-compile-and-run-a-node-cd3138c68c15
- https://www.aclu.org/blog/privacy-technology/internet-privacy/edward-snowden-explains-blockchain-his-lawyer-and-rest-us

---

# Repos

- https://github.com/pointbiz/bitaddress.org
- https://github.com/iancoleman/bip39
- https://github.com/ShahanaFarooqui/RTL
- https://github.com/ValyrianTech/BitcoinSpellbook

---

# _Mastering Bitcoin_

## Introduction

1. What Is Bitcoin?
   1. A decentralized peer-to-peer network (the bitcoin protocol)
   2. A public transaction ledger (the blockchain)
   3. A set of rules for independent transaction validation and currency issuance (consensus rules)
   4. A mechanism for reaching global decentralized consensus on the valid blockchain (Proof-of-Work algorithm)
2. History of Bitcoin
3. Bitcoin Uses, Users, and Their Stories
4. Getting Started
   1. Full-node client
      1. A full client, or “full node,” is a client that stores the entire history of bitcoin transactions (every transaction by every user, ever), manages users’ wallets, and can initiate transactions directly on the bitcoin network. A full node handles all aspects of the protocol and can independently validate the entire blockchain and any transaction. A full-node client consumes substantial computer resources (e.g., more than 125 GB of disk, 2 GB of RAM) but offers complete autonomy and independent transaction verification
   2. Lightweight client
      1. A lightweight client, also known as a simple-payment-verification (SPV) client, connects to bitcoin full nodes (mentioned previously) for access to the bitcoin transaction information, but stores the user wallet locally and independently creates, validates, and transmits transactions. Lightweight clients interact directly with the bitcoin network, without an intermediary
   3. Bitcoin addresses start with a 1 or 3

## How Bitcoin Works

1. Transactions, Blocks, Mining, and the Blockchain
2. Bitcoin Transactions
   1. Transactions are like lines in a double-entry bookkeeping ledger. Each transaction contains one or more “inputs,” which are like debits against a bitcoin account. On the other side of the transaction, there are one or more “outputs,” which are like credits added to a bitcoin account
   2. Outputs add up to slightly less than inputs and the difference represents an implied transaction fee
   3. The transaction also contains proof of ownership for each amount of bitcoin (inputs) whose value is being spent
   4. “spending” is signing a transaction that transfers value from a previous transaction over to a new owner identified by a bitcoin address
   5. Transaction Chains
      1. Alice’s payment to Bob’s Cafe uses a previous transaction’s output as its input.
      2. Alice received bitcoin from her friend Joe in return for cash. That transaction created a bitcoin value locked by Alice’s key
      3. Her new transaction to Bob’s Cafe references the previous transaction as an input and creates new outputs to pay for the cup of coffee and receive change
      4. The transactions form a chain, where the inputs from the latest transaction correspond to outputs from previous transactions
      5. Alice’s key provides the signature that unlocks those previous transaction outputs, thereby proving to the bitcoin network that she owns the funds
      6. She attaches the payment for coffee to Bob’s address, thereby “encumbering” that output with the requirement that Bob produces a signature in order to spend that amount
      7. This represents a transfer of value between Alice and Bob
   6. Making Change
      1. Transaction inputs, like currency notes, cannot be divided
      2. If you purchased an item that costs 5 bitcoin but only had a 20 bitcoin input to use, you would send one output of 5 bitcoin to the store owner and one output of 15 bitcoin back to yourself as change
      3. The change address does not have to be the same address as that of the input and for privacy reasons is often a new address from the owner’s wallet
      4. Transactions move value from transaction inputs to transaction outputs
      5. An input is a reference to a previous transaction’s output, showing where the value is coming from
      6. A transaction output directs a specific value to a new owner’s bitcoin address and can include a change output back to the original owner
      7. Outputs from one transaction can be used as inputs in a new transaction, thus creating a chain of ownership as the value is moved from owner to owner
   7. Common Transaction
      1. The most common form of transaction is a simple payment from one address to another, which often includes some “change” returned to the original owner
   8. Transaction aggregating funds
      1. Another common form of transaction is one that aggregates several inputs into a single output
      2. This represents the real-world equivalent of exchanging a pile of coins and currency notes for a single larger note
   9. Transaction distributing funds
      1. Finally, another transaction form that is seen often on the bitcoin ledger is a transaction that distributes one input to multiple outputs representing multiple recipients
      2. This type of transaction is sometimes used by commercial entities to distribute funds, such as when processing payroll payments to multiple employees
3. Constructing a Transaction
   1. Getting the Right Inputs
      1. Alice’s wallet application will first have to find inputs that can pay for the amount she wants to send to Bob
      2. Most wallets keep track of all the available (unspent) outputs belonging to addresses in the wallet
      3. A full-node client actually contains a copy of every unspent output from every transaction in the blockchain
      4. Most user wallets run “lightweight” clients that track only the user’s own unspent outputs
   2. Creating the Outputs
      1. A transaction output is created in the form of a script that creates an encumbrance on the value and can only be redeemed by the introduction of a solution to the script
         1. In simpler terms, Alice’s transaction output will contain a script that says something like, “This output is payable to whoever can present a signature from the key corresponding to Bob’s public address.”
         2. Because only Bob has the wallet with the keys corresponding to that address, only Bob’s wallet can present such a signature to redeem this output
         3. Alice will therefore “encumber” the output value with a demand for a signature from Bob
      2. This transaction will also include a second output, because Alice’s funds are in the form of a 0.10 BTC output, too much money for the 0.015 BTC cup of coffee
         1. Alice will need 0.085 BTC in change
         2. Alice’s change payment is created by Alice’s wallet as an output in the very same transaction as the payment to Bob
         3. She can then use (spend) the change output in a subsequent transaction
      3. Finally, Alice’s wallet application will add a small fee.
         1. This is not explicit in the transaction; it is implied by the difference between inputs and outputs.
         2. If instead of taking 0.085 in change, Alice creates only 0.0845 as the second output
         3. There will be 0.0005 BTC transaction fee that is collected by the miner as a fee for validating and including the transaction in a block to be recorded on the blockchain
   3. Transmitting the transaction
      1. Any system, such as a server, desktop application, or wallet, that participates in the bitcoin network by “speaking” the bitcoin protocol is called a bitcoin node
      2. Alice’s wallet application can send the new transaction to any bitcoin node it is connected to
      3. Any bitcoin node that receives a valid transaction it has not seen before will immediately forward it to all other nodes to which it is connected
      4. A propagation technique known as flooding
      5. The transaction will reach Bob’s wallet within a few seconds
      6. Bob’s wallet will immediately identify Alice’s transaction as an incoming payment because it contains outputs redeemable by Bob’s keys
      7. Bob’s wallet application can also independently verify that the transaction is well formed, uses previously unspent inputs, and contains sufficient transaction fees to be included in the next block
4. Bitcoin Mining
   1. Transactions do not become part of the blockchain until it is verified and included in a block by a process called mining
   2. Transactions are bundled into blocks, which require an enormous amount of computation to prove, but only a small amount of computation to verify as proven.
   3. The mining process serves two purposes in bitcoin:
      1. Mining nodes validate all transactions by reference to bitcoin’s consensus rules. Therefore, mining provides security for bitcoin transactions by rejecting invalid or malformed transactions
      2. Mining creates new bitcoin in each block, almost like a central bank printing new money. The amount of bitcoin created per block is limited and diminishes with time, following a fixed issuance schedule
   4. Mining computers compete against thousands of similar systems in a global race to find a solution to a block of transactions
   5. Finding such a solution, the so-called Proof-of-Work (PoW), involves repeatedly hashing the header of the block and a random number with the SHA256 cryptographic algorithm until a solution matching a predetermined pattern emerges
   6. The first miner to find such a solution wins the round of competition and publishes that block into the blockchain
5. Mining Transactions in Blocks
   1. New transactions are constantly flowing into the network from user wallets and other applications. As these are seen by the bitcoin network nodes, they get added to a temporary pool of unverified transactions maintained by each node. As miners construct a new block, they add unverified transactions from this pool to the new block
   2. Each miner starts the process of mining a new block of transactions as soon as he receives the previous block from the network, knowing he has lost that previous round of competition. He immediately creates a new block, fills it with transactions and the fingerprint of the previous block, and starts calculating the Proof-of-Work for the new block
   3. Each miner includes a special transaction in his block, one that pays his own bitcoin address the block reward (currently 12.5 newly created bitcoin) plus the sum of transaction fees from all the transactions included in the block. If he finds a solution that makes that block valid, he “wins” this reward because his successful block is added to the global blockchain and the reward transaction he included becomes spendable
   4. In a mining pool, the reward is assigned to a pool address. From there, a share of the reward is distributed to other miners in proportion to the amount of work they contributed in the last round
   5. Alice’s transaction was picked up by the network and included in the pool of unverified transactions. Once validated by the mining software it was included in a new block, called a candidate block, generated by a mining pool. All the miners participating in that mining pool immediately start computing Proof-of-Work for the candidate block. Approximately five minutes after the transaction was first transmitted by Alice’s wallet, one of the miners found a solution for the candidate block and announced it to the network. Once other miners validated the winning block they started the race to generate the next block
   6. The winning block containing Alice’s transaction is counted as one “confirmation” of that transaction
   7. As the blocks pile on top of each other, the “height” in blocks increases, as does the computation difficulty for each block and the chain as a whole
6. Spending the Transaction
   1. Now that Alice’s transaction has been embedded in the blockchain as part of a block, it is part of the distributed ledger of bitcoin and visible to all bitcoin applications
   2. Full-node clients can track the source of the funds from the moment the bitcoin were first generated in a block, incrementally from transaction to transaction, until they reach Bob’s address
   3. Lightweight clients can do what is called a simplified payment verification (SPV) by confirming that the transaction is in the blockchain and has several blocks mined after it, thus providing assurance that the miners accepted it as valid
   4. Bob can now spend the output from this and other transactions

## Bitcoin Core: The Reference Implementation

1. Bitcoin Development Environment
2. Compiling Bitcoin Core from the Source Code
3. Running a Bitcoin Core Node
   1. `bitcoind —help`
      1. view configuration options that modify the behavior of the network node
   2. `bitcoind -printtoconsole`
      1. run in the foreground with output to the console
   3. `bitcoind -daemon`
      1. run in the background as a process
   4. Password
      1. Create a file inside the .bitcoin directory (under your user’s home directory) so that it is named .bitcoin/bitcoin.conf and provide a username and password:
      2. rpcuser=bitcoinrpc
      3. rpcpassword=CHANGE_THIS
   5. Common Options
      1. `alertnotify`
         1. Run a specified command or script to send emergency alerts to the owner of this node, usually by email.
      2. `conf`
         1. An alternative location for the configuration file.
         2. This only makes sense as a command-line parameter to bitcoind, as it can’t be inside the configuration file it refers to.
      3. `datadir`
         1. Select the directory and filesystem in which to put all the blockchain data.
         2. By default this is the .bitcoin subdirectory of your home directory.
         3. Make sure this filesystem has several gigabytes of free space.
      4. `prune`
         1. Reduce the disk space requirements to this many megabytes, by deleting old blocks.
         2. Use this on a resource-constrained node that can’t fit the full blockchain.
      5. `txindex`
         1. Maintain an index of all transactions.
         2. This means a complete copy of the blockchain that allows you to programmatically retrieve any transaction by ID.
         3. By default, Bitcoin Core builds a database containing only the transactions related to the user’s wallet.
      6. `maxconnections`
         1. Set the maximum number of nodes from which to accept connections.
         2. Reducing this from the default will reduce your bandwidth consumption.
         3. Use if you have a data cap or pay by the gigabyte.
      7. `maxmempool`
         1. Limit the transaction memory pool to this many megabytes.
         2. Use it to reduce memory use of the node.
      8. `maxreceivebuffer`/`maxsendbuffer`
         1. Limit per-connection memory buffer to this many multiples of 1000 bytes.
         2. Use on memory-constrained nodes.
      9. `minrelaytxfee`
         1. Set the minimum fee transaction you will relay.
         2. Below this value, the transaction is treated as zero fee.
         3. Use this on memory-constrained nodes to reduce the size of the in-memory transaction pool.
   6. .bitcoin/bitcoin.conf:

```
// fully indexed node, running as an API backend for a bitcoin application
alertnotify=myemailscript.sh "Alert: %s"
datadir=/lotsofspace/bitcoin
txindex=1
rpcuser=bitcoinrpc
rpcpassword=CHANGE_THIS
```

```
// resource-constrained node running on a smaller server
alertnotify=myemailscript.sh "Alert: %s"
maxconnections=15
prune=5000
minrelaytxfee=0.0001
maxmempool=200
maxreceivebuffer=2500
maxsendbuffer=500
rpcuser=bitcoinrpc
rpcpassword=CHANGE_THIS
```

    1. Bitcoin Core Application Programming Interface (API)
        1. The Bitcoin Core client implements a JSON-RPC interface that can also be accessed using the command-line helper `bitcoin-cli`
            1. `bitcoin-cli help`
                1. a list of the available bitcoin RPC commands
                2. To get additional help, a detailed description, and information on the parameters, add the command name after help
            2. `bitcoin-cli getinfo`
                1. monitor the progress and runtime status of your bitcoin node
                2. displays basic information about the status of the bitcoin network node, the wallet, and the blockchain database
            3. `bitcoin-cli getrawtransaction <TRANSACTION ID>`
                1. returns a serialized transaction in hexadecimal notation
            4. `bitcoin-cli decoderawtransaction <TRANSACTION HEX DATA>`
                1. decodes `getrawtransaction`
                    1. pass the hex data as a parameter
                2. shows all the components of this transaction, including the transaction inputs and outputs
            5. Blocks can be referenced either by the block height or by the block hash
            6. `bitcoin-cli getblockhash <BLOCK HEIGHT>`
                1. returns the block hash for that block
            7. `bitcoin-cli getblock <BLOCK HASH>`
                1. returns info for that block
            8. `bitcoin-cli getnewaddress`
                1. generate a new key pair
                2. for security reasons it displays the public key only
            9. `bitcoin-cli dumpprivkey <PUBLIC KEY>`
                1. shows the private key in a Base58 checksum-encoded format called the Wallet Import Format (WIF)
        2. Remote Procedure Call (RPC)
            1. Calls procedures (functions) that are remote (on the Bitcoin Core node) via a network protocol
            2. Use `bitcoin-cli help <COMMAND>` to show an example call using curl
    2. Alternative Clients, Libraries, and Toolkits
        1. Python
            1. python-bitcoinlib
                1. A Python bitcoin library, consensus library, and node by Peter Todd
            2. pycoin
                1. A Python bitcoin library by Richard Kiss
            3. pybitcointools
                1. A Python bitcoin library by Vitalik Buterin
        2. JavaScript
            1. bcoin
                1. A modular and scalable full-node implementation with API
            2. Bitcore
                1. Full node, API, and library by Bitpay
            3. BitcoinJS
                1. A pure JavaScript Bitcoin library for node.js and browsers

// fully indexed node, running as an API backend for a bitcoin application
alertnotify=myemailscript.sh "Alert: %s"
datadir=/lotsofspace/bitcoin
txindex=1
rpcuser=bitcoinrpc
rpcpassword=CHANGE_THIS
// fully indexed node, running as an API backend for a bitcoin application
alertnotify=myemailscript.sh "Alert: %s"
datadir=/lotsofspace/bitcoin
txindex=1
rpcuser=bitcoinrpc
rpcpassword=CHANGE_THIS

## Keys, Addresses

1. Introduction
   1. Asymmetric cryptography is used to prove knowledge of a secret without revealing that secret (digital signature), or prove the authenticity of data (digital fingerprint)
      1. The useful property of asymmetric cryptography is the ability to generate digital signatures
      2. A private key can be applied to the digital fingerprint of a transaction to produce a numerical signature
      3. This signature can only be produced by someone with knowledge of the private key
      4. However, anyone with access to the public key and the transaction fingerprint can use them to verify the signature
   2. Public key cryptography is used to create a key pair that controls access to bitcoin
   3. Ownership of bitcoin is established through digital keys, bitcoin addresses, and digital signatures
   4. Keys
      1. The key pair consists of a private (secret) key and—derived from it—a unique public key
      2. Both private and public keys can be represented in a number of different formats
      3. Public key
         1. Used to receive funds
         2. Similar to a bank account number
         3. A public key is a point (x,y) on an elliptic curve
         4. Calculated from the private key using elliptic curve multiplication (secp256k1), a one-way cryptographic function
            1. public key (K) = private key (k) \* generator point (G)
            2. G is a constant point (x,y) on an elliptic curve
         5. Usually presented as either compressed or uncompressed public keys.
      4. Private key
         1. Used to create signatures that are required to spend bitcoin by proving ownership of funds used in a transaction
         2. Similar to the secret PIN, or signature on a check, that provides control over the account
         3. A 256-bit number, generated from a cryptographically secure pseudorandom number generator (CSPRNG)
         4. Hexadecimal and raw binary formats are used internally in software and rarely shown to users
         5. WIF is used for import/export of keys between wallets and often used in QR code (barcode) representations of private keys
   5. Signature
      1. There is a mathematical relationship between the public and the private key that allows the private key to be used to generate signatures on messages.
      2. This signature can be validated against the public key without revealing the private key.
      3. Most bitcoin transactions requires a valid digital signature to be included in the blockchain, which can only be generated with a secret key.
         1. Anyone with a copy of that key has control of the bitcoin.
         2. The digital signature used to spend funds is also referred to as a witness.
         3. The witness data in a bitcoin transaction testifies to the true ownership of the funds being spent.
   6. Address
      1. In the payment portion of a bitcoin transaction, the recipient’s public key is represented by its digital fingerprint, called a bitcoin address, which is used in the same way as the beneficiary name on a check
         1. (i.e., “Pay to the order of”).
         2. In most cases, a bitcoin address is generated from and corresponds to a public key.
         3. They can also represent other beneficiaries such as scripts.
   7. Summary
      1. The private key is a number, usually picked at random
      2. From the private key, we use elliptic curve multiplication to generate a public key.
      3. From the public key, we use a one-way cryptographic hash function to generate a bitcoin address.
      4. When spending bitcoin, the current bitcoin owner presents her public key and a signature (different each time, but created from the same private key) in a transaction to spend those bitcoin.
      5. Through the presentation of the public key and signature, everyone in the bitcoin network can verify and accept the transaction as valid, confirming that the person transferring the bitcoin owned them at the time of the transfer.
2. Bitcoin Addresses
   1. A string of digits and characters that can be shared with anyone who wants to send you money.
   2. Addresses produced from public keys begin with the digit “1.”
      1. pay-to-public-key-hash (P2PKH)
   3. The algorithms used to make a bitcoin address from a public key are:
      1. the Secure Hash Algorithm (SHA)
      2. RACE Integrity Primitives Evaluation Message Digest (RIPEMD)
      3. specifically SHA256 and RIPEMD160.
   4. Starting with the public key, we compute the SHA256 hash and then compute the RIPEMD160 hash of the result, producing a 160-bit (20-byte) number.
   5. Then, Bitcoin addresses are almost always encoded as “Base58Check”, which uses 58 characters (a Base58 number system) and a checksum, to help human readability, avoid ambiguity, and protect against errors in address transcription and entry.
      1. Base58 is Base64 without the 0 (number zero), O (capital o), l (lower L), I (capital i), and the symbols “+” and “/”.
      2. Base58Check is also used in many other ways in bitcoin, such as a private key, an encrypted key, or a script hash.

| Type                         | Version prefix (hex) | Base58 result prefix |
| ---------------------------- | -------------------- | -------------------- |
| Bitcoin Address              | 0x00                 | 1                    |
| ---                          | ---                  | ---                  |
| Pay-to-Script-Hash Address   | 0x05                 | 3                    |
| Bitcoin Testnet Address      | 0x6F                 | m or n               |
| Private Key WIF              | 0x80                 | 5, K, or L           |
| BIP-38 Encrypted Private Key | 0x0142               | 6P                   |
| BIP-32 Extended Public Key   | 0x0488B21E           | xpub                 |

1. Implementing Keys and Addresses in Python
2. Advanced Keys and Addresses
   1. Encrypted Private Keys (BIP-38)
      1. A common standard for encrypting private keys with a passphrase and encoding them with Base58Check
      2. The standard for encryption uses the Advanced Encryption Standard (AES)
      3. Takes as input a bitcoin private key, usually encoded in the WIF, as a Base58Check string with the prefix of “5.”
      4. Additionally, it takes a passphrase—a long password—usually composed of several words or a complex string of alphanumeric characters.
      5. The result is a Base58Check-encoded encrypted private key that begins with the prefix 6P.
      6. If you see a key that starts with 6P, it is encrypted and requires a passphrase in order to convert (decrypt) it back into a WIF-formatted private key (prefix 5) that can be used in any wallet.
   2. Pay-to-Script Hash (P2SH) (BIP-16)
      1. Addresses that begin with the number “3.”
      2. They designate the beneficiary of a bitcoin transaction as the hash of a script, instead of the owner of a public key.
      3. The spending requirements are designated at the time the address is created, within the script, and all inputs to this address will be encumbered with the same requirements.
      4. The most common implementation of the P2SH function is the multi-signature address script
         1. The underlying script requires more than one signature to prove ownership and therefore spend funds.
         2. The bitcoin multi-signature feature is designed to require M signatures (also known as the “threshold”) from a total of N keys, known as an M-of-N multisig, where M is equal to or less than N.
   3. Vanity Addresses
      1. Addresses that contain human-readable messages.
      2. The process essentially involves picking a private key at random, deriving the public key, deriving the bitcoin address, and checking to see if it matches the desired vanity pattern, repeating billions of times until a match is found.

## Wallets

1. Wallet Technology Overview
   1. A wallet is an application that serves as the primary user interface.
   2. It controls access to a user’s money, managing keys and addresses, tracking the balance, and creating and signing transactions
   3. Wallets are really keychains containing pairs of private/public keys
   4. There are two primary types of wallets, distinguished by whether the keys they contain are related to each other or not.
2. Nondeterministic
   1. Each key is independently generated from a random number.
   2. The keys are not related to each other.
   3. The disadvantage is that each key must be backed up, or the funds it controls are irrevocably lost if the wallet becomes inaccessible
3. Deterministic
   1. All the keys are derived from a single master key, known as the seed.
      1. The seed is a randomly generated number that is combined with other data, such as an index number or “chain code”
      2. Private keys are all derived from the seed through the use of a one-way hash function.
   2. All the keys in this type of wallet are related to each other and can be generated again if one has the original seed.
   3. There are a number of different key derivation methods used in deterministic wallets.
      1. The most commonly used derivation method uses a tree-like structure and is known as a hierarchical deterministic or HD wallet.
   4. Seeds are encoded as English words, also known as mnemonic code words.
4. Hierarchical Deterministic (HD) Wallets (BIP-32)
   1. HD wallets contain keys derived in a tree structure, such that a parent key can deterministically derive a sequence of children keys, each of which can derive a sequence of grandchildren keys, and so on.
   2. The tree structure can be used to express additional organizational meaning, such as when a specific branch of subkeys is used to receive incoming payments and a different branch is used to receive change from outgoing payments.
   3. The second advantage of HD wallets is that users can create a sequence of public keys without having access to the corresponding private keys.
      1. This allows HD wallets to be used on an insecure server or in a receive-only capacity, issuing a different public key for each transaction.
      2. The public keys do not need to be preloaded or derived in advance, yet the server doesn’t have the private keys that can spend the funds.
   4. The process of creating the master keys and master chain code:
      1. The root seed is input into the HMAC-SHA512 algorithm and the resulting hash is used to create a master private key and a master chain code.
      2. The master private key then generates a corresponding master public key using the normal elliptic curve multiplication process.
      3. The chain code is used to introduce entropy in the function that creates child keys from parent keys.
   5. Private child key derivation
      1. HD wallets use a child key derivation (CKD) function to derive child keys from parent keys.
         1. The child key derivation functions are based on a one-way hash function that combines:
            1. A parent private or public key (ECDSA uncompressed key)
            2. A seed called a chain code (256 bits)
            3. An index number (32 bits)
         2. These three items (parent key, chain code, and index) are combined and hashed to generate children keys.
   6. Using derived child keys
      1. Child private keys are indistinguishable from nondeterministic (random) keys.
      2. The child key cannot be used to find any parent or sibling keys.
      3. Without the child chain code, the child key cannot be used to derive any grandchildren either.
   7. Hardened child key derivation
      1. If a child private key is known, or somehow leaked, it can be used with the chain code to derive all the other child private keys.
      2. To counter this risk, HD wallets use an alternative derivation function called hardened derivation, which “breaks” the relationship between parent public key and child chain code.
      3. The index number for hardened children is displayed starting from zero, but with a prime symbol.
         1. When you see an HD wallet index i', that means 2^31+i.
   8. Extended keys
      1. Think of an extended key as the root of a branch in the tree structure of the HD wallet.
         1. With the root of the branch, you can derive the rest of the branch.
      2. There are two types of extended keys:
         1. Extended private key is the combination of a private key and chain code
            1. Can be used to derive child private keys (and from them, child public keys).
         2. Extended public key (XPUB) is a public key and chain code, which can be used to create child public keys (public only)
      3. The extended private key can create a complete branch, whereas the extended public key can only create a branch of public keys.
      4. Can be used to create a very secure public key–only deployments where a server or application has a copy of an extended public key and no private keys whatsoever.
         1. This kind of deployment can produce an infinite number of public keys and bitcoin addresses, but cannot spend any of the money sent to those addresses.
         2. Meanwhile, on another, more secure server, the extended private key can derive all the corresponding private keys to sign transactions and spend the money.
   9. HD wallet key identifier (path)
      1. Keys in an HD wallet are identified using a “path” naming convention.
      2. Each level of the tree separated by a slash (/) character.
      3. Private keys derived from the master private key start with “m.”
      4. Public keys derived from the master public key start with “M.”
      5. The “ancestry” of a key is read from right to left, until you reach the master key from which it was derived.
         1. The first child private key of the master private key is m/0.
         2. The first child public key is M/0.
         3. M/23/17/0/0
            1. The first great-great-grandchild public key of the first great-grandchild of the 18th grandchild of the 24th child
5. Seeds and Mnemonic Codes (BIP-39)
   1. Mnemonic code words are word sequences that represent (encode) a random number used as a seed to derive a deterministic wallet.
   2. The sequence of words is sufficient to re-create the seed and from there re-create the wallet and all the derived keys.
   3. Optional passphrase
      1. BIP-39 standard allows the use of an optional passphrase in the derivation of the seed.
      2. Creates two important features:
         1. A second factor (something memorized) that makes a mnemonic useless on its own, protecting mnemonic backups from compromise by a thief.
         2. A form of plausible deniability or “duress wallet,” where a chosen passphrase leads to a wallet with a small amount of funds used to distract an attacker from the “real” wallet that contains the majority of funds.
6. Multipurpose HD wallet structure (BIP-43)
   1. Proposes the use of the first hardened child index as a special identifier that signifies the “purpose” of the tree structure.
   2. An HD wallet should use only one level-1 branch of the tree, with the index number identifying the structure and namespace of the rest of the tree by defining its purpose.
7. Multicurrency and multiaccount wallets (BIP-44)
   1. Proposes a multiaccount structure as “purpose” number 44' under BIP-43.
   2. All HD wallets following the BIP-44 structure are identified by the fact that they only used one branch of the tree: m/44'/.
   3. Specifies the structure as consisting of five predefined tree levels:
      1. m / purpose' / coin_type' / account' / change / address_index
   4. The first-level is “purpose”.
      1. Always set to 44'.
   5. The second-level is “coin_type”.
      1. Specifies the type of cryptocurrency coin, allowing for multicurrency HD wallets.
      2. There are three currencies defined for now:
      3. Bitcoin is m/44'/0'
      4. Bitcoin Testnet is m/44'/1'
      5. and Litecoin is m/44'/2'.
   6. The third level is “account”.
      1. Allows users to subdivide their wallets into separate logical subaccounts, for accounting or organizational purposes.
      2. For example, an HD wallet might contain two bitcoin “accounts”: m/44'/0'/0' and m/44'/0'/1'.
         1. Each account is the root of its own subtree.
   7. The fourth level is “change”.
      1. It has two subtrees, one for creating receiving addresses and one for creating change addresses.
      2. Note that whereas the previous levels used hardened derivation, this level uses normal derivation.
         1. This is to allow this level of the tree to export extended public keys for use in a nonsecured environment.
   8. The fifth level is “address_index”.
      1. Usable addresses are derived by the HD wallet as children of the fourth level
      2. M/44'/0'/3'/1/14
         1. The fifteenth change-address public key for the fourth bitcoin account.
      3. m/44'/2'/0'/0/1
         1. The second private key in the Litecoin main account, for signing transactions.
8. Wallet Technology Details

## Transactions

1. Introduction
   1. Everything in bitcoin is designed to ensure that transactions can be created, propagated on the network, validated, and finally added to the global ledger of transactions (blockchain).
   2. Transactions are data structures that encode the transfer of value between participants in the bitcoin system.
2. Transactions in Detail
   1. Raw Transaction:

```
{
  "version": 1,
  "locktime": 0,
  "vin": [
    {
      "txid": "7957a35fe64f80d234d76d83a2a8f1a0d8149a41d81de548f0a65a8a999f6f18",
      "vout": 0,
      "scriptSig": "3045022100884d142d86652a3f47ba4746ec719bbfbd040a570b1deccbb6498c75c4ae24cb02204b9f039ff08df09cbe9f6addac960298cad530a863ea8f53982c09db8f6e3813[ALL] 0484ecc0d46f1918b30928fa0e4ed99f16a0fb4fde0735e7ade8416ab9fe423cc5412336376789d172787ec3457eee41c04f4938de5cc17b4a10fa336a8d752adf",
      "sequence": 4294967295
    }
  ],
  "vout": [
    {
      "value": 0.01500000,
      "scriptPubKey": "OP_DUP OP_HASH160 ab68025513c3dbd2f7b92a94e0581f5d50f654e7 OP_EQUALVERIFY OP_CHECKSIG"
    },
    {
      "value": 0.08450000,
      "scriptPubKey": "OP_DUP OP_HASH160 7f9b1a7fb68d60c536c2fd8aeaa53a8f3cc025a8 OP_EQUALVERIFY OP_CHECKSIG"
    }
  ]
}
```

1. Transaction Outputs and Inputs
   1. The fundamental building block of a bitcoin transaction is a transaction output.
   2. A transaction consumes previously recorded unspent transaction outputs and creates new transaction outputs that can be consumed by a future transaction.
   3. This way, chunks of bitcoin value move forward from owner to owner in a chain of transactions consuming and creating UTXO.
   4. Outputs are indivisible chunks of bitcoin currency, recorded on the blockchain, and recognized as valid by the entire network.
   5. A transaction output can have a value denominated as a multiple of satoshis down to eight decimal places.
   6. Bitcoin full nodes track all available and spendable outputs, known as unspent transaction outputs, or UTXO.
   7. The collection of all UTXO is known as the UTXO set and currently numbers in the millions of UTXO.
   8. Every transaction represents a change (state transition) in the UTXO set.
   9. When a wallet has “received” bitcoin, it means that the wallet has detected a UTXO that can be spent with one of the keys controlled by that wallet.
   10. A wallet’s “balance” is the sum of all UTXO's that the wallet can spend.
   11. If an UTXO is larger than the desired value of a transaction, it must still be consumed in its entirety and change must be generated in the transaction.
   12. The user’s wallet will typically select from the user’s available UTXO to compose an amount greater than or equal to the desired transaction amount.
   13. The exception to the output and input chain is a special type of transaction called the coinbase transaction.
       1. It's the first transaction in each block.
       2. This transaction is placed there by the “winning” miner and creates brand-new bitcoin payable to that miner as a reward for mining.
       3. This special coinbase transaction does not consume UTXO; instead, it has a special type of input called the “coinbase.”
2. Transaction Outputs
   1. Every bitcoin transaction creates outputs, which are recorded on the bitcoin ledger.
   2. Almost all of these outputs, with one exception (“Data Recording Output (RETURN)”) create spendable chunks of bitcoin called UTXO.
   3. UTXO are tracked by every full-node bitcoin client in the UTXO set.
   4. New transactions consume (spend) one or more of these outputs from the UTXO set.
   5. Transaction outputs consist of two parts:
      1. An amount of bitcoin, denominated in satoshis, the smallest bitcoin unit.
      2. A cryptographic puzzle that determines the conditions required to spend the output.
         1. Also known as a locking script, a witness script, or a scriptPubKey.
   6. In the JSON encoding, the outputs are in an array named vout.
      1. The second part of each output is the cryptographic puzzle that sets the conditions for spending.

```
"vout": [
  {
    "value": 0.01500000,
    "scriptPubKey": "OP_DUP OP_HASH160 ab68025513c3dbd2f7b92a94e0581f5d50f654e7 OP_EQUALVERIFY OP_CHECKSIG"
  },
  {
    "value": 0.08450000,
    "scriptPubKey": "OP_DUP OP_HASH160 7f9b1a7fb68d60c536c2fd8aeaa53a8f3cc025a8 OP_EQUALVERIFY OP_CHECKSIG",
  }
]
```

1. Transaction Inputs
   1. Transaction inputs identify (by reference) which UTXO will be consumed and provide proof of ownership through an unlocking script.
   2. To build a transaction, a wallet selects from the UTXO's it controls, UTXO's with enough value to make the requested payment.
   3. For each UTXO that will be consumed to make this payment, the wallet creates one input pointing to the UTXO and unlocks it with an unlocking script.
   4. The input contains four elements:
      1. A transaction ID, referencing the transaction hash recorded in the blockchain that contains the UTXO being spent.
      2. An output index (vout), identifying which UTXO from that transaction is referenced.
         1. The first one is zero.
      3. A scriptSig, which satisfies the conditions placed on the UTXO, unlocking it for spending
         1. An unlocking script, which the wallet constructs in order to satisfy the spending conditions set in the UTXO.
         2. The unlocking script is constructed by first retrieving the referenced UTXO, examining its locking script, and then using it to build the necessary unlocking script to satisfy it.
         3. Most often, the unlocking script is a digital signature and public key proving ownership of the bitcoin.
         4. Not all unlocking scripts contain signatures.
      4. A sequence number

```
"vin": [
  {
    "txid": "7957a35fe64f80d234d76d83a2a8f1a0d8149a41d81de548f0a65a8a999f6f18",
    "vout": 0,
    "scriptSig": "3045022100884d142d86652a3f47ba4746ec719bbfbd040a570b1deccbb6498c75c4ae24cb02204b9f039ff08df09cbe9f6addac960298cad530a863ea8f53982c09db8f6e3813[ALL] 0484ecc0d46f1918b30928fa0e4ed99f16a0fb4fde0735e7ade8416ab9fe423cc5412336376789d172787ec3457eee41c04f4938de5cc17b4a10fa336a8d752adf",
    "sequence": 4294967295
  }
]
```

    1. Transactions on their own seem incomplete because they lack context.
    2. They reference UTXO in their inputs but without retrieving that UTXO we cannot know the value of the inputs or their locking conditions.
    3. To find this information, the wallet needs to retrieve the UTXO referenced in the inputs.
        1. Once this transaction is broadcast to the network, every validating node will also need to retrieve the UTXO referenced in the transaction inputs in order to validate the transaction.

1. Transaction serialization
   1. When transactions are transmitted over the network or exchanged between applications, they are serialized.
   2. Serialization is the process of converting the internal representation of a data structure into a format that can be transmitted one byte at a time.
      1. Also known as a byte stream.
   3. For convenience and readability, bitcoin libraries store transactions internally in data structures.
   4. The process of converting from the byte-stream representation of a transaction to a library’s internal representation data structure is called deserialization or transaction parsing.
2. Transaction Fees
   1. Transaction fees serve as an incentive to include (mine) a transaction into the next block.
   2. They also serve as a disincentive against abuse of the system by imposing a small cost on every transaction, making it economically infeasible for attackers to flood the network with transactions.
   3. Transaction fees are collected by the miner who mines the block that records the transaction on the blockchain.
   4. Transaction fees are calculated based on the size of the transaction in kilobytes, not the value of the transaction in bitcoin.
      1. Fee estimation algorithms calculate the appropriate fee, based on capacity and the fees offered by “competing” transactions.
   5. Transaction fees are not mandatory, and transactions without fees might be processed eventually; however, including transaction fees encourages priority processing.
   6. In Bitcoin Core, fee relay policies are set by the minrelaytxfee option.
      1. The current default minrelaytxfee is 0.00001 bitcoin or a hundredth of a millibitcoin per kilobyte.
      2. Therefore, by default, transactions with a fee less than 0.0001 bitcoin are treated as free and are only relayed if there is space in the mempool; otherwise, they are dropped.
      3. Bitcoin nodes can override the default fee relay policy by adjusting the value of minrelaytxfee.
   7. The data structure of transactions does not have a field for fees.
      1. Instead, any excess amount that remains after all outputs have been deducted from all inputs is the fee that is collected by the miners:
      2. `Fees = Sum(Inputs) – Sum(Outputs)`
      3. If you forget to add a change output in a manually constructed transaction, you will be paying the change as a transaction fee.
3. Transaction Scripts and Script Language
   1. The bitcoin transaction script language, called Script, is a Forth-like reverse-polish notation stack-based execution language.
   2. Both the locking script placed on a UTXO and the unlocking script are written in this scripting language.
   3. When a transaction is validated, the unlocking script in each input is executed alongside the corresponding locking script to see if it satisfies the spending condition.
   4. Locking scripts can be written to express a vast variety of complex conditions.
   5. Script contains many operators, but is deliberately limited.
      1. There are no loops or complex flow control capabilities other than conditional flow control.
      2. It's stateless, in that there is no state prior to execution of the script, or state saved after execution of the script.
4. Script Construction (Lock + Unlock)
   1. Bitcoin’s transaction validation engine relies on two types of scripts to validate transactions:
      1. A locking script and an unlocking script.
   2. A locking script is a spending condition placed on an output.
      1. It specifies the conditions that must be met to spend the output in the future.
      2. Known as a scriptPubKey, locking script, witness script, or cryptographic puzzle.
   3. An unlocking script is a script that “solves,” or satisfies, the conditions placed on an output by a locking script and allows the output to be spent.
      1. Unlocking scripts are part of every transaction input.
      2. Most of the time they contain a digital signature produced by the user’s wallet from his or her private key.
      3. Known as a scriptSig, unlocking script, or witness.
   4. Every bitcoin validating node will validate transactions by executing the locking and unlocking scripts together.
      1. Each input contains an unlocking script and refers to a previously existing UTXO.
      2. The validation software will copy the unlocking script, retrieve the UTXO referenced by the input, and copy the locking script from that UTXO.
      3. The unlocking and locking script are then executed in sequence.
      4. The input is valid if the unlocking script satisfies the locking script conditions.
      5. All the inputs are validated independently, as part of the overall validation of the transaction.
   5. A valid transaction that correctly satisfies the conditions of the output results in the output being considered as “spent” and removed from the set of unspent transaction outputs (UTXO set).
5. The script execution stack
   1. Bitcoin’s scripting language is called a stack-based language because it uses a data structure called a stack.
   2. A stack is a very simple data structure that can be visualized as a stack of cards.
      1. Also called a Last-In-First-Out, or “LIFO” queue.
   3. A stack allows two operations: push and pop.
      1. Push adds an item on top of the stack.
      2. Pop removes the top item from the stack.
      3. Operations can only act on the topmost item on the stack.
   4. The scripting language executes the script by processing each item from left to right.
   5. Numbers (data constants) are pushed onto the stack.
   6. Operators (OP codes) push or pop one or more parameters from the stack, act on them, and might push a result onto the stack.
      1. https://en.bitcoin.it/wiki/Script#Opcodes
   7. Conditional operators evaluate a condition, producing a boolean result of TRUE or FALSE.
   8. Bitcoin transaction scripts usually contain a conditional operator, so that they can produce the TRUE result that signifies a valid transaction.
   9. Any combination of locking and unlocking scripts that results in a TRUE value is valid.
   10. Example validation:
       1. The following locking script:
          1. `3 OP_ADD 5 OP_EQUAL`
       2. Can be satisfied by a transaction containing an input with the unlocking script:
          1. `2`
       3. The validation software evaluates the locking and unlocking scripts and compares the result:
          1. `2`
          2. `3 OP_ADD 5 OP_EQUAL`
             1. evaluates to (2 + 3 = 5) = TRUE
       4. The result is OP_TRUE, making the transaction valid.
          1. The resulting UTXO can be spent by anyone knowing that the number 2 satisfies the script.
6. Pay-to-Public-Key-Hash (P2PKH)
   1. These outputs contain a locking script that locks the output to a public key hash, more commonly known as a bitcoin address.
   2. An output locked by a P2PKH script can be unlocked (spent) by presenting a public key and a digital signature created by the corresponding private key.
   3. locking script
   4. OP_DUP OP_HASH160 <Cafe Public Key Hash> OP_EQUALVERIFY OP_CHECKSIG
   5. Example validation:
      1. Locking script:
         1. `OP_DUP OP_HASH160 <Cafe Public Key Hash> OP_EQUALVERIFY OP_CHECKSIG`
      2. Unlocking script:
         1. `<Cafe Signature> <Cafe Public Key>`
      3. The result will be TRUE if the unlocking script has a valid signature from the cafe’s private key that corresponds to the public key hash set as an encumbrance.
7. Digital Signatures (ECDSA)
   1. Elliptic Curve Digital Signature Algorithm
   2. The digital signature algorithm used in bitcoin.
   3. Based on elliptic curve private/public key pairs.
   4. Used by the script functions `OP_CHECKSIG`, `OP_CHECKSIGVERIFY`, `OP_CHECKMULTISIG`, and `OP_CHECKMULTISIGVERIFY`.
   5. A digital signature serves three purposes:
      1. It proves that the owner of the private key, who is by implication the owner of the funds, has authorized the spending of those funds (authentication).
      2. The proof of authorization is undeniable (nonrepudiation).
      3. It proves that the transaction (or specific parts of the transaction) have not and cannot be modified by anyone after it has been been signed (integrity).
   6. Each transaction input is signed independently.
      1. This is critical, as neither the signatures nor the inputs have to belong to or be applied by the same “owners.”
      2. A specific transaction scheme called “CoinJoin” uses this fact to create multi-party transactions for privacy.
   7. A digital signature is a mathematical scheme that consists of two parts:
      1. The first part is an algorithm for creating a signature, using a private key (the signing key), from a message (the transaction).
      2. The second part is an algorithm that allows anyone to verify the signature, given also the message and a public key.
   8. Creating a digital signature
      1. In bitcoin’s implementation of the ECDSA algorithm, the “message” being signed is the transaction, or more accurately a hash of a specific subset of the data in the transaction.
      2. The signing key is the user’s private key.
      3. The function produces a signature that is composed of two values, commonly referred to as R and S.
      4. Then they are serialized into a byte-stream using an international standard encoding scheme called the Distinguished Encoding Rules, or DER.
         1. `3045022100884d142d86652a3f47ba4746ec719bbfbd040a570b1deccbb6498c75c4ae24cb02204b9f039ff08df09cbe9f6addac960298cad530a863ea8f53982c09db8f6e381301`
   9. Verifying the Signature
      1. To verify the signature, one must have the signature (R and S), the serialized transaction, and the public key (that corresponds to the private key used to create the signature).
      2. Essentially, verification of a signature means “Only the owner of the private key that generated this public key could have produced this signature on this transaction.”
      3. The signature verification algorithm takes:
         1. the message (a hash of the transaction or parts of it)
         2. the signer’s public key
         3. the signature (R and S values)
      4. And returns TRUE if the signature is valid for this message and public key.
   10. Signature Hash Types (SIGHASH)
       1. Bitcoin signatures have a way of indicating which part of a transaction’s data is included in the hash signed by the private key using a SIGHASH flag.
       2. The SIGHASH flag is a single byte that is appended to the signature.
       3. Every signature has a SIGHASH flag and the flag can be different from to input to input.
       4. A transaction with three signed inputs may have three signatures with different SIGHASH flags, each signature signing (committing) different parts of the transaction.
       5. Many of the SIGHASH flag types only make sense if you think of multiple participants collaborating outside the bitcoin network and updating a partially signed transaction.
          1. Transactions may contain inputs from different “owners,” who may sign only one input in a partially constructed (and invalid) transaction, collaborating with others to gather all the necessary signatures to make a valid transaction.
       6. There are three SIGHASH flags:
          1. `ALL` (`0x01`)
             1. Signature applies to all inputs and outputs
          2. `NONE` (`0x02`)
             1. Signature applies to all inputs, none of the outputs
          3. `SINGLE` (`0x03`)
             1. Signature applies to all inputs but only the one output with the same index number as the signed input
       7. In addition, there is a modifier flag SIGHASH_ANYONECANPAY
          1. When ANYONECANPAY is set, only one input is signed, leaving the rest (and their sequence numbers) open for modification.
          2. Can be combined with each of the preceding flags.
          3. `ALL|ANYONECANPAY` (`0x81`)
             1. Signature applies to one inputs and all outputs
             2. Can be used to make a “crowdfunding”-style transaction.
                1. Someone attempting to raise funds can construct a transaction with a single output.
                   1. The single output pays the “goal” amount to the fundraiser.
                2. Others can now amend it by adding an input of their own, as a donation.
                   1. They sign their own input with ALL|ANYONECANPAY.
                3. Each donation is a “pledge,” which cannot be collected by the fundraiser until the entire goal amount is raised.
                   1. Unless enough inputs are gathered to reach the value of the output, the transaction is invalid.
          4. `NONE|ANYONECANPAY` (`0x82`)
             1. Signature applies to one inputs, none of the outputs
             2. Can be used to create a “bearer check” or “blank check” of a specific amount.
                1. It commits to the input, but allows the output locking script to be changed.
                2. Anyone can write their own bitcoin address into the output locking script and redeem the transaction.
                   1. However, the output value itself is locked by the signature.
          5. `SINGLE|ANYONECANPAY` (`0x83`)
             1. Signature applies to one input and the output with the same index number
             2. Can be used to build a “dust collector.”
                1. Users who have tiny UTXO in their wallets can’t spend these without the cost in fees exceeding the value of the dust.
                2. With this type of signature, the dust UTXO can be donated for anyone to aggregate and spend whenever they want.
8. Bitcoin Addresses, Balances and other abstractions
   1. The information presented to users through wallet applications, blockchain explorers, and other bitcoin user interfaces is often composed of higher-level abstractions that are derived by searching many different transactions, inspecting their content, and manipulating the data contained within them.
   2. When a blockchain explorer shows a bitcoin address as the “sender” (left side), this information is not in the transaction itself.
      1. When the blockchain explorer retrieved the transaction it also retrieved the previous transaction referenced in the input and extracted the first output from that older transaction.
      2. Within that output is a locking script that locks the UTXO to Alice’s public key hash (a P2PKH script).
      3. The blockchain explorer extracted the public key hash and encoded it using Base58Check encoding to produce and display the bitcoin address that represents that public key.
   3. On the right side, the blockchain explorer shows the two outputs; the first to Bob’s bitcoin address and the second to Alice’s bitcoin address (as change).
      1. Once again, to create these bitcoin addresses, the blockchain explorer extracted the locking script from each output, recognized it as a P2PKH script, and extracted the public-key-hash from within.
      2. Finally, the blockchain explorer reencoded that public key hash with Base58Check to produce and display the bitcoin addresses.
   4. To construct the “Total Received” amount:
      1. The blockchain explorer first will decode the Base58Check encoding of the bitcoin address to retrieve the 160-bit hash of Bob’s public key that is encoded within the address.
      2. Then, the blockchain explorer will search through the database of transactions, looking for outputs with P2PKH locking scripts that contain Bob’s public key hash.
      3. By summing up the value of all the outputs, the blockchain explorer can produce the total value received.
   5. Constructing the current balance (displayed as “Final Balance”)
      1. The blockchain explorer keeps a separate database of the outputs that are currently unspent, the UTXO set.
      2. To maintain this database, the blockchain explorer must monitor the bitcoin network, add newly created UTXO, and remove spent UTXO, in real time, as they appear in unconfirmed transactions.
         1. This is a complicated process that depends on keeping track of transactions as they propagate, as well as maintaining consensus with the bitcoin network to ensure that the correct chain is followed.
      3. From the UTXO set, the blockchain explorer sums up the value of all unspent outputs referencing Bob’s public key hash and produces the “Final Balance” number shown to the user.

## Advanced Transactions and Scripting

1. Introduction
2. Multi-Signature
3. Pay-to-Script-Hash (P2SH)
4. Data Recording Output (RETURN)
5. Timelocks
6. Scripts with Flow Control (Conditional Clauses)
7. Complex Script Example

## The Bitcoin Network

1. Peer-to-Peer Network Architecture
2. Nodes Types and Roles
3. The Extended Bitcoin Network
4. Bitcoin Relay Networks
5. Network Discovery
6. Full Nodes
7. Exchanging “Inventory”
8. Simplified Payment Verification (SPV) Nodes
9. Bloom filters
10. How SPV nodes use bloom filters
11. SPV nodes and privacy
12. Encrypted and Authenticated Connections
13. Transaction Pools

## The Blockchain

1. Introduction
2. Structure of a Block
3. Block Header
4. Block Identifiers: Block Header Hash and Block Height
5. The Genesis Block
6. Linking Blocks in the Blockchain
7. Merkle Trees
8. Merkle Trees and Simplified Payment Verification (SPV)
9. Bitcoin’s Test Blockchains
10. Segnet – The Segregated Witness Testnet
11. Regtest – The local blockchain
12. Using test blockchains for development

## Mining and Consensus

1. Introduction
2. Decentralized Consensus
3. Independent Verification of Transactions
4. Mining Nodes
5. Aggregating Transactions into Blocks
6. Constructing the Block Header
7. Mining the Block
8. Successfully Mining the Block
9. Validating a New Block
10. Assembling and Selecting Chains of Blocks
11. Mining and the Hashing Race
12. Consensus Attacks
13. Changing the Consensus Rules
14. Soft Fork Signaling with Block Version
15. Consensus Software Development

## Bitcoin Security

- Security Principles
  - Developing Bitcoin Systems Securely
  - The Root of Trust
- User Security Best Practices
  - Physical Bitcoin Storage
  - Hardware Wallets
  - Balancing Risk
  - Diversifying Risk
  - Multisig and Governance
  - Survivability
- Conclusion

## Blockchain Applications

### Introduction

### Building Blocks (Primitives)

### Applications from Building Blocks

### Colored Coins

1. Using Colored Coins
2. Issuing Colored Coins
3. Colored Coins Transactions

### Counterparty

### Payment Channels and State Channels

1. State Channels—Basic Concepts and Terminology
2. Simple Payment Channel Example
3. Making Trustless Channels
4. Asymmetric Revocable Commitments
5. Hash Time Lock Contracts (HTLC)

### Routed Payment Channels (Lightning Network)

1. Basic Lightning Network Example\
2. Lightning Network Transport and Routing
3. Lightning Network Benefits

### Conclusion

## Appendix A: Bitcoin – A Peer-to-Peer Electronic Cash System

- Introduction
- Transactions
- Timestamp Server
- Proof-of-Work
- Network
- Incentive
- Reclaiming Disk Space
- Simplified Payment Verification
- Combining and Splitting Value
- Privacy
- Calculations
- Conclusion
- References
- License

## Appendix B: Transaction Script Language Operators, Constants, and Symbols

## Appendix C: Segregated Witness

## Appendix D: Bitcoin Improvement Proposals

- Appendix C: Bitcore
- Bitcore’s Feature List
- Bitcore Library Examples

## Appendix E: pycoin, ku, and tx

- Key Utility (KU)

## Appendix F: Bitcoin Explorer (bx) Commands

- Examples of bx command use

---

A transaction ID is not authoritative until a transaction has been confirmed. Absence of a transaction hash in the blockchain does not mean the transaction was not processed. This is known as “transaction malleability,” because transaction hashes can be modified prior to confirmation in a block. After confirmation, the txid is immutable and authoritative.
