# sg-writing-skill

> 把情绪藏在事实里。

`sg-writing-skill` 是一个中文写作 Agent Skill，用于生成、改写和润色克制的冰山式散文、回忆、人物故事、情感叙事和个人陈述。

它把以下技法组合成可执行的工作流：

- 情绪高点使用更短的句子
- 用少量、准确的数字或可测量细节增加重量
- 让行为、物件和身体反应代替情绪解释
- 用两个事实并置制造落差
- 在场景完成处留白，用克制的句子收束

本项目是独立维护的中文写作 Skill。它抽象公开文本中可观察的叙事技法，不复刻原文，不模拟真实人物身份，也不把虚构细节包装成现实事实。

## 安装

使用支持 Agent Skills / `SKILL.md` 的 Agent：

```bash
npx skills add qianzhu18/sg-writing-skill
```

先查看可发现的 Skill：

```bash
npx skills add qianzhu18/sg-writing-skill --list
```

指定安装：

```bash
npx skills add qianzhu18/sg-writing-skill --skill sg-writing-skill
```

安装后重新加载 Agent，使 Skill 生效。

## 直接使用

下面的请求会触发它：

```text
用 SG 写作写一段关于等待的散文，只写成稿。
```

```text
把这段分手回忆改成冰山叙事。保留日期和事实，少用形容词，不要直接解释情绪。
```

```text
用数字锚点和行为细节，写一个人在医院门口等消息的短篇，控制在六百字以内。
```

```text
帮我诊断这段文字为什么有 AI 味，并给出三处具体的收紧建议，先不要重写全文。
```

也支持原有的自然表达：`SYC 风格`、`孙宇晨文风`、`克制散文`、`冰山叙事`、`数字锚点散文`。

## 示例

请求：`用 SG 写作写一个人在车站等不会来的人。`

```text
末班车是二十三点四十分。
我二十二点五十五分到了。

电子屏改了两次颜色。
先是晚点七分钟。后来变成取消。

我给她发了一条消息。
没有问她到哪里了。

站台上还剩十六个人。
十一分钟后，只剩我一个。

我把车票折成四折，放回口袋。
那里已经有三张了。
```

数字、车票和动作承担了等待感，文本没有替读者命名情绪。示例中的数字是虚构细节，不代表现实事件。

## 它会怎么工作

1. 识别任务是生成、改写、收紧还是分析。
2. 提取视角、字数、硬事实和用户要求。
3. 为核心情绪选择行为、物件或身体反应。
4. 选择一至三个有叙事价值的数字锚点，不机械堆数。
5. 安排场景的快慢：重要过程慢写，过渡和决定快写。
6. 用事实并置和留白推进段落。
7. 检查事实一致性、AI 套话、直白情绪和结尾解释。

## 关键改进

本版本重点补足了：

- **事实保真**：改写时保护用户提供的日期、金额、人物关系和事件，不为制造真实感凭空改数。
- **少量锚点**：数字服务于叙事，不再要求固定密度，避免文字变成流水账。
- **四种任务模式**：区分生成、改写、去 AI 味和文本诊断。
- **柔性禁止清单**：把“禁用”改为针对核心情绪和无意义修辞的检查，保留引用、事实和用户指定格式。
- **可控格式**：默认只给成稿，但尊重用户对标题、章节、引号、字数和人称的要求。
- **原创边界**：只抽象高层技法，不复用参考文本的原句、数字组合、人物关系或标志性细节。

## 适用范围

适合：

- 第一人称回忆和关系故事
- 克制的中文短篇散文
- 情绪叙事和个人陈述的收紧
- 将抽象情绪转成动作、物件和场景细节
- 对已有文本做节奏、留白和叙事视角调整

不适合单独承担：

- 新闻报道、技术文档、学术论文
- 需要强转化目标的营销文案
- 未经核实的真实人物或现实事件叙述
- 冒充真实人物本人发布内容

## 文件结构

```text
sg-writing-skill/
├── SKILL.md                    # Agent 执行规则
├── agents/interface.yaml       # 界面与兼容信息
├── evals/evals.json             # 写作能力测试用例
├── evals/trigger_cases.json     # 触发与近邻测试
├── references/style-dna.md      # 风格机制参考
├── reports/                     # 设计与静态评测记录
├── manifest.json                # 发布元数据
└── LICENSE
```

## 常见问题

| 问题 | 处理方法 |
|---|---|
| 安装时提示 `No valid skills found` | 更新 Node.js 与 `skills` CLI，再运行 `npx skills add qianzhu18/sg-writing-skill --list` |
| 安装成功但没有触发 | 重新加载 Agent，并明确说 `SG 写作`、`SYC 风格`、`冰山叙事` 或 `sg-writing-skill` |
| 输出仍像普通 AI | 补充“只写成稿，用动作和物件承载情绪，不要解释” |
| 数字太多 | 要求“只保留一至三个最有反差的数字，其余改成动作细节” |
| 改写后事实变了 | 明确“只改写法，保留所有人物、日期、数字和事件” |
| 文本过度像参考作者 | 要求更换人物、场景、物件和数字，只保留高层叙事机制 |

## English

`sg-writing-skill` is a Chinese prose-writing Agent Skill for restrained, iceberg-style narratives. It uses short sentences, a small number of precise anchors, physical actions, objects, juxtaposed facts, and quiet endings.

It supports generation, rewriting, tightening, and diagnosis. It preserves user-supplied facts, avoids inventing factual claims, and treats named-author requests as high-level technique abstraction rather than identity imitation or text reproduction.

Install:

```bash
npx skills add qianzhu18/sg-writing-skill --skill sg-writing-skill
```

## 许可

本项目以 MIT 许可发布，许可文本见 [LICENSE](LICENSE)。
