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


To compile the contract, load the code from Voting.sol in to a string variable and compile it.</b>

```
> code = fs.readFileSync('Voting.sol').toString()

> solc = require('solc')

> compiledCode = solc.compile(code)
```

In order to deploy the contract. First create a contract object (VotingContract below) which is used to deploy and initiate contracts in the blockchain.</b>

```
> abiDefinition = JSON.parse(compiledCode.contracts[':Voting'].interface)

> VotingContract = web3.eth.contract(abiDefinition)

> byteCode = compiledCode.contracts[':Voting'].bytecode

> deployedContract = VotingContract.new['Rama','Nick','Jose'],{data:byteCode,from:web3.eth.accounts[0], gas: 4700000})

> deployedContract.address

> contractInstance = VotingContract.at(deployedContract.address)
```

## Interact with the contract in the nodejs console

Here we are voting three times for the candidate 'Rama'

```
> contractInstance.totalVotesFor.call('Rama')

> contractInstance.voteForCandidate('Rama',{from:web3.eth.accounts[0]})

> contractInstance.voteForCandidate('Rama', {from: web3.eth.accounts[0]})

> contractInstance.voteForCandidate('Rama', {from: web3.eth.accounts[0]})

>contractInstance.totalVotesFor.call('Rama').toLocaleString()
```
Try the above commands in your node console and you should see the vote count increment. Every time you vote for a candidate, you get back a transaction id.

## Webpage to connect to the blockchain and vote

Create a simple html file with candidate names and invoke the voting commands (which we already tried and tested in the nodejs console) in a js file. Drop both of them in the hello_world_voting directory and open the index.html in your browser.

```
>wget https://gist.githubusercontent.com/maheshmurthy/f6e96d6b3fff4cd4fa7f892de8a1a1b4/raw/e7e7d4e063c5bdd4fb6bc17d7b75370de42d48ee/index.html

>wget https://gist.githubusercontent.com/maheshmurthy/f6e96d6b3fff4cd4fa7f892de8a1a1b4/raw/e7e7d4e063c5bdd4fb6bc17d7b75370de42d48ee/index.js

```

In your nodejs console, execute contractInstance.address to get the address at which the contract is deployed and change the index.js accordingly to use your deployed address.