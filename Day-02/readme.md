# Proof of Work (PoW)

**Proof of Work (PoW)** is a method used in blockchain (like Bitcoin) to make sure that everyone agrees on the same data and that no one cheats.

## Simple Explanation

- People called **miners** compete to solve a hard math puzzle.  
- Solving this puzzle takes a lot of **computer power** and **electricity** — that’s the “work”.  
- The first miner to solve it gets to **add a new block of transactions** to the blockchain and **earns a reward** (like Bitcoin).  
- Since solving it takes effort, it proves that the miner **did real work**, so others can trust the result.

 **In short:**  
> **Proof of Work = “Show you used real computer effort to add a valid block.”**

---

# Why It Takes 10 Minutes

In **Bitcoin’s Proof of Work**, the network is designed so that **one block is added roughly every 10 minutes** — not faster, not slower (on average).

## Here’s Why 👇

###  To Keep the Network Stable
- If blocks were created too quickly, there would be too many blocks spreading across the world, causing confusion and more chances of conflicts (two miners finding different valid blocks at almost the same time).  
- 10 minutes gives enough time for new blocks to spread (**propagate**) through the global network.

###  To Control Bitcoin Supply
- Bitcoin has a limited supply of **21 million coins**.  
- Slower block creation ensures new bitcoins are released gradually, keeping **inflation under control**.

###  Difficulty Adjustment
- The Bitcoin system automatically adjusts the **difficulty** of the math puzzle every **2016 blocks** (about every 2 weeks).  
- If miners start solving puzzles too fast, the difficulty increases.  
- If they’re too slow, it decreases — keeping the average at around **10 minutes per block**.

 **In short:**  
> It takes 10 minutes because Bitcoin is designed to keep block creation **slow and steady**, ensuring **fairness, security, and controlled coin supply.**

#  Step-by-Step: What Happens When Vijay Sends 1 BTC to Priya

## Step 1: Transaction Creation
Vijay opens his Bitcoin wallet and sends **1 BTC** to Priya’s Bitcoin address.  

This creates a **transaction** containing:
- **Sender:** Vijay’s wallet address  
- **Receiver:** Priya’s wallet address  
- **Amount:** 1 BTC  
- **Digital signature:** from Vijay (to prove it’s really him)  

✅ This transaction is then **broadcast** to the entire Bitcoin network.

---

##  Step 2: Enters the Mempool (Memory Pool)
- The transaction first goes to a place called the **mempool (memory pool)**.  
- Think of the mempool as a **waiting room** for all unconfirmed transactions.  
- Every node in the network keeps a copy of the mempool.

💡 **In short:**  
> The mempool holds all transactions waiting to be confirmed by miners.

---

##  Step 3: Miners Pick Transactions
- Miners look into the mempool and pick transactions they want to include in the next block.  
- Usually, they **choose the ones with higher transaction fees** first (to earn more).  

✅ So, if Vijay added a **higher fee**, his transaction to Priya will get confirmed faster.

---

## Step 4: Miners Compete (Proof of Work)
- Now all miners compete to solve a **complex math puzzle** (the Proof of Work).  
- The goal is to find a special number called a **nonce** that makes the block’s **hash valid**.  
- This process requires **huge computation and electricity**.  

💡 It takes about **10 minutes (on average)** for one miner somewhere in the world to solve it.

---

## Step 5: Block Is Added to Blockchain
- The **first miner** to solve the puzzle broadcasts their block to the network.  
- Other nodes verify that:  
  - All transactions are valid  
  - The miner’s work (hash) is correct  

✅ Once verified, the block is **added permanently** to the blockchain.

---

##  Step 6: Transaction Confirmation
- Vijay’s transaction (1 BTC to Priya) is now inside a block.  
- This is called **1 confirmation**.  
- As more blocks are added after it (**2, 3, 6 confirmations…**), the transaction becomes **more secure and irreversible**.

---

##  Step 7: Priya Receives the Bitcoin
- Priya’s wallet detects the transaction after the first block confirmation.  
- After around **6 confirmations (~1 hour)**, it’s considered **fully confirmed**.  
- The Bitcoin network now officially shows **Priya owns 1 BTC** and **Vijay’s balance is reduced**.

---

✅ **In short:**
1. Vijay sends 1 BTC → transaction created.  
2. It goes to the **mempool** → waiting for miners.  
3. Miners pick it up → solve puzzle (**Proof of Work**).  
4. Block gets added to blockchain (~10 minutes).  
5. Priya receives BTC after confirmations.

#  What Is Hashing in Blockchain?

**Hashing** means converting any data (like a message, transaction, or block) into a **fixed-length unique code** using a mathematical function called a **hash function**.

This code is called a **hash**.

In **Bitcoin**, the hash function used is **SHA-256** (Secure Hash Algorithm 256-bit).  
No matter how big the input, the output is **always 256 bits (64 hexadecimal characters)**.

---

##  Example

Let’s take a simple text:
"Vijay sends 1 BTC to Priya"

If we apply **SHA-256 hashing**, we might get something like:
f4c3d0d8c6f98e36a83e5c9e28b6c3e41cf5a6e3c5b4a1f8e92a9a3b3c3e7b9a


Even if we change one letter (like `"Vijay"` → `"vijay"`),  
the hash will become **completely different**.  
That’s called the **avalanche effect**.

---

##  Why Hashing Is Important in Blockchain

###  Security
- Hashes are **one-way** — you can’t reverse a hash to find the original data.  
- So, it protects all data stored in blocks.

###  Linking Blocks
- Every block contains the **hash of the previous block**.  
- That’s how they form a **chain**.  
- If someone tries to change data in one block, its hash changes — and all next blocks become invalid.

###  Verification
- Instead of comparing full data, nodes just **compare hashes** to check if the data is same or changed.

###  Efficiency
- Hashes make validation **fast** because they are small, fixed-size values.

---

## 🔁 In Short
> **Hashing = Converting data into a unique digital fingerprint to ensure security, integrity, and linkage between blocks in the blockchain.**

#  Why the Longest Chain is the Source of Truth in Blockchain

##  Step 1: Many Miners Compete
When a transaction (like **Vijay → Priya 1 BTC**) goes into the **mempool**, many miners try to include it in their next block.  
Each miner builds their own version of the blockchain and tries to **solve the Proof of Work puzzle** (find a valid hash).

---

##  Step 2: One Miner Wins
Suppose **Miner A** finds the valid hash first.  
He broadcasts his block to the entire network.  
Now everyone verifies it and adds it to their copy of the blockchain.

But sometimes, **two miners** may find a valid block at nearly the same time → leading to a **temporary fork**.

---

##  Step 3: Competing Chains (Forks)
Now there are **two versions** of the blockchain:

- **Chain 1** (ending with Miner A’s block)  
- **Chain 2** (ending with Miner B’s block)

Both are valid initially, so some nodes follow Chain 1, others follow Chain 2.

---

##  Step 4: Miners Keep Mining
Miners continue to mine the **next block** on whichever chain they received first.  
Soon, **one of the chains becomes longer** (gets more Proof of Work done).

---

##  Step 5: Longest Chain Wins
As per **Bitcoin’s consensus rule**:

> “The valid chain with the most accumulated Proof of Work is considered the true blockchain.”

So, the shorter chain is discarded (its blocks become *orphaned*),  
and all miners switch to the longer one.

---

##  Step 6: Why It Works
Because adding each block requires **huge computation (energy + time)**,  
it’s practically impossible for an attacker to outpace the entire network’s combined work.

Hence,  
✅ The **longest chain** = the **most honest effort** + **most Proof of Work**,  
and becomes the **source of truth** for everyone.

---

#  Bitcoin Supply Limit

##  Total Supply Limit

There will only ever be **21 million Bitcoins** in existence.  
This limit was set by **Satoshi Nakamoto**, the creator of Bitcoin, in the code itself.

So, no matter how much time passes, **Bitcoin cannot exceed 21 million — ever.**

---

##  Why the Limit?

The idea was to make Bitcoin **scarce**, like gold.  
Scarcity increases value and prevents **inflation** (unlike paper currency, where more can be printed anytime).

---

##  Mining and Halving

New Bitcoins are created as **rewards to miners** when they add new blocks to the blockchain.

Initially, the reward was **50 BTC per block** in 2009.  
Every **4 years**, this reward is **cut in half** — this event is called **“Halving.”**

| Year | Block Reward | Total BTC in Circulation (approx.) |
|------|---------------|------------------------------------|
| 2009 | 50 BTC        | — |
| 2012 | 25 BTC        | — |
| 2016 | 12.5 BTC      | — |
| 2020 | 6.25 BTC      | — |
| 2024 | 3.125 BTC     | — |

By around **2140**, all **21 million Bitcoins** will have been mined.

---

##  After 2140

After that, no new Bitcoins will be created.  
Miners will earn **transaction fees only** — not block rewards.

---

## ✅ In Short

- **Bitcoin supply:** Fixed (21 million)  
- **Purpose:** Scarcity + Anti-inflation  
- **Created by:** Mining  
- **Reduced by:** Halving  
- **End year:** ~2140  
