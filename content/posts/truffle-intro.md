---
title: "初探 Truffle"
date: 2022-02-12T16:04:48+08:00
draft: false
summary: "初探 Truffle 筆記，安裝、部署、測試相關指令"
---
{{<figure src="https://trufflesuite.com/img/truffle-logo-dark.svg" height="250px" >}}

## Truffle 簡介
`Truffle` 是智能合約編譯、測試、除錯、部屬的開發工具。

## Truffle 安裝
```bash
npm install -g truffle
```

## Truffle 專案結構

以下指令可於資料夾，直接產生一個對應`box-name`的專案結構。
[官方 boxes 連結](https://trufflesuite.com/boxes/)
```bash
truffle unbox <box-name>
```

範例：以下為產生一個 `metacoin` 的專案，這是一個簡單的 `token` 範例。
```bash
truffle unbox metacoin
```

一般專案結構
```cmd
truffle-sample
├── build // 編譯後產生的內容
|  └── contracts
├── contracts // 合約
|  ├── ConvertLib.sol
|  ├── MetaCoin.sol
|  └── Migrations.sol
├── LICENSE
├── migrations // migrations 部屬流程
|  ├── 1_initial_migration.js
|  └── 2_deploy_contracts.js
├── test // 測試
|  ├── metacoin.js
|  └── TestMetaCoin.sol
└── truffle-config.js // 配置鏈與開發相關環境
```
## Truffle 編譯

編譯並產生 `build` 編譯後檔案
```bash
truffle compile
```

## Truffle 測試

自動測試 `test` 部署合約，可指定 `truffle-config.js` 內的網路設定，可區分開發與正式環境。
```bash
truffle test --network development
```

## Truffle Migration

Migration 目的是將我們撰寫的合約部署至鏈上。

部署合約可指定 `truffle-config.js` 內的網路設定，可區分開發與正式環境。
```bash
truffle migrate --network development
```

## 測試鏈

可使用 `Ganache` 建立本地測試鏈 [Ganache 官網](https://trufflesuite.com/ganache/)