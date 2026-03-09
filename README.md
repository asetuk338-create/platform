# AI agent接入平台之后

成员：秘琳、陈嘉怡、郭淑仪、郭亦佳

## 一、项目背景：消费决策范式的三次转移 (Motivation)

消费范式演进对比

| 范式阶段           | 核心逻辑   | 决策主体               | 搜索成本与时间价值                     | 典型应用场景                     |
|--------------------|------------|------------------------|----------------------------------------|----------------------------------|
| 范式一：传统电商    | 人找货     | 消费者自主决策         | 搜索成本高，以时间换价格               | 淘宝/京东网页版比价              |
| 范式二：即时零售    | 货追人     | 平台LBS匹配+消费者选择 | 搜索成本中，以金钱换时间               | 美团闪购、同城急送               |
| 范式三：AI代理消费  | AI代决策   | AI预测+消费者确认      | 搜索成本趋零，时间被折叠               | AI购物助手、智能托管推荐         |

## 二、文献支撑

**1、[AER 2024 Data, Competition, and Digital Platforms](./data,competition,platform_notes.md)**

A monopolist platform uses data to match heterogeneous consumers with multiproduct sellers. The consumers can purchase the products on the platform or search off the platform. The platform sells targeted ads to sellers that recommend their products to consumers and reveals information to consumers about their match values. The revenue-optimal mechanism is a managed advertising campaign that matches products and preferences efficiently. In equilibrium, sellers offer higher qualities at lower unit prices on than off platform. The platform exploits its information advantage to increase its bargaining power vis-à-vis the sellers. Finally, privacy-respecting data-governance rules can lead to welfare gains for consumers. (JEL D11, D42, D44, D82, D83, M37)

## 三、我们的想法

### 1、 2 parallel channel

On-platform (AI 代理渠道，如接入大模型的超级App)：消费者的搜索成本极低（$s=0$），AI 具有绝对的“产品导流权（Steering）”，以及只推荐最优解。

Off-platform (传统搜索渠道，如传统货架电商)：消费者的搜索成本为正（$s=c>0$，需要花费时间比价），但该渠道是一个开放竞争的货架，商家面临充分竞争。

### 2、 4 players

1、AIagent platform : steering能力很强

2、traditional platform ：作为outside option

3、Multi-homing Merchants ：多栖商家，同时在ai-empowered platform和traditional platform备货，追求总利润最大化。面对抽成会选择差异化价格歧视，把数字地租转嫁给消费者

4、consumers：追求个人consumer surplus最大化，具有异质性时间价值

### 3、 决策变量

对于 AI 平台：最优的抽成比例/佣金率。

对于多栖商家：在 AI 渠道的定价以及在传统渠道的定价。

对于消费者：渠道选择策略（选择 AI 代理、选择传统搜索、或退出市场）。

### 4、 模型构建

第一阶段（纳什谈判与分润博弈）：AI 平台与商家就佣金率进行谈判。商家的谈判底气（威胁点/外部选择）取决于其在传统平台能获得多少利润。AI 越是垄断消费者，商家的外部选择越小，AI 获得的实际议价权就越高。

第二阶段（歧视性定价博弈）：商家根据第一阶段确定的抽成比例，决定2 parallel channel的价格。此时会出现类似ai tax的东西，即 $P_{AI} > P_{Trad}$。

第三阶段（消费者自选择博弈）：消费者观察到（或理性预期到）两个渠道的价格差。时间价值高的消费者愿意支付“AI 溢价”留在 AI 渠道；时间价值低的消费者则切出 AI，前往传统渠道承担搜索成本 $c$ 以获取低价。

### 5、 求解方法：逆向求解+数值模拟

## 四、 备选

我们认为，ai agent相当于一个信息漏斗，会集中分散信息。基于ai agent的这种特性，我们可以试图讨论：

### 1、长尾效应是否仍然成立？

传统电商通过降低搜索成本，造成“长尾理论（The Long Tail）”（Brynjolfsson et al., 2011），使得海量小众商品得以曝光。然而，AI Agent 虽然进一步将消费者的物理搜索成本降至零，但受限于对话框的交互形式，其推荐结果呈现同质化、收敛性（往往只给出 Top 1 或 Top 3 的极少数解）。当 AI 算法掌握steering的权力时，市场销量分布是否会反转变成赢者通吃呢？

### 2、AI平台会不会造成一种“双轨制”的市场结构？

AI 平台的“高导流效率 + 高抽成要求”天然具有筛选机制。异质性平台（AI平台 vs 传统货架平台）的存在，将如何导致商家的选择策略？会不会出现一种情况是：高利润率、高品牌溢价的头部商家可能独占 AI 代理渠道（On-platform）；而对价格敏感、利润微薄的中小商家将被挤出进入off-platform市场。
