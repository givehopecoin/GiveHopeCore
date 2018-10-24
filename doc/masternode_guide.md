# GiveHope
Shell script to install a [GiveHope Masternode](https://givehope.world/) on a Linux server running Ubuntu 16.04. Use it on your own risk.
***

## Installation
```
wget -q https://github.com/givehopecoin/masternode/blob/master/auto-install.sh
bash auto-install.sh
```
***

## Desktop wallet setup  

After the MN is up and running, you need to configure the desktop wallet accordingly. Here are the steps:  
1. Open the GiveHope Desktop Wallet.  
2. Go to RECEIVE and create a New Address: **MN1**  
3. Send **3000** HOPC to **MN1**. You need to send all 3000 coins in one single transaction.
4. Wait for 15 confirmations.  
5. Go to **Help -> "Debug Window - Console"**  
6. Type the following command: **masternode outputs**  
7. Open Windows Explorer and go to **%APPDATA%\givehope** folder
8. Open/create masternode.conf
9. Add the following entry:
```
Alias Address Privkey TxHash TxIndex
```
* Alias: **MN1**
* Address: **VPS_IP:PORT**
* Privkey: **Masternode Private Key**
* TxHash: **First value from Step 6**
* TxIndex:  **Second value from Step 6**
10. Save and close the file.
11. Open Windows Explorer and go to **%APPDATA%\givehope** folder
12. Open/create givehope.conf
13. Add this addnodes 
```
addnode=95.179.202.146:23375
addnode=144.202.48.152:23375
addnode=199.247.9.174:23375
addnode=45.63.65.67:23375
addnode=158.69.223.139:23375
addnode=104.168.167.66:23375
```
14. Save and close the file.
15. Open **Debug Console** and type:
```
masternode start-alias MN1
```
16. Login to your VPS and check your masternode status by running the following command. If you get **Status 9**, it means your masternode is active.
```
givehope-cli masternode status
```
***

## Usage:
```
givehope-cli mnsync status
givehope-cli masternode status  
givehope-cli getinfo
```
Also, if you want to check/start/stop **GiveHope**, run one of the following commands as **root**:

```
systemctl status givehope #To check if GiveHope2 service is running
systemctl start givehope #To start GiveHope2 service
systemctl stop givehope #To stop GiveHope2 service
systemctl is-enabled givehope #To check if GiveHope2 service is enabled on boot
```  
***

## Donations

Any donation is highly appreciated

**BTC**: 3CsdpkawMuhSqBrdvCcHacSyuzmjzHVTTR  
**ETH**: 0xd95D69c7BF0D611e436fcC49974FD48d24420036  
**LTC**: LgJSd5q3ETyZtDVEdocivxpPHrKQY5x31k  
