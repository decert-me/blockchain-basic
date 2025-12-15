# Web3 实操入门

在前面的章节中，我们系统学习了区块链的理论知识：从[比特币](https://learnblockchain.cn/tags/比特币?map=BTC)的诞生、以太坊的[智能合约](https://learnblockchain.cn/tags/%E6%99%BA%E8%83%BD%E5%90%88%E7%BA%A6)，到各种区块链应用场景，再到Web3安全防护。现在，是时候将理论转化为实践了。

"纸上得来终觉浅，绝知此事要躬行"。无论理论知识学得多好，只有亲自动手操作，才能真正理解Web3世界的运作方式。本文将带你完成第一次Web3操作：创建钱包、发送交易、与DApp交互、参与DeFi、购买NFT等实际操作。

通过这些实践，你将从一个Web3的学习者，真正成为Web3世界的参与者。

> **重要提醒**：本文的实操建议先在测试网进行，熟练后再使用真实资金。记住上一篇学到的安全知识，保护好你的私钥和资产。


## 第一步：安装钱包

钱包是你进入Web3世界的入口。我们以最流行的MetaMask为例。

### 安装MetaMask

**支持平台：**
- Chrome、Firefox、Edge等浏览器扩展
- iOS和Android移动应用

**安装步骤：**

1. **访问官网**
   - 官网：https://metamask.io
   - ⚠️ 注意：一定要通过官方网站下载，警惕钓鱼网站

2. **安装扩展**
   - 点击"Download"
   - 选择你的浏览器
   - 点击"Install MetaMask for XXX"
   - 安装完成后，浏览器工具栏会出现小狐狸图标

3. **创建钱包**
   - 点击"创建新钱包"
   - 设置一个强密码（这个密码只保护本地，不是助记词）
   - ⚠️ 重要：阅读并理解安全提示

4. **备份助记词**
   - 系统会显示12个单词的助记词
   - ⚠️ 极其重要：用笔抄写在纸上，不要截图
   - 按顺序记录，不要记错顺序
   - 妥善保管，不要让任何人看到
   - 验证助记词：按要求点击单词，确认记录正确

5. **完成**
   - 恭喜！你已经有了第一个Web3钱包
   - 你会看到你的钱包地址，类似：`0x1234...abcd`

### MetaMask界面介绍


![MetaMask 主界面](https://img.learnblockchain.cn/attachments/2025/12/T3e4m4ku693fee5332c40.png)

**主要功能：**
- **账户地址**：点击顶部左上角可复制地址
- **余额**：显示当前网络的代币余额
- **发送**：转账给他人
- **收款**：显示二维码，接收转账
- **代币**：查看持有的代币
- **活动**：查看交易历史


**网络切换：**
- 点击左上角的网络名称
- 可以切换到不同的区块链网络
- 默认是以太坊主网


## 第二步：获取测试币

在正式操作前，先在测试网练手。测试网的币是免费的，没有价值，可以随意实验。

### 切换到测试网

1. **显示测试网络**
   - 点击MetaMask右上角的三个点
   - 设置 → 高级 → 显示测试网络（开启）

2. **切换到Sepolia测试网**
   - 点击左上角网络名称
   - 选择"Sepolia测试网络"

### 获取测试ETH

**Sepolia测试网水龙头：**

1. **Alchemy水龙头**
   - 访问：https://sepoliafaucet.com
   - 登录Alchemy账户（需要注册）
   - 输入你的钱包地址
   - 点击"Send Me ETH"
   - 等待几分钟，查看MetaMask余额

2. **Infura水龙头**
   - 访问：https://www.infura.io/faucet/sepolia
   - 输入钱包地址
   - 完成验证
   - 领取测试ETH

3. **其他水龙头**
   - https://faucet.quicknode.com/ethereum/sepolia
   - https://www.alchemy.com/faucets/ethereum-sepolia

**其他测试网：**
- **BSC测试网**：https://testnet.bnbchain.org/faucet-smart


## 第三步：发送第一笔交易

现在你有了测试ETH，可以尝试发送交易了。

### 转账操作

1. **点击"发送"按钮**

2. **输入接收地址**
   - 可以发送到你的另一个钱包
   - 或者发送到朋友的地址
   - ⚠️ 仔细检查地址，区块链交易不可撤销

3. **输入金额**
   - 例如：0.01 ETH
   - 确保留一些ETH作为Gas费

4. **查看Gas费**
   - MetaMask会自动估算Gas费
   - 可以选择"慢"、"市场"、"快速"
   - 测试网可以选择最低的

5. **确认交易**
   - 点击"确认"
   - 等待交易被确认（通常几秒到几分钟）

6. **查看交易状态**
   - 在"活动"标签查看
   - 点击交易可以看到详情
   - 点击"在区块浏览器中查看"可以看到链上记录

### 理解交易详情

点击交易后，你会看到：
- **状态**：待处理 → 已确认
- **从（From）**：你的地址
- **到（To）**：接收方地址
- **Nonce**：这是你发出的第几笔交易
- **金额**：转账数量
- **Gas费用**：实际支付的手续费
- **交易哈希**：这笔交易的唯一标识符


## 第四步：使用区块链浏览器

区块链浏览器是查看链上信息的窗口。

### 以太坊区块链浏览器

**主要浏览器：**
- **Etherscan**：https://etherscan.io （以太坊主网）
- **Sepolia Etherscan**：https://sepolia.etherscan.io （Sepolia测试网）

### 查看你的地址

1. **复制你的钱包地址**
   - 在MetaMask点击地址复制

2. **在Etherscan搜索**
   - 访问 https://sepolia.etherscan.io
   - 在搜索框粘贴你的地址
   - 按回车

3. **查看地址信息**
   - **Overview**：余额、价值
   - **Transactions**：所有交易记录
   - **Token Holdings**：持有的ERC-20代币
   - **NFTs**：持有的NFT

### 查看交易详情

点击任意一笔交易，你会看到：

- **Transaction Hash**：交易的唯一标识
- **Status**：成功或失败
- **Block**：被打包进哪个区块
- **Timestamp**：交易时间
- **From**：发送方
- **To**：接收方
- **Value**：转账金额
- **Transaction Fee**：手续费
- **Gas Price**：Gas单价
- **Gas Limit & Usage**：Gas限制和实际使用量
- **Input Data**：如果是合约交互，会有输入数据

### 查看智能合约

如果你查看的是合约地址，会看到：

- **Contract**：合约标签
- **Code**：合约源代码（如果已验证）
- **Read Contract**：读取合约状态
- **Write Contract**：写入合约（需要连接钱包）
- **Events**：合约事件日志


## 第五步：添加自定义代币

MetaMask默认只显示ETH，要查看其他代币需要手动添加。

### 自动添加（推荐）

当你接收到某个代币后，MetaMask可能会自动识别并提示添加。

### 手动添加

1. **获取代币合约地址**
   - 访问代币的官网或CoinGecko
   - 复制合约地址
   - ⚠️ 一定要从官方渠道获取，警惕假代币

2. **在MetaMask中添加**
   - 切换到对应的网络
   - 点击"资产"标签
   - 点击"导入代币"
   - 粘贴合约地址
   - 代币符号和小数位数会自动填充
   - 点击"添加自定义代币"

3. **查看余额**
   - 回到"资产"标签
   - 可以看到该代币的余额

### 常见代币合约地址（以太坊主网）

- **USDT**: `0xdac17f958d2ee523a2206206994597c13d831ec7`
- **USDC**: `0xa0b86991c6218b36c1d19d4a2e9eb0ce3606eb48`
- **DAI**: `0x6b175474e89094c44da98b954eedeac495271d0f`

⚠️ 使用前请在Etherscan上验证地址的正确性。


## 第六步：与DApp交互

[DApp](https://learnblockchain.cn/tags/DApp)（去中心化应用）是运行在区块链上的应用。让我们尝试使用一个简单的DApp。

### 使用Uniswap（去中心化交易所）

Uniswap是最流行的去中心化交易所，我们在测试网上体验一下。

1. **访问Uniswap**
   - 官网：https://app.uniswap.org
   - ⚠️ 确保是官方网站

2. **连接钱包**
   - 点击右上角"连接钱包"
   - 选择MetaMask
   - 在弹出的MetaMask窗口点击"连接"
   - ⚠️ 检查网站URL，确保是官方网站

3. **切换到测试网**
   - 在Uniswap界面切换网络到Sepolia
   - 如果钱包网络不匹配，MetaMask会提示切换

![image.png](https://img.learnblockchain.cn/attachments/2025/12/8tRKfnQr693fef6934dfc.png)

4. **兑换代币**
   - 在测试网上，你可以尝试兑换操作
   - 选择要兑换的代币对
   - 输入数量
   - 点击"兑换"
   - 在MetaMask中确认交易

### 签名时的注意事项

与DApp交互时，你可能遇到不同类型的签名请求：

**1. 连接钱包（安全）**
- 只是授权网站查看你的地址
- 不会花费Gas，不会转移资产

**2. 签名消息（需小心）**
- 用于身份验证或登录
- 不会花费Gas，不会直接转移资产
- 但要确保你信任这个网站

**3. 批准/授权代币（需谨慎）**
- 允许合约操作你的代币
- 需要花费少量Gas
- ⚠️ 只授权你信任的合约
- ⚠️ 定期检查和撤销不必要的授权

**4. 交易确认（最需谨慎）**
- 会执行实际操作
- 需要花费Gas
- 可能转移资产
- ⚠️ 仔细检查交易详情


## 第七步：购买NFT

[NFT](https://learnblockchain.cn/tags/NFT)（非同质化代币）是区块链上的独特数字资产。

### 在OpenSea购买NFT（主网）

> [OpenSea](https://learnblockchain.cn/tags/OpenSea) 测试网现在已经关闭, 如果要体验只能在正式的主网上进行。因此你可能需要从朋友处或交易所购买一点以太坊，然后转入到你的钱包。


1. **访问OpenSea**
   - https://opensea.io
   - 点击右上角钱包图标
   - 连接MetaMask
   - 确保MetaMask在以太坊等正式网络上

2. **浏览NFT**
   - 在搜索框搜索测试NFT项目
   - 点击感兴趣的NFT

3. **购买或铸造**
   - 有些测试NFT可以免费铸造（Mint）
   - 点击"Mint"按钮
   - 在MetaMask中确认交易
   - 等待交易确认

4. **查看你的NFT**
   - 点击右上角头像 → My Items
   - 可以看到你拥有的NFT
   - 在MetaMask的"[NFT](https://learnblockchain.cn/tags/NFT)"标签也能看到


## 第八步：探索更多DApp

现在你已经掌握了基础操作，可以探索更多DApp：

### DeFi应用

**去中心化交易所：**
- **[Uniswap](https://learnblockchain.cn/tags/Uniswap?map=EVM)**：https://app.uniswap.org
- **1inch**：https://app.1inch.io
- **[Curve](https://learnblockchain.cn/tags/Curve?map=EVM)**：https://curve.fi

**借贷平台：**
- **Aave**：https://app.aave.com
- **Compound**：https://app.compound.finance

**稳定币：**
- **MakerDAO**：https://app.spark.fi （原Oasis）

### NFT平台

- **[OpenSea](https://learnblockchain.cn/tags/OpenSea)**：https://opensea.io （最大NFT市场）
- **[Blur](https://learnblockchain.cn/tags/Blur)**：https://blur.io （专业交易者）
- **LooksRare**：https://looksrare.org

### 其他有趣的DApp

- **ENS**：https://app.ens.domains （[以太坊](https://learnblockchain.cn/tags/以太坊?map=EVM)域名服务）
- **Snapshot**：https://snapshot.org （DAO投票平台）
- **Gitcoin**：https://gitcoin.co （开源项目捐赠）

### 探索DApp目录

- **DappRadar**：https://dappradar.com
- **[DeFi](https://learnblockchain.cn/tags/DeFi?map=EVM) Llama**：https://defillama.com
- **Dapp.com**：https://www.dapp.com


## 进阶操作

### 添加自定义网络

除了[以太坊](https://learnblockchain.cn/tags/以太坊?map=EVM)，你可能需要使用其他区块链：

**添加BNB Chain（原BSC-币安智能链）：**
1. 打开MetaMask
2. 点击网络下拉菜单
3. 点击"添加网络"
4. 点击"手动添加网络"
5. 填入以下信息：
```
网络名称: BSC Mainnet
RPC URL: https://bsc-dataseed.binance.org
链 ID: 56
货币符号: BNB
区块浏览器: https://bscscan.com
```
6. 点击"保存"

其他网络在在 [chainlist.com](https://chainlist.org/) 寻找。
 

### 使用硬件钱包

当你有了一定资产后，建议使用硬件钱包：

1. **购买硬件钱包**
   - Ledger Nano S/X
   - Trezor Model One/T
   - OneKey

2. **连接MetaMask**
   - 在MetaMask点击账户图标
   - "连接硬件钱包"
   - 选择Ledger或Trezor
   - 按照提示操作

### 管理多个账户

MetaMask支持创建多个账户：

1. **创建新账户**
   - 点击右上角圆形图标
   - "创建账户"
   - 命名新账户
   - 点击"创建"

2. **导入[账户](https://learnblockchain.cn/tags/账户?map=EVM)**
   - 如果你有其他钱包的私钥或助记词
   - 可以导入到MetaMask
   - ⚠️ 不建议在一个MetaMask中导入过多[账户](https://learnblockchain.cn/tags/账户?map=EVM)

### 撤销代币授权

定期检查和撤销不必要的授权：

1. **访问Revoke.cash**
   - https://revoke.cash
   - 连接MetaMask
   - 切换到对应网络

2. **查看授权**
   - 看到所有授权列表
   - 查看哪些合约可以操作你的代币

3. **撤销授权**
   - 点击不需要的授权旁边的"Revoke"
   - 在MetaMask中确认交易
   - 支付少量Gas费


## 常见问题

### Q: 交易一直pending（待处理）怎么办？

**原因：**Gas价格设置过低，矿工不愿意打包。

**解决方法：**
1. 等待网络不拥堵时自动确认
2. 加速交易（Replace/Speed Up）：
   - 点击pending的交易
   - 点击"加速"
   - 提高Gas价格
   - 确认

3. 取消交易（Cancel）：
   - 点击pending的交易
   - 点击"取消"
   - 需要支付Gas费
   - 发送一笔相同Nonce的交易覆盖原交易

### Q: 为什么我的交易失败了？

**常见原因：**
- Gas限制太低
- 合约执行失败（如余额不足）
- Slippage（滑点）设置太低
- 网络拥堵

**解决方法：**
- 在Etherscan查看交易详情
- 查看错误信息
- 增加Gas限制或Slippage
- 等待网络不拥堵时再试

### Q: 如何判断一个DApp是否安全？

**检查清单：**
- ✅ 通过官方渠道访问
- ✅ 检查URL是否正确
- ✅ 查看社区评价
- ✅ 合约是否经过审计
- ✅ 项目是否开源
- ✅ 使用钱包安全插件

### Q: 不小心授权了不安全的合约怎么办？

立即撤销授权：
1. 访问 https://revoke.cash
2. 连接钱包
3. 找到该授权
4. 点击"Revoke"撤销


## 实践建议

### 学习路径

1. **第一周：熟悉基础操作**
   - 创建钱包
   - 在测试网发送交易
   - 使用区块链浏览器

2. **第二周：体验DApp**
   - 使用DEX兑换代币（测试网）
   - 尝试铸造测试NFT
   - 探索不同的DApp

3. **第三周：小额实战**
   - 在主网进行小额操作
   - 购买少量主流币
   - 参与DeFi流动性挖矿（小额）

4. **持续学习**
   - 关注安全新闻
   - 学习新的DApp和协议
   - 参与社区讨论

### 风险管理

- 🟢 **小额试水**：先用小额资金熟悉操作
- 🟢 **测试网练习**：重要操作先在测试网试一遍
- 🟢 **分散风险**：不要把所有资产放在一个地方
- 🟢 **保持学习**：Web3发展很快，要持续学习
- 🔴 **不要梭哈**：不要投入超过你能承受的损失
- 🔴 **警惕FOMO**：不要因为害怕错过而冲动投资


## 总结

现在你已经完成了Web3的入门实操：
- ✅ 创建并备份了[钱包](https://learnblockchain.cn/tags/%E9%92%B1%E5%8C%85)
- ✅ 发送了第一笔交易
- ✅ 学会了使用区块链浏览器
- ✅ 尝试了与DApp交互
- ✅ 了解了安全注意事项

Web3之旅才刚刚开始，保持好奇心，谨慎操作，持续学习。祝你在Web3世界探索愉快！


## 学习资源

**[钱包](https://learnblockchain.cn/tags/%E9%92%B1%E5%8C%85)教程：**
- [MetaMask官方文档](https://support.metamask.io/)
- [imToken帮助中心](https://support.token.im/)
  
**系统教程：**
[区块链技术集训营 - 线下](https://learnblockchain.cn/openspace/1)
[区块链应用开发系统课 - 线上](https://learnblockchain.cn/course/28)

**学习平台：**
- [登链社区](https://learnblockchain.cn/)
- Twitter：关注加密朋克们的 Twitter

开始你的Web3旅程吧！