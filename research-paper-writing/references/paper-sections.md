# 各章模板

先为每项贡献填写主张与证据表，再按 [发布会原则](presentation-principles.md) 选定主线。以下英文用于搭建论证结构。按 [Humanizer](humanizer/upstream-skill.md) 将骨架写成自然的正文，方括号中的内容须替换为稿件事实或用草稿标记注明缺失。

| 章节 | 组织顺序 | 可复用英文骨架与完成条件 |
|---|---|---|
| Title | 任务或现象 + 关键新机制 | “[Mechanism] for [specific task] under [scope]”。标题中的性质必须在文中成立。 |
| Abstract | 问题 → 现有缺口 → 洞察 → 方法 → 证据与范围 | “In [setting], [failure] arises when [condition]. We propose [mechanism], which [operation tied to the gap]. Under [assumptions], we establish [bounded result]. On [benchmark and protocol], [observed result against comparator].” 无理论或无结果时删去相应句子。 |
| Introduction | 具体障碍 → 最近方案的限制 → 可检验的关键洞察 → 方法与核心贡献 → 证据预告 | “The central difficulty is [measurable mismatch]. Existing [specific methods] address [aspect], leaving [verified gap] under [condition]. Our key observation is [supported relation]. This motivates [design].” 将贡献分别锚定到式、定理或表，区分主贡献与实现。 |
| Related Work | 以问题和机制分组 → 明确最接近方法 → 在同一坐标系中对照 | “Both [ours] and [prior work] use [shared component]. [Prior work] assumes [X], whereas our formulation [verified delta], enabling [bounded consequence].” 核实引用原文。空白检索不能支持首创声明。 |
| Preliminaries / Problem | 对象、符号、数据或反馈来源 → 目标、比较类和约束 → 失败判据 | “Let [symbol] denote [object and domain]. Given [inputs], we seek [output] minimizing [risk] subject to [constraint]. We measure failure by [observable criterion].” |
| Method | 失效机制 → 定义及必要假设 → 推导 → 目标 → 算法与实现差异 | “To test whether [mechanism] explains [failure], we first define [quantity]. Under [assumptions], [relation] yields [design]. Algorithm [id] implements this objective using [approximation], whose effect is evaluated in [experiment].” |
| Theory | 主张与假设 → 结论 → 证明要点与原文定位 → 适用范围 | “Proposition [id]. Under [explicit conditions], [quantified conclusion]. The proof uses [key argument]. The conclusion concerns [object/scope].” |
| Experiments / Results | 问题对应实验 → 协议 → 主要对照 → 实际结果及不确定性 → 失败或限制 | “We test [claim] by varying [intervention] while holding [controls] fixed. Compared with [matched baseline], [observed result and uncertainty].” 检查预算、调参、数据划分、指标方向与重复次数。 |
| Ablations | 设计预测 → 单因素移除或替换 → 指标 → 结果允许的解释 | “If [mechanism] drives [effect], replacing [factor] with [simpler alternative] should change [direct metric] under [conditions].” 区分结果汇报和待做实验。 |
| Limitations / Ethics | 条件、边界、失败实例 → 可能的影响 → 已验证的缓解措施或验证计划 | “The analysis assumes [A]. When [A] fails, [observed or plausible failure with label]. We evaluate [scope] and leave [specific unresolved setting] open.” |
| Conclusion | 回答研究问题 → 最强贡献及证据范围 | “We formulated [problem] as [representation] and showed [supported result] under [conditions].” 在局限节交代影响结论的重要未解决问题。 |
| Appendix / Reproducibility | 完整证明 → 假设表 → 伪代码 → 配置和数据细节 → 附加实验 | 写明版本、随机种子、数据划分、算力、调参预算、运行或复现入口、报告统计量和未验证项。正文要保留决定结论范围的条件。 |
| Rebuttal | 复述争议 → 证据与位置 → 可核实的修订 → 剩余范围 | “We agree that [specific ambiguity] warrants clarification. [Evidence] in [location] establishes [bounded claim]. We revised [location] to state [actual edit].” |

## 可直接填写

```text
核心研究问题：
一句话贡献（相对哪个最近方法，改了什么，在何种范围内）：
主张编号｜位置｜类型（已证明/已测/假设）｜证据｜反例或局限｜尚缺验证
段落编号｜一句话主张｜支持句与证据｜承接下一段的理由
```

审稿意见附在稿件之外。交付正文前检查摘要、引言、图表、方法、附录和结论中的范围及数字是否一致。保留公式编号、引用键和其他段落的依赖。
