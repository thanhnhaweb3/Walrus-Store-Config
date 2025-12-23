# 1 INSTALLATION 

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

**References:**  
- [Official Walrus Setup Guide](https://docs.wal.app/usage/setup.html)  
- [GitHub Releases](https://github.com/MystenLabs/walrus/releases)

---

Do you need help with a specific OS or installation method?
