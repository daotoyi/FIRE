+++
title = "Create NFTs"
date = 2022-03-12T15:19:00+08:00
lastmod = 2022-03-12T15:19:52+08:00
draft = false
+++

## Reference {#reference}

[NFT制作与OpenSea部署教程](https://learnblockchain.cn/article/2366)


## Resource {#resource}


### [NFT Brownie Mix](https://github.com/PatrickAlphaC/nft-mix) {#nft-brownie-mix}

工作代码库，有非常多样板代码。


### Metamask {#metamask}


### [Infura](https://infura.io/) {#infura}

Infura 是出色的开放以太坊节点，它免费提供了标准的 RPC API 可供开发者 调用。除了支持以太坊，Infura 还提供 IPFS 网关和 API，并且提供多个 数字货币交易所的行情信息 API。

**为开发人员提供了一种不必运行全节点就可以连接以太坊网络的方法**

Infura 是一种 IaaS（Infrastructure as a Service）产品，目的是为了降低访问以太坊数据的门槛。可以让你的 dApp 快速接入以太坊的平台，不需要本地运行以太坊节点。

Infura 是由唯一的一家供应商运营的——以太坊开发工作室 Consensys——它依赖于亚马逊托管的云服务器。


## Install {#install}


### eth-brownie {#eth-brownie}

```shell
git clone https://github.com/PatrickAlphaC/nft-mix
cd nft-mix

pip install eth-brownie
# apt install npm
npm install -g ganache-cli
```


### .env {#dot-env}

```shell
export PRIVATE_KEY=YOUR_KEY_HERE
export WEB3_INFURA_PROJECT_ID=YOUR_PROJECT_ID_HERE
```

-   your_key_here
    PRIVATE_KEY:(MetaMask: Account Details --&gt; Export Private Key)

-   your_project_id_here
    Web3 Infura Project ID


### brownie run {#brownie-run}

```shell
# deploy NFT contract to Rinkeby blockchain.
brownie run scripts/simple_collectible/deploy_simple.py --network rinkeby

# create collect
brownie run scripts/simple_collectible/create_collectible.py --network rinkeby
```


## ERC721 {#erc721}

```c
 // SPDX-License-Identifier: MIT
pragma solidity 0.6.6;

// transfer 意味着把我们的代币转移给新用户，
import "@openzeppelin/contracts/token/ERC721/ERC721.sol";

// 承继ERC721 代币合约功能
contract SimpleCollectible is ERC721 {
    uint256 public tokenCounter;
    // 部署合约时，constructor会被自动调用. 构造函数只需要取一个名字和一个符号, 如"Dogie"和"DOG"
    constructor () public ERC721 ("Dogie", "DOG"){
      // 计数我们创建了多少这个类型的 NFT
        tokenCounter = 0;
    }


    // 也可以用 createCollectible 函数创建一个 NFT。这就是在我们的 create_collectible.py 脚本里调取的函数。
    function createCollectible(string memory tokenURI) public returns (uint256) {
        uint256 newItemId = tokenCounter;
        // safeMint表示创建新的代币， NFT。并把它分给任何调用了 createdCollectible的账户，即 msg.sender，且会有一个从 tokenCounter派生的 newItemId
        _safeMint(msg.sender, newItemId);
        _setTokenURI(newItemId, tokenURI);
        tokenCounter = tokenCounter + 1;
        return newItemId;
    }

}
```


## TokenURI {#tokenuri}

要一种轻量方法储存 NFT 的属性信息——这就是需要 tokenURI 和元数据的地方。

一个 NFT 上的 tokenURI 是能展示这个代币的唯一标识符。

一个 URI 可以是 HTTPS 上的 API 调用、一个 IPFS 的哈希、或任何其他代表唯一的东西。

```json
  {
    "name": "name",
    "description": "description",
    "image": "https://ipfs.io/ipfs/QmTgqnhFBMkfT9s8PHKcdXBn1f5bG3Q5hmBaR4U6hoTvb1?filename=Chainlink_Elf.png",
    "attributes": [
        {
            "trait_type": "trait",
            "value": 100
        }
    ]
}
```

我们专注在链上元数据上，这样我们才可以对我们的 NFT 进行编程，使它们互相交互。 尽管如此，我们仍然需要 image 部分的链下元数据.


## Deploy on Opensea {#deploy-on-opensea}

动态 NFT 是那种随时间变化的，或具有我们可以用来互相交互的链上功能的 NFT。这些 NFT 给了我们无限制的自定义空间去制作整个游戏、构建世界、以及某种交互艺术。

-   确认你的 metamask 里有足够的 ETH 和 LINK 测试币, 然后：

    ```shell
    # 这里的收藏品是从 Chainlink VRF (Virtual Routing and Forwarding，虚拟路由和转发) 返回的一个随机犬种
    brownie run scripts/advanced_collectible/deploy_advanced.py --network rinkeby
    brownie run scripts/advanced_collectible/create_collectible.py --network rinkeby

    # 创建它的元数据
    brownie run scripts/advanced_collectible/create_metadata.py --network rinkeby
    ```

-   选择性地上载这个数据到 IPFS，这样我们就会获得一个 tokenURI.

    如这个样本 tokenURI：<https://ipfs.io/ipfs/Qmd9MCGtdVz2miNumBHDbvj8bigSgTwnr4SbyH6DNnpWdt?filename=1-PUG.json>

-   set_tokenuri.py

    ```shell
    brownie run scripts/advanced_collectible/set_tokenuri.py --network rinkeby

    # -----------------
    # output such:
    Running 'scripts/advanced_collectible/set_tokenuri.py::main'...
    Working on rinkeby
    Transaction sent: 0x8a83a446c306d6255952880c0ca35fa420248a84ba7484c3798d8bbad421f88e
    Gas price: 1.0 gwei   Gas limit: 44601   Nonce: 354
    AdvancedCollectible.setTokenURI confirmed - Block: 8331653   Gas used: 40547 (90.91%)

    Awesome! You can view your NFT at https://testnets.opensea.io/assets/0x679c5f9adC630663a6e63Fa27153B215fe021b34/0
    Please give up to 20 minutes, and hit the "refresh metadata" button
    ```

    点击里面的链接看看它在 Opensea 上怎么样的。(可能需要点 refresh metadata ，等上几分钟)