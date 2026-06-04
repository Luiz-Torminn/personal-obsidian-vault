---
type: concept
tags: [database, security, encryption, cryptography]
---
# What is encryption

Encryption protects the data value itself. It is useful for protecting sensitive data in case it is leaked (e.g., via backups, logs, or a database breach).

# Types of encryption

## One-way (Hashing)

Hashing is designed to be **non-reversible**. You store the hash and later verify by hashing the input again and comparing results (common for passwords).

Use the [[SQL Data Types#^6e49b1 |CHAR data type]] for hashed columns because hash outputs have a fixed length.

### BCrypt

- Generates a salt automatically.
- Outputs are typically **60 characters** long.

### SHA-512

- Does **not** generate a salt by default (you must add one yourself if needed).
- Outputs are typically **88 characters** long when Base64-encoded.

## Symmetric

Symmetric encryption is **reversible**: the same secret key is used to encrypt and decrypt the data. Use it when the application must be able to read the original value (e.g., some secrets or regulated fields, depending on requirements).

### AES-256

## Extras

### Payment Card Security Standards

![[Captura de Tela 2026-06-01 às 13.00.54.png|357]]