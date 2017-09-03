# Hello World Ethereum

This document is an update on the [Hello World Article](https://medium.com/@mvmurthy/full-stack-hello-world-voting-ethereum-dapp-tutorial-part-1-40d2d0d807c2) found on Medium. 

## Big Picture

1. Install OS environment
1. Install Node JS environment
1. Install Test RPC

## Operating System

We will use Ubuntu 16.04.  The service requires node and [testrpc](https://github.com/ethereumjs/testrpc) says it requires node 6.9.1.  To make that happen: 

```
sudo apt-get update && sudo apt-get upgrade
curl -sL https://deb.nodesource.com/setup_6.x -o nodesource_setup.sh
sudo bash nodesource_setup.sh
sudo apt-get install nodejs build-essential

```
(note: nodejs installs npm)

## Set NodeJS environment up for Testrpc

```
mkdir hello_world_voting
cd hello_world_voting
npm install ethereumjs-testrpc web3@0.20.1
./node_modules/.bin/testrpc
```

This creates 10 accounts and 10 keys and then listens on port :8545.  This you should leave up so you can actually use these keys and plug into this interface. 

## Running contract

In a separate window, and while ```testrpc``` is still running, we will run the contract. 

```
cd hello_world_voting
wget https://gist.githubusercontent.com/maheshmurthy/3da385a42678c3e36a8328cbe47cae5b/raw/e451f3b141042de86d4fac9e0eddc151b666ef68/Voting.sol
npm install solc
```

The next set of commands we run on the node REPL: 

```
node
```

Now enter the following commands: 

```
> Web3 = require('web3')
> web3 = new Web3(new Web3.providers.HttpProvider("http://localhost:8545"))
```
To make sure we are connected we look at the eth accounts: 

```
> web3.eth.accounts
```

At this point, you should be able to go through the rest of the [tutorial here](https://medium.com/@mvmurthy/full-stack-hello-world-voting-ethereum-dapp-tutorial-part-1-40d2d0d807c2) without issues. Pick up half way through the part called <b>2. Simple voting contract</b>




