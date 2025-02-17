# NFT Lottery

[link to demo](https://joe11-y.github.io/NFT-Lottery-Frontend/)

A simple lottery contract that awards a lucky winner with a minted nft and half of the generated prizepot.

Check operator section for how to operate lottery.


## 1. Tech Stack
This boilerplate uses the following tech stack:
- [React](https://reactjs.org/) - A JavaScript library for building user interfaces.
- [use-Contractkit](contractkit
) - A frontend library for interacting with the Celo blockchain.
- [Hardhat](https://hardhat.org/) - A tool for writing and deploying smart contracts.
- [Bootstrap](https://getbootstrap.com/) - A CSS framework that provides responsive, mobile-first layouts.

## 2. Quick Start

To get this project up running locally, follow these simple steps:

### 2.1 Clone the repository:

```bash
git clone https://github.com/JoE11-y/NFT-Lottery-Frontend.git
```

### 2.2 Navigate to the directory:

```bash
cd NFT-Lottery-Frontend
```

### 2.3 Install the dependencies:

```bash
npm install
```

### 2.4 Run the dapp:

```bash
npm start
```

To properly test the dapp you will need to have a Celo wallet with testnet tokens.
This learning module [NFT Contract Development with Hardhat](https://hackmd.io/exuZTH2hTqKytn2vxgDmcg) will walk you through the process of creating a Metamask wallet and claiming Alfajores testnet tokens.

## 3. Smart-Contract Deployment

### 3.1 Compile the smart contract

```bash
npx hardhat compile
```

### 3.2 Run tests on smart contract

```bash
npx hardhat test
```

### 3.3 Update env file

- Create a file in the root directory called ".env"
- Create a key called ACCOUNT_KEY and paste in your private key. e.g

```js
ACCONT_KEY = "...";
```
You can find more details about the whole process in the Dacade [NFT Contract Development with Hardhat](https://hackmd.io/exuZTH2hTqKytn2vxgDmcg) learning module. It will also show you how to get testnet tokens for your account so you can deploy your smart contract in the next step.

### 3.5 Deploy the smart contract to the Celo testnet Aljafores

```bash
npx hardhat run --network alfajores scripts/deploy.js
```

This command will update the src/contract files with the deployed smart contract ABI and contract address.

## 4. Operator Section

This section contains node-js terminal scripts to be run to control the operation of the lottery.

### 4.1 Setting the operator

```bash
node ./operator/setOperator.js --operatorAddress {your address}
```

This command is the first command that should be run after deploying the contract, it sets the operator address giving that address access to functions like starting the lottery and other admin restricted functions.

### 4.2 Starting the Lottery

```bash
node ./operator/startLottery.js
```

This command will start a new lottery session

### 4.3 Getting the winning ticket

```bash
node ./operator/getWinningTickets.js
```

This command gets the winning the ticket for that lottery session, can be only ran once the current lottery session time range has been exhausted.

### 4.4 Payout Winner

```bash
node ./operator/payoutWinner.js
```

This command pays out the winner, after the winning ticket has been gotten. The function also sets the lottery state to idle, meaning a new lottery session can be started.

### 4.5 Withdraw Contract Funds

```bash
node ./operator/withdrawContractFunds.js 
```

This command allows the lottery owner to be able to withdraw his own winnings from the lottery, function can only be called after the has been paid off.


### 4.6 Update Lottery Interval

```bash
node ./operator/updateLotteryInterval.js --interval {interval} --timeUnit {timeUnit}
```
- This command allows the operator to be change the lottery interval, i.e. how long a lottery session can last.

- The value for interval can only be a number/integer, while for the timeUnit can only be in the string format and the accepted values are (seconds, minutes, hours, days and weeks) any other format will result in function failure.


## Dev Opinion
A much better implementation would be to use either oracles or a collab with chainlink to use their keeper service for contract automation
