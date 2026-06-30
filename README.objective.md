<div align="center">

![objectivize](assets/hero.png)

# objectivize

**把带主观立场与内部口吻的草稿，改写成可对外发布的客观第三方分析。**

*A Claude Code / Agent Skill that rewrites subjective, fourth-wall-breaking drafts into publishable, neutral third-party analysis.*

[![Built for Claude Code](https://img.shields.io/badge/built_for-Claude_Code-4f46e5)](https://docs.anthropic.com/en/docs/claude-code)
[![License](https://img.shields.io/github/license/TsekaLuk/objectivize?color=18181b)](LICENSE)

</div>

---

## 功能

内部文稿常带有圈内口吻——指名道姓的内部角色、第二人称喊话、把臆测当事实、自指生产过程——直接对外发布会显得像内部备忘录。`objectivize` 将其改写为中性的第三方分析：移除立场与内心戏，保留判断与证据。

## 设计原则（非固定流程）

改写的形状由文稿本身决定，方法论不被固化：

1. **先感知** —— 先识别该文稿特有的主观泄漏，再对症处理；不同文稿重新识别。
2. **改写而非删除** —— 替换框架而非丢弃内容（如"某方的真实意图"→"项目意图"：立场移除、信息保留）。
3. **统一称谓** —— 为每个内部角色定一个中性称谓并全篇一致。
4. **客观不等于虚假自信** —— 保留置信度、局限、存疑等标注。
5. **规模化有纪律** —— 术语字典按文稿现建；机械替换后检查病句；下游渲染产物同步重建。

## 核心判据：区分"泄漏"与"证据"

客观化的主要风险是误删证据或篡改真实数据。唯一判据：内容是**被观察到的事实**，还是**写作者的口吻**——事实保留，口吻改写。

| 类型 | 处理 | 示例 |
|---|---|---|
| 直接引语（证据） | 保留（可中性归因） | 受访者原话「我绝对不碰软件」保留 |
| 第一人称转述（口吻） | 改写 | 「别给我天马行空」→「要求方案有据可循」 |
| 真实数据 / 用户原话 | 一字不动 | 数据中出现的特定词原样保留；改动即篡改 |

## 转换示例

| 主观草稿 | 客观成稿 |
|---|---|
| 某方真正想要的不是一份功能清单 | 项目要的不是一份功能清单 |
| 否则你会把错的前提做成漂亮的错答案 | 否则容易把错的前提做成漂亮的错答案 |
| 章节标题"这场会为什么这么讲" | 深层动机、商业逻辑与隐性约束 |
| 自指"本文档即此项交付" | （删除，或客观陈述其结论） |

## 安装

```bash
git clone https://github.com/TsekaLuk/objectivize ~/.claude/skills/objectivize
```

重启一个 [Claude Code](https://docs.anthropic.com/en/docs/claude-code) 会话后生效。

## 触发

通过自然语言触发，例如：

- 「把这份客观化一下，可对外发布」
- 「去掉内部口吻，改为第三方口吻」
- *“make this read like a neutral analyst wrote it — strip the insider voice”*

## 自检清单

- 是否仍有把读者或内部人拉入的称呼（引语除外）
- 是否把猜测写成事实，或暴露生产过程
- 同一角色是否全篇统一为一个称谓
- 真实数据与直接引语是否未被改动
- 置信度与局限是否保留

## License

MIT © TsekaLuk
