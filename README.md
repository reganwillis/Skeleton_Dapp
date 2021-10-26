# Skeleton Dapp
This is a working development dapp which is able to make a simple transaction on a local blockchain using [MetaMask](https://metamask.io/). It is intended to be used as a skeleton dapp to plug in your own smart contract and front end. It also uses [Truffle](), [Ganache](), [Webpack](), and [Web3JS](https://web3js.readthedocs.io/en/v1.2.11/getting-started.html).

Download [Truffle]() and [Ganache]() to use this project.

TODO: add links

## Usage Instructions
TODO: clear steps from clone -> running working server
TODO: all npm installs

1. Start the webpack dev server with "npx webpack serve"
2. Start the local ethereum blockchain with "ganache-cli"
3. Compile the smart contracts with "truffle compile"
4. Deploy the smart contracts with "truffle migrate --reset"

https://www.trufflesuite.com/docs/truffle/getting-started/truffle-with-metamask#using-metamask-with-ganache-cli

## Iterating on this Repo
TODO: how to use this repo as intended, like a skeleton

template for how to write your own tests

TODO: add comments in index.js showing user where to add code

### Smart Contracts
TODO: basic info about how to create a smart contract
TODO: maybe this should be in a seperate repo that has a smart contract
TODO: separate repo could be pulled in using a git command
create your own smart contract with remix (or truffle only)
debugging with truffle: https://www.trufflesuite.com/docs/truffle/getting-started/debugging-your-contracts

## Deploy to Ethereum Blockchain
TODO: instructions for how to host app on the blockchain
TODO: add code to index.js to connect to metamask instead of ganache

## Hosting the Dapp on a Server
TODO: instructions for hosting the dapp on a server and connecting to a website

## Creation Process
These are the steps I took to create this dapp. There is more information about where code can be found and how it was created inline. My smart contract is named `SmartContract` and the naming convensions used throughout this project should be followed for new smart contracts.

### Truffle and Ganache
In a new project folder, create a base Truffle project with this command in the command prompt:
    
    truffle init

These folders and files are automatically generated:

    /contracts
        Migrations.sol
    /migrations
        1_initial_migration.js
    /test
    truffle-config.js

Add a smart contract (written in [Solidity]()) and a migration to handle deployment:

    /contracts
        Migrations.sol
        SmartContract.sol
    /migrations
        1_initial_migration.js
        2_smart_contract.js

In order to compile and deploy the smart contract, the blockchain must be running and connected to the dapp.

Take the comments off development in truffle-config.js.

    development: {
    host: "127.0.0.1",     // Localhost (default: none)
    port: 8545,            // Standard Ethereum port (default: none)
    network_id: "*",       // Any network (default: none)
    },

In a separate command prompt, start the blockchain with:

    ganache-cli

To compile and deploy the contract, run:

    truffle compile
    truffle migrate --reset

These folders and files are automatically generated:
    /build
        /contracts
            Migrations.json
            SmartContract.json

If successful, the command line output should say that the contract has been deployed.

### Frontend Using Webpack
I used Webpack to create the frontend. This makes it easier to import and use smart contracts. Many of the below steps follow the [Getting Started](https://webpack.js.org/guides/getting-started/) tutorial.

In the command line, run:

    npm init -y
    npm install webpack webpack-cli --save-dev

These folders and files are automatically generated:

    /node_modules
    package-lock.json
    package.json

Manually create these folders and files to hold the frontend:

    /dist
        index.html
    /src
        index.js

The html file should have a script tag for `main.js`, the JavaScript file that will be created by Webpack.

Create and fill `webpack.config.js` as directed by [Using a Configuration]() and [NPM Scripts]() in the tutorial.

### Development Server
Start a local server to test the dapp. The below steps use the [DevServer](https://webpack.js.org/configuration/dev-server/) webpack tutorial.

Add dev server code to webpack config:

    devServer: {
        static: {
            directory: path.join(__dirname, 'dist'),
        },
        compress: true,
        port: 9000,
    },

The path.join contents need to match the path.resolve contents in the configuration file. They should reflect the file structure of the dapp.

To start the server, run:

    npx webpack serve

### Web 3
Install web3.js with [the following command](https://www.oreilly.com/library/view/mastering-blockchain/9781788839044/ba606636-cbca-4bf5-acf1-0552dc6b0cd1.xhtml):

    npm install web3

To use web3.js with Webpack, the [Node Polyfill Webpack Plugin](https://github.com/Richienb/node-polyfill-webpack-plugin) is needed. Follow their README to install and use in the webpack config file.

A [circular dependancy bug](https://github.com/Richienb/node-polyfill-webpack-plugin/issues/18) with this plugin was identified in July 2021. The suggested temporary fix is to [exclude polyfilling the console](https://github.com/Richienb/node-polyfill-webpack-plugin/tree/27be8def3f3d42464fa77fd240c38a8bce982f8e#excludealiases).

Add code to `index.js` to connect to web3 and the smart contract (more detail inline). Build a simple interface in `index.html` to interact with the blockchain.

### Testing
Truffle has a [testing feature for smart contracts](https://www.trufflesuite.com/docs/truffle/testing/testing-your-contracts). In the `/test` folder, add a testing script: `smartContract.js`. Follow the steps for [writing JavaScript tests for Truffle](https://www.trufflesuite.com/docs/truffle/testing/writing-tests-in-javascript).

To run the tests, use

    truffle test