# 验证器常见问题

::: 警告 建议
在成为验证者之前，请仔细阅读本文档。
:::

## 一般概念

### 什么是验证器？

Terra Core 由 Tendermint 共识提供支持。验证者运行全节点，通过广播投票参与共识，向区块链提交新区块，并参与区块链的治理。验证者可以代表他们的委托人投票。验证者的投票权根据他们的总股份进行加权。

### 什么是全节点？

全节点是验证区块链交易和区块的程序。验证者必须运行完整节点。全节点比轻节点需要更多的资源，轻节点只处理区块头和一小部分交易。运行全节点意味着您正在运行非妥协和最新版本的 Terra Core 软件，具有低网络延迟和无停机时间。

任何用户都可以并鼓励他们运行完整节点，即使他们不打算成为验证者。

### 什么是质押？

当 Luna 持有者将他们的 Luna 委托给验证者时，他们就是 *** staking。*** Staking 会增加验证者的权重，这对他们有帮助，作为回报，委托人会得到奖励。

Columbus-5 Mainnet 是公开的权益证明 (PoS) 区块链。这意味着验证者的权重(总权益)由他们委托给自己的权益代币 (Luna) 的数量加上外部委托人绑定给他们的 Luna 数量决定。验证者的权重决定了他们是否是活跃的验证者以及他们提出区块的频率。权重较高的验证者会提出更多的区块，从而获得更多的收入。

活跃验证者集由 130 个验证者组成，他们持有 Luna 的数量最多。底层验证者的权益总是构成进入网络的障碍。创建一个比底部验证器拥有更多权益的验证器是进入活跃集的唯一方法。如果验证者双重签名，或经常离线，他们将冒着质押的 Luna(包括用户委托的 Luna)被协议削减以惩罚疏忽和不当行为的风险。 

### 什么是委托人？

委托人是 Luna 持有者，他们希望获得质押奖励，而无需负责运行验证人。通过 Terra Station，用户可以将 Luna 委托给验证者，并作为交换获得验证者的部分收入。有关如何分配收入的更多详细信息，请参阅[什么是股权激励？](#what-are-the-incentives-to-stake) 和[什么是验证人的佣金？](#what-is-a-验证人委员会)。

委托人与他们的验证人分享质押的好处和奖励。如果验证者成功，其委托人将始终共享奖励结构。如果验证人被削减，委托人的股份也将被削减。这就是为什么委托人应该在委托之前对验证人进行尽职调查。委托人还可以通过将他们的股份分散到多个验证人上来实现多样化。

委托人在系统中起着至关重要的作用，因为他们负责选择验证人。作为委托人并不是一个被动的角色。委托人应保持警惕，积极监控验证人的行为，并在感觉当前验证人不能满足其需求时重新委托。

## 成为验证者

### 如何成为验证者？

网络中的任何参与者都可以通过创建验证器并注册其验证器配置文件来表示他们想要成为验证器的意图。候选人然后广播一个 `create-validator` 交易，其中包含以下数据:

- **公钥:** 验证者运营商可以拥有不同的账户来验证和持有流动资金。提交的 PubKey 必须与验证器将用于签署 _prevotes_ 和 _precommits_ 的私钥相关联。

- **地址:** `terravaloper-` 地址。这是用于公开识别您的验证者的地址。与此地址关联的私钥用于绑定、解绑和索取奖励。

- **姓名**(也称为**绰号**)

- **网站** _(可选但推荐)_

- **描述** _(可选但推荐)_

- **初始佣金率:** 区块规定、区块奖励和向委托人收取的费用的佣金率。

- **最高佣金:** 允许验证者收取的最高佣金率。 (这个不能改)

- **佣金变动率**:验证人佣金的每日最大增幅。(无法更改)

- **最小自绑定数量**:验证者始终需要的最小绑定 Luna 数量。如果验证者的自绑定质押低于此限制，则其整个质押池将被解绑。

- **初始自绑定数量**:验证者自绑定Luna的初始数量。

**例子:**
```bash
terrad tx staking create-validator
    --pubkey terravalconspub1zcjduepqs5s0vddx5m65h5ntjzwd0x8g3245rgrytpds4ds7vdtlwx06mcesmnkzly
    --amount "2uluna"
    --from tmp
    --commission-rate="0.20"
    --commission-max-rate="1.00"
    --commission-max-change-rate="0.01"
    --min-self-delegation "1"
    --moniker "gazua"
    --chain-id "test-chain-uEe0bV"
    --gas auto
    --node tcp://127.0.0.1:26647
```

创建并注册验证者后，Luna 持有者可以将 Luna 委托给他们，从而有效地向其池中增加股份。一个验证人的总权益是他们自己绑定的 Luna 加上外部委托人绑定的 Luna 的总和。

**只有前 130 个验证器被视为活跃或 *绑定验证器***。如果验证者的总权益低于前 130，验证者将失去其验证者特权，不再作为活跃集的一部分，进入**解绑模式**并最终成为**解封**或不活跃。

## 验证器键和状态

### 有哪些不同类型的密钥？

有两种类型的键:

- **Tendermint 密钥:** 用于签署与公钥“terravalconspub”关联的区块哈希的唯一密钥。

  - 当使用 `terrad init` 创建节点时会生成此密钥。
  - 使用`terrad tendenmint show-validator`查看密钥

    **示例:** `terravalconspub1zcjduc3qcyj09qc03elte23zwshdx92jm6ce88fgc90rtqhjx8v0608qh5ssp0w94c`

- **应用程序密钥:** 这些密钥是从应用程序创建的，用于签署交易。作为验证者，您可能会使用一个密钥来签署与 staking 相关的交易，并使用另一个密钥来签署与 oracle 相关的交易。应用程序密钥与公钥“terrapub-”和地址“terra-”相关联。两者都源自由“terrad keys add”生成的帐户密钥。

::: 警告 警告
验证器的操作员密钥直接与应用程序密钥相关联，但仅为此目的使用保留前缀:`terravaloper` 和 `terravaloperpub`
:::

### 验证器可以处于哪些不同状态？

使用 `create-validator` 交易创建验证器后，它可以处于三种状态:

- `bonded`:处于活动集中并参与共识的验证器。该验证器正在获得奖励，并且可能会因不当行为而被削减。

- `unbonding`:不在活动集中且不能不参与共识的验证器。该验证者没有获得奖励，但仍可能因不当行为而受到惩罚。这是从“bonded”到“unbonded”的过渡状态。如果验证者在“解除绑定”模式下未发送“重新绑定”交易，则状态转换将需要三周时间才能完成。

- `unbonded`:一个不在活动集中且不签署区块的验证器。未绑定的验证者不能被削减，也不能从他们的操作中获得任何奖励。仍然可以将 Luna 委托给未绑定的验证器。从“非绑定”验证器取消委托是立即的。

所有委托人都与其验证人具有相同的状态。

代表团不一定是绑定的。 Luna 可以是委托和保税、委托和非保税、委托和非保税或流动的。 

### 什么是“自我绑定”？我怎样才能增加我的“自我绑定”？

验证者运营商的“自我绑定”是指委托给自己的 Luna 数量。您可以通过将更多 Luna 委托给您的验证者账户来增加您的自我绑定。

### 我可以委托给活动集之外的验证器吗？

即使他们没有出现在 Terra Station 上，您仍然可以委托给验证者。只需将所需验证器的 terravaloper 地址添加到以下 URL 的末尾:

`https://station.terra.money/validator/<terravaloper-address>`

向您的验证器询问他们的 terravaloper 地址。

委托给活动集之外的验证者时要小心。一些不活跃的验证器可能会被监禁或不再受支持。 Station 仅显示能够参与共识的活跃或最近活跃的验证者。

### 有水龙头吗？

使用 [Terra faucet](https://faucet.terra.money/) 获取测试网币。

### 是否有最低数量的 Luna 必须抵押才能成为活跃(绑定)验证器？

没有最低限度。总权益最高的前 130 个验证者(其中总权益 = 自绑定权益 + 委托权益)构成了活跃验证者集。底部的第 130 个验证器设置了活动集的进入壁垒。

### 委托人将如何选择他们的验证人？

委托人可以根据自己的标准自由选择验证人。这可能包括:

- **自绑定 Luna 的数量:**验证者自绑定到其抵押池的 Luna 数量。拥有更多自绑定 Luna 的验证器在游戏中拥有更多的皮肤，使其对自己的行为负有更大的责任。

- **委托的Luna数量:**委托给验证者的Luna总量。高权益表明社区信任这个验证者；然而，这也意味着验证器是黑客的更大目标。大股份提供大投票权。这削弱了网络。在任何给定时间，如果 33% 或更多质押的 Luna 无法访问，网络将停止运行。通过激励和教育，我们可以通过委托拥有过多投票权的验证者来防止这种情况发生。验证者有时会随着他们委托的 Luna 数量的增加而变得不那么有吸引力。

- **佣金率:** 在分配给其委托人之前，验证者应用于奖励的佣金。

- **跟踪记录:** 委托人可以查看他们计划委托给的验证人的跟踪记录。这包括资历、过去对提案的投票、历史平均正常运行时间以及节点被入侵的频率。

验证者还可以提供一个网站地址来完成他们的简历。验证者需要建立良好的声誉来吸引委托人。验证者的设置由第三方审核是一种很好的做法。请注意，Terra 团队不会批准或进行任何审核。

## 职责

### 验证器需要公开识别吗？

不，他们没有。每个委托人将根据自己的标准评估验证人。通常建议验证者在提名自己时注册一个网站地址，以便他们可以在他们认为合适的时候宣传他们的操作。

### 验证者的职责是什么？ 

验证者必须:

- **运行正确的软件版本:**验证者需要确保他们的服务器始终在线，并且他们的私钥没有被泄露。

- **积极参与价格发现和稳定:** 高度激励验证者提交 Luna 真实市场价格的诚实和正确投票。还鼓励验证者进行套利掉期以稳定 Terra 稳定币的价格。

- **对社区池资金的正确部署提供监督和反馈:** Terra 协议包括一个提案治理系统，以促进其货币的采用。验证者应持有预算执行者以提供透明度并有效地使用资金。

- **成为社区的活跃成员:** 验证者应始终了解生态系统的当前状态，以便他们可以轻松适应任何变化。

### 质押意味着什么？

将抵押的 Luna 视为验证者活动的安全押金。当验证者或委托人想要取回部分或全部存款时，他们会发送一个解绑交易。质押的 Luna 然后会经历_三周的解绑期，_在此期间，它很容易因为验证者在解绑过程开始之前犯下的潜在不当行为而受到大幅削减的风险。

验证者收到区块供应、区块奖励和费用奖励，并与他们的委托人分享这些。如果验证者行为不当，则其总权益的一部分将被削减(惩罚的严重程度取决于不当行为的类型)。这意味着每个将 Luna 绑定到被削减的验证器的用户都会按他们的股份比例受到惩罚。鼓励委托人委托给安全运行的验证人。

### 验证者可以带着委托人的 Luna 逃跑吗？

**不可以。**通过委托给验证者，用户委托权益。验证者拥有的权益越多，它在共识和流程中的权重就越大。这并不意味着验证者对其委托人的 Luna 拥有保管权。

::: 警告 警告
验证者不可能带着委托人的资金逃跑。
:::

尽管委托资金不能被验证人窃取，但如果验证人行为不端，委托人仍需承担责任。发生这种情况时，委托人的股份将根据其相对股份的比例被部分削减。

### 多久会选择一个验证者来提议下一个区块？它会随着 Luna 质押的数量而增加吗？

被选中挖掘下一个区块的验证者被称为**提议者**，或该轮共识中的“领导者”。每个提议者都是确定性选择的，被选中的频率等于验证者的相对总股权(总股权 = 自绑定股权 + 委托人股权)。例如，如果所有验证者的总抵押权益为 100 Luna，而一个验证者的总权益为 10 Luna，则该验证者将有 10% 的时间被选为提议者。

要了解有关 Tendermint BFT 共识中提议者选择过程的更多信息，请阅读更多 [在他们的官方文档中](https://docs.tendermint.com/master/spec/consensus/proposer-selection.html)。

## 激励措施

### 质押的动机是什么？

验证者权益池的每个成员都会获得不同类型的收入:

- **计算费用(gas)**:为了防止垃圾邮件，验证者可以为要包含在其内存池中的交易设置最低gas费用。在每个区块结束时，计算费用按比例分配给参与验证者。

- **稳定费**:为了稳定 Luna 的价值，协议对每笔 Terra 交易收取 0.1% 到 1% 的小额费用，上限为 1 TerraSDR。这是以任何 Terra 货币支付的，并在 TerraSDR 中每个区块结束时根据每个验证者的股份按比例支付。 

该总收入根据每个验证者的权重在验证者的权益池中分配。然后根据每个委托人的股份比例在委托人之间分配收入。请注意，委托人收入的佣金在分配之前由验证人收取。

- **掉期费用**:Luna 和任何 Terra 货币之间的市场掉期交易会收取少量点差，然后用于奖励忠实报告预言机汇率的验证器。不同 Terra 稳定币之间的互换费用称为托宾税。

### 运行验证器的动机是什么？

验证者通过佣金获得的收入比他们的委托人多。他们还在通过 [`Oracle`](../dev/spec-oracle.md) 确定链上汇率方面发挥着重要作用，在那里他们会因忠实地报告汇率和掉期费用而获得奖励。

### 什么是验证人佣金？

验证者池收到的收入在验证者和他们的委托人之间分配。验证者可以根据其委托人的收入部分收取佣金。该佣金设置为百分比。每个验证器都可以自由设置其初始佣金、最大每日佣金变化率和最大佣金。主网强制执行每个验证器设置的参数。这些参数只能在最初宣布候选资格时定义，并且只能在宣布后进一步限制。

### 区块条款是如何分布的？

区块供应相对于他们的总权益按比例分配给每个验证者。这意味着即使每个验证者通过每个条款获得 TerraSDR \(SDT\)，所有验证者仍将保持相等的权重。

 **示例:** 取 10 个具有相同 Staking 权重且佣金率为 1% 的验证器。区块规定为 1000 SDT，每个验证者拥有 20% 的自绑定 Luna。这些代币不会直接交给提议者。相反，它们均匀分布在验证器中。所以现在每个验证者的矿池有 100 个 SDT，根据每个参与者的权益分配:

- 佣金:100 SDT ~ * ~ 80\% ~ * ~ 1\%$ = 0.8 SDT

- 每个验证者获得:100 SDT ~ * ~ 20\% ~ + ~ Commission$ = 20.8 SDT

- 所有委托人获得:100 SDT ~ * ~ 80\% ~ - ~ Commission$ = 79.2 SDT

每个委托人都可以按照其在池中的股份比例要求其部分 79.2 SDT。请注意，验证者的佣金不适用于区块条款。区块奖励(以 SDT 支付)按照相同的机制分配。

### 费用如何分配？

费用以与佣金相同的方式分配给验证器:按每个验证器相对于其总股份的比例分配。如果提议者包括超过最低要求的预提交，则区块提议者也可以获得奖金。

#### 奖励

当验证者被选中提出下一个区块时，他们必须以验证者签名的形式包含至少三分之二的前一个区块的预提交。包含超过三分之二的提议者将获得与额外预提交数量成正比的奖金。如果提议者包含三分之二的预提交，则此奖励范围为 1%，如果提议者包含 100% 的预提交，则奖励范围为 5%。然而，如果提议者等待太久，其他验证者可能会超时并转移到下一个提议者。这就是为什么验证者必须在获得最多签名的等待时间和失去提议下一个区块的风险之间找到平衡。此功能旨在激励非空块提议，验证者之间更好的网络，并减轻审查。 

**示例:** 有 10 个验证者的权益相等。 每个都有 1% 的佣金和 20% 的自保 Luna。 如果一个成功的区块收取 1005 SDT 的费用，并且提议者在他们的区块中包含 100% 的签名，他们将获得 5% 的全额奖金。

我们可以使用一个简单的等式来计算每个验证器的奖励 $R$: 
$$9R ~ + ~ R ~ + ~ 5\%(R) ~ = ~ 1005 ~ \Leftrightarrow ~ R ~ = ~ 1005 ~/ ~10.05 ~ = ~ 100$$

- 对于提出区块的验证者:
  - 矿池获得 $R ~ + ~ 5\%(R)$: 105 SDT
  - 佣金:105 SDT ~ * ~ 80\% ~ * ~ 1\%$ = 0.84 SDT
  - 验证者的奖励:105 SDT ~ * ~ 20\% ~ + ~ Commission$ = 21.84 SDT
  - 委托人的奖励:105 SDT ~ * ~ 80\% ~ - ~ 佣金$ = 83.16 SDT \(每个委托人都可以按照他们的股份比例领取这些奖励的部分\)

- 对于所有其他验证器:
  - 矿池获得 $R$:100 SDT
  - 佣金:100 SDT ~ * ~ 80\% ~ * ~ 1\%$ = 0.8 SDT
  - 验证者奖励:100 SDT ~ * ~ 20\% ~ + ~ Commission$ = 20.8 SDT
  - 委托人的奖励:100 SDT ~ * ~ 80\% ~ - ~ 佣金$ = 79.2 SDT \(每个委托人都可以按照他们的股份比例领取这些奖励的一部分\)

### Luna 供应如何随时间变化？

Luna 是 Terra Proof of Stake 链的原生质押代币。 Luna 代表挖矿能力，并作为 Terra 稳定币的抵押品。当 Terra 稳定币的价格较低时，相关的 Terra 稳定币被烧毁，Luna 被铸造。这增加了 Terra 稳定币的价格。为了限制 Luna 通货膨胀，该协议将所有铸币税和股息掉期费用烧毁给汇率预言机投票获胜者，然后将 Luna 供应返回给目标。 Terra 协议本质上是通货紧缩的。

### 砍单条件是什么？

如果验证者行为不端，他们的抵押股份和委托人的股份将被削减。惩罚的严重程度取决于过错的类型。有3个主要错误可能导致资金大幅削减:

- **双重签名:** 如果有人在链 A 上报告说一个验证者在链 A 和链 B 上签署了两个高度相同的区块，并且如果链 A 和链 B 共享一个共同的祖先，那么这个验证者将被削减在链 A 上。

- **不可用:** 如果验证者的签名未包含在最后的 X 个区块中，则验证者将被削减与 X 成比例的边际数量。如果 X 高于某个限制，则验证者将被取消绑定。

- **Non-voting:** 如果验证者不对提案进行投票，其股份将收到小幅斜线。

:::warning 警告
 即使验证者不是故意行为不端，如果其节点崩溃、失去连接、受到 DDoS 攻击或者其私钥被泄露，它仍然可能被削减。
:::

### 验证者是否需要自我绑定 Luna？

不，但自结合有好处。验证者的总权益由其自绑定权益加上其委托权益组成。这意味着验证者可以通过吸引更多委托人来补偿少量的自绑定 Luna。这就是为什么声誉对验证者非常重要的原因。

虽然验证者不需要自我绑定 Luna，但我们建议所有验证者都拥有“皮肤在游戏中”。这有助于使验证器更值得信赖。

为了让委托人对他们的验证人拥有多少“游戏皮肤”有一定的保证，验证人可以发出最低数量的自绑定 Luna 信号。如果验证者的自我绑定低于其预定义的限制，则该验证者及其所有委托人将解除绑定。 

## 技术要求

### 硬件要求是什么？

我们建议使用以下方法来运行 Terra Core:

- 4 核计算优化 CPU
- 16GB RAM(32GB 用于导出创世)
- 1TB 存储空间(SSD 或更好)
- 至少 100mbps 的网络带宽

### 软件要求是什么？

除了运行 Terra Core 节点之外，验证者还应该开发监控、警报和管理解决方案。

验证者应该期望执行定期软件更新以适应升级和错误修复。网络不可避免地会出现问题，这需要保持警惕。

### 人员要求是什么？

成功的验证器操作需要多个高技能人员的努力和持续的操作关注。运行验证器比挖掘比特币要复杂得多。

运行有效的操作对于避免意外松脱或被切割至关重要。这包括能够响应攻击、中断以及维护数据中心的安全性和隔离性。

### 验证者如何保护自己免受拒绝服务攻击？

当攻击者向验证器的 IP 地址发送大量互联网流量时，就会发生拒绝服务攻击。这可以防止验证者的服务器连接到互联网。

为此，攻击者会扫描网络，尝试了解各种验证器节点的 IP 地址，并通过向它们注入流量来断开它们的连接。

减轻这些风险的一种方法是使用哨兵节点架构仔细构建验证器网络。

验证器节点应该只连接到他们信任的全节点。它们可以由同一个验证器或他们认识的其他验证器运行。验证器节点通常会在数据中心内运行。大多数数据中心提供与主要云提供商的直接链接。验证者可以使用这些链接连接到云中的哨兵节点。这将拒绝服务的负担从验证者的节点直接转移到其哨兵节点。这可能需要启动或激活新的哨兵节点以减轻对现有哨兵节点的攻击。

Sentry 节点可以快速启动或用于更改 IP 地址。由于指向哨兵节点的链接位于私有 IP 空间中，因此基于 Internet 的攻击无法直接干扰它们。这将确保验证者的区块提议和投票总是能够到达网络的其余部分。

有关哨兵节点架构的更多信息，请参阅 [this](https://forum.cosmos.network/t/sentry-node-architecture-overview/454)。 