# Tari-Mining-with-Clore.AI
This guide will help you setup a multiminer on a rented Clore.Ai server. This will mine on both Sha3 +  RandomX.

# 🚀 Dual Mining Setup Guide (SHA3X + RandomX)

## **1️⃣ Rent & Access the Server**
Choose a **GPU/CPU server** from **CloreAI or another provider**, then connect:
```bash
ssh root@<server_ip> -p <port>

2️⃣ Install Dependencie
apt update && apt upgrade -y
apt install wget unzip git build-essential cmake libhwloc-dev libuv1-dev libssl-dev -y

3️⃣ Download & Extract SRBMiner-MULT
wget -O SRBMiner-MULTI.tar.gz https://github.com/doktor83/SRBMiner-Multi/releases/download/2.8.8/SRBMiner-Multi-2-8-8-Linux.tar.gz
tar -xzvf SRBMiner-MULTI.tar.gz
cd SRBMiner-Multi-2-8-8

4️⃣ Create Startup Script
#!/bin/bash
cd /root/SRBMiner-Multi-2-8-8
./SRBMiner-MULTI --algorithm sha3x --pool tari.luckypool.io:6118 --wallet TARI_WALLET+MONERO_WALLET=DIFF.WORKERNAME --algorithm randomx --pool mine-tari-monero.luckypool.io:8118 --enable-cpu --disable-huge-pages

5️⃣ Make the Script Executable & Start Mining
chmod +x start_mining.sh
./start_mining.sh
