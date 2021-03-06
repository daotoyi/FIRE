---
title: "Filecoin"
description: "去中心化储存平台"
date: "2022-03-12 12:05:00"
lastmod: "2022-07-02 09:39:22"
categories: ["Blockchain"]
draft: false
---

## Filecoin {#filecoin}

Filecoin 是一个去中心化的存储网络，能将海量用户的闲散存储资源充分利用起来，从而构建一套超低成本的可靠存储系统。

没有中心，所以会用到区块链技术.

一般区块链使用的是算力挖矿的工作量证明（Proof-of-Work mining），而 Filecoin 使用的是存储工作量证明(Proof-of-Storage)。


## Filecoin 架构 {#filecoin-架构}

我们可以把 Filecoin 简化为两层:

-   一个是区块链，主要是记录全网状态（一个去中心化的状态机），包括所有钱包账户和余额，市场订单匹配记录。
-   一个是存储的解决方案，主要包括副本策略（纠删码，多副本），端到端加密，存储时间和续费策略，存储市场匹配等。

它主要包括 4 种角色：

-   存储矿工（Storage miners）： 将自己的磁盘抵押出来，提供存储服务，类似云厂商的对象存储
-   检索矿工（Retrieval miners）：可以帮助用户快速的检索到内容，类似于传统意义的 CDN
-   存储客户端（Storage clients）：能够上传内容到 Filecoin，类似对象存储上传客户端
-   检索客户端（Retrieval clients）：能够从 Filecin 检索到内容，类似对象存储下载客户端


## 市场 {#市场}

Filecoin 一共有两个市场:

-   存储市场
-   检索市场

**只有存储矿工才有系统的奖励，才真正属于 IPFS 的挖矿(系统的奖励).**


## 挖矿 {#挖矿}

挖矿就是在 Filecoin 网络中获取虚拟货币（FIL），主要可以通过以下途径：

-   成为存储矿工，在市场中通过报价的方式出租存储空间，当匹配成功，将获取相应报酬
-   成为检索矿工，帮助内容下载客户端下载内容
-   成为数据修复矿工，帮助修复丢失或损坏的数据