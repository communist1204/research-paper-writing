# venue-与稿件类型自适应规则

## 先读当前目标 venue 的最新 author guide

以下仅作为本轮检索的结构指南，不代替当前投稿规则；决定篇幅、引言是否命名、是否允许/建议独立方法章、是否需贡献类型、补充材料和声明时必须查当年官方页面。

### ICLR / NeurIPS：较强调论点、可审计的贡献与数学/实验
- 适合论文类型：理论、机制分析、目标函数、优化、训练、算法等；常用 Problem/Preliminaries → Analysis/Method → Experiments，但具体顺序依实际研究。
- 引言简述问题及**可复述的核心发现**；理论工作可提前给非技术性的定理意义，正文显示关键条件和结果，附录完整证明。
- 会议准则强调摘要/引言主张与证据一致，不提供“越华丽越高分”的捷径；不得将局部代数式包装成端到端性质。
- 原始规则：https://neurips.cc/public/guides/PaperChecklist ; https://iclr.cc/Conferences/2026/AuthorGuide

### CVPR：视觉动机、图形/输入输出、关键机制与可复现系统
- 概览图/首图常能承担“输入→输出→关键统一接口/范式对比”职责；叙事与视觉证据相配合。
- 对于架构模型，Method 可以先是 I/O interface 与框架，再给各支路/损失；不要硬造数学定理。问题与最近工作的差异在 introduction/related work 读得清楚。
- 参考：https://cvpr.thecvf.com/Conferences/2026/ReviewerTrainingMaterial ; https://cvpr.thecvf.com/Conferences/2025/BestPapersDemos

### Nature Machine Intelligence（Article）/ Nature Portfolio 期刊
- 文章服务跨领域科研读者，更强调概念可理解、学术语境和研究含义；不能把会议模板生搬硬套。Nature MI 官方当前 Article：摘要不超过150词；Introduction（不使用该标题）、Results、Discussion、Methods，结果和方法有主题性副标题；按投稿规范组织，别硬添加 Related Work 章。
- 方法可列在结果/讨论之后，仍须提供解释和复现必要的信息。研究背景与相关工作可自然融入前文；Discussion 比会议式 Conclusion 更承担解释结果意义与限制的作用。
- 参考：https://www.nature.com/natmachintell/content ; https://www.nature.com/natmachintell/submission-guidelines/writing-and-language

### TPAMI / IJCV / TIP / Information Fusion 等专业期刊
- 不能泛化成 Nature 结构；先看目标期刊 guide、篇幅、章节习惯、related-work 和独立 analysis 的需要，按具体规范写。专业期刊可容纳更详细的技术论证、实验范围与讨论，但更长并不等于允许冗余。
- 对期刊稿与会议稿融合，先锁定一份叙事母版，保持逻辑/章节保护；另一版仅作为理论、附录或验证依据。按照用户范围进行局部迁移。

## 类型驱动而非 venue 冒名驱动

- 数学理论贡献→主定理和假设组织全文。
- 机制诊断贡献→现象、解释、控制实验的因果链。
- 系统/模型贡献→统一接口、关键设计、实现与比较。
- 数据集/benchmark→任务缺口、构建原则、覆盖范围与评测协议。
- 混合型→一个主轴，其他作为支撑，防止每部分像独立小论文。

用最接近论文类型 + 目标 venue + 作者原文三重信号选择风格。用户对既有章节明确满意时，原版优先，不能为了“顶会范本”强制改章节次序。不要承诺写作满分或高录用率。
