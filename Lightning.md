# _Lightning_

- https://bitcoinmagazine.com/articles/understanding-the-lightning-network-part-building-a-bidirectional-payment-channel-1464710791/
- https://en.bitcoin.it/wiki/Lightning_Network
- Instead of broadcasting each transaction on blockchain, you can:
  - Create a private LN channel with your friend
  - Exchange funds inside the channel for many times without paying any fees
  - Close your channel by broadcasting the final state (balances) on the blockchain
- With LN you need to pay onchain transaction fees only 2 times
  - To open and to close the channel
- Users can also create many channels and route their payments via other people’s channels
  - Similar to how Tor works

---

# _Implementations_

- There are at least 3 different open-source implementations that are interoperable and BOLT (Basics Of Lightning Technology) compliant
  - lnd ([Lightning Labs](https://twitter.com/lightning))
  - eclair ([ACINQ](https://twitter.com/acinq_co))
  - c-lightning ([Blockstream](https://twitter.com/Blockstream))
- https://github.com/mit-dci/lit/tree/master/watchtower
- https://github.com/LightningPeach/watchtower

---

# _Watchtowers_

- https://diyhpl.us/wiki/transcripts/scalingbitcoin/milan/unlinkable-outsourced-channel-monitoring/

## Implementation

- When Alice’s payment channel state gets updated (Bob transfers 0.1 BTC to Alice)
- Alice sends to a LN watchtower encrypted signatures authorizing the movement of all channel’s funds back to Alice
- The package sent by Alice has no info about state’s balances, so Alice’s privacy should be safe (disputable)
  - Unless the channel will be closed unilaterally
- Basically, Alice is pre-signing a transaction of all channel’s funds back to her
  - So she can be offline at the time the breach happens
- Each sent package also contains a “hint” about how to find potential breaching on-chain transaction
- The LN watchtower constantly watches the blockchain by checking all new transactions against its hash table of “hints”

## _Cheating_

- Bob decides to cheat Alice by closing the LN channel unilaterally with an old state
  - A state before he sent 0.1 BTC to Alice
- When the LN watchtower spots the breaching transaction, it’s able to decrypt the signatures from Alice’s package and reconstruct the penalty transaction which moves all funds back to Alice
- Since a channel was closed unilaterally, there is a time-lock on funds
- The LN watchtower has some time to react before Bob would be able to spend the “stolen” funds

## _Offline_

### Problem

- Going offline introduces security risks of losing money
  - If a counter-party decides to cheat by closing an off-chain payment channel with an invalid state

### _Solution_

- Outsource to dedicated 3rd party watchtowers an ability to watch the blockchain 24/7 on behalf of their clients, and broadcast penalty transactions if needed

---

# _Challenges_

- Watchtowers have to cover operating costs, which most likely will increase quadratically for privacy-oriented implementations
- How much users should pay for watchtower’s services, and how will payments be made
- How to preserve privacy while paying somebody to watch all your economic activities
- How to keep watchtowers accountable without damaging privacy or UX

---

# _Business models_

- Business-oriented to refer to watchtowers that can link together all state updates made by the same channel or account
- Privacy-oriented to refer to watchtowers that cannot link together state updates made by the same channel or account

## Business-oriented model

- The business-oriented model implies that a watchtower can link state updates made by the same person
  - channel, account, KYC, etc.
- The business-oriented model allows watchtowers to significantly reduce operating costs by truncating their databases of state updates, which is a deal-breaker when it comes to surviving as a business
- The ability to link state updates to a certain channel or person will allow watchtowers to introduce account-based system to monetize their services, which is the most viable business model
- LN watchtowers will be able to store only latest state updates for each channel after [eltoo](https://blockstream.com/2018/04/30/eltoo-next-lightning/) will be implemented, which requires [BIP 118](https://github.com/bitcoin/bips/commit/98b7238f68d17f0e01275dd32075078702225356) activation, which might be deployed together with schnorr, since both require a seguito script bump, according to [Christian Decker](https://twitter.com/Snyke/status/1065926936793354241)
  - Will financially incentivize watchtowers to link state updates together and shrink their ever growing databases by deleting old states, because that’s a more viable business modal
  - There still be privacy-oriented watchtowers that won’t link state updates together, but most laymen will use cheapest watchtowers with low privacy, which store only latest state updates

### Downsides

- Collaborate with other watchtowers, financial institutions, and merchants to perform traffic analysis to determine a final destination of a transaction, even if it was routed with multiple hops
- Analyze transaction frequency to determine user’s economic activity and wherever they are an end node or a routing node
- Analyze the timing of each transaction (most laymen will be end nodes) to determine user’s approximate location, his habits/time-schedule, and potentially identify a user if he has a very unique fingerprint, or often changes his timezone (changing a timezone just 2–3 times will be enough to identify a user, if he uses his ID for traveling: airplanes, trains, hotels, crossing borders, etc.)
- And, of course, link all previous state updates to a certain channel in Raiden’s implementation, or in case of a unilateral close in Lightning’s implementation

## Privacy-oriented model

- Lightning’s approach might change after eltoo, but the current design of LN watchtowers has a privacy-oriented approach
  - Watchtowers cannot link all previous state updates together until they try to monetize their services with account-based system
  - A watchtower can get 10 new state updates from 1 channel, but it will not know whether those 10 state updates came from 1 channel or from 10 different channels
  - Even if there was unilateral close and watchtower was able to decrypt the received package, it will only know the exact channel (two on-chain addresses) to which the latest state belongs, but watchtower will not know to which channel/account other 9 state updates belong to
- The inability to link state updates together to truncate the database will force a watchtower to store all previous state updates that it has ever received, except for those that have been closed unilaterally (a tiny amount)
- Privacy-oriented watchtowers have to be online 24/7 with a decant bandwidth, store lots of data, and perform computations — insert new state updates into databases and check all on-chain transactions against their databases of previous state updates, in order to find a breaching transaction

### Operating requirements

- Bandwidth
  - Bandwidth requirements will be fairly low, because watchtowers don’t need to serve the received data (state updates) back to clients, nor distribute across the network of other watchtowers/nodes
- Computation time
  - Watchtowers have to insert all received “hints” into hash table and check all transactions in new on-chain blocks against that hash table in order to find a breaching transaction and punish the cheater by reconstructing and broadcasting a penalty transaction
  - Hash lookups are O(1) regardless of the map’s size, and can be done on commodity hardware. Really large datasets can shard the keyspace on multiple machines
    - Insertion is O(1) amortized, just like an in-memory hash table. Doesn't need to be ordered, just bucketed by key
    - [O(1)](https://stackoverflow.com/questions/697918/what-does-o1-access-time-mean) means that the time to access something is independent of the number of items in the collection, and you will spend a constant amount of time to find a matching hash in a table of 1 million or 1 billion hashes, so computation burden shouldn’t be a bottleneck
- Disk space
  - Watchtowers have to store all received data (state updates) in order to check new on-chain blocks for breaching transactions
  - Quadratic growth problem
    - Eve decided to become a privacy-oriented watchtower
    - Let’s assume that Eve will get 10 new users in the beginning of each day
    - The economic activity of average user will be 10 transactions per day
    - Here are the results at the end of each day:
      - **Day 1:** \***\*10 users, 100 daily TXs, and **100\*\* state updates stored (0+100)
      - **Day 2:** \***\*20 users, 200 daily TXs, and **300\*\* state updates stored (100+200)
      - **Day 3:** \***\*30 users, 300 daily TXs, and **600\*\* state updates stored (300+300)
      - **Day 4:** \***\*40 users, 400 daily TXs, and **1,000\*\* state updates stored (600+400)
      - **Day 5:** \***\*50 users, 500 daily TXs, and **1,500\*\* state updates stored (1K+500)

---

# _Eltoo_

- https://blockstream.com/eltoo.pdf
- Allows users to only store the latest state and prove that it’s the later state without providing the entire state history
- So LN watchtowers can delete all previous state updates, but only if they know that those state updates belong to the same channel
-

---
