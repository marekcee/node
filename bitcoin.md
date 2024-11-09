RUN BITCOIN
```
bitcoind -daemon

/usr/local/bin/bitcoin-qt
```
STOP
```
bitcoin-cli stop
```
AUTOSTART
```
crontab -e
@reboot /usr/local/bin/bitcoind -daemon
```
CONFIG
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
