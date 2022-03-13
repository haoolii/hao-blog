---
title: "Truffle 部屬 Kovan"
date: 2022-03-13T16:58:02+08:00
draft: false
summary: "Truffle 部屬合約至 Kovan 網路"
tags: ["truffle", "web3", "blockchain"]
categories: ["web3"]
---
{{<figure src="https://trufflesuite.com/img/truffle-logo-dark.svg" height="250px" >}}

## 簡介
使用 `web3.js` 需要搭配 `JSON-RPC Server` 使用，最快速方便的方式是使用 `Infura`，可快速建置並管理追蹤 APP 使用情況。

## Infura
是一套開發工具，提供安全、可靠、擴充性高的存取乙太坊和 `IPFS`。支援 `HTTPS` 和 `WebSockets`。

https://infura.io/

## 流程

1. 註冊 `infura`
2. 建立 `Application`
3. 取得對對應 `ENDPOINT` 的網路網址
4. 設定於 `Truffle Config`
5. `Truffle` 部署
6. 完成

## Truffle 設定

先安裝 `Truffle hdwallet`

```bash
yarn add truffle-hdwallet-provider
```

設定發布地址的 `PRIVATEKEY`，與 `infura APP` 對應網路的 `ENDPOINT` 填入。
`PRIVATEKEY` 使用陣列方式設定，如果非陣列代表輸入助憶詞。
```javascript
const HDWalletProvider = require('truffle-hdwallet-provider');

const PRIVATEKEY = "";
const ENDPOINT = "";

module.exports = {
  networks: {
   development: {
     host: "127.0.0.1",
     port: 7545,
     network_id: "*"
   },
   kovan: {
    provider: function() {
      return new HDWalletProvider(
        //private keys array
        [PRIVATEKEY],
        //url to ethereum node
        ENDPOINT
      )
    },
    network_id: "*"
   }
  },
  compilers: {
    solc: {
      version: "^0.8.11"
    }
  }
};

```

## 發布

發布並指定 `truffle config` 內的 `network`
```bash
truffle migrate --network kovan
```

## 補充
因部署至測試網路時，需要消耗 Gas，因此需要水龍頭領取 ETH。

[Chain Link faucets](https://faucets.chain.link/)

[gitter kovan-testnet](https://gitter.im/kovan-testnet/faucet)