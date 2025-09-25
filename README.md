
# StacksFlick - A Decentralized Video Streaming Platform

**Version:** `1.0.2`
**Language:** Clarity (Stacks blockchain)
**Description:**
This smart contract powers a decentralized video streaming platform that enables creators to publish video content, users to subscribe or purchase content, and a community governance system to propose and vote on changes. The platform also manages revenue distribution, subscriptions, and access control in a decentralized manner.

---

## 🚀 Features

### 👤 User Features

* **Video Purchase**: Buy individual videos uploaded by verified content creators.
* **Premium Subscription**: Subscribe to premium access on a time-based model.
* **View Video Metadata**: Query video details and creator earnings.
* **Subscription Status**: Verify premium subscription validity.

### 🎬 Creator Features

* **Creator Registration**: Self-register as a content creator.
* **Upload Video**: Upload new video content with title, description, and price.
* **Revenue Tracking**: Automatically track creator revenue from views/purchases.

### 🛠 Admin Features

* **Add Admins**: Grant administrative privileges to other principals.
* **Set Platform Fee**: Adjust platform-wide transaction fee (capped at 10%).
* **Pause/Unpause Contract**: Temporarily disable critical platform functionality.

### 🗳 Governance (Planned/Partial)

* **Proposals Map**: Track governance proposals (votes, execution status).
* (Note: Voting/execution logic not yet implemented.)

---

## 📦 Data Structures

### 📁 Video

Each video is stored with:

* `creator`: Principal of the uploader
* `title` / `description`
* `content-hash`: 32-byte buffer (e.g., IPFS hash)
* `price`: In micro-STX
* `created-at`, `views`, `revenue`, `is-active`

### 📊 Revenue Maps

* `creator-revenue`: Tracks each creator’s total revenue
* `platform-revenue`: Tracks overall platform earnings

### 🔐 Access Control

* `administrators`: Admins with elevated privileges
* `content-creators`: Verified creators
* `premium-subscribers`: Users with active subscriptions

---

## 💸 Payments

### Video Purchase

* Direct payment from user to creator
* Views and revenue automatically updated

### Premium Subscription

* 10 STX per duration (≈1 day = 144 blocks)
* Paid to the contract owner
* Access based on block height expiry

---

## 🧪 Key Read-Only Functions

```clojure
(get-video-details <video-id>)                 ;; Returns video metadata
(get-creator-revenue <creator>)               ;; Returns revenue earned
(is-premium-subscriber <user>)                ;; Checks premium status
```

---

## 🔐 Access Control Functions

```clojure
(register-as-creator)                         ;; Self-registration as creator
(add-administrator <principal>)               ;; Only admins
(set-platform-fee <new-fee>)                  ;; Admins can set platform fee
(toggle-contract-pause)                       ;; Emergency switch
```

---

## 📛 Error Codes

| Code   | Description              |
| ------ | ------------------------ |
| `u100` | Not authorized           |
| `u101` | Resource not found       |
| `u102` | Already exists           |
| `u103` | Invalid input parameters |
| `u104` | Insufficient funds       |
| `u105` | Contract is paused       |

---

## ⚙️ Deployment Notes

* Contract owner is automatically the first admin upon deployment.
* Platform fee is initialized to 5% (`u50 / u1000`).
* Use admin functions for setup before onboarding creators.

---

## 📌 Future Improvements

* Implement governance proposal creation and voting
* Add royalty splitting / multi-recipient payments
* Integrate with decentralized storage (IPFS, Arweave)
* Analytics dashboard for creators
* NFTs for ownership or licensing

---

## 📄 License

MIT License (or custom if preferred)
Smart contract is open-source and intended for use on the Stacks blockchain.

---
