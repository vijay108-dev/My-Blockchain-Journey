###  Seed Phrase in Blockchain

A **Seed Phrase** (also known as a *recovery phrase* or *mnemonic phrase*) is a sequence of 12, 18, or 24 random words that serves as a **human-readable backup** of your crypto wallet’s private key.

It’s generated when you create a new wallet and can be used to **recover all your funds** if you lose access to your device.

#### How It Works

* The seed phrase is created using the **BIP39 (Bitcoin Improvement Proposal 39)** standard.
* Each word in the phrase represents a portion of a large random number that forms your **private key**.
* From this single phrase, your wallet can deterministically generate **multiple private keys and addresses**.

####  Example

```
ripple smile engine better orchard dawn quantum token sugar canyon gravity risk
```

#### Security Tips

* Never share your seed phrase with anyone.
* Store it **offline**, ideally on paper or a hardware wallet.
* Anyone with your seed phrase can access your entire wallet.
* Losing it means **permanent loss of access** to your funds.

####  Summary

| Term        | Meaning                                  |
| ----------- | ---------------------------------------- |
| Seed Phrase | Backup of private key in readable words  |
| BIP39       | Standard for generating mnemonic phrases |
| Purpose     | Wallet recovery & backup                 |
| Security    | Keep offline and private                 |

---

###  UTXO in Blockchain

**UTXO (Unspent Transaction Output)** is a fundamental concept in blockchain systems like Bitcoin. It represents the amount of cryptocurrency that remains unspent after a transaction. These unspent outputs can later be used as **inputs** in new transactions.

####  How It Works

* Every transaction consumes previous UTXOs and creates new ones.
* A wallet's balance is the **sum of all its UTXOs**.
* Each UTXO is linked to an address and can only be spent by the owner with the correct private key.

####  Example

If you receive 1 BTC and later 0.5 BTC from two transactions, your wallet has **two UTXOs**:

```
UTXO1 = 1 BTC
UTXO2 = 0.5 BTC
```

When you send 1.2 BTC to someone, the blockchain will consume these UTXOs and create:

```
New UTXO (for receiver) = 1.2 BTC
Change UTXO (back to you) = 0.3 BTC
```

####  Key Points

* UTXOs ensure **transparency and traceability** in blockchain transactions.
* They prevent **double spending** since each UTXO can be spent only once.
* UTXO models are used in Bitcoin, while Ethereum uses an **account-based** model.

## Example

Maan le tu ko do transactions milti hain:

1 BTC  (Tx1)
0.5 BTC (Tx2)


Ab tere wallet me 2 UTXO hain:

UTXO1 = 1 BTC

UTXO2 = 0.5 BTC

Ab tu 1.2 BTC bhejta hai kisi ko.
To blockchain ye karega 

Pichle dono UTXO (1 + 0.5) use karega

1.2 BTC bhej dega receiver ko

Aur bacha hua 0.3 BTC naya UTXO banake tujhe wapas de dega (change).

####  Summary

| Term     | Meaning                                             |
| -------- | --------------------------------------------------- |
| UTXO     | Unspent Transaction Output                          |
| Purpose  | Represents remaining unspent crypto balance         |
| Prevents | Double spending                                     |
| Used In  | Bitcoin, Litecoin, and other UTXO-based blockchains |
