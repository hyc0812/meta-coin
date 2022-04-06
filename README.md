## This blog will take you through the basics of creating a local blockchain, deploying a smart contract and interacting with it. (MacOS)

> _This tutorial is meant for those with a basic knowledge of Ethereum and smart contracts, who have some knowledge of HTML and JavaScript, but who are new to dApps._
> The purpose of building this blog is to write down the detailed operation history and my memo for learning the dApps.
> If you are also interested and want to get hands dirty, just follow these steps below and have fun!~

### Prerequisites

- MacOS
- CLI with [Homebrew](https://brew.sh/) installed
- Coding IDE e.g. [VS Code](https://code.visualstudio.com/). 
- [Truffle](https://trufflesuite.com/truffle/)
- [Ganache UI](https://trufflesuite.com/ganache/)
- [MetaMask](https://metamask.io/) (optional)

### Intro & Review
In this tutorial we will be covering:

1. Create a truffle project
2. Test the smart contract
2. Compile and deploy the smart contract
3. Interact with the smart contract

#### What are Truffle and Ganache?
**Truffle** is a world-class development environment, testing framework and asset pipeline for blockchains using the Ethereum Virtual Machine (EVM), aiming to make life as a developer easier. With Truffle, you get:
- Built-in smart contract compilation
- Automated contract testing
- extensible deployment & migrations framework
- Network management for deploying to public & private networks
- Package management using the ERC190 standard
- Interactive console for direct contract communication
- Configurable build pipeline
- External script runner 

**Ganache** is a personal blockchain for rapid Ethereum and Corda distributed application development. You can use Ganache across the entire development cycle; enabling you to develop, deploy, and test your dApps in a safe and deterministic environment. Ganache comes in two flavours: a UI and CLI. In this blog, we choose to use Ganache UI. 


## Getting started
Project structure:

> **contracts/**: Directory for Solidity contracts

> **migrations/**: Directory for scriptable deployment files

> **test/**: Directory for test files for testing your application and contracts

> **truffle-config.js**: Truffle configuration file

> **LICENSE**: License for your project


### Test the smart contract

We will find the test code has already been done for us at **/meta-coin/test**.

![Image description](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/owc9tgr5a9eb9ozegeb1.png)
Let's run the solidity test in the CLI:
```linux
truffle test ./test/metacoin.js
```

![Image description](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/qj9hxzm8dmmf4b4s1ra4.png)

### Compile and deploy the smart contract

Now we compile our smart contract:

```linux
truffle compile
```

![Image description](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/ch4w3x5tj5oz8d9rjqlo.png)

Next, we need to connect to a blockchain. Truffle has a built-in personal blockchain that can be used. This blockchain is local to your system and does not interact with the main Ethereum network.

> We have two options to connect to a local blockchain: 
> Option 1: using command `truffle develop`
> Option 2: using Ganache UI to visualize. 
> In this blog we use option2 to demonstrate.


Next, we open Ganache UI, click **QUICKSTART**, and **ADD PROJECT** by selecting **truffle-config.js**, and click restart:

![Image description](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/mxraeucnimfucurzxfu7.png)

![Image description](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/7t0yfrmuj75yatpxywte.png)


![Image description](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/trz1mtjwj82pw6wlzfca.png)

By finishing the previous step, we have launched a local blockchain. 
We can now migrate and deploy our smart contracts to the blockchain using the following command:
```linux
truffle migrate
```

This shows the transaction IDs and addresses of the deployed contracts. It also includes a cost summary and real-time status updates.

![Image description](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/gf3so3ckoek17ptgq6x8.png)

In Ganache, click the “BLOCKS”, “TRANSACTIONS”, and “CONTRACTS”  to see the transactions that have been processed.

![Image description](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/km4tvh8hj5x8001yiod2.png)

![Image description](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/8w3iy8d6k2kni75vqfu6.png)

![Image description](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/mnaefxae4jv0ly0dz6dq.png)

![Image description](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/ehyh1i2hgnfgpk5mwmwe.png)

The MetaMask extension also provides us ETH balance if the first account in Ganache is imported.

![Image description](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/gdoby3ijus6agbevx3j1.png)

![Image description](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/xxzwoypdv2yuktay0en6.png)

![Image description](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/w69ionlx6xpd2qzugdds.png)
![Image description](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/u4a0tmpv8i70vj6cl5l3.png)



### Interact with the smart contract

We use the **Truffle Console** to interact with the smart contract. Let's run the following command to launch the console:
```linux
truffle console
```

![Image description](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/2kxurhfw6unppjsj692c.png)

First, we establish the deployed meta-coin instance and the accounts created by Ganache:
> NOTE: `>` means we are currently working in **Truffle Console**

```linux
> let instance = await MetaCoin.deployed()
> let accounts = await web3.eth.getAccounts()
```

![Image description](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/j2q28zgku1mshx44pjb6.png)

We can check the meta-coin balance of the account which has deployed the contract:
```linux
> let balance = await instance.getBalance(accounts[0])
> balance.toNumber()
```

![Image description](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/ouzs1phgnc7lnnz98b75.png)


We can transfer some meta-coin from one account to another:
```linux
> instance.sendCoin(accounts[1], 500)
```

![Image description](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/2b7kc8i9zqpy48qybny0.png)

Check the balance of the meta-coin receiving account:
```linux
> let received = await instance.getBalance(accounts[1])
> received.toNumber()
```

![Image description](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/nk88jg9enx0q5sqjcsyx.png)

Check the balance of the meta-coin sending account:
```linux
> let newBalance = await instance.getBalance(accounts[0])
> newBalance.toNumber()
```

![Image description](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/58o4z12b2isrw7z7r7tg.png)

Really COOL isn't it!

### References
https://trufflesuite.com/docs/truffle/index.html

