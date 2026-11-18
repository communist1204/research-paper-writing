# Scientific Language Craft｜严谨、丝滑、可反复推敲的英文

## 总原则

**一级写作质量模块，而非三级微调。** 从文章构思时就把段间语义、句法推进、节奏、关键词、修辞、标题及图注作为核心编辑对象；文字是思想的呈现方式，不能等到完成数学与结构后才随手润色。对重要表达采取“多候选→准确性与读者感受盲比→只保留最佳”的主动精修，兼顾严谨和少量有创造性的概念闪光点。允许善用结构对照、准确的短语、巧妙的前后呼应；拒绝空泛高级词。

让专业读者在不牺牲精确性的情况下，最省力地理解最多的实质信息。成熟学术英文通常**精确 > 凝练 > 自然 > 独特**；独特不意味着罕见词汇。修改顺序先逻辑、再段落、再句法、最后词语，不通过同义替换实现“高级感”。

## 一段一段写，而非一句一句孤立替换

1. **段落任务**：用一句中文或英文陈述本段要推动的认知变化。不能只写“介绍方法”；要写“解释为何固定深度在简单输入上浪费计算，并给出决策机制”。
2. **信息结构**：上一句给出的概念，成为下一句的自然起点（given→new）；用适量指代（`this discrepancy`, `the resulting ratio`）而不是重复全部名词，也不要让 `this` 指代模糊。
3. **主干动词**：优先 `measures`, `constrains`, `decouples`, `aligns`, `reweights`, `bounds`, `estimates`, `recovers` 等只有在语义准确时使用；避免 `leverages`, `significantly enhances`, `facilitates` 等无明确机制的表达。
4. **长度与节奏**：句子长短服务于信息层次；复杂定义可拆分，推导中可以用短句形成清楚的步进。不要全篇整齐的同长句或机械的三句排比。
5. **清楚的限定**：`under ...`, `for ...`, `when ...`, `in the idealized setting` 应紧贴相应主张。不因追求流畅省略关键假设。`suggests`, `is consistent with`, `implies`, `guarantees` 对应不同证据强度。
6. **符号与叙事配合**：定义对象，再写关系，再解释结论；所有符号首次出现可定位。避免为了文字优雅改变变量指向或运算含义。
7. **交叉段呼应**：核心术语尽量固定（同一个物理/数学对象不在相邻段用三个名字）。重要对照基于真实比较轴，做到呼应而不是口号式反复。

## 逐句编辑的七问

- 主句要表达什么新事实？删去这句，读者失去什么？
- 句首是否接得住前一句，句尾是否放在下一句最需接住的信息上？
- 主语、动词是否揭示真实作用，是否有悬空代词或多余名词化？
- 技术名词、数学量词、时态和证据强度是否精确？
- 能否删去一句自夸、两处重复形容词或模糊连接词而不丢信息？
- 有没有一个更简洁、自然、属于该研究领域的表达，而不是生硬的“高端词”？
- 如果改写后没有可说明的改善，是否应该恢复原句？

## 正向写作示范：完全相同的技术内容

**技术事实固定**：一个 12-block 图像分类器，在第 4/8 block 设置两个出口；在中间头比较前两类概率之差，高于阈值就退出，否则继续；两个中间头使用标签 CE 和最终头的蒸馏；评价准确率和平均计算量。以下没有实验结果、理论或机制保证。

普通但合格：

> To reduce inference cost, we develop an adaptive early-exit framework for a twelve-block image classifier. Specifically, auxiliary heads are attached after the fourth and eighth blocks. The prediction margin between the top two class probabilities is compared with a threshold. If it exceeds the threshold, the model exits; otherwise, inference continues. The heads are trained with cross-entropy and distillation from the final head. We evaluate accuracy and average computation under different thresholds.

经过结构与语言编辑：

> A twelve-block classifier spends the same amount of computation on every input, even when its intermediate predictions are already decisive. We therefore place exit points after the fourth and eighth blocks. At each point, the gap between the two highest class probabilities determines whether to return the intermediate prediction or continue to deeper layers. We train these heads using ground-truth labels and distillation from the final classifier, then vary the exit threshold to measure the resulting accuracy–computation trade-off.

为何更好：第二句直接回应第一句的计算分配问题；`At each point` 沿用 exit points；训练与评估被压缩为一条自然的验证链；未虚构“准确率不下降”或“保证正确”。但若原稿已有更好的技术动机与语言，保留原稿。

## 优美不是复杂

不要：连续五句 `Furthermore/Moreover/Additionally`; 每段 `Not only X but also Y`; 用 `paradigm-shifting`, `remarkably`, `unprecedented` 增加气势；用 `we elegantly` 自夸；每段尾部补一句空洞“this highlights effectiveness”。可以偶尔使用真正有信息的对照和有条件的反问，但整篇一般应以陈述和推理为主。

## 校对与风格匹配

检查术语/时态/单复数/冠词、平行引用、图表指代、方法简称、符号和量纲；优先参照用户原稿中质量较高的相邻段落与目标会议体例。完成后以“脱离稿件的新读者”身份重新阅读，检查是否不需要回读即可理解每步；再对照原文确认所有有效主张都未丢失。
