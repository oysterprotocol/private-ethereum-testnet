# private-ethereum-testnet
Dockerized Private Ethereum Testnet

### Getting Started with Go Docker
Start by installing [Docker](https://www.docker.com/) in your local system to host the testnet container.

### Docker 
Start by pulling the Ethereum Go Client image

```bash
docker pull ethereum/client-go
```

### Start the JSON-RPC Interface
```bash
docker run -it -p 8545:8545 -p 30303:30303 ethereum/client-go --rpc --rpcaddr "0.0.0.0"
```
### Blockchain Storage (Optional)
Store the blockchain data on a persistent volume.
```bash
docker run -it -p 30303:30303 -v /path/on/host:/root/.ethereum ethereum/client-go
```

### Ganache Setup
Setting up Ganache can be beneficial when you need to run a localized version of the Ethereum Blockchain. 
[Truffle Framework](http://truffleframework.com/) provides the installer for your platform which you can download here;
[Ganache](http://truffleframework.com/ganache). 

Once installed you can run the binary to start the blockchain interface http://127.0.0.1:7545, when you run the first time it will create 10 test ethereum accounts with 100.00 ether available to spend.

### Interacting with Ethereum
Interacting with the Ethereum Blockchain is done with [Web3](https://github.com/ethereum/web3.js/) by creating an instance of the web3 client.

```javascript
if (typeof web3 !== 'undefined') {
  web3 = new Web3(web3.currentProvider);
} else {
  // set the provider you want from Web3.providers, 8545 for Ethereum Testnet / 7545 for Ganache Testnet
  web3 = new Web3(new Web3.providers.HttpProvider("http://localhost:7545"));
}
```

Once the provider is initialized you can begin to call methods on the web3 interface.
```javascript
const coinbase = web3.eth.coinbase;
const balance = web3.eth.getBalance(coinbase);
```
