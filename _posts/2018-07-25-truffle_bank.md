---
layout: post
title: "[Truffle] Bank Example"
categories: dev
tags: blockchain truffle
---

> Truffle is the most popular development framework for Ethereum with a mission to make your life a whole lot easier.

## 프로젝트 생성

```
$ mkdir bank
$ cd sample
$ truffle init
```

## Bank Contract

```
$ truffle create contract Bank
```

`contracts/Bank.sol`
```
pragma solidity ^0.4.4;

contract Bank {
    address public owner;

    function Bank(address _owner) public {
        owner = _owner;
    }

    function deposit() public payable {
        require(msg.value > 0);
    }

    function withdraw() public {
        require(msg.sender == owner);
        owner.transfer(address(this).balance);
    }
}
```

```
$ truffle compile
Compiling .\contracts\Bank.sol...
Compiling .\contracts\Migrations.sol...

Writing artifacts to .\build\contracts
```

## Ganache

![Ganache](/assets/img/ganache.png)

## 배포

`truffle.js`
```
module.exports = {
  // See <http://truffleframework.com/docs/advanced/configuration>
  // to customize your Truffle configuration!
  networks: {
    development: {
      host: "127.0.0.1",
      port: 7545,
      network_id: "*" // Match any network id
    }
  }
};
```

```
$ truffle create migration bank
```

`migrations/1532503784_bank.js`
```
module.exports = function(deployer) {
  // Use deployer to state migration tasks.
};
```

```
var Bank = artifacts.require("Bank");

module.exports = function(deployer) {
  let ownerAddress = web3.eth.accounts[0];
  deployer.deploy(Bank, ownerAddress);
};
```

```
$ truffle migrate
Using network 'development'.

Running migration: 1_initial_migration.js
  Deploying Migrations...
  ... 0x217a4c792c920be8e32ed59d16a14205cf81fa77da3100dcb0add8f72ab5c431
  Migrations: 0x13c9f9ac9691ac047e90c253b75d9ec08be13b01
Saving successful migration to network...
  ... 0xcd0404b13daeda92f6f27f40d2559a6905019723fa28f8dc3f8a37a3d8421f8a
Saving artifacts...
Running migration: 1532503784_bank.js
  Deploying Bank...
  ... 0xe02911110604c0986dcf55ff072fb2ffac3a6d1d63ebfdb32a7f83cc02fdf0f7
  Bank: 0xdcbfcb0e112babddbca6af311a75ebb080e4f563
Saving successful migration to network...
  ... 0xb839d9e409c632cf9c5cbec70af02b0a0476ac3ac9178d8ce9c923feb5b58ecb
Saving artifacts...
```

## 테스트

```
$ truffle console
truffle(development)>
```

```
truffle(development)> Bank.deployed().then(instance => bank = instance)
```

```
truffle(development)> bank.owner()
'0x597193c7db57b66b53f7cea4877f20961a98b0d2'
```

```
truffle(development)> bank.deposit({value: web3.toWei(10, 'ether')})
{ tx: '0xbae00009b4a915c8342ceef64b06d307e99e20d3bc72e0e538770d6224111948',
  receipt:
   { transactionHash: '0xbae00009b4a915c8342ceef64b06d307e99e20d3bc72e0e538770d6224111948',
     transactionIndex: 0,
     blockHash: '0x4cdaf5ab1ea8df72ac116484771a360214b1b781fb0cc2d3e1f65fcef70dedad',
     blockNumber: 5,
     gasUsed: 21453,
     cumulativeGasUsed: 21453,
     contractAddress: null,
     logs: [],
     status: '0x1',
     logsBloom: '0x00000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000' },
  logs: [] }
```

참조: http://ethdocs.org/en/latest/contracts-and-transactions/account-types-gas-and-transactions.html

![deposit](/assets/img/bank_deposit.png)

```
truffle(development)> bank.withdraw()
{ tx: '0x85d78f1db258514b92c76420332ef04faf9a2bc49b08f43ff722ce0358e20680',
  receipt:
   { transactionHash: '0x85d78f1db258514b92c76420332ef04faf9a2bc49b08f43ff722ce0358e20680',
     transactionIndex: 0,
     blockHash: '0xa2427d52882d9d20b28cb00cae5aed6844cc70c05701014b66c2814a94f234f2',
     blockNumber: 6,
     gasUsed: 29826,
     cumulativeGasUsed: 29826,
     contractAddress: null,
     logs: [],
     status: '0x1',
     logsBloom: '0x00000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000' },
  logs: [] }
```

![withdraw](/assets/img/bank_withdraw.png)
