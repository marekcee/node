RUN BITCOIN
```
bitcoind -daemon

/usr/local/bin/bitcoin-qt

bitcoin-cli stop
```
AUTOSTART
```
crontab -file
@reboot /usr/local/bin/bitcoind -daemon
```
CONFIG F
```
sudo nano /home/pi/.bitcoin/bitcoin.conf
```
------------------------------------------

CLI INTERACTIONS
```
bitcoin-cli -getinfo
bitcoin-cli -netinfo
bitcoin-cli getblockchaininfo
bitcoin-cli getblockcount
bitcoin-cli getnetworkinfo
bitcoin-cli getconnectioncount
```
------------------------------------------
