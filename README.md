# Ethereum Experiments

Playground with Ethereum to better understand it. 

## OS Setup

Assuming Ubuntu 16.04 instance freshly created on Metacloud.  First we get Docker installed: 

```
sudo apt-get udpate
sudo apt-get upgrade # twiddle thumbs, wait 5 minutes.
sudo apt-get install docker.io # gets docker 1.12.6
```

Now add your user to be able to run docker commands so you don't have to do any of this ```sudo``` business: 

```
sudo gpasswd -a $USER docker
newgrp docker
```

You should now be able to run: 

```
docker ps
```

And not get errors. 

## Docker Setup

The instructions are similar to [the Ethereum Tutorial](https://github.com/ethereum/go-ethereum/wiki/Running-in-Docker)

```
docker pull ethereum/client-go
```

There are two ports we expose with the docker command we will run: 

* ```30303``` - This is the listener (TCP) and discovery (UDP) port that is used by Ethereum to communicate with other nodes. 
* ```8545``` - JSON-RPC interface.  This interface is used for running JSON-RPC calls against the node.  Because this port allows admin operations we do not open it to the outside world.  

The 30303 port is opened both UDP and TCP on our cluster so that it can join the chain. We will open 8545 but because Metacloud blocks the port, external people will not be able to get in. 

We also desire that we be allowed to stop and restart images and have the transactions persist.  For this reason, we use the ```-v``` option to mount the docker contents onto the host to persist through reboots. 


```
docker run -d -p 3030:30303 -p 8545:8545 -v /var/lib/ethereum:/root/.ethereum --name ethereum ethereum/client-go --rpc --rpcaddr "0.0.0.0" 
```

Running ```docker logs -f ethereum``` you should be able to see the blocks building.  

## Initial Exercises

How many peers are connected? 

```
curl -X POST --data '{"jsonrpc":"2.0","method":"net_peerCount","params":[],"id":74}' localhost:8545
```

Run a few more of the samples from the [JSON-RPC wiki](https://github.com/ethereum/wiki/wiki/JSON-RPC) 


