# Tari-Mining-with-Clore.AI
This guide will help you setup a multiminer on a rented Clore.Ai server. This will mine on both Sha3 + RandomX.

# 🚀 Dual Mining Setup Guide (SHA3X + RandomX)

## 1️⃣ Rent & Access the Server
Rent a GPU/CPU server from CloreAI: https://clore.ai?ref_id=5dw6bmhr

Open Powershell to connect to your rented server<br>
**Replace Serever IP and Port**
```bash
ssh root@<server_ip> -p <port>
```
*example: ssh root\@n1.de.clorecloud.net -p 1219*
<br>


2️⃣ Install Dependencie
```bash
apt update && apt upgrade -y
apt install wget unzip git build-essential cmake libhwloc-dev libuv1-dev libssl-dev -y
```
When prompted select "Use Existing SSH" option 2
<br>


3️⃣ Download & Extract SRBMiner-MULT and Change Directory to SRB-Miner-2-8-8
```bash
wget -O SRBMiner-MULTI.tar.gz https://github.com/doktor83/SRBMiner-Multi/releases/download/2.8.8/SRBMiner-Multi-2-8-8-Linux.tar.gz
tar -xzvf SRBMiner-MULTI.tar.gz
cd SRBMiner-Multi-2-8-8
```
<br>


4️⃣ Create Startup Script
```bash
nano start_mining.sh
```
Replace Tari wallet address, Monerao wallet address and Miner names.
```bash
#!/bin/bash
cd /root/SRBMiner-Multi-2-8-8
./SRBMiner-MULTI --algorithm sha3x --pool tari.luckypool.io:6118 --wallet TARI_WALLET+MONERO_WALLET=DIFF.WORKERNAME --algorithm randomx --pool mine-tari-monero.luckypool.io:8118 --enable-cpu --disable-huge-pages
```
Save the file:
- Press Ctrl + X (Exit nano)
- Press Y (Confirm save changes)
- Press Enter (Save the file with the same name)
<br>


5️⃣ Make the Script Executable & Start Mining
```bash
chmod +x start_mining.sh
./start_mining.sh
```
<br>


6️⃣ Keep SRBMiner Running in Background
To keep mining active even after disconnecting:
```bash
screen -S srminer
./start_mining.sh
```
- Detach: (Ctrl+A, then D).
- Reattach anytime:
```bash
screen -r srminer
```
