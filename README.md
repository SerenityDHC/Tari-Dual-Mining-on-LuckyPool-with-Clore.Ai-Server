# 🚀 Tari Dual Mining Setup Guide on LuckyPool using a CLORE.AI Server<br>

**Install Tari Universe at home to create a Tari and Monero Wallet: https://airdrop.tari.com/download/8uJGPuK4jX**
<br>
1️⃣ Rent a GPU/CPU server from CloreAI: https://clore.ai?ref_id=5dw6bmhr<br>
<br><br>

Open Powershell to connect to your rented server<br>
```bash
ssh root@<server_ip> -p <port#>
```
**Replace <server_ip> and <port#> with your server information**<br>
```example: ssh root@n1.de.clorecloud.net -p 1219```
<br>
Type "YES" to accept SSH Fingerprint
<br>
Enter SSH Password
<br><br>


2️⃣ Install Dependencie
```bash
apt update && apt upgrade -y
apt install wget unzip git build-essential cmake libhwloc-dev libuv1-dev libssl-dev -y
```
When prompted select "Keep the local version" option 2
<br><br>


3️⃣ Download & Extract SRBMiner-MULT and Change Directory to SRB-Miner-2-8-8
```bash
wget -O SRBMiner-MULTI.tar.gz https://github.com/doktor83/SRBMiner-Multi/releases/download/2.8.8/SRBMiner-Multi-2-8-8-Linux.tar.gz
tar -xzvf SRBMiner-MULTI.tar.gz
cd SRBMiner-Multi-2-8-8
```
<br><br>

 # ***⚒ Choose Your Mining Setup*** <br>

Option 1: Mines both CPU & GPU in a single instance ~ Simpler setup, but if an issue occurs, mining stops entirely.<br>
Option 2: Runs CPU and GPU mining separately ~ Slightly more setup, but allows independent operation to prevent full downtime if one fails.

<br><br>





# OPTION 1
1️⃣A   Create Startup Script
```bash
nano start_mining.sh
```
Copy this code into notepad
```
#!/bin/bash
# Get total available CPU threads dynamically
TOTAL_THREADS=$(nproc)
CPU_THREADS=$(( TOTAL_THREADS * 90 / 100 ))  # Set exactly 90% of available threads

# Start SRBMiner with SHA3X (Tari) on GPU + RandomX (Monero) on CPU (without huge pages)
./SRBMiner-MULTI \
  --algorithm sha3x \
  --pool <POOL>:6118 \
  --wallet <TARI_WALLET>.<WORKER_NAME> \
  --algorithm randomx \
  --pool mine-tari-monero.luckypool.io:8118 \
  --wallet <TARI_WALLET>+<MONERO_WALLET=DIFF.WORKER_NAME> \
  --enable-cpu \
  --disable-huge-pages \
  --cpu-threads $CPU_THREADS \
  --disable-msr-tweaks \
  --log-file /root/SRBMiner-Multi-2-8-8/debug.log \
 ```
Replace <TARI_WALLET>,<WORKER_NAME>, <MONERO_WALLET=DIFF.WORKER_NAME> with wallets listed on Tari Universe<br>
Adjust CPU thread usage if desired, currently using 95% of CPU threads.<br>
<DIFF> Difficulty based on CPU power, average 50000-100000<br> 
Replace <POOL> with closest server:<br>
France: 	  tari.luckypool.io<br>
Canada:    ca.luckypool.io<br>
Singapore: sg.luckypool.io  <br>
Poland:    pl-eu.luckypool.io<br>
Germany:   de-eu.luckypool.io<br><br>

Paste the edited notepad version into the start_mining.sh file<br>
Save the file:
- Press Ctrl + X (Exit nano)
- Press Y (Confirm save changes)
- Press Enter (Save the file with the same name)
<br><br>


1️⃣B Make the Script Executable
```bash
chmod +x start_mining.sh
```
<br><br>

1️⃣C Start Mining
```
./start_mining.sh
```

<br><br>

# OPTION 2
2️⃣A Create GPU Mining Startup Script
```bash
nano start_gpu_mining.sh
```
Copy this code into notepad 
```
#!/bin/bash
# Start SRBMiner with SHA3X (Tari) on GPU
./SRBMiner-MULTI \
  --algorithm sha3x \
  --pool <POOL>.io:6118 \
  --wallet <TARI_WALLET>.<WORKER_NAME> \
  --log-file /root/SRBMiner-Multi-2-8-8/gpu_debug.log \
 ```
Replace <TARI_WALLET>,<WORKER_NAME>, <MONERO_WALLET=DIFF.WORKER_NAME> with wallets listed on Tari Universe<br>
Replace <POOL> with closest server:<br>
France:    	tari.luckypool.io<br>
Canada:     ca.luckypool.io<br>
Singapore:  sg.luckypool.io  <br>
Poland:     pl-eu.luckypool.io<br>
Germany:    de-eu.luckypool.io<br><br>

Paste the edited notepad version into the start_gpu_mining.sh file

Save the file:
- Press Ctrl + X (Exit nano)
- Press Y (Confirm save changes)
- Press Enter (Save the file with the same name)
<br><br>
2️⃣B Create CPU Mining Startup Script
```bash
nano start_cpu_mining.sh
```
<br><br>
Copy this code into notepad 

Then paste the edited version into the start_gpu_mining.sh file
```
#!/bin/bash
TOTAL_THREADS=$(nproc)
CPU_THREADS=$(( TOTAL_THREADS * 95 / 100 ))  # Sets exactly 95% of available threads

# Start SRBMiner with SHA3X (Tari) on GPU + RandomX (Monero) on CPU
./SRBMiner-MULTI \
  --algorithm randomx \
  --pool mine-tari-monero.luckypool.io:8118 \
  --wallet <TARI_WALLET>+<MONERO_WALLET=DIFF.WORKER_NAME> \
  --enable-cpu \
  --disable-huge-pages \
  --cpu-threads $CPU_THREADS \
  --disable-msr-tweaks \
  --log-file /root/SRBMiner-Multi-2-8-8/debug.log \
 ```
Replace <TARI_WALLET>,<WORKER_NAME>, <MONERO_WALLET=DIFF.WORKER_NAME> with wallets listed on Tari Universe<br>
<WORKER_NAME> can be anything to identify worker<br>
<DIFF> Difficulty based on CPU power, average 50000-100000<br> 



Paste the edited version into the start_gpu_mining.sh file<br>

Save the file:
- Press Ctrl + X (Exit nano)
- Press Y (Confirm save changes)
- Press Enter (Save the file with the same name)
<br><br>

2️⃣C  Make both files executable
```
chmod +x start_cpu_mining.sh start_gpu_mining.sh
```
<br><br>
2️⃣D Start GPU Mining
```
./start_gpu_mining.sh
```
<br><br>
2️⃣E
Open a Second PowerShell Tab<br> 
Log in with same information
```bash
ssh root@<server_ip> -p <port#>
```
<br>
Enter SSH Password
<br><br>

2️⃣F
Change Directory to SRBMiner
```
cd SRBMiner-Multi-2-8-8
```
<br><br>
2️⃣G Start CPU Miner
```
./start_cpu_mining.sh
```


**Check your mining status for each pool:**
<br>

Tari (Sha3): https://tari.luckypool.io/<BR>
Use Tari Wallet Address
<BR><BR>
Monero (RandomX): https://tari-monero.luckypool.io/<BR>
Use Tari+Monero Wallet Address


