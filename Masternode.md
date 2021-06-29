
# SwapDEX Masternode Guide

This guide will explain the steps required to set up a Masternode for the SwapDEX Smart Chain.

## Requirements for running a masternode:-

The following are the <b> minimum recommended requirements </b> to run a Masternode smoothly. If you use lower capacity device or VPS, we cannot guarantee your Masternode will run smoothly and you may not receive the full allotment of rewards. Using a device or VPS with higher specifications is not fine, but is not required.

1) Ubuntu operating system with device or VPS with the following minimum specifications:
```bash
16GB RAM
120GB SSD
2 core CPU
```

2) A MetaMask wallet with at least 10,010 SDX in the wallet. While you only need 10,000 SDX to stake, we recommend the wallet holding a little more to cover gas fees.

## You are now ready to start installation process.

This guide is written for the Ubuntu Operating System version 20.
For those who are unfamiliar to using terminal commands in Ubuntu, you should write the commands written ``in these text boxes`` exactly as they are written in the guide and at the end of each line press enter.
There will be commands which require you confirm you want to proceed or times you are prompted to enter your VPS password.
This guide assumes you will confirm all processes and enter your password as required when prompted.

# Install Tmux, Go & Gvm

To run a Masternode, you will need Tmux Go & GVM.
For full details, you can refer to https://github.com/moovweb/gvm however this guide includes all the steps you will need.

```bash 
sudo apt update
sudo apt upgrade
sudo apt install git
sudo apt-get install tmux
bash < <(curl -s -S -L https://raw.githubusercontent.com/moovweb/gvm/master/binscripts/gvm-installer) 
```
Restart the terminal

```bashexport GOROOT_BOOTSTRAP=$G
sudo apt-get install curl git mercurial make binutils bison gcc build-essential
```

# Installing Go 1.13.8+
```bash
gvm install go1.13.8
gvm use go1.13.8
```

# Lets start building.
```bash
git clone https://github.com/69th-byte/SmartDex-Chain.git sdxchain
cd sdxchain 
make all
sudo mv /root/sdxchain/build/bin/sdx /usr/bin/sdx
```
# Last step of running Masternode.
```bash
sdx account new
[ENTER SECURE PASSWORD]
```
Take a note of the Address that is created, this is your server generated SDX Masternode Account Address.

```bash
sdx init swapdex.json
nano pass.txt
```

## $ Put the password here which you used to create server generated SDX Masternode Account.
ctrl + x & y enter to save then exit the txt

Open tmux
```bash
tmux
```
Now you will need to enter the details for your node. Entries within square brackets will be unique to each user, please remove the square brackets, but keep the quotation marks.
```bash
sdx  --syncmode "full" --networkid 7879 --port 10303 --rpc --rpccorsdomain "*" --rpcaddr 0.0.0.0 --rpcport 8501 --rpcvhosts "*"   --rpcapi "db,eth,net,web3,personal,debug" --gcmode "archive" --identity "[Name for node]" --etherbase "[SDX Masternode Account address]" --unlock "[SDX Masternode Account address]" --password pass.txt console
```

## Congratulations, you have now set up your own Masternode.

The final step is to go to the SDXMaster site to stake your 10,000 SDX and attach your wallet to your node so you can start receiveing rewards.

These details will be finalised once SDXMaster is finished...
