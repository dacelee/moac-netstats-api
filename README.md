MOAC Network Stats API
============
[![Build Status][travis-image]][travis-url] [![dependency status][dep-image]][dep-url]

This is the backend service which runs along with MOAC and tracks the network status, fetches information through JSON-RPC and connects through WebSockets to [moac-netstats](https://github.com/dacelee/moac-netstats) to feed information. For full install instructions please read the [wiki](https://github.com/ethereum/wiki/wiki/Network-Status).


## Prerequisite
* moac
* node
* npm


## Installation on MOAC And link to the network（Ubuntu16.0.4 x64）

Need MOAC JS-RPC OPEN 

```bash
adduser nodemoac
adduser nodemoac sudo
su - nodemoac
sudo apt-get update
sudo apt-get install unzip build-essential
sudo wget https://github.com/MOACChain/moac-core/releases/download/v1.0.2/nuwa-vnode1.0.2.ubuntu.tar.gz
sudo unzip -x nuwa-vnode1.0.2.ubuntu.tar.gz
cd nuwa-vnode1.0.2.ubuntu
chmod 755 moac
./moac account new   （set up Address）
screen -S wallet
./moac --rpc


```
## Installation as docker container (optional)

There is a `Dockerfile` in the root directory of the repository. Please read through the header of said file for
instructions on how to build/run/setup. Configuration instructions below still apply.

## Configuration

Configure the app modifying [processes.json](/eth-net-intelligence-api/blob/master/processes.json). Note that you have to modify the backup processes.json file located in `./bin/processes.json` (to allow you to set your env vars without being rewritten when updating).

```json
"env":
	{
		"NODE_ENV"        : "production", // tell the client we're in production environment
		"RPC_HOST"        : "localhost", // eth JSON-RPC host
		"RPC_PORT"        : "8545", // eth JSON-RPC port
		"LISTENING_PORT"  : "30303", // eth listening port (only used for display)
		"INSTANCE_NAME"   : "", // whatever you wish to name your node
		"CONTACT_DETAILS" : "", // add your contact details here if you wish (email/skype)
		"WS_SERVER"       : "wss://rpc.ethstats.net", // path to eth-netstats WebSockets api server
		"WS_SECRET"       : "see http://forum.ethereum.org/discussion/2112/how-to-add-yourself-to-the-stats-dashboard-its-not-automatic", // WebSockets api server secret used for login
		"VERBOSITY"       : 2 // Set the verbosity (0 = silent, 1 = error, warn, 2 = error, warn, info, success, 3 = all logs)
	}
```

## Run

Run it using pm2:

```bash
cd ~/bin
pm2 start processes.json
```

## Updating

To update the API client use the following command:

```bash
~/bin/www/bin/update.sh
```

It will stop the current netstats client processes, automatically detect your ethereum implementation and version, update it to the latest develop build, update netstats client and reload the processes.

[travis-image]: https://travis-ci.org/cubedro/eth-net-intelligence-api.svg
[travis-url]: https://travis-ci.org/cubedro/eth-net-intelligence-api
[dep-image]: https://david-dm.org/cubedro/eth-net-intelligence-api.svg
[dep-url]: https://david-dm.org/cubedro/eth-net-intelligence-api
