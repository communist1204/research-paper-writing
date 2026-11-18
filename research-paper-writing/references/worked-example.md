# 完整示范｜流匹配监督中的噪声分层

这是合成练习，不代表任何真实稿件或 DiffusionNFT 的方法与实验。下文用经典的逆方差加权演示如何把观察到的现象写成可验证的研究假设、分析和实验，并给出经过修改的英文段落。

## 1. Research Formulation｜把现象改写成机制问题

**起点。** 假设在流匹配训练的某个位置，同一状态的速度标签来自两个可辨别的来源。第二个来源的标签更分散。先问两组的条件均值是否一致、分散是否来自条件方差，以及这种差异是否使有限样本下的速度估计更不稳定。工程上的第一反应可能是添加门控模块。这个示范先检验现有的标签信息能否解释并减少估计误差。

**问题与范围。** 固定训练状态和时间 $z=(x,t)$，只看一个速度分量。令 $Y_{gi}$ 为来自来源 $g\in\{1,2\}$ 的第 $i$ 个速度标签。固定每组样本数 $m_g\ge2$。在此状态下假设所有标签相互独立，且每组具有共同目标均值 $\mu(z)$ 和组内方差 $v_g(z)\in(0,\infty)$。在合成设置中，$\mu(z)$ 也是预先指定的干净目标。实际应用中，来源之间均值相等、共同均值等于干净目标、标签独立是三项各自需要依据的条件。重复样本共享轨迹或随机种子时，独立性就可能失败。

**可证伪机制。** 如果共享目标均值的前提成立，组均值的精度差异会改变合并估计的方差。基线用样本数合并标签。候选方案按组均值的精度合并。若均值不同，加权可能改变估计所指向的目标，误差甚至可能增加。研究结论限于一个固定状态下的标量估计。生成指标、训练稳定性和端到端收敛需要各自的分析与证据。

## 2. Mathematical Reasoning｜逐步验证设计从哪里来

记 $\bar Y_g=m_g^{-1}\sum_{i=1}^{m_g}Y_{gi}$，且 $a_g=\operatorname{Var}(\bar Y_g)=v_g/m_g$。这一等式使用了同组独立性和同方差。考虑确定性线性估计器 $\hat\mu_w=\sum_g w_g\bar Y_g$。对任意共享均值 $\mu$ 保持无偏，须有 $\sum_g w_g=1$。组间独立性给出 $\operatorname{MSE}(\hat\mu_w)=\operatorname{Var}(\hat\mu_w)=\sum_g a_gw_g^2$。

**命题。** 在上述条件下，已知 $a_g$ 时，在所有满足 $\sum_g w_g=1$ 的确定性线性估计器中，最小 MSE 由下式取得。

$$
w_g^*=\frac{a_g^{-1}}{\sum_h a_h^{-1}}=\frac{m_g/v_g}{\sum_h m_h/v_h},
\qquad
\operatorname{MSE}(\hat\mu_{w^*})=\left(\sum_h a_h^{-1}\right)^{-1}.
$$

**证明。** 柯西–施瓦茨不等式给出 $(\sum_g w_g)^2\le (\sum_g a_gw_g^2)(\sum_g a_g^{-1})$。左侧为 1，因此右侧给出 MSE 的下界。等号成立当且仅当 $(\sqrt{a_g}w_g)_g$ 与 $(1/\sqrt{a_g})_g$ 成比例。归一化即得 $w^*$。方差严格为正，因此最优解唯一且权重均为正。证毕。

**独立核对。** 等组样本数 $m_1=m_2=m$、方差 $v_1=1,v_2=9$ 时，简单合并权重为 $(0.5,0.5)$，MSE 为 $2.5/m$。已知方差时，最优权重为 $(0.9,0.1)$，MSE 为 $0.9/m$。若 $v_1=v_2$，最优权重退化为按样本数合并。若第一组均值变成 $\mu+\delta$，第二组仍以 $\mu$ 为均值，且方差和独立性保持，则 $\hat\mu_w$ 对干净目标的偏差是 $w_1\delta$。等样本数、方差比为 9 时，最优无偏权重在这组失配条件下相对简单合并的 MSE 差变为 $0.56\delta^2-1.6/m$。取 $m=32,\delta=0.5$，差为 $0.09$，加权的 MSE 更高。这里的“最优”只指共享均值条件下的估计器类别。

**从目标到实现。** 计算 $\bar Y_g$，再按 $m_g/v_g$ 归一化汇总。等价地，求解关于标量 $u$ 的二次目标 $\min_u\sum_g\sum_i(Y_{gi}-u)^2/v_g$。对 $u$ 求导并令其为零即可得到相同的组均值权重。实践候选方案使用独立先导样本估计组方差，对估计值设 $10^{-8}$ 的下限，再计算权重。独立先导样本使估计器在共享均值条件下给定先导数据仍无偏。估计方差带来的权重波动需要单独评估。命题只为使用真实方差的方案保证最优性。

| 引入项 | 解决的问题 | 假设与推导检查 | 对贡献的作用 | 更简单的替代 | 可证伪检查 |
|---|---|---|---|---|---|
| 共享均值、组内方差与 $a_g=v_g/m_g$ | 区分标签偏差与估计波动 | 有限正方差、固定样本数、独立标签。实际数据还要核查共享均值是否为干净目标 | 定义机制可以成立的条件 | 直接报告两组均值和方差 | 有干净目标时分别量化两组均值偏移，并检查轨迹内相关性 |
| MSE 目标与最优权重命题 | 确定不同来源的合并系数 | 确定性线性无偏类、组间独立、方差已知。用不等式及等号条件核对 | 把估计误差的机制与设计接起来。这里没有主张理论新颖性 | 按样本数合并 | 等方差退化检查、异方差下 MSE 数值核对、均值失配反例 |
| 加权二次目标 | 把组权重落成标签级目标 | 对固定状态的标量 $u$ 验证一阶条件，二阶导严格为正 | 建立目标与估计器的精确对应 | 直接计算加权组均值 | 对同一数据比较二者输出，误差应在预设数值容差内 |
| 独立先导估计与方差下限 | 在方差未知时给出可运行设计 | 先导与估计样本独立，正则化下限只定义实现行为。无偏由条件期望得到 | 区分可分析机制与实际性能 | 直接使用按样本数合并 | 扫描先导规模，固定总标签预算复测，报告何时收益消失 |

## 3. Scientific Writing｜先锁定证据，再写英文

本例的贡献句只写“分离条件均值与条件方差，并给出一个有限样本设计及其失效条件”。若移植到真实稿件，需要另列最近相关工作，确定真正新增的是机制识别、领域验证、算法或理论。表里已核对的解析值可以写进方法或分析。未运行的指标留在实验计划中。

**需修订的段落。** “We introduce a novel filter that suppresses noisy velocities, ensuring stable flow training and a more accurate generative model.”

**可使用的英文正文。** “At a fixed flow-matching state and time, velocity labels from different sources can have unequal variances even when they share the same conditional mean. Under independent sampling, the sampling variance of each source mean is the label variance divided by the source's sample count. When these variances are known, inverse-variance weighting minimizes mean squared error among linear unbiased combinations of the source means. If the sources instead have different conditional means, the same weights can shift the estimate away from the clean target. We use this distinction to motivate separate tests for variance reduction and sensitivity to source-dependent bias.”

## 4. Reviewer Simulation｜逐段审核与放行

采用 [逐段与整稿审查](review-protocol.md) 中的统一量表和门槛。本例在同一示范内分开模拟角色，分数用于定位问题。

| 审核视角 | 初稿风险 | 修改后核查 |
|---|---|---|
| 作者自审 | 数学 1，证据 0，清晰度 2。“ensuring” 把局部设计升级成了端到端保证，没有依据 | 数学 4，事实忠实性 4，清晰度 4。逐句对应共享均值、独立性、估计器类和失配反例。末句只给出计划 |
| 领域审稿人视角 | 新颖性 0，理论严密性 1，证据 0。逆方差加权是否已知，何时会选中有偏来源，端到端稳定性的证据在哪里？ | 理论严密性 4，证据 4，清晰度 4。范围已缩到局部的已知方差结论，并给出可计算的失效条件。这段用于方法动机，未提出新颖性主张。全文新颖性仍待相关工作对照 |
| AI 辅助审稿视角 | 清晰度 2，事实忠实性 0，可复现性 1。若只提取主张句，容易把“stable flow training”读成已验证事实，且找不到算法计算方式 | 清晰度 4，数学 4，事实忠实性 4，可复现性 3。抽取到固定状态、已知方差、线性无偏估计与均值失配。计算式在相邻方法段，实验设置由下节提供 |

把审稿与修订分两轮执行。审稿轮只给审稿者论文段落、相邻公式、计划和判分标准，由其先独立列出主张及证据位置。修订轮再提供作者意图和审稿意见。可调用另一个模型时，将审稿提示交给独立的模型或新上下文。只有一个模型时，分别记录作者轮和隔离上下文的模拟轮，并说明独立性的实际程度。

修改后逐段放行记录。分数检查对象是修订后的方法动机段落和相邻公式。

| 视角 | 新颖性 | 数学与技术严密性 | 证据与事实忠实度 | 清晰度 | 可复现性 | 相关工作 | 实验设计 |
|---|---|---|---|---|---|---|---|
| 作者自审 | N/A | 4 | 4 | 4 | 3 | N/A | N/A |
| 领域审稿 | N/A | 4 | 4 | 4 | 3 | N/A | N/A |
| AI 辅助审稿 | N/A | 4 | 4 | 4 | 3 | N/A | N/A |

修订段仅说明局部方法动机，未作新颖性或相关工作比较，也未描述实验协议，三项转交相应章节。可复现性 3 指能根据相邻公式重建局部估计器，完整训练和实验的复现仍待整稿检查。段落通过只覆盖局部数学与表达。

## 5. 验证、消融与失败后的回路

用一个固定状态和 $\mu=0$。两组每次独立抽样，用正态分布生成标签，每组 $m=32$。每组场景运行 10,000 次重复，使用固定的公开种子（如 20261108），把同一次抽样同时交给各方法。比较简单合并、已知方差加权和独立先导估方差加权。先导方案每组另外抽 $k\in\{4,16,64\}$ 个标签，用 `ddof=1` 估方差。报告偏差、方差、对干净目标的 MSE，以及各方法配对平方误差之差的 95% 蒙特卡洛区间。区间反映模拟误差。另做一次固定总预算对照，让简单合并也使用 $m+k$ 个样本每组，先导加权仍把 $k$ 个样本仅用于估方差。

| 场景 | 预先写下的预测 | 读数不符时的检查 |
|---|---|---|
| 共享均值，$v=(1,9)$ | 已知方差加权和简单合并的理论 MSE 分别为 $0.9/32$ 和 $2.5/32$ | 核查模拟标准差是否用了 $\sqrt{v}$、权重是否正确归一化、配对是否共用数据 |
| 共享均值，$v=(1,1)$ | 已知方差加权与简单合并逐次相同。先导权重波动可能使 MSE 增加 | 检查退化行为。若先导方案声称稳定优于基线，排查预算、数据复用与估计误差 |
| $v=(1,9)$，低方差组均值偏移 $\delta=0.5$ | 已知方差加权相对简单合并的 MSE 差为 $0.09$ | 核对偏移加在哪组、评估目标是否仍为干净的 $\mu$。如果真实数据类似，先识别或估计偏差，再决定是否加权 |
| 从已知方差改为估计方差，并配平总标签数 | 量化估计权重带来的成本。收益大小由数据决定 | 若效果只在额外标签预算下出现，收窄实际性能主张。若估计方差不稳定，先保留简单合并基线 |

以下脚本可直接生成合成检查数据。将这段代码存为单独的 Python 文件后运行。它需要 NumPy。

```python
import numpy as np

rng = np.random.default_rng(20261108)
n_replicates, m = 10_000, 32


def summarize(name, estimate, reference):
    # The clean target is zero, so squared predictions equal squared errors.
    squared_error_difference = estimate**2 - reference**2
    difference = squared_error_difference.mean()
    margin = 1.96 * squared_error_difference.std(ddof=1) / np.sqrt(n_replicates)
    print(
        f"{name}: bias={estimate.mean():.5f}, "
        f"variance={estimate.var(ddof=1):.5f}, MSE={(estimate**2).mean():.5f}, "
        f"paired MSE difference={difference:.5f} "
        f"[{difference - margin:.5f}, {difference + margin:.5f}]"
    )


scenarios = [
    ("shared mean, unequal variance", (0.0, 0.0), (1.0, 9.0)),
    ("shared mean, equal variance", (0.0, 0.0), (1.0, 1.0)),
    ("biased low-variance source", (0.5, 0.0), (1.0, 9.0)),
]

for scenario, means, variances in scenarios:
    print(f"\n{scenario}")
    location = np.array(means)[None, :, None]
    scale = np.sqrt(variances)[None, :, None]
    labels = rng.normal(location, scale, size=(n_replicates, 2, m))
    pilot_labels = rng.normal(location, scale, size=(n_replicates, 2, 64))
    source_means = labels.mean(axis=2)
    pooled = source_means.mean(axis=1)
    oracle_precision = m / np.array(variances)
    oracle = source_means @ (oracle_precision / oracle_precision.sum())
    summarize("pooled", pooled, pooled)
    summarize("known variance vs pooled", oracle, pooled)
    for k in (4, 16, 64):
        pilot = pilot_labels[:, :, :k]
        estimated_variances = np.maximum(pilot.var(axis=2, ddof=1), 1e-8)
        precision = m / estimated_variances
        estimate = (precision * source_means).sum(axis=1) / precision.sum(axis=1)
        pooled_equal_budget = (labels.sum(axis=(1, 2)) + pilot.sum(axis=(1, 2))) / (
            2 * (m + k)
        )
        summarize(f"estimated variance, k={k}, vs pooled", estimate, pooled)
        summarize(
            f"estimated variance, k={k}, vs pooled at equal budget",
            estimate,
            pooled_equal_budget,
        )
```

**一次复核。** 用 NumPy 2.2.6 运行上述脚本，共享均值且方差不等时，已知方差加权与简单合并的 MSE 分别约为 0.02782 和 0.07821，对应理论值 0.028125 和 0.078125。低方差组有偏时，MSE 差约为 0.08809，模拟区间 [0.08482, 0.09135] 包含理论值 0.09。共享均值且方差不等时，先导样本取每组 64 个，按同等总标签数比较反而增加约 0.00187 的 MSE。这支持在真实方案评估前就保留标签预算对照，并缩小任何关于先导估计普遍有效的主张。

**模拟投稿判断。** 该方法段落可作为局部机制说明。整稿当前应标为“待证据”。以上合成检查只对应局部分析。真实任务结果、相关工作比较与实际贡献均未建立。下一轮先提交真实任务复现表和相关工作矩阵，再由审稿轮检查新增证据是否支撑方法范围与贡献措辞。用户完成练习并要求记录时，可将“出现分组效果差异时，先区分偏差与方差”连同实际完成的推导或反例，交给「科研学习与积累」处理。
