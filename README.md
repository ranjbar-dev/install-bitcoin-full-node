# Install bitcoin full node
this rep is simplified documentation of https://bitcoin.org/en/full-node#what-is-a-full-node


### Minimum Requirements
- 4 Gigabytes of memory
- 500 Gigabytes of free disk
- An unMetered connection, a connection with high upload limits


### Download and install bitcoin core 
check this url for latest bitcoin core version https://bitcoin.org/bin
```
sudo curl -o ./bitcoin.tar.gz https://bitcoin.org/bin/bitcoin-core-22.0/bitcoin-22.0-x86_64-linux-gnu.tar.gz
tar -xvf ./bitcoin.tar.gz
sudo install -m 0755 -o root -g root -t /usr/local/bin ./bitcoin-22.0/bin/*
```

### Config file 
generate config file using this link https://jlopp.github.io/bitcoin-core-config-generator 
```
# [core]
# Run in the background as a daemon and accept commands.
daemon=1
# Specify a non-default location to store blockchain data.
blocksdir=/root/.bitcoin/data
# Specify a non-default location to store blockchain and other data.
datadir=/root/.bitcoin/data
# Set database cache size in megabytes; machines sync faster with a larger cache. Recommend setting as high as possible based upon machine's available RAM.
dbcache=6000
# Keep the transaction memory pool below <n> megabytes.
maxmempool=5000
# Do not keep transactions in the mempool longer than <n> hours.
mempoolexpiry=50
# Maintain a full transaction index, used by the getrawtransaction rpc call.
txindex=1

# [rpc]
# Enable Sign Raw Transaction RPC
deprecatedrpc=signrawtransaction

# Accept command line and JSON-RPC commands.
server=1
# Accept public REST requests.
rest=1
# Bind to given address to listen for JSON-RPC connections. This option is ignored unless -rpcallowip is also passed. Port is optional and overrides -rpcport. Use [host]:port notation for IPv6. This option can be specified multiple times. (default: 127.0.0.1 and ::1 i.e., localhost)
rpcbind=0.0.0.0
# Username and hashed password for JSON-RPC connections. The field <userpw> comes in the format: <USERNAME>:<SALT>$<HASH>. RPC clients connect using rpcuser=<USERNAME>/rpcpassword=<PASSWORD> arguments. You can generate this value at https://jlopp.github.io/bitcoin-core-rpc-auth-generator/. This option can be specified multiple times.
rpcauth=********
# Allow JSON-RPC connections from specified source. Valid for <ip> are a single IP (e.g. 1.2.3.4), a network/netmask (e.g. 1.2.3.4/255.255.255.0) or a network/CIDR (e.g. 1.2.3.4/24). This option can be specified multiple times.
rpcallowip=3.65.118.119
# Listen for JSON-RPC connections on this port
rpcport=3333

# [debug]
# Enable debug logging for all categories.
debug=1
# Location of the debug log
debuglogfile=/root/.bitcoin/debug.log
# Log IP Addresses in debug output.
logips=1

# [relay]
# Accept transaction replace-by-fee without requiring replaceability signaling.
mempoolfullrbf=1

# [wallet]
# Do not load the wallet and disable wallet RPC calls.
disablewallet=1


# [Sections]
# Most options automatically apply to mainnet, testnet, and regtest networks.
# If you want to confine an option to just one network, you should add it in the relevant section.
# EXCEPTIONS: The options addnode, connect, port, bind, rpcport, rpcbind and wallet
# only apply to mainnet unless they appear in the appropriate section below.

# Options only for mainnet
[main]

# Options only for testnet
[test]

# Options only for regtest
[regtest]
```
create `bitcoin.conf` file at `~/.bitcoin` location
```
touch ~/.bitcoin/bitcoin.conf && nano ~/.bitcoin/bitcoin.conf
```

### Start bitcoind on startup
add `@reboot bitcoind` to end of crontab file
```
crontab -e
```

### Start bitcoind service
start and test bitcoind, you should see integer output, check https://blockchain.info/latestblock for latest block on blockchain 
```
bitcoind
bitcoin-cli getblockcount
```