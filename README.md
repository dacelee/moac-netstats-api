MOAC Network Stats API
============
[![Build Status][travis-image]][travis-url] [![dependency status][dep-image]][dep-url]

This is the backend service which runs along with MOAC and tracks the network status, fetches information through JSON-RPC and connects through WebSockets to [moac-netstats](https://github.com/dacelee/moac-netstats) to feed information. 


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
## Installation Moac-netstats-api
Install NodeJS through NVM

```bash
curl -o- https://raw.githubusercontent.com/creationix/nvm/v0.32.1/install.sh | bash
source ~/.bashrc
nvm install v6.9.1
```
Install  Moac-netstats-api

```bash
git clone https://github.com/dacelee/moac-netstats-api
cd moac-netstats-api
npm install
npm install -g pm2
```

## Configuration

Configure the app modifying [processes.json](https://github.com/dacelee/moac-netstats-api/blob/master/processes.json). Note that you have to modify the backup processes.json file located in `./bin/processes.json` (to allow you to set your env vars without being rewritten when updating).

```json
"env":
	{
		"NODE_ENV"        : "production", // tell the client we're in production environment
		"RPC_HOST"        : "localhost", // eth JSON-RPC host
		"RPC_PORT"        : "8545", // eth JSON-RPC port
		"LISTENING_PORT"  : "30333", // eth listening port (only used for display)
		"INSTANCE_NAME"   : "name your node", // whatever you wish to name your node
		"CONTACT_DETAILS" : "you eamil", // add your contact details here if you wish (email/skype)
		"WS_SERVER"       : "ws://stats.moacdev.com", // path to eth-netstats WebSockets api server
		"WS_SECRET"       : "moacdev.com", // WebSockets api server secret used for login
		"VERBOSITY"       : 2 // Set the verbosity (0 = silent, 1 = error, warn, 2 = error, warn, info, success, 3 = all logs)
	}
```

## Run

Run it using pm2:

```bash
sudo mv processes.json /home/nodemoac
cd ~
pm2 start processes.json
```
##Donations
MOAC: 0x53be4cb8f27152893b448f9f569624afd1a97e0c


[travis-image]: https://travis-ci.org/cubedro/eth-net-intelligence-api.svg
[travis-url]: https://travis-ci.org/cubedro/eth-net-intelligence-api
[dep-image]: https://david-dm.org/cubedro/eth-net-intelligence-api.svg
[dep-url]: https://david-dm.org/cubedro/eth-net-intelligence-api
