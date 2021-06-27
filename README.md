# Puppernet Blockchain
---
## Environment Setup
---
Download latest version of Geth & Tools for your operating system. (Puppernet was set up using Geth & Tools version 1.10.4)  

### Node Creation
1. Create accounts for two nodes for the network with a separate directory for each  
./geth --datadir node1 account new  
./geth --datadir node2 account new

### Genesis Creation
1. Run puppeth.exe, name the network and configure a new genesis block
2. Include addresses from both nodes to seal
3. Pre-fund both addresses
4. Export genesis configuration  

![](/Screenshots/puppeth_config.png)

## Mining
---
1. Initialising the Geth Database  
./geth --datadir node1 init networkname.json  
./geth --datadir node2 init networkname.json  
**datadir** - specifies directory for nodes and keystore files

2. Running nodes  
./geth --datadir node1 --unlock "SEALER_ONE_ADDRESS" --mine --rpc --allow-insecure-unlock  
./geth --datadir node2 --unlock "SEALER_TWO_ADDRESS" --mine --port 30304 --bootnodes "enode://SEALER_ONE_ENODE_ADDRESS@127.0.0.1:30303" --ipcdisable --allow-insecure-unlock  
**unlock** - accounts must be unlocked before mining  
**mine** - enables mining  
**rpc** - enables the http-rpc server  
**port** - specifies a different network port for node2  
**bootnodes** - allows P2P connection between node1 and node2  
**ipcdisable** - disables the IPC-RPC server  
**allow-insecure-unlock** - required after rpc has been enabled  

3. Unlock nodes using Node passwords
## Network Configuration
---
* Blocktime: Default 15 seconds  
Expected transaction time
* Chain ID: 202
* Node passwords (case sensitive): iliketrains  
Node passwords are used to unlock the nodes when mining and also to access the keystore files for the respective wallets
* Ports: node1 - 30303, node2 - 30304  
* URL: http://127.0.0.1:8545  
Default used by MyCrypto to connect to the blockchain

## Connecting to MyCrypto & Sending a Transaction
---
1. You will need to set up a custom network using the Chain ID above on MyCrypto  

![](/Screenshots/custom_node_setup.png)
2. Select the Keystore File option, locate the keystore file from the node1/keystore directory and unlock using the node password  

![](/Screenshots/node_keystore.png)
3. Input the public address of the intended recipient, the amount to be sent and the transaction fees  

![](/Screenshots/send_transaction.png)
4. Transaction Status can be located by the hash via "TX Status"  

![](/Screenshots/transaction_metadata.png)

## Troubleshooting
---
* If the TX status does not update, try:
1. Terminating both nodes using control+C
2. Change networks in MyCrypto
3. Restart the nodes
4. Reconnect to the custom network in MyCrypto
5. Unlock and refresh the wallet amount