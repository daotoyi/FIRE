+++
title = "IPFS"
description = "去中心化储存平台"
date = 2022-03-12T12:03:00+08:00
lastmod = 2022-03-12T12:04:49+08:00
draft = false
+++

## IPFS {#ipfs}

IPFS 全称为 Inter Planetary File System. 星际文件系统.

-   用于存储和访问文件、网站、应用程序和数据的分布式文件系统。
-   “一个点对点的超媒体传输协议”.点对点的分布式文件存储系统.
-   它的目标是成为更快、更安全、更开放的下一代互联网,用来替代传统中心化的服务器模式.
-   所有的IPFS节点组成一个分布式网络，每个节点都可以存储文件.
-   用户可以从IPFS构建的网络中以DHT(Distributed Hash Table，分布式哈希表) 的方式获取文件.


## 工作原理 {#工作原理}

IPFS 可以从本质上改变网络数据的分发机制

-   每个文件及其中的所有块都被赋予一个称为加密散列的唯一指纹。
-   IPFS 通过网络删除重复具有相同哈希值的文件，通过计算是可以判断哪些文件是冗余重复的。并跟踪每个文件的版本历史记录。
-   每个网络节点只存储它感兴趣的内容，以及一些索引信息，有助于弄清楚谁在存储什么。
-   查找文件时，你通过文件的哈希值就可以在网络查找到储存改文件的节点，找到想要的文件。
-   使用称为 IPNS（去中心化命名系统），每个文件都可以被协作命名为易读的名字。通过搜索，就能很容易地找到想要查看的文件。

从 IPFS 的介绍可以看出， IPFS 设想的是让所有的网络终端节点不仅仅只充当 Browser 或 Client 的角色，其实人人都可以作为这个网络的运营者，人人都可以是服务器。


## 基本使用 {#基本使用}


### Install &amp; use {#install-and-use}

参考官网：<https://ipfs.io/docs/install>
使用参考：<https://ipfs.io/docs/getting-started>

```shell
wget https://dist.ipfs.io/go-ipfs/v0.4.14/go-ipfs_v0.4.14_linux-amd64.tar.gz
tar xvfz go-ipfs_v0.4.14_linux-amd64.tar.gz
cd go-ipfs
./install.sh

# test
ipfs help

# start
ipfs init

# start daemon to keep connection with internet
ipfs daemon &

# show point connectted on IPFS
ipfs swarm peers
```


### Practice {#practice}

上传GitHub Pages主页到IPFS

```shell
git clone <git-pages-repo>
ipfs add -r <git-gages-repo>
# 以下输入会生成哈希码,标识了文件在网路上的位置

# 只要IPFS进程还开启着，数据就不会被垃圾回收
ipfs pin add -r <your-hash>

# 过网址访问个人主页
https://gateway.ipfs.io/ipfs/<your-hash>
```


## IPNS {#ipns}

一个命名系统，它可以把文件的哈希值命名为一个简单易懂的名字。

IPFS系统有版本管理系统，并且每一个节点上都有所存文件的哈希值构成的哈希表


## Reference {#reference}

-   [IPFS——它能取代 HTTP 协议？](https://www.jianshu.com/p/ddccae89a49a)