# INSTALLATION WALRUS CLI

## 1. **Install via Script (Recommended for macOS & Linux)**

Open your terminal and run one of the following commands:

```sh
# Install the latest Mainnet version
curl -sSf https://install.wal.app | sh

# Install the latest Testnet version
curl -sSf https://install.wal.app | sh -s -- -n testnet

# Update an existing installation (overwrites prior version)
curl -sSf https://install.wal.app | sh -s -- -f
```

- This will install `walrus` to your `"$HOME"/.local/bin` directory.
- **Make sure** that `"$HOME"/.local/bin` is in your `$PATH`.

---

## 2. **Install on Windows**

Open **PowerShell** and run:

```powershell
(New-Object System.Net.WebClient).DownloadFile(
  "https://storage.googleapis.com/mysten-walrus-binaries/walrus-testnet-latest-windows-x86_64.exe",
  "walrus.exe"
)
```

- Move `walrus.exe` to a directory in your `PATH`.

---

## 3. **Install via suiup (Experimental, All Platforms)**

If you use [suiup](https://github.com/MystenLabs/suiup?tab=readme-ov-file#installation):

```sh
suiup install walrus@testnet      # Latest testnet release
suiup install walrus@mainnet      # Latest mainnet release
suiup install walrus@testnet-v1.27.1 # Specific release
```

---

## 4. **Install via Cargo (Rust Users)**

If you have Rust and Cargo installed:

```sh
cargo install --git https://github.com/MystenLabs/walrus --branch mainnet walrus-service --locked
```

- You can also specify a tag or commit with `--tag` or `--rev`.

---

## 5. **Download from GitHub Releases**

Go to [Walrus GitHub Releases](https://github.com/MystenLabs/walrus/releases), download the binary for your OS, and extract it.

---

## 6. **Build from Source**

Clone the repo and follow the instructions in the `README.md` to build from source:  
[https://github.com/MystenLabs/walrus](https://github.com/MystenLabs/walrus)

---

**After installation**, you can check if it works by running:

```sh
walrus --help
```

---

# CLIENT CONFIG FILE

Here is a sample `client_config.yaml` file for Walrus, as provided in the official documentation. This file supports both Mainnet and Testnet configurations and is placed at `~/.config/walrus/client_config.yaml`:

```yaml
contexts:
  mainnet:
    system_object: 0x2134d52768ea07e8c43570ef975eb3e4c27a39fa6396bef985b5abc58d03ddd2
    staking_object: 0x10b9d30c28448939ce6c4d6c6e0ffce4a7f8a4ada8248bdad09ef8b70e4a3904
    exchange_objects: []
    wallet_config:
      # Optional path to the wallet config file.
      # path: ~/.sui/sui_config/client.yaml
      # Sui environment to use.
      active_env: mainnet
      # Optional override for the Sui address to use.
      # active_address: 0x0000000000000000000000000000000000000000000000000000000000000000
    rpc_urls:
      - https://fullnode.mainnet.sui.io:443
  testnet:
    system_object: 0x6c2547cbbc38025cf3adac45f63cb0a8d12ecf777cdc75a4971612bf97fdf6af
    staking_object: 0xbe46180321c30aab2f8b3501e24048377287fa708018a5b7c2792b35fe339ee3
    exchange_objects:
      - 0xf4d164ea2def5fe07dc573992a029e010dba09b1a8dcbc44c5c2e79567f39073
      - 0x19825121c52080bb1073662231cfea5c0e4d905fd13e95f21e9a018f2ef41862
      - 0x83b454e524c71f30803f4d6c302a86fb6a39e96cdfb873c2d1e93bc1c26a3bc5
      - 0x8d63209cf8589ce7aef8f262437163c67577ed09f3e636a9d8e0813843fb8bf1
    wallet_config:
      # Optional path to the wallet config file.
      # path: ~/.sui/sui_config/client.yaml
      # Sui environment to use.
      active_env: testnet
      # Optional override for the Sui address to use.
      # active_address: 0x0000000000000000000000000000000000000000000000000000000000000000
    rpc_urls:
      - https://fullnode.testnet.sui.io:443
default_context: testnet
```

**How to use:**
- Place this file at `~/.config/walrus/client_config.yaml`.
- You can switch between `mainnet` and `testnet` by changing the `default_context` or using the `--context` flag in CLI commands.
- Update the `wallet_config` section with your actual wallet path and address if needed.

---

# WAL Faucet on Walrus Testnet

## What is it?
- The WAL faucet allows you to obtain Testnet WAL tokens, which are used to buy storage and stake on the Walrus Testnet.
- Testnet WAL tokens have no real-world value and are only for testing and development.

---

## How to Use the WAL Faucet

1. **Prerequisites**
   - You need a Sui Testnet wallet with some SUI tokens.
   - You can set this up using the Sui CLI or generate a wallet with:
     ```sh
     walrus generate-sui-wallet --sui-network testnet
     ```
   - Make sure your wallet is connected to the Sui Testnet (`https://fullnode.testnet.sui.io:443`).

2. **Get Testnet SUI**
   - Use the [Sui Testnet faucet](https://faucet.sui.io/?network=testnet) to get SUI for gas.

3. **Request WAL from the Faucet**
   - Run the following command:
     ```sh
     walrus get-wal
     ```
   - By default, 0.5 SUI are exchanged for 0.5 WAL.
   - You can specify a different amount (in MIST/FROST) with the `--amount` option.
   - You can also specify a particular SUI/WAL exchange object with the `--exchange-id` option.
   - For more options, run:
     ```sh
     walrus get-wal --help
     ```

4. **Check Your WAL Balance**
   - After a few seconds, check your balances:
     ```sh
     sui client balance
     ```
   - Example output:
     ```
     │ Sui   8869252670        8.86 SUI    │
     │ WAL   500000000         0.50 WAL    │
     ```

---
# Store DATA on Walrus 

## 1. Store `music.txt` for 10 days

Walrus uses **epochs** for storage duration. On Mainnet, **1 epoch = 14 days**.  
To store for 10 days, you need to store for **1 epoch** (the minimum unit).

**Command:**
```sh
walrus store music.txt --epochs 1
```
- This will store `music.txt` for 1 epoch (14 days).  
- There is no way to store for less than 1 epoch.

**Reference:**  
> The epoch duration on Mainnet is 2 weeks.  
> [Source](https://docs.wal.app/usage/client-cli.html)

---

## 2. Store `music.txt` "forever" (maximum duration)

The maximum is **53 epochs** (about 2 years).  
To store for the maximum allowed time:

**Command:**
```sh
walrus store music.txt --epochs max
```
or
```sh
walrus store music.txt --epochs 53
```

**Reference:**  
> There is an upper limit on the number of epochs a blob can be stored for, which is 53, corresponding to two years. In addition to a positive integer, you can also use `--epochs max` to store the blob for the maximum number of epochs.  
> [Source](https://docs.wal.app/usage/client-cli.html)

---

## 3. Store as Permanent (not deletable before expiry)

By default, blobs are **deletable** (can be deleted before expiry).  
To make it **permanent** (cannot be deleted before expiry):

**Command for 10 days (1 epoch):**
```sh
walrus store music.txt --epochs 1 --permanent
```

**Command for maximum duration:**
```sh
walrus store music.txt --epochs max --permanent
```

---

## Summary Table

| Duration         | Command                                              |
|------------------|-----------------------------------------------------|
| 10 days (1 epoch)| `walrus store music.txt --epochs 1 [--permanent]`   |
| Forever (max)    | `walrus store music.txt --epochs max [--permanent]` |

---

**Note:**  
- All blobs on Walrus are public and discoverable by all. Do not store secrets or private data without additional protection.
- You can check the status of your blob with:
  ```sh
  walrus blob-status --file music.txt
  ```
---

# WALRUS DOCUMENT

https://docs.wal.app/docs/usage/setup#configuration
