# 🔐 Password Management System for Students (PMSS)

A desktop password manager built in Java Swing, presented at the **ICCES 2022 International Conference** — designed to give students a simple, secure way to generate, encrypt, store, and retrieve account passwords locally.

![screenshot](img/screenshot.png)

## Why

Students juggle logins for a dozen college portals, labs, and personal accounts, and tend to reuse weak passwords out of convenience. PMSS is a small, self-contained utility that removes the excuse: generate a strong password, store it encrypted, and pull it back up when you need it — no cloud account, no third-party service.

## Features

- 🔑 **Password generation** — cryptographically random passwords (`SecureRandom`) mixing uppercase, lowercase, digits, and symbols
- 🔒 **SHA-1 + salt hashing** — passwords are never stored in plain text; each one is salted before hashing
- 🗂️ **Custom hash table (linear probing)** — account/password pairs are stored in a hand-built open-addressing hash table rather than relying on `java.util.HashMap`, implemented from first principles for the underlying data-structure practice
- 🔍 **Add, search, and delete accounts** — a full Swing GUI for day-to-day password management
- 🎨 **Custom look and feel** — themed with the JTattoo library instead of default Swing styling
- 🖼️ **Animated splash screen** on launch

## Tech Stack

| Layer | Technology |
|---|---|
| Language | Java |
| GUI | Java Swing |
| Cryptography | SHA-1 message digest + random salt |
| Data structure | Custom hash table with linear probing |
| Look & Feel | [JTattoo](https://www.jtattoo.net/) |

## Project Structure

```text
Password-Management-System/
├── src/
│   ├── PasswordManager.java      # Main application window & controller
│   ├── SplashScreen.java         # Startup splash screen
│   ├── HashtablePassword.java    # Custom hash table (linear probing)
│   ├── hashTableMap.java         # Interface for the hash table
│   ├── PasswordGenerator.java    # Secure random password generator
│   ├── passwordEncryption.java   # SHA-1 + salt hashing
│   └── META-INF/MANIFEST.MF
├── lib/
│   └── JTattoo-1.6.13.jar        # UI theming dependency
├── img/
│   ├── icon.png
│   └── screenshot.png
├── PMSS.jar                      # Prebuilt runnable jar
└── README.md
```

## Running it

**Option 1 — run the prebuilt jar**

```bash
java -cp "PMSS.jar;lib/JTattoo-1.6.13.jar" PasswordManager     # Windows
java -cp "PMSS.jar:lib/JTattoo-1.6.13.jar" PasswordManager     # macOS/Linux
```

**Option 2 — compile from source**

```bash
cd src
javac -cp ../lib/JTattoo-1.6.13.jar *.java
java -cp ".;../lib/JTattoo-1.6.13.jar" PasswordManager     # Windows
java -cp ".:../lib/JTattoo-1.6.13.jar" PasswordManager     # macOS/Linux
```

## How the security works

1. When you add an account, `PasswordGenerator` can produce a random password from a full character set (upper, lower, digits, symbols).
2. Before anything is stored, `passwordEncryption` generates a random salt (`SHA1PRNG`) and hashes the password with it via SHA-1 — so identical passwords never produce identical stored values.
3. The salted hash is stored against the account name in `HashtablePassword`, a hash table implemented from scratch using **linear probing** for collision resolution, rather than a built-in Java collection.

## Presented at

**ICCES 2022 International Conference** — presented as a solution addressing digital security awareness among students, with potential as a mobile or system-based utility app.

## Author

**Arjun K**
- GitHub: [@Arjunkalliyadath](https://github.com/Arjunkalliyadath)
- Email: arjunkalliyadath2001@gmail.com
