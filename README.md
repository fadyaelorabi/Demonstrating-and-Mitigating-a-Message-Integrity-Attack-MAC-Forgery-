# MAC Forgery and Length Extension Attack Demonstration

This project demonstrates the security implications of using insecure MAC (Message Authentication Code) implementations. It includes both vulnerable and secure implementations, and showcases how an attacker can exploit the vulnerable system using a length extension attack.

## 📁 Project Structure

```
project/
├── venv/                  # Python virtual environment
├── server.py              # Insecure server using MD5
├── server_mitg.py         # Secure server using HMAC-SHA256
├── client.py              # Attack simulation on server.py
├── client_mitg.py         # Attack simulation on server_mitg.py (expected to fail)
├── README.md              # This file
```

## 📌 Setup

1. Create a virtual environment:

   ```bash
   python -m venv venv
   ```

2. Activate the virtual environment:

   * Windows:

     ```bash
     venv\Scripts\activate
     ```
   * macOS/Linux:

     ```bash
     source venv/bin/activate
     ```

3. Install required package:

   ```bash
   pip install hashpumpy
   ```

## 🧪 Files Overview

### `server.py`

Implements an insecure MAC using:

```python
hashlib.md5(SECRET_KEY + message)
```

This is vulnerable to a **length extension attack**.

### `client.py`

Simulates an attacker performing a length extension attack against `server.py` using `hashpumpy`.

### `server_mitg.py`

Uses a secure HMAC with SHA-256:

```python
hmac.new(SECRET_KEY, message, hashlib.sha256)
```

This prevents length extension attacks.

### `client_mitg.py`

Attempts the same attack as `client.py` against `server_mitg.py`, but it will **fail** because HMAC is secure against such attacks.

## ✅ Expected Behavior

* Running `server.py` prints a valid MAC and attempts to verify both a legitimate and a forged message. The forged one fails.
* Running `client.py` successfully forges a message and bypasses the insecure verification.
* Running `client_mitg.py` fails to bypass verification, demonstrating the strength of HMAC.

## 🔐 Key Concepts

* **MAC (Message Authentication Code):** Ensures integrity and authenticity of a message.
* **Length Extension Attack:** A vulnerability in naive constructions like `hash(secret + message)` where an attacker can forge a valid MAC for a longer message.
* **HMAC:** A secure construction that prevents length extension attacks.

## 💡 Recommendation

Always use `HMAC` from Python’s `hmac` module instead of manually hashing `secret + message`.

## 📜 License

This project is for educational purposes only.
