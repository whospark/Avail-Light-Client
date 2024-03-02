🚀 Setting up your Avail Light Client - A step-by-step guide! 🌐

**Part 1: Preparations**
To get started, update your packages by running these commands in the terminal:

```bash
sudo apt update && sudo apt upgrade -y
sudo apt install make git nano clang pkg-config libssl-dev build-essential
```

**Part 2: Install Rust**
Install Rust using rustup installer. Enter "1" for the default installation when prompted.

```bash
curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh
source $HOME/.cargo/env
rustc --version
```

**Part 3: Download And Build Light Client Binaries**
Clone the repository and build the Light Client with Cargo:

```bash
git clone https://github.com/availproject/avail-light.git
cd avail-light
cargo build --release
```

**Part 4: Create Avail Light Client Service**
Install the Avail Light Client Service:

```bash
sudo tee /etc/systemd/system/availightd.service > /dev/null <<EOF
[Unit]
Description=Avail Light Client
After=network.target
StartLimitIntervalSec=0
[Service]
User=root
ExecStart=/root/avail-light/target/release/avail-light --network goldberg
Restart=always
RestartSec=120
[Install]
WantedBy=multi-user.target
EOF
```

**Part 5: Register And Start Avail Light Client Service**
Register and start the Avail Light Client Service:

```bash
sudo systemctl daemon-reload
sudo systemctl enable availightd
sudo systemctl restart availightd
```

**Part 6: Change Your Avail Wallet**
If you have an existing wallet, stop the Avail Light Client, edit the identity.toml file, and restart the service:

```bash
sudo systemctl stop availightd
nano /identity.toml
# Insert your secret seed phrase
sudo systemctl daemon-reload
sudo systemctl restart availightd
```

**Check Your Service Logs**
Monitor your Service Logs and manage the Avail Light client with these commands:

```bash
systemctl status availightd.service
journalctl -u availightd -fo cat
```

🌟 Now you're all set! Explore the world of Avail Light Client and contribute to the Incentivized Testnet. Don't forget to mint NFTs for support! 🚀🔗 #Avail #AvailLightClient #Web3 #CryptoGuide
