# **How to Create a Digital Wallet**

## **Step 0: The True Beginning — Entropy (Randomness)**

###  What is it?
This is the very first step in creating a digital (crypto) wallet.  
A **random number** is generated — this will later become your **seed phrase** (the 12 or 24 secret words that protect your wallet).

For a 12-word seed, the number has **128 bits**.  
For a 24-word seed, it has **256 bits**.  
Example (just a small part of it):
10100101110101110010000110110101...

markdown
Copy code

###  How is it generated?
1. A **hardware wallet** has a special chip called a **True Random Number Generator (TRNG)**.  
   - It creates randomness using physical noise, heat, or electrical signals — things that are impossible to predict.  
2. Some wallets also let you add your own randomness — for example:
   - Rolling dice 🎲  
   - Pressing random buttons  

###  In Simple Words
This step is all about creating a **completely unpredictable random number**.  
That number is then converted into your **seed phrase** — the master key to your digital wallet 🔐.  
The more random the number, the more secure your wallet.

### **Step 1: Creating the Seed Phrase (Your Human-Friendly Backup)**

Humans can’t remember or write down a long 128-bit binary number — it’s just a bunch of 1s and 0s.  
So, we turn that random number into **simple words** that people can easily read and write.  
This process follows a rule called **BIP-39 (Bitcoin Improvement Proposal 39).**

---

###  1. The BIP-39 Wordlist
There is an official list of **2048 English words**, like:
abandon, ability, able, ... , zoo

Each word has a unique number (from 0 to 2047).

---

###  2. Chopping the Entropy
Your 128-bit random number is **split into 11-bit parts**.  
Why 11 bits?  
Because **2¹¹ = 2048**, and that perfectly matches the number of words in the list.  
Each 11-bit chunk will point to one word.

---

###  3. Adding a Checksum
To protect against mistakes (like writing one word wrong),  
the wallet adds a **checksum** — a few bits taken from the hash of the original entropy.  
This checksum becomes part of the last word.  

That’s why, if you type one word incorrectly into your wallet,  
it will show an error like **“Invalid seed phrase”** instead of creating a wrong wallet.

---

###  4. Mapping to Words
Now the wallet converts each 11-bit chunk (plus the checksum bits) into words using the BIP-39 list.  
The result is your **12-word seed phrase**, something like:
ripple salad bone sphere ... tunnel

These words are your **master backup** —  
anyone who knows them can fully access your wallet,  
so store them safely and never share them.

### What is a Checksum? (The "Why")

A **checksum** is a small piece of data used to check if something has an error.

**Simple Example:**  
Think about your **credit card number** — the **last digit** is not random.  
It is made from all the other digits using a rule (called the Luhn algorithm).  
If you type one digit wrong, the last digit will not match, and the system will know something is wrong.

In the same way, a **seed phrase checksum** helps your wallet know if you wrote any word wrong.  
If one word is incorrect, it shows **“Invalid seed phrase”** instead of creating a wrong wallet.  
This helps keep your wallet **safe and correct**.

[ Initial 128-bit Entropy ]
|
└─>  Run through SHA-256 Hashing Algorithm
|
└─>  Take the First 4 bits
|
[ 4-bit Checksum ]
|                      |
└──────────┬───────────┘
|
▼
[ A Combined 132-bit Data Block ]
|
└─>  Split into 12 chunks of 11 bits each
|
┌───────────┴───────────┐ ...
|           |           |
▼           ▼           ▼
[ Word 1 ]  [ Word 2 ] ... [ Word 12 ]
(from 1st   (from 2nd     (from 12th
11-bit      11-bit       11-bit
chunk)      chunk)       chunk)


### Step 2: From Seed Phrase to Master Private Key
What PBKDF2 Does

When you enter your 12/24-word Seed Phrase, a special function called
PBKDF2 (Password-Based Key Derivation Function 2) converts it into a 512-bit Seed.

This Seed is 64 bytes

It is the starting point of your entire crypto wallet

PBKDF2(Seed Phrase)  --->  512-bit Seed

Splitting the 512-bit Seed

The 512-bit Seed is then split into two equal 256-bit parts:

[ 512-bit Seed ]
        |
        |---- split into two halves ----
        |
Left 256 bits        Right 256 bits

┌──────────────────┐        ┌──────────────────┐
│ Left 256 bits    │        │ Right 256 bits   │
└──────────────────┘        └──────────────────┘

Meaning of the Two Halves
1. Left 256 bits → Master Private Key

This becomes the root private key of your entire wallet.

All your future private keys and addresses come from this.

2. Right 256 bits → Master Chain Code

This acts like an extra security parameter.

It helps generate child keys in a secure and predictable way.

Together, these two form the Master Node (m) used in HD wallets (BIP-32).


### Step 3: From Master Key to a Specific Private Key

This step explains how a wallet creates many private keys and addresses from a single Master Private Key.
This is what makes modern crypto wallets powerful, organized, and secure.

Why Many Keys Are Needed
1. Privacy

If you use the same address for every transaction:

Anyone can look it up on a block explorer

They can see all your payments

Your entire financial history becomes visible

HD wallets solve this problem by creating new addresses automatically, which keeps your financial activity more private.

2. Organization

A single seed phrase can control many different wallets and accounts. For example:

Bitcoin (Savings)

Bitcoin (Spending)

Ethereum

Litecoin

A separate account for apps

A separate account for exchanges

HD wallets use structured paths to keep everything organized and separate.

BIP-32 and BIP-44: The Standards Behind HD Wallets

These standards define how keys are generated.

Hierarchical (BIP-32)

Your wallet uses a tree-like structure:

Master Key
   ├── Account 0
   │      ├── Address 0
   │      ├── Address 1
   │      └── Address 2
   ├── Account 1
   └── Account 2


A parent key can create child keys

Each child key can create even more child keys

This forms a large, organized structure of keys

Deterministic (BIP-32 / BIP-44)

Everything is predictable and repeatable from the seed phrase:

Same Seed Phrase → Same Master Key

Same Master Key → Same Accounts

Same Accounts → Same Addresses

This is why you can recover your entire wallet using only your seed phrase, even on a new device.

### The Solution: The BIP-32 & BIP-44 Standards to generate private key

The system that solves this is called a **Hierarchical Deterministic (HD) Wallet**.

- **Hierarchical:** It's a tree structure. Parent keys can create child keys.
- **Deterministic:** The same master seed will *always* generate the exact same tree of keys.
| **Path Part** | **Name**          | **Simple Meaning**                                                                                                     |
| ------------- | ----------------- | ---------------------------------------------------------------------------------------------------------------------- |
| **m**         | **Master**        | Starting point. This is the *master private key* created from your seed phrase.                                        |
| **/**         | **Separator**     | Just like a folder separator. Means “go one level deeper.”                                                             |
| **44'**       | **Purpose**       | Says we are using the **BIP-44 standard**. It tells wallets how the rest of the path is structured.                    |
| **0'**        | **Coin Type**     | Tells which cryptocurrency this branch is for. <br>**0 = Bitcoin**, **60 = Ethereum**, **2 = Litecoin**, etc.          |
| **0'**        | **Account**       | Lets you create multiple accounts from the same seed. <br>Example: Account 0 = savings, Account 1 = daily use.         |
| **0**         | **Change**        | `0` = **External** (receive addresses you share). <br>`1` = **Internal** (change addresses wallet uses automatically). |
| **0**         | **Address Index** | Picks the specific address. <br>`0` = first address, `1` = second, `2` = third…                                        |

### Step 4: From Private Key to Public Key

Here's the cryptographic magic. The Private Key is put through a one-way mathematical function called **Elliptic Curve Cryptography (ECC)**.