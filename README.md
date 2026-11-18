# 科研论文写作

面向高水平学术论文的科研写作 Skill，当前版本 **0.4.3**。支持主动理论支撑、全文与章节叙事设计、逐句逐词英文精修、概念提炼、LaTeX 核查、审稿与 rebuttal。

以真实贡献和可核实证据为基础，按需研究优质论文的表达方式；已有文本默认保真精修，结构重写和理论融合遵循读者指定的编辑范围。审校包含图表与子图对应关系、实验事实和论证依据的核查。

## 使用

将完整的 [`research-paper-writing` 目录](research-paper-writing/) 添加到支持 `SKILL.md` 的环境，在会话中调用 `$research-paper-writing`，并提供稿件、目标章节与编辑要求。需要资料库或文献检索时，应由使用者指定可访问的材料与范围；持久读写和检索能力取决于实际运行环境。

例如：

> 请用科研论文写作 skill 精修这段 Introduction，保留技术主张与引用，只改进叙事衔接和英文表达。

## 配套与来源

论文和书籍带读可使用 [`research-learning`](https://github.com/communist1204/research-learning)。本 Skill 聚焦作者自己的写作、修改与审校。

附带的 Humanizer 参考规则保留于 [`references/humanizer`](research-paper-writing/references/humanizer/)，其第三方 [MIT 许可与版权](research-paper-writing/references/humanizer/LICENSE) 保持不变。示例和方法指南不构成对论文录用或写作评分的保证。
