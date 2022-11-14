# Security

## Vault Data

All Vault data is encrypted on your local device before being sent to the MicroPass server.
This means that even if your data is compromised, it will be useless without the encryption key.

## Encryption

MicroPass uses [AES](https://en.wikipedia.org/wiki/Advanced_Encryption_Standard)-[CBC](https://en.wikipedia.org/wiki/Block_cipher_mode_of_operation#Cipher_block_chaining_(CBC)) 256-bit encryption
for all your Vault data, and [PBKDF2](https://en.wikipedia.org/wiki/PBKDF2) SHA-256 to derive your encryption key from your master password.

## Encryption Key

Encryption Key is derived from your master password using PBKDF2 SHA-256, using 100,000 iterations using your email address as salt, and then there is an additional iteration with a random salt.

## AES-CBC

[AES](https://en.wikipedia.org/wiki/Advanced_Encryption_Standard)-CBC [(Cipher Block Chaining)](https://en.wikipedia.org/wiki/Block_cipher_mode_of_operation#Cipher_block_chaining_(CBC))
is used to encrypt all Vault data, is a standard in cryptography and used by the US government and other government agencies around the world for protecting top-secret data.

## PBKDF2

SHA-256 is used to derive the encryption key from your master password.
MicroPass [salts](https://www.okta.com/blog/2019/03/what-are-salted-passwords-and-password-hashing/) and hashes your master password with your email address and hashes **on your local device**.
The Encryption Key has one additional SHA-256 iteration with a random salt and the Master Password has an additional SHA-512 iteration with email address as salt before being sent to the server.

The iterations count used with PBKDF2 is 100,001 (100,000 + 1) on the client, and then an additional 120,000 iterations on our servers (for a total of 220,001 iterations).

The utilized hash function are one-way hashes, meaning they cannot be reverse engineered by anyone at MicroPass to reveal your master password.

## Cryptography Libraries Used

**MicroPass does not write any cryptographic code.**

- Golang (Server and TODO CLI)
    - [crypto](https://github.com/golang/go/tree/master/src/crypto)
    - [golang.org/x/crypto](https://github.com/golang/crypto)
- Dart (Mobile)
    - [pointycastle](https://github.com/bcgit/pc-dart)
