# 🏦 Secure CLI Banking Engine

A high-integrity Command Line Interface (CLI) banking simulation built with **Python 3.x**. This project focuses on **secure credential handling**, **data persistence via JSON**, and **atomic transaction logic**, simulating the core backend of a modern financial institution.

## 🌟 Key Engineering Highlights

* **Low-Level Security Masking:** Implements the `msvcrt` library to intercept keyboard buffers, allowing for real-time password/PIN masking (`****`) without echoing characters to the console—a standard for secure terminal applications.
* **Persistent JSON Data Layer:** Utilizes a structured JSON database for asynchronous data storage, ensuring that user balances, security credentials, and transaction logs persist across system reboots.
* **Automated ID Architecture:** Features an algorithmic account generation system that ensures every new user is assigned a unique, collision-resistant 5-digit Account ID.
* **State-Based User Dashboard:** A robust session management system that handles complex state transitions (Login → Session → Transaction → Logout) to prevent unauthorized data access.
* **Account Recovery Protocol:** A "Forgot PIN" workflow utilizing security question-response pairs, demonstrating an understanding of basic identity and access management (IAM).

---

## 🛠️ Technical Deep Dive

### 1. The Security Layer (`msvcrt`)
Unlike standard `input()` calls which display text as you type, this system uses the Windows-specific `msvcrt.getch()` method. 
* **Logic:** It captures every individual keystroke, appends it to a hidden variable, and prints an asterisk (`*`) to the screen. 
* **Recruiter Note:** This demonstrates an ability to handle low-level system libraries to solve real-world security vulnerabilities like "shoulder surfing."

### 2. Transaction Integrity & History
Banking systems require absolute accuracy. The transaction logic follows a "Check-then-Commit" pattern:
* **Validation:** Before any withdrawal or transfer, the system validates the `Sufficient Balance` constraint.
* **Atomicity:** For transfers, the system ensures that the deduction from the sender and the credit to the receiver happen as a single logical unit.
* **Persistence Formula:**
    $$Balance_{final} = Balance_{initial} + \sum \text{Deposits} - \sum \text{Withdrawals}$$

### 3. Data Schema (JSON)
The database (`bank_data.json`) is structured for rapid parsing:
```json
{
  "12345": {
    "name": "John Doe",
    "pin": "8888",
    "balance": 5000.0,
    "security_q": "What is your pet's name?",
    "answer": "Rex",
    "history": [
        {"timestamp": "2026-03-30 14:00", "type": "Deposit", "amount": 1000.0}
    ]
  }
}
```

---

## 🚀 Getting Started

### 📋 Prerequisites
* **Operating System:** Windows (Required for `msvcrt` console control).
* **Environment:** Python 3.8 or higher.

### 🔧 Installation
1.  **Clone/Download:** Save the script as `bank_system.py`.
2.  **Initialize:** Run the script for the first time to generate the database:
    ```bash
    python bank_system.py
    ```

### 🎮 Usage Flow
1.  **Registration:** Create an account to generate your unique 5-digit ID.
2.  **Authentication:** Log in using your ID and masked PIN.
3.  **Operations:** * **Deposit:** Instantly update your persistent balance.
    * **Transfer:** Send funds to any other valid 5-digit User ID.
    * **History:** View your last 7 activities with precise timestamps.

---

## 📊 Features & Capabilities

| Feature | Implementation | Benefit |
| :--- | :--- | :--- |
| **Authentication** | PIN-based Masked Input | Prevents credential theft. |
| **Data Storage** | Serialized JSON | Lightweight, portable database. |
| **Transaction Logs** | Historical Array | Provides a clear audit trail for users. |
| **Error Handling** | Input Validation | Prevents system crashes from invalid amounts. |

