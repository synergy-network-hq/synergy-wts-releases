# synergy-wts CLI tool

The `synergy-wts` CLI tool is the public-facing community version of the Synergy Address Engine.

It is designed for interactive terminal use. When you launch `synergy-wts`, it opens an arrow-key driven menu with a startup banner, and you move through the available functions with the keyboard instead of typing long command strings.

This tool allows the community to create the following Synergy Testnet-beta assets:

- Wallets
- Fungible tokens
- NFT collections
- Multi-asset token contracts
- Custom contract identities
- General multisig identities

## What It Does

The `synergy-wts` CLI tool currently supports:

- Interactive arrow-key navigation for all primary community workflows
- Generating community-safe Synergy identities
- Producing public metadata files and encrypted private-key files
- Building full wallet outputs with seed phrases for wallet address types
- Preparing on-chain token and NFT deployment transactions
- Submitting token and NFT deployment transactions over JSON-RPC when a reachable Synergy node is provided
- Decrypting previously generated encrypted key files
- Verifying that an address matches a public key
- Listing supported community address types
- Listing supported cryptographic algorithms
- Printing the canonical burn address

All generated private key material is written in encrypted form using the CLI's hybrid encryption flow.

## Community Address Types

The following address types are open to the community in the `synergy-wts` CLI tool.

| Prefix | Type | Standard | Purpose |
| --- | --- | --- | --- |
| `synw` | Primary Wallet | Wallet | Main user wallet |
| `syns` | Secondary / Utility Wallet | Wallet | Secondary user wallet for operational separation |
| `syna` | Standard Account | Wallet | General-purpose account identity |
| `synz` | UMA Smart Wallet | Wallet | Smart-wallet style account |
| `synb1` | Fungible Token Tier 1 | STS-9 | Community fungible token deployment |
| `synb2` | Fungible Token Tier 2 | STS-9 | Community fungible token deployment |
| `synb3` | Fungible Token Tier 3 | STS-9 | Community fungible token deployment |
| `synn1` | NFT Collection Type 1 | STS-NF | Community NFT collection deployment |
| `synn2` | NFT Collection Type 2 | STS-NF | Community NFT collection deployment |
| `synj` | Multi-Asset Token | STS-MA | Multi-asset game and application contracts |
| `sync` | Custom Contract | Contract | Community-deployed custom contract identity |
| `synm` | General Multisig | Multisig | Shared control identity |

## Installation

Download the release archive that matches your platform:

- `synergy-wts-macos-arm64.tar.gz`
- `synergy-wts-linux-x64.tar.gz`
- `synergy-wts-windows-x64.zip`

### macOS and Linux

```bash
tar xzf synergy-wts-macos-arm64.tar.gz
chmod +x synergy-wts
sudo mv synergy-wts /usr/local/bin/
```

### Windows

1. Extract `synergy-wts.exe` from the release zip.
2. Place it in a directory you control.
3. Add that directory to `PATH`, or run it directly from PowerShell or Command Prompt.

### Verify the Download

Each release archive includes a `.sha256` checksum file.

```bash
shasum -a 256 -c synergy-wts-macos-arm64.tar.gz.sha256
```

### macOS Gatekeeper Note

The public release binaries are not Apple code-signed. On first run, macOS may block the binary. Use one of these methods:

- Right-click `synergy-wts` in Finder and choose `Open`
- Remove the quarantine flag:

```bash
xattr -d com.apple.quarantine /usr/local/bin/synergy-wts
```

- Open it once, then approve it in `System Settings > Privacy & Security`

## Getting Started

To open the interactive interface, run:

```bash
synergy-wts
```

When the tool starts, it displays the startup banner and opens the main menu. Use:

- `Up` and `Down` arrow keys to move through options
- `Enter` to select
- Text prompts when the tool asks for names, output file bases, metadata, RPC details, or verification inputs

The main menu currently includes:

- `Generate address, wallet, token, or contract`
- `Decrypt an encrypted key file`
- `Verify an address against a public key`
- `List community address types`
- `List supported algorithms`
- `Show burn address`
- `Exit`

## Interactive Generation Flow

When you choose `Generate address, wallet, token, or contract`, the tool walks you through the correct prompts for the selected community-safe address type.

The general flow is:

1. Choose an address type
2. Choose a cryptographic algorithm
3. Enter an output base name
4. Complete any additional prompts required for that asset type
5. Enter an encryption passphrase when prompted
6. Receive the generated `.pub.json` and `.enc.json` files

### Wallets

Wallet address types are:

- `synw`
- `syns`
- `syna`
- `synz`

For wallet types, the interactive flow lets you choose between:

- `Generate address only`
- `Generate full wallet with seed phrase`

If you choose full wallet generation, the tool then asks you to choose:

- `12 words`
- `24 words`

Wallet-mode output includes:

- Synergy address
- Public key
- Encrypted private key
- Seed phrase
- External address metadata generated by the wallet flow

### STS-9 Fungible Tokens

Fungible token address types are:

- `synb1`
- `synb2`
- `synb3`

For STS-9 generation, the interactive flow prompts for:

- Deployment mode
- Chain ID
- Network identifier
- RPC node URL if you choose live submission
- Optional manual nonce
- Gas limit
- Gas price
- Metadata URI
- Metadata file path
- Token name
- Token symbol
- Decimals
- Maximum supply
- Initial supply
- Mintable setting
- Burnable setting
- Pausable setting

The tool can either:

- Prepare a dry-run transaction without submitting it
- Submit the deployment to a reachable Synergy JSON-RPC node

### STS-NF NFT Collections

NFT collection address types are:

- `synn1`
- `synn2`

For STS-NF generation, the interactive flow prompts for:

- Deployment mode
- Chain ID
- Network identifier
- RPC node URL if you choose live submission
- Optional manual nonce
- Gas limit
- Gas price
- Metadata URI
- Metadata file path
- Collection name
- Collection symbol
- Collection type
- Display title
- Description
- Media type
- Default token URI

The tool can either:

- Prepare a dry-run deployment package
- Submit the collection deployment to a reachable Synergy JSON-RPC node

### STS-MA Multi-Asset Contracts

The multi-asset community address type is:

- `synj`

For STS-MA generation, the interactive flow prompts for:

- Deployment mode
- Chain ID
- Network identifier
- RPC node URL if you choose live submission
- Optional manual nonce
- Gas limit
- Gas price
- Metadata URI
- Metadata file path
- Contract name
- Asset ID
- Asset type
- Asset name
- Asset symbol
- Decimals
- Maximum supply
- Initial supply
- Transferability
- Mintable setting
- Burnable setting

This flow supports multi-asset deployments for gaming and application-oriented use cases.

### Custom Contracts

The custom contract community address type is:

- `sync`

For custom contracts, the tool generates the contract identity artifacts and encrypted key material. Runtime logic and deployment behavior remain application-specific.

### General Multisig

The community multisig address type is:

- `synm`

For general multisig identities, the tool generates the multisig identity artifacts and encrypted key material. Signer policy, thresholds, and governance behavior are not configured automatically by this CLI.

## Decrypting Encrypted Output

Choose `Decrypt an encrypted key file` from the main menu.

The tool will prompt for:

- Encrypted file path
- Output file path

After you provide the correct passphrase, it writes the decrypted private-key material to the output path you selected.

## Verifying an Address

Choose `Verify an address against a public key` from the main menu.

The tool will prompt for:

- Address
- Base64 public key

It then checks whether the address matches the provided public key.

## Listing Address Types, Algorithms, and Burn Address

The main menu also provides direct read-only options for:

- `List community address types`
- `List supported algorithms`
- `Show burn address`

These options are useful for inspection and reference without generating any new assets.

## Output Files

Identity generation writes two files using the output base name you provide during the interactive flow:

- `<NAME>.pub.json`
- `<NAME>.enc.json`

### Public File

The public file contains non-secret material such as:

- Address
- Public key
- Address type
- Algorithm
- Creation timestamp
- Wallet metadata for wallet outputs
- Token metadata and on-chain deployment data for token standards

### Encrypted Private File

The encrypted private file contains private key material protected by the CLI's encryption envelope.

For wallet outputs, the encrypted file also contains the seed phrase.

For token and NFT flows, the generated public output may also include deployment-oriented data such as:

- Contract address
- Issuer address
- Canonical metadata hash
- Asset fingerprint
- Deployment transaction payload
- Human-readable deployment manifest
- Signed issuer genesis attestation
- Deployment transaction hash and ID

## Supported Algorithms

The `synergy-wts` CLI tool supports the algorithm families exposed by the engine for community-safe generation:

- `ml-dsa-44`
- `ml-dsa-65`
- `ml-dsa-87`
- `fn-dsa-512`
- `fn-dsa-1024`
- `ml-kem-512`
- `ml-kem-768`
- `ml-kem-1024`
- `hqc-128`
- `hqc-192`
- `hqc-256`
- `ed25519`

For on-chain token deployment, use a signature algorithm. KEM algorithms are not valid for signing deployment transactions.

## Security Notes

- Keep `.enc.json` files and passphrases separate
- Treat decrypted private-key files as highly sensitive
- Use dry-run mode first when preparing a token or NFT deployment
- Preserve the generated public file for auditability and later verification
- Unverified token outputs should be treated as unverified until accepted by the canonical registry flow

## Quick Start

1. Install the `synergy-wts` binary for your platform
2. Run `synergy-wts`
3. Choose `Generate address, wallet, token, or contract`
4. Select the community address type you want to create
5. Follow the prompts until the tool writes your `.pub.json` and `.enc.json` files
