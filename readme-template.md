# uPort Identity Contracts
[![npm](https://img.shields.io/npm/v/uport-identity.svg)](https://www.npmjs.com/package/uport-identity)
![CircleCI](https://img.shields.io/circleci/project/github/uport-project/uport-identity.svg)
<coverage>
[![Join the chat at](https://badges.gitter.im/Join%20Chat.svg)](https://gitter.im/uport-project/Lobby?utm_source=badge&utm_medium=badge&utm_campaign=pr-badge&utm_content=badge)

Please read our [Whitepaper](http://whitepaper.uport.me) for information on what uPort is, and what is currently possible as far as integration.

<contract-deployments>

## Using the contracts
To use the contract we provide truffle artifacts. Once you require the `uport-identity` module you will get an object containing a versioned index of the uport contracts. You can specify which version you want to user, or just use the latest one. Keep in mind that different versions will be deployed to different addresses.
```javascript
const uportIdentity = require('uport-identity')
const Contract = require('truffle-contract')

// use specific version
const IdentityManagerArtifact = uportIdentity.IdentityManager.v1

// or use latest version
const version = uportIdentity.IdentityManager.latestVersion
const IdentityManagerArtifact = uportIdentity.IdentityManager[version]
```

 You can use `truffle-contract` to utilize these artifacts.
```javascript
let IdentityManager = Contract(IdentityManagerArtifact)
IdentityManager.setProvider(web3.currentProvider)
let identityManager = IdentityManager.deployed()
```
You can also use web3.
```javascript
let networkId = 1 // Mainnet
let IdentityManager = web3.eth.contract(IdentityManagerArtifact)
let identityManager = IdentityManager.at(IdentityManagerArtifact.networks[networkId].address)
```

If you want to learn more about this structure, checkout the document about the [artifact index](./docs/artifact-index.md).

## Testing the contracts
All aspects of the contracts need to be tested. To do this we use `truffle` and `testrpc` behind the scenes. Right now we only have tests written in javascript, but in the future we plan on adding tests written in solidity as well.

To execute the tests you simply run:
```
$ yarn test
```

If you want to run run a specific test you can just add the filename:
```
$ yarn test test/testName.js
```

You can also run the tests on a [geth node](./docs/private-geth-testing.md).

## Contract documentation
This repository contains the contracts currently in use by uPort. This is also where you find the addresses of these contracts currently deployed on Mainnet and relevant test networks. Below you can find descriptions of each of the contracts and the rationale behind the design decisions.

#### [Proxy](./docs/proxy.md)
#### [TxRelay](./docs/txRelay.md)
#### [IdentityManager](./docs/identityManager.md)
#### [MetaIdentityManager](./docs/metaIdentityManager.md)

### Main contract interactions
The most important interactions with the contracts are creation of identities and sending transactions. Here are visual representations of this being executed.

#### Creating an identity with the IdentityManager
![identity creation](./docs/diagrams/create-identity.seq.png)

#### Transfer an identity to IdentityManager
![register identity](./docs/diagrams/register-identity.seq.png)

#### Send a meta-tx
![meta-tx](./docs/diagrams/send-tx.seq.png)

## Contributing
Want to contribute to uport-contracts? Cool, please read our [contribution guidelines](./CONTRIBUTING.md) to get an understanding of the process we use for making changes to this repo.
