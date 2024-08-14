
<table border=10 align=center>
  <tr>
    <td><img src="https://github.com/user-attachments/assets/da5331f5-f19a-418d-affc-a1dceaa24d12" width=150></td>
  </tr>
</table>

This guide was made by user: KALElist

<h1 align=center> How-to-run-0g-Validator-Node </h1>
This simple guide will talk about how to become a 0g labs project validator. It will be very easy)

### 1. **Prepare the Server**
- **Hardware Requirements**:
  - 64 GB RAM
  - 8-Core CPU
  - 1 TB NVMe SSD
  - 100 Mbps Network

### 2. **Install Dependencies**
- Ensure `git`, `Go`, and other dependencies are installed:
  ```bash
  sudo apt update && sudo apt install build-essential git curl jq -y
  ```

- **Install Go** (version 1.19+):
  ```bash
  wget https://golang.org/dl/go1.19.linux-amd64.tar.gz
  sudo tar -C /usr/local -xzf go1.19.linux-amd64.tar.gz
  export PATH=$PATH:/usr/local/go/bin
  ```

### 3. **Clone and Build 0G Chain**
- Clone the 0G repository:
  ```bash
  git clone -b v0.2.3 https://github.com/0glabs/0g-chain.git
  cd 0g-chain
  make install
  ```

### 4. **Configure Node**
- **Initialize the node**:
  ```bash
  0gchaind init <your_node_name> --chain-id zgtendermint_16600-2
  ```

- **Download `genesis.json`**:
  Replace the existing `genesis.json` with the correct file from the network.
  
- **Edit `config.toml`**:
  Set peers and seeds, ensuring you connect with other nodes in the network.

### 5. **Start the Node**
- Run the node:
  ```bash
  0gchaind start
  ```

### 6. **Create Validator**
1. **Generate a new key** for your validator:
   ```bash
   0gchaind keys add <your_validator_name>
   ```

2. **Send some funds** to your wallet (obtain testnet tokens or mainnet ZG tokens).

3. **Create the validator**:
   ```bash
   0gchaind tx staking create-validator \
   --amount <amount_in_uzg> \
   --pubkey $(0gchaind tendermint show-validator) \
   --moniker "<your_validator_name>" \
   --chain-id zgtendermint_16600-2 \
   --commission-rate 0.10 \
   --commission-max-rate 0.20 \
   --commission-max-change-rate 0.01 \
   --min-self-delegation 1 \
   --gas auto \
   --from <your_wallet_name>
   ```

4. **Check your validator status**:
   ```bash
   0gchaind query staking validator $(0gchaind keys show <your_wallet_name> --bech val -a)
   ```

### 7. **Optional: Configure Validator Monitoring**
- Install monitoring tools like Prometheus and Grafana for network statistics.
