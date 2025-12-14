# 区块链分层

在前一篇中，我们了解了公链、私链和联盟链的不同特点，并看到公链已成为区块链技术最成功和最具活力的应用方向。然而，公链在追求去中心化和安全性的同时，也面临着可扩展性的挑战——这就是著名的"不可能三角"问题。

为了解决扩容问题，开发人员开始探索在垂直方向上扩展区块链，这就产生了我们常听到的 Layer1、Layer2 这样的术语。

以比特币及以太坊为例，去中心化及安全性是比特币、以太坊的基石，正是这些才保证中立、抗审查、开放性等特性，但这在某种程度上牺牲一些可扩展性来换取而来，比如：比特币网络每秒可处理的交易约 10 笔，以太坊每秒可处理的交易通常也只有几十笔。而 Visa 这样的电子支付网络每秒可以处理超过 20,000 笔交易。

开发人员试图以各种方式对区块链网络扩容，一个广泛被采用的方案是把一些计算放到链下进行（即链上叠加一层），链上只进行计算的校验和存储。

以下是一个分层架构图：

![](https://img.learnblockchain.cn/pics/20230209171636.png)

我们来分别介绍一下每一层。

## Layer0 

第 0 层，其实第0层的定义目前行业还没有完全一致的理解。

多数人认为第0层是 **加密数据连接层及其硬件**，对应上图下半部分。
也有一些人把跨链或可以创建链的基础设施为作为第0层，他们的代表有: [LayerZero](https://layerzero.network/)、[Substrate](https://substrate.io/) / [Polkadot](https://polkadot.network/) 及 [Cosmos](https://cosmos.network/)

## Layer1

第 1 层是我们常说的区块链，如比特币、以太坊、BSC 、[Solana](https://learnblockchain.cn/tags/Solana?map=Solana) 等。 这些区块链在自己的区块链上根据共识处理并最终完成交易，

第 1 层区块链网络为开发dApps提供了基础架构，开发者可以在第1层网络上其他协议，比如我们看到MAKER DAO 稳定币协议、加密朋克 [NFT](https://learnblockchain.cn/tags/NFT) 及 [Uniswap](https://learnblockchain.cn/tags/Uniswap?map=EVM) [DEX](https://learnblockchain.cn/tags/DEX?map=EVM) 协议等。

随着链上应用不断增长，网络“吞吐量”无法满足快速增加的需求，经常导致网络拥堵。增加区块链网络自身处理能力，一个常见的方法是扩大区块大小，以便在单个区块里可以容纳更多的交易，以太坊社区也确实多次提高过区块大小限制，但提高更快意味着更慢网络传播速度，以及更大数据意味着节点需要更大的存储容量，会提高节点参与网络的门槛，使得网络更中心化；另一个是方法是以太坊之前尝试的分片（Sharding）扩容方案，将区块链数据分成不同的组（分片），每个分片负责网络活动中的不同数据子集。

> 不过由于工程复杂度太高，以太坊基本上放弃了分片扩容方案。

## Layer2（二层网络）

Layer2 是针对底层区块链（Layer1）扩容的一种链下解决方案，Layer2 是一个独立的区块链，但使用第一层的安全性保证。

扩容主要思想是将原本 Layer1 的交易放在链下(Layer2)执行，减轻 Layer1 的负担，并且 Layer2 定期与Layer1通信，将Layer2的交易批量提交到 Layer1 。



### 比特币闪电网络


比特币上的 一个主要的 Layer2 扩容方案是**闪电网络（Lightning Network）**，为小额支付场景进行优化。闪电网络的主要是实现是，支付的双方在链下建立一个"通道"，双方可以在这个“通道”多次进行支付交易，在需要结算时，关闭通道即可。当支付的双方没有直接的"通道"可以借助第三方节点进行中转，如下路，A 要向 F 交易时，可借助 节点C 形成"通道"链路。所有节点一起就形成了一个支付网络。

![支付信道网状网络路由](https://img.learnblockchain.cn/pics/20230214173851.png)


与[比特币](https://learnblockchain.cn/tags/比特币?map=BTC)链上交易相比，闪电网络有几个好处：
1. **更低的交易费用，对小额交易非常友好**，由于比特币链上交易需要用户之间相互竞价，[比特币](https://learnblockchain.cn/tags/比特币?map=BTC)上一笔交易手续费通常在几美金，巅峰时期这需要几十美金，对于小额的交易，手续费往往比转移的金额还要多，闪电网络上通道费用是动态的，通常按转移的BTC数量的万分之几收取。
2. 在闪电网络协议下每秒可以发生的**支付数量没有基本限制**，仅受每个节点的容量和速度限制。
3. **更好的隐私**，闪电网络支付的细节不会公开记录在区块链上。闪电网络支付可以通过许多连续的通道进行路由，每个节点运营商都可以通过他们的通道看到支付，但如果不相邻，他们将无法看到这些资金的来源或目的地。



闪电网络也有一些**限制**：
闪电网络要求节点一直保持在线以充当支付通道，比较容易受到黑客攻击和盗窃；
多数用户可能会你来某个关键枢纽节点，这样的枢纽的离线可以迅速带来网络的集体（或完全）崩溃。



### 以太坊的 Rollup 方案



以太坊上主要的 Layer2 扩容方案是 Rollup，Rollup 意思是卷起，Rollup的核心思想是：**由 Rollup 层负责执行交易，然后将许多笔交易压缩成一笔交易批量提交给以太坊**。这样既能享受以太坊的安全性，又能大幅提升交易处理能力。

#### Rollup 的两种类型

Rollup 目前分为两种类型：**Optimistic Rollup（乐观 Rollup）和 ZK Rollup（零知识证明 Rollup）**，它们的主要区别在于如何向以太坊主网证明交易的有效性。

**1. Optimistic Rollup（乐观 Rollup）**

Optimistic Rollup 采用**乐观假设**策略，假设从 Layer2 上执行的交易都是可信的，并批量提交到以太坊上。为了保证安全性，设置了一个挑战期（通常为一周左右），在此期间任何人都可以发起欺诈证明（Fraud Proof）来验证交易的真实性。若挑战成功，原有交易被拒绝，并惩罚 Layer2 的排序器。

**主要项目：**
- **Arbitrum**：由 Offchain Labs 开发，目前是 TVL 最高的 Layer2 项目
- **Optimism**：采用 OP Stack 技术栈，支持一键发链
- **Base**：由 Coinbase 基于 OP Stack 构建，面向大众市场

Optimistic Rollup 的优势是可以实现 EVM 等效，现有的以太坊[智能合约](https://learnblockchain.cn/tags/%E6%99%BA%E8%83%BD%E5%90%88%E7%BA%A6)大部分不用做任何修改就可以直接部署。缺点是资金提现需要等待挑战期结束。

**2. ZK Rollup（零知识证明 Rollup）**

ZK Rollup 通过生成零知识证明（Zero-Knowledge Proof）来证明所有交易的有效性。每次向以太坊提交交易批次时，都会附带一个有效性证明（Validity Proof），以太坊验证这个证明后即可确认交易的正确性。

**技术优势：**
- 无需挑战期，资金提现更快（通常几小时）
- 更高的数据压缩率，成本更低
- 更强的安全性保证

**技术挑战：**
- 为通用计算生成[零知识证明](https://learnblockchain.cn/tags/%E9%9B%B6%E7%9F%A5%E8%AF%86%E8%AF%81%E6%98%8E)难度大，开发复杂度高
- 证明生成需要较高的计算资源

**主要项目：**
- **ZKSync Era**：由 Matter Labs 开发，2023 年 3 月上线主网，支持 [Solidity](https://learnblockchain.cn/tags/Solidity?map=EVM) 开发
- **Polygon zkEVM**：2023 年 3 月上线主网，实现了与以太坊 EVM 的高度等效性
- **Scroll**：2023 年 10 月上线主网，专注于 EVM 等效的 [zkEVM](https://learnblockchain.cn/tags/zkEVM?map=EVM)
- **StarkNet**：使用 [Cairo](https://learnblockchain.cn/tags/Cairo?map=Web3) 语言，采用 STARK 证明系统，虽不兼容 [EVM](https://learnblockchain.cn/tags/EVM?map=EVM) 但性能更高

**技术特性对比：**

![](https://img.learnblockchain.cn/pics/20230215143350.png)

#### Rollup 生态发展现状

经过几年的发展，Rollup 生态已经取得了显著成果。Layer2 上的交易量已经赶超以太坊主网，越来越多的应用选择在 Layer2 上部署。

![image-20230215120513798](https://img.learnblockchain.cn/pics/20230215120521.png)

上图是以太坊与 Arbitrum、Optimism 交易量的对比，可以看出 Layer2 已经成为以太坊生态不可或缺的重要组成部分。ZK Rollup 项目的成功上线也标志着[零知识证明](https://learnblockchain.cn/tags/%E9%9B%B6%E7%9F%A5%E8%AF%86%E8%AF%81%E6%98%8E)技术已经从理论走向成熟应用阶段。

#### 以太坊 Rollup 为中心路线图

2020年10月，[Vitalik](https://learnblockchain.cn/tags/Vitalik?map=EVM) 提出了以太坊以 Rollup 为中心的扩容路线图，这标志着以太坊扩容策略的重大转变（放弃分片方案）。这个路线图的核心思想是：**以太坊主网专注于提供安全性和数据可用性，而将交易执行和计算主要交给 Layer2 Rollup 来完成**。

> 相比分片需要对以太坊进行更深层的架构改造，Rollup 方案可以在现有技术框架下实现扩容，同时又可继承以太坊主网的安全性。


**Rollup 扩容方案的发展历程**

**第一阶段（2020-2021）：概念验证与早期部署**
- 2020年下半年，Optimistic Rollup 率先推出测试网
- 2021年，Arbitrum 和 Optimism 先后上线主网，开始承载实际应用

**第二阶段（2022-2023）：生态爆发与技术成熟**
- Layer2 上的 TVL（总锁仓量）快速增长，交易量超过以太坊主网
- ZK Rollup 项目陆续上线主网，ZKSync Era、Polygon [zkEVM](https://learnblockchain.cn/tags/zkEVM?map=EVM)、Scroll 等实现了 [EVM](https://learnblockchain.cn/tags/EVM?map=EVM) 兼容
- 出现了 Base（Coinbase）、UniChain、Lighter 等新一代 Rollup 链


**第三阶段（2024-）：数据可用性优化**
- EIP-4844（Proto-Danksharding）的实施，引入了 Blob 数据存储，大幅降低了 Rollup 的数据发布成本
- Rollup 交易费用进一步下降，使得更多应用场景成为可能


不过目前，多数 Rollup 仍处于中心化运营阶段，排序器（Sequencer）主要由项目方控制，同时多个 Rollup 之间的流动性割裂问题也日益凸显。未来 Rollup 的发展方向主要包括：

1. **完全去中心化**：逐步实现排序器、证明者和治理机制的去中心化，提升网络的抗审查性和安全性
2. **跨 Rollup 互操作性**：建立标准化的跨 Rollup 通信协议，实现不同 Rollup 之间无缝的资产和数据转移，解决流动性割裂问题
3. **ZK 技术的普及**：随着 ZK 证明生成效率的提升和成本的降低，ZK [Rollup](https://learnblockchain.cn/tags/Rollup) 有望成为主流扩容方案


### 侧链及其他方案

另一个和 [Layer2](https://learnblockchain.cn/tags/Layer2?map=EVM) 类似的二层扩容方案是侧链， 侧链和以太坊L2解决方案的主要区别是，**Layer2继承以太坊主网络的安全性，而侧链依赖于自己的安全性**。一个流行的侧链是Polygon ，他使用自己的PoS共识，有自己的验证者。但是 Polygon 会定期把交易的状态提交到[以太坊](https://learnblockchain.cn/tags/以太坊?map=EVM)。

在出现Rollup之前，状态通道、Plasma 等技术也是广泛讨论的扩容解决方案，但由于通用性不够、安全性不足等问题，被 [Rollup](https://learnblockchain.cn/tags/Rollup) 方案取代。

下图是[以太坊](https://learnblockchain.cn/tags/以太坊?map=EVM)链下扩容技术方案图。


![](https://img.learnblockchain.cn/pics/20230215164740.png)



## Layer 3

Layer3（第 3 层）目前行业还没有一致认可的定义，[Vitalik](https://learnblockchain.cn/tags/Vitalik?map=EVM) 在他的文章 [什么样的 Layer3 有意义](https://vitalik.ca/general/2022/09/17/layer_3.html) 里提出了对 Layer3 的 3 个愿景：

1. **L2 用于扩容，L3 用于自定义功能，例如隐私。**
2. **L2 用于通用扩容，L3 用于自定义扩容**， 
3. **L2 用于无信任扩展（rollups），L3 用于弱信任扩展（validiums）**。



还有一些人，将 [Layer2](https://learnblockchain.cn/tags/Layer2?map=EVM) 上的应用层，称为第 3 层，例如 [Uniswap](https://learnblockchain.cn/tags/Uniswap?map=EVM) 、[AAVE](https://learnblockchain.cn/tags/AAVE?map=EVM) 、MarkerDAO 等。

