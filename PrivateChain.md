# Creating an Ethereum Private Network

This README shows how to create an ethereum private network to mine your own blocks.  This is a practical addition to the instructions posted at [the main Ethereum README](https://github.com/ethereum/go-ethereum/blob/master/README.md).  

## 1. High Level Concepts

Basically, you'll be creating a couple of keys for your Ethereum cluster. From there you will place the keys in a genesis config file.  You will then launch a boot node.  Then you will launch 2 miners to start mining blocks from the boot nodes.  

## 2. Setup Ubuntu

All commands should be run as root or appended with ```sudo```

```
apt-get update && apt-get upgrade -q -y
apt-get install -q -y git curl software-properties-common
add-apt-repository ppa:ethereum/ethereum
add-apt-repository ppa:ethereum/ethereum-dev
apt-get update
apt-get install -q -y geth bootstrap
```

You should now have a node ready to run Ethereum. Do this with 2 other machines so you have 3 in total. 

## 3. Create some keys

On a node run:

```
geth account new
```
Follow the prompts and enter some passphrase.  A new key will be placed in the ```~/.ethereum/keystore

You can make note of the key of this file.  It will be the address that is output from the password command.  

```
Address: {b12e8690427604c49809524aba1012fb622ae6e9}
```

Do this to add more keys and accounts.  Accounts can be added later. 

## 4. Create the Genesis file

The genesis file looks like the following: 

```
{
  "config": {
        "chainId": 0,
        "homesteadBlock": 0,
        "eip155Block": 0,
        "eip158Block": 0
    },
  "alloc"      : {
     "0x176b284c24e716db068cb5d9e3c99bbd9de3231d": {"balance": "111111111"},
     "0x15db06db03ab3522780ef1b5d5c068616acc7676": {"balance": "111111111"},
     "0x3ebf50b49ad648fe52af2018594503adf34feb8f": {"balance": "111111111"}
  },
  "coinbase"   : "0x0000000000000000000000000000000000000000",
  "difficulty" : "0x20000",
  "extraData"  : "",
  "gasLimit"   : "0x2fefd8",
  "nonce"      : "0x00000000000c15c0",
  "mixhash"    : "0x0000000000000000000000000000000000000000000000000000000000000000",
  "parentHash" : "0x0000000000000000000000000000000000000000000000000000000000000000",
  "timestamp"  : "0x00"
}
```

A few notes about the above file: 

* The ```alloc``` section creates a balance for the three keys that were created already.  You should substitute your own keys. We are allocating 111111111 amount of ethers, or whatever this new token is called for our private Ethereum network. 
* Change the  ```nonce```  value to something unique that still contains the same amount of digits. 

## 4. Start the boot node

Chose one of your nodes to be the boot server.  To make this work run: 

```
bootnode --genkey=boot.key
bootnode --nodekey=boot.key
```

This will output an address similar to : 

```
INFO [08-23|19:54:03] UDP listener up  \
                        self=enode://734ec34f38e5dc9f25f8235e714755c37b1b7151f29a97f40da9b4ebfaec387f3fa301f5000f07253a8eab1e01cd4239e16091a150b5427d92ebaac9f986aa7c@[::]:30301
```

At the end of this long line is a ```[::]```.  This is where you'll substitute the IP address of the node (for example 192.168.2.3 if this were the IP address of this ethereum node.  We will take this value and then start our other ethereum nodes to join the bootnode cluster. 

## 5. Add nodes to the peer to peer network.  

On the other nodes (that aren't the bootnode) we will start the p2p connections.  To add peers that mine to the peer to peer connection ```geth``` is started with flags.  Run: 

```
geth --bootnodes=enode://734ec34f38e5dc9f25f8235e714755c37b1b7151f29a97f40da9b4ebfaec387f3fa301f5000f07253a8eab1e01cd4239e16091a150b5427d92ebaac9f986aa7c@10.100.2.209:30301 \
--mine --minerthreads=1 \
--etherbase=0x176b284c24e716db068cb5d9e3c99bbd9de3231d
```

Notice a few things about the flags: 

* The ```enode``` is the enode of the boot server but the ```[::]``` is replaced with the real IP address of the boot node. 
* The ```etherbase``` is set to one of the keys you generated so that this miner will now collect the newly created tokens for each block that is mined.  You can start different nodes with different etherbase values that correspond to your keys. 

At this point you'll see the miners mine the blocks and you now have a super fun private Ethereum chain. 

