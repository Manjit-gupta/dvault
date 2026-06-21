# dVault

`dVault` is a decentralized secret delivery system for edge devices. It combines smart contracts, IPFS, and encrypted key exchange to securely rotate and distribute certificates, SSH keys, API tokens, and other private data.

## Why it matters

The IIoT and DePIN sectors are growing fast, with billions of connected devices expected in the near future. Securely distributing and rotating private data to remote devices is critical for maintaining trust, preventing compromise, and reducing reliance on centralized infrastructure.

| Problem | dVault solution |
| - | - |
| No secure decentralized way to distribute private data across devices. Centralized solutions are not transparent and require infrastructure. | Use smart contracts for integrity and IPFS for distributed storage so secrets can be shared without a central server. |

## Benefits

- Activity history is publicly available and immutable.
- No centralized or managed infrastructure required.
- Transparent integrity without trusting a third party.
- Distributed responsibility and stronger fault tolerance.

## Use cases

### SSH key rotation

Remote access to drones, vehicles, and robots often depends on SSH. Secure key rotation improves overall system security by making credential updates frequent and automated.

Typical rotation flow:

1. Issue a new SSH key pair.
2. Sign the key pair with a certificate authority (CA).
3. Deliver the encrypted key pair to the device.
4. Revoke the old key pair.

`dVault` enables this flow to run securely and repeatedly.

## How it works

The system uses a combination of smart contract verification, encrypted storage, and distributed delivery:

1. Admin generates a new key pair for a client or server.
2. The key pair is signed by a Certificate Authority (CA).
3. Using Diffie-Hellman key exchange, the key pair is encrypted.
4. The encrypted data is stored on IPFS.
5. Smart contracts publish metadata and verify the integrity of the delivered secret.
6. Clients download from IPFS, decrypt the data, and apply the new key pair.

With this approach, the client can verify the secret belongs to the correct admin, and keys can be rotated without relying on a centralized server.

This model also works for TLS certificates and other secret material that must be distributed securely.

## Advantages

1. Certificate authority actions and key operations are publicly auditable.
2. System activity history remains immutable.
3. Secret distribution is safer and more transparent.
4. Certificate and key rotation becomes faster and easier.
5. No centralized infrastructure or cloud dependency.
6. Distributed trust improves resilience against security failures.
7. A hacked root CA can be replaced quickly.
8. Secret storage is decentralized rather than centralized.
9. Smart contracts make integrity logic auditable.
10. Only the smart contract private key holder can issue or revoke certificates.

## Future work

### Decentralized SSH certificate authority

A smart contract can act as a distributed trust anchor instead of a centralized SSH CA. Devices would trust the contract and the admin public key interacting with it, allowing secure key delivery and policy enforcement through `authorized_keys` updates.

### Temporary IIoT device access

For short-lived device access, issue a temporary SSH or certificate key pair, deliver it to the device, and revoke it after the task is complete. This enables secure, time-limited access with rollback protection.

### Microservices communication

For cloud-native deployments, `dVault` can provide per-service key pairs and distribute public keys to other services. This supports secure microservice communication with automated trust updates.
