# 区块链扩容

在前一篇中，我们了解了公链、联盟链和私链的不同特点，并看到公链已成为区块链技术最成功和最具活力的应用方向。然而，公链在追求去中心化和安全性的同时，也面临着可扩展性的挑战——这就是著名的"不可能三角"问题。

## 扩容问题的由来

以比特币和以太坊为例，去中心化和安全性是它们的基石，正是这些特性保证了网络的中立性、抗审查性和开放性。但这在某种程度上需要牺牲一些可扩展性：

- **比特币**：每秒处理约 7-10 笔交易
- **以太坊**：每秒处理约 20-40 笔交易
- **Visa 网络**：每秒可以处理超过 20,000 笔交易

这样的性能差距，使得区块链在高频交易场景下面临网络拥堵、手续费飙升等问题。2017年的加密猫（CryptoKitties）曾一度让以太坊网络几乎瘫痪，2021年的 DeFi 热潮中，以太坊的 Gas 费用一度高达数百美元。

为了解决扩容问题，开发者们探索了多种方案。目前最主要的思路是**分层扩容**：Layer1 负责安全性，Layer2 负责性能。这就是我们常听到的 Layer1、Layer2 等术语的由来。

以下是区块链的分层架构图：

![](https://img.learnblockchain.cn/pics/20230209171636.png)

## Layer1 扩容方案

Layer1（第一层）就是我们常说的区块链本身，如比特币、以太坊、[Solana](https://learnblockchain.cn/tags/Solana?map=Solana) 等。Layer1 为去中心化应用（DApps）提供了基础架构，开发者可以在 Layer1 上构建各种协议，比如 MakerDAO 稳定币协议、[Uniswap](https://learnblockchain.cn/tags/Uniswap?map=EVM) 去中心化交易所、CryptoPunks [NFT](https://learnblockchain.cn/tags/NFT) 等。

### Layer1 的扩容尝试

随着链上应用不断增长，网络吞吐量无法满足快速增加的需求，经常导致网络拥堵。为了提升 Layer1 本身的处理能力，主要有以下几种方案：

**1. 扩大区块大小**

这是最直观的扩容方式，通过增大区块容量来容纳更多交易。比特币现金（BCH）就是采用这个方案，将区块大小从 1MB 提升到 32MB。

**优点**：简单直接，立即生效
**缺点**：
- 区块更大意味着更慢的网络传播速度
- 需要更大的存储空间，提高了节点参与网络的门槛
- 使得网络更加中心化（只有资源充足的节点能参与）

**2. 分片（Sharding）**

分片是将区块链数据分成不同的组（分片），每个分片负责网络活动中的不同数据子集，多个分片可以并行处理交易。

以太坊曾经计划采用分片扩容方案，但由于工程复杂度太高，后来放弃了这个方案，转而采用以 Rollup 为中心的路线图。

**3. 高性能共识机制**

一些新公链通过采用高性能的共识机制来提升 TPS（每秒交易数）：

- **Solana**：使用历史证明（PoH）+ PoS，理论 TPS 可达 65,000
- **BNB Chain（币安智能链）**：使用 PoSA 共识，由 21 个验证节点维护，TPS 约 160

**优点**：性能显著提升
**缺点**：通常需要牺牲一定的去中心化程度

### Layer1 扩容的局限

Layer1 扩容面临根本性的权衡：要保持去中心化和安全性，就很难在 Layer1 层面实现大幅扩容。这就是为什么业界逐渐转向 Layer2 扩容方案。

## Layer2 扩容方案

Layer2（第二层）是针对底层区块链（Layer1）扩容的链下解决方案。Layer2 本身也是一个独立的区块链，但它使用 Layer1 的安全性保证。

**核心思想**：将原本在 Layer1 上执行的交易放到 Layer2 上处理，减轻 Layer1 的负担，然后 Layer2 定期与 Layer1 通信，将交易批量提交到 Layer1。这样既能享受 Layer1 的安全性，又能大幅提升交易处理能力。



### 比特币闪电网络

比特币上的主要 Layer2 扩容方案是**闪电网络（Lightning Network）**，专为小额支付场景优化。

闪电网络的实现原理是：支付的双方在链下建立一个"通道"，双方可以在这个"通道"内多次进行支付交易，在需要结算时再关闭通道。当支付的双方没有直接的"通道"时，可以借助第三方节点进行中转。例如下图中，A 要向 F 交易时，可借助节点 C 形成"通道"链路。所有节点一起就形成了一个支付网络。

![支付信道网状网络路由](https://img.learnblockchain.cn/pics/20230214173851.png)

**闪电网络的优势：**

1. **更低的交易费用**：对小额交易非常友好。比特币链上交易手续费通常在几美元，巅峰时期需要几十美元，对于小额交易来说，手续费往往比转移的金额还要多。而闪电网络的通道费用是动态的，通常按转移的 BTC 数量的万分之几收取。

2. **极高的吞吐量**：闪电网络协议下每秒可以发生的支付数量没有基本限制，仅受每个节点的容量和速度限制。

3. **更好的隐私**：闪电网络支付的细节不会公开记录在区块链上。支付可以通过许多连续的通道进行路由，每个节点运营商只能看到通过他们通道的支付，如果不相邻，他们将无法看到这些资金的来源或目的地。

**闪电网络的局限：**

- 节点需要一直保持在线以充当支付通道，容易受到黑客攻击和盗窃
- 多数用户可能会依赖某个关键枢纽节点，这样的枢纽离线可能会导致网络的局部（或完全）崩溃
- 主要适用于小额高频支付场景，不适合大额转账



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


## 总结

区块链扩容是一个复杂但至关重要的问题。通过本篇的学习，我们了解了主流的扩容方案：

**扩容方案对比：**

| 方案类型 | 代表项目 | TPS | 安全性来源 | 优点 | 缺点 |
|---------|---------|-----|-----------|------|------|
| **Layer1 本身** | 比特币、以太坊 | 7-30 | 自身共识 | 最高安全性 | 性能受限 |
| **Layer1 优化** | Solana、BSC | 160-65000 | 自身共识 | 性能大幅提升 | 牺牲去中心化 |
| **比特币闪电网络** | Lightning Network | 无上限 | 比特币主网 | 低费用、高吞吐 | 仅适合小额支付 |
| **Optimistic Rollup** | Arbitrum、Optimism | ~4000 | 以太坊主网 | EVM 兼容性好 | 提现等待期长 |
| **ZK Rollup** | ZKSync、Scroll | ~2000 | 以太坊主网 | 提现快、安全性高 | 开发复杂度高 |
| **侧链** | Polygon | ~7000 | 自身共识 | 灵活性高 | 安全性较低 |

**关键要点：**

1. **不可能三角依然存在**：去中心化、安全性、可扩展性三者难以兼得，所有扩容方案都是在做权衡
2. **分层是主流方向**：Layer1 保证安全性，Layer2 提升性能，这已成为行业共识
3. **技术仍在快速发展**：从 Optimistic Rollup 到 ZK Rollup，从单一 Rollup 到跨 Rollup 互操作，扩容技术还在不断演进

对于区块链的未来，扩容不是目的，而是手段。真正的目标是在保持去中心化和安全性的前提下，让更多人能够以更低的成本使用区块链技术。随着 Layer2 生态的成熟和新技术的突破，这个目标正在逐步实现。

