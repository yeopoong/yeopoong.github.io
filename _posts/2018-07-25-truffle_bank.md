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

## 배포

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
$ truffle console
truffle(development)>
```