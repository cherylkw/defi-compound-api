## Introduction

This is a backend blockchain development APP which use REST API to interact DeFi project - Compound lending protocol.

## API Architecture

Interfacing with Compound by building API that runs on Node.js server. Client side make a http request to this API , then API will forward this request to Compound's smart contract on blockchain by using Web3. Then smart contract of compund will send a response to this API and the API will send request to client. Client can be a browser, a server or mobile APP.

## Setup development enviornment:

1. Install Node.js
2. mkdir <directory name>
3. Inside the directory, intinal project : npm init -y
4. Create HTTP server for API, can create directly with node.js but easier to use framework like KOA
5. Install Koa framework (lightweight version of express): npm install koa @koa/router
5. Install web3 : npm install web3
 
## Connect to Ethereum blockchain main net:

Use infura (Eth nodes as a service) service which provide some nodes connect to mainnet and able to access to these nodes.
1. Open an account
2. Create a new project
3. Copy the API Key from Endpoints choose MAINNET
4. Copy the API Key in .env file
5. Install dotenv

## Create Web3 contract instance to point to the smart contract of Compound

- Find and copy the Token smart contract address and ABI under documentation of Compound's network section in config.json

## Create endpoint API

1. Token balance API 
    - For lending token, send the token to contract's name start with "c". When returning your token balance, the balance will be included interest you earned.
    - From Etherscan, search for example of cDAI/DAI contract : 0xd7a8843025d55405637a5c952f625bb2fbc258a2
    - Try out the API using this contract :
        curl http://localhost:3000/tokenbalance/cDai/0xd7a8843025d55405637a5c952f625bb2fbc258a2

2. cToken balance API
    - For lending token to compound protocol, the fund will be locked in cToken contract , in exchange you will get some cToken which represent the token you sent to Compound. This can be used to redeem the token that you initially invested plus the earned interest.
    - Try : curl http://localhost:3000/cTokenBalance/cDai/0xd7a8843025d55405637a5c952f625bb2fbc258a2

3. Mint new cToken balance API
    - For lending token to Compound protocol, need a private key to sign in and need an address. To generate an address, go to Vanity-ETH.
    - store it in .env
    - add private key to Web3

4. Redeem the cToken API 
    - Return the amont of cToken that we want to redeem e.g. redeem 10 cToken doesn't mean you get back 10 token, it depends on the exchange rate between token and cToken, also the interest you've earned.

# Deploy to Heroku

1. Create a Heroku account
2. Install Heroku-cli
3. Install Git
4. Create repository in Git
    - git init
    - git add -A
    - git commit -m "init"
5. In command line : Heroku login
6. After login , create Heroku project : Heroku create
7. Since we do not upload the .env file , set the env variable in Heroku : heroku config:set INFURA_URL=<the link> , also the PRIVATE_KEY=<your private key>
8. Upload the project to Heroku : git push heroku master

# Endpoint API testing

Try cDai/Dai :
curl https://localhost:3000/tokenBalance/cDai/0xc2b58e6b037b19cfba17b1290b1fbbebc00bd967
curl https://localhost:3000/ctokenBalance/cDai/0xc2b58e6b037b19cfba17b1290b1fbbebc00bd967

## Author : Cheryl Kwong  Email : cherylkwong@gmail.com
## Project developed by : Node.js, Rest API, Koa, Infura, Web3, Heroku
