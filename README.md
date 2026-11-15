# ClearMind

ClearMind 是一个面向中文交流的 Agent Skill，帮助用户澄清需求、获得有依据且直接的回答，并改善中文表达。当前版本为 **0.7**。

## 设计思路

用户有时知道自己想得到什么，却难以准确描述；模型也可能过早按自己的理解行动，或者不断追问、迟迟不完成任务。ClearMind 把需求理解、分析判断和中文表达放在同一次协作中处理，以任务实际需要决定澄清和分析的深度。

- **意图理解与确认**：判断目标是否清楚；必要时结合使用场景探索交付物背后的目的。不同方向可能带来明显差异时说明判断和取舍；改变已确认的目标或实质扩大范围前，先获得用户同意。
- **去防御性回答**：减少空泛免责声明、假对比和机械迎合；保留影响事实、适用范围及决策的限定。复杂任务按需使用原始材料、专业方法和可核验标准。
- **中文表达优化**：以信息准确、逻辑连贯、表达自然和格式适配为顺序处理文字，保留事实、引用、术语、原意与论证强度。

这些规则的目标是提升任务质量和协作效率。简单、明确的请求可以直接完成；专业分析与跨领域方法只在对任务有实质收益时使用。

## 特点

- **智能确认**：目标清晰时直接做；部分模糊且试错成本低时可以先给诊断或小样；关键歧义会显著影响结果时再确认。
- **严格确认**：说“严格确认”或“每次都先问我”，新任务先说明理解并等待肯定；说“智能确认”或“自主执行”切回默认。一次性要求只影响当前任务；确认后的同一任务不重复确认已决定的方向。
- **从交付物回到使用行为**：对“做一个知识库”等不够明确的请求，结合上下文询问谁在什么场景需要完成什么事；用具体例子帮助表达，同时允许用户否定选项。
- **深入而不擅自扩范围**：区分已有直接应用、可迁移的方法和待验证的组合设想；不把猜测写成事实，不为显示专业性堆砌术语。
- **保留必要边界**：比例变化不自动等于数量变化；未经验证的建议不写成已经证实的效果；局部润色不擅自变成全文重写。

## 使用方法

将仓库里的 `clearmind` 文件夹整体放入所使用工具的 Skill 目录，保留 `SKILL.md`、`references/` 和 `evals/` 的相对结构。具体安装与发现方式取决于宿主工具。也可以在对话中明确要求使用 ClearMind。

```text
clearmind/
├── SKILL.md
├── references/
│   ├── intent-clarification.md
│   ├── anti-defensive.md
│   └── chinese-writing.md
└── evals/
    └── evals.md
```

## 适用示例

- “把这句话里的重复字去掉”：直接修改，不为简单任务增加目标分析。
- “我想做一个知识库，但不知道做成什么样”：从具体使用场景入手，帮助用户明确检索、关联或其他实际需求。
- “这项政策实施后指标上升，所以一定有效”：检查数据口径、其他解释、可比证据与验证方法，而非仅附和结论。

## 思路来源与致谢

ClearMind 在设计中参考和改编了以下材料。各来源有各自适用范围和许可；这里说明的是具体借鉴关系，不表示获得原作者背书。

- [OpenAI 模型使用指南](https://developers.openai.com/zh-Hans/api/docs/guides/latest-model)：参考其中有关明确表达、适当澄清、主动推进和避免冗余措辞的建议。
- [obra/superpowers — brainstorming](https://github.com/obra/superpowers/blob/main/skills/brainstorming/SKILL.md)：借鉴通过提问探索需求、明确设计方向的思路。ClearMind 结合普通任务增加了直接执行和智能确认机制。
- [Kiterlin/anti-defensive-writing](https://github.com/Kiterlin/anti-defensive-writing)：借鉴识别防御性措辞、保留必要限定并改善表达的思路。
- [Weijinchen/humanizer-zh](https://github.com/Weijinchen/humanizer-zh)：参考中文写作中识别模板化、冗余和不自然表达的思路，并将使用范围扩展到日常对话。
- [Felix Rieseberg — How to Be More Ambitious](https://felixrieseberg.com/how-to-be-more-ambitious-a-tutorial-for-humans-with-models/)：参考文章中的目标高度、专业分析深度和方法广度，并结合 ClearMind 增加授权范围与任务复杂度的约束。

## 评测与局限

`clearmind/evals/evals.md` 提供人工评测样例，覆盖意图识别、确认效率、防御性控制、中文质量和任务完成度。开发过程中进行过隔离会话对照、多轮确认测试，以及基于 [Our World in Data 数据](https://ourworldindata.org/grapher/share-of-final-energy-consumption-from-renewable-sources)的文件读取和计算检查。这些测试样本有限；部分评审由模型完成，不能证明所有模型和任务中都有稳定提升。实际行为也取决于宿主工具的规则优先级、可用数据和工具权限。
