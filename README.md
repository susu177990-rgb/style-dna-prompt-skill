# Style DNA Prompt Skill | 风格 DNA 提取与锁定

中文 | [English](#english)

`Style DNA Prompt Skill` 把一组风格参考图提炼成可复用、可迁移、可继续出新图的 `Style DNA`。它不是普通反推提示词，也不是照抄原图内容，而是帮你锁住风格系统本身——主体、场景、动作可以换，风格不乱。

## 适合搜索的关键词

Style DNA, style extraction, style board, style locking, style consistency, visual DNA, 风格DNA, 风格锁定, 风格提取, 风格板, Nano Banana style, GPT Image style, reusable style prompt, style transfer, style rule set, 风格一致性, 风格复用.

## 这个 Skill 能做什么

- 从 `3×3`、`4×4`、拼贴板或一组同风格参考图中提取重复风格信号。
- 自动区分"风格机制"和"源图内容"：保留可迁移的风格，清走不可迁移的内容。
- 产出三件套：`style_dna.md`（人审阅）、`style_dna.json`（机读分析）、`execution_prompt.txt`（直接喂模型）。
- 附带 `scene_request_template`，后续换主体和场景时继续沿用。
- 适合长期复用：`STYLE_DNA` 固定，`SCENE_REQUEST` 可变。
- 对 GPT Image、Nano Banana 等黑盒模型尤其有用。

## 为什么不是普通反推提示词

普通反推提示词会描述"这张图是什么"。这个 skill 会回答"这组图为什么看起来像同一个视觉体系"：

- 哪些是风格机制（保留）
- 哪些是源图内容（剔除）
- 频率阈值辅助判断：70%+ 重复信号锁死、40–70% 强风格、20–40% 软风格、单次出现直接剔除
- 不把源图里的人、衣服、道具、事件误锁进风格规则

## 支持的输入类型

- `single_style_grid`：单张 3×3 或 4×4 风格格栅
- `multi_image_reference_set`：多张同风格参考图
- `collage_reference_board`：拼贴参考板
- `low_information_reference`：信息量低的参考
- `mixed_uncertain_set`：不确定是否同风格的混合图集

## 安装

```bash
npx skills add susu177990-rgb/style-dna-prompt-skill
```

Fork 版本：

```bash
npx skills add <YOUR_GITHUB_USERNAME>/style-dna-prompt-skill
```

## 使用示例

### 标准提取流程

```text
/start
[发送风格参考板]
/analyze
```

### 只拿分析结果

```text
/json
```

### 只拿执行提示词

```text
/prompt
```

### 后续换场景时

```text
把 SCENE_REQUEST 换成新的场景描述，STYLE_DNA 不动
```

## 常用命令

| 命令 | 作用 |
|---|---|
| `/start` | 说明 skill 作用、输入要求和三件套输出 |
| `/analyze` | 执行默认 Style DNA 提取 |
| `/json` | 只输出风格分析结果 |
| `/prompt` | 只输出 `execution_prompt.txt` |
| `/help` | 查看帮助 |

## 核心输出

- `style_dna.md`：给人看的中文风格说明
- `style_dna.json`：含 `analysis_trace`、`generation_contract`、`content_removed`、`forbidden`、`verification`
- `execution_prompt.txt`：含 `<visual_dna>`、`<consistency_backbone>`、`<allowed_variation>`、`<forbidden>`、`<verify>`
- `scene_request_template`：后续换主体和场景时继续沿用

## 项目结构

```text
style-dna-prompt-skill/
├── SKILL.md
├── README.md
├── agents/
├── examples/
├── references/
├── schemas/
└── tests/
```

## 三条核心规则

- `STYLE_DNA` 要稳定
- `SCENE_REQUEST` 才是后续可变部分
- 不要把源图里的人、衣服、道具、事件误锁进风格规则

## 质量标准

一个合格输出必须满足：

- 选择的风格模块类别与实际图片匹配，而不是模板填充。
- `style_dna.json` 包含 `analysis_trace`、`generation_contract`、`content_removed`、`forbidden`、`verification`。
- `generation_contract.STYLE_DNA` 保留了风格、情绪、氛围，排除了源图主体和道具。
- `execution_prompt.txt` 包含五个必要标签块。
- 场景变化隔离在 `SCENE_REQUEST` 中，`STYLE_DNA` 保持稳定。
- 输出可以迁移到新主体，不复制源图内容。
- 不使用 `beautiful`、`cinematic`、`dreamy`、`high quality` 等空泛词汇，除非有具体视觉机制支撑。

---

## English

`Style DNA Prompt Skill` extracts a transferable style contract from a style board or same-style reference set. It locks the visual system while keeping subject, scene, and action free to change.

## Search Keywords

Style DNA, style extraction, style board, style locking, style consistency, visual DNA, Nano Banana, GPT Image, reusable style prompt, style transfer, style rule set, 风格DNA, 风格锁定.

## What It Does

- Extracts repeated style signals from style grids, collages, or same-style image sets.
- Separates transferable style mechanisms from non-transferable source content.
- Outputs three formats: human-readable `style_dna.md`, machine-readable `style_dna.json`, and copy-ready `execution_prompt.txt`.
- Includes `scene_request_template` for future subject/scene changes.
- Built for long-term reuse: one stable `STYLE_DNA`, infinite `SCENE_REQUEST` variants.

## Install

```bash
npx skills add susu177990-rgb/style-dna-prompt-skill
```

For forks:

```bash
npx skills add <YOUR_GITHUB_USERNAME>/style-dna-prompt-skill
```

## Fast Path

```text
/start -> send style board -> /analyze
```

## Core Rule

Keep `STYLE_DNA` fixed. Change future content through `SCENE_REQUEST`.

## License / 许可

仓库内如有单独许可文件，以仓库实际文件为准。