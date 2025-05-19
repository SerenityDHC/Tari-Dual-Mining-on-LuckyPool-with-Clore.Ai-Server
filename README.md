# Tari-Mining-with-Clore.AI
This guide will help you setup a multiminer on a rented Clore.Ai server. This will mine on both Sha3 + RandomX.

# 🚀 Dual Mining Setup Guide (SHA3X + RandomX)

#Install Tari Universe to create a Tari and Monero Wallet: 
1️⃣ Rent & Access the Server
Rent a GPU/CPU server from CloreAI: https://clore.ai?ref_id=5dw6bmhr

Open Powershell to connect to your rented server<br>
**Replace <server_ip> and <port>**
```bash
ssh root@<server_ip> -p <port>
```
```*example: ssh root@n1.de.clorecloud.net -p 1219*```
<br><br>


2️⃣ Install Dependencie
```bash
apt update && apt upgrade -y
apt install wget unzip git build-essential cmake libhwloc-dev libuv1-dev libssl-dev -y
```
When prompted select "Use Existing SSH" option 2
<br><br>


3️⃣ Download & Extract SRBMiner-MULT and Change Directory to SRB-Miner-2-8-8
```bash
wget -O SRBMiner-MULTI.tar.gz https://github.com/doktor83/SRBMiner-Multi/releases/download/2.8.8/SRBMiner-Multi-2-8-8-Linux.tar.gz
tar -xzvf SRBMiner-MULTI.tar.gz
cd SRBMiner-Multi-2-8-8
```
<br><br>


4️⃣ Create Startup Script
```bash
nano start_mining.sh
```
Copy this code into notepad and replace <TARI_WALLET>, <MONERO_WALLET=DIFF.WORKERNAME> with wallets listed on Tari Universe
```*./SRBMiner-MULTI --algorithm sha3x --pool tari.luckypool.io:6118 --wallet 122fAGPkVujEx****ALY1RFbBAMjaPpC+41yhipnXz7Cdnxo****f73UJ1vBpQ=500000.Serenity1 --algorithm randomx --pool mine-tari-monero.luckypool.io:8118 --enable-cpu --disable-huge-pages*```
Then paste the edited version into the start_mining.sh file
```bash
#!/bin/bash
cd /root/SRBMiner-Multi-2-8-8
./SRBMiner-MULTI --algorithm sha3x --pool tari.luckypool.io:6118 --wallet <TARI_WALLET>+<MONERO_WALLET=DIFF.WORKERNAME> --algorithm randomx --pool mine-tari-monero.luckypool.io:8118 --enable-cpu --disable-huge-pages
```
Save the file:
- Press Ctrl + X (Exit nano)
- Press Y (Confirm save changes)
- Press Enter (Save the file with the same name)
<br><br>


5️⃣ Make the Script Executable & Start Mining
```bash
chmod +x start_mining.sh
./start_mining.sh
```
<br><br>


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
