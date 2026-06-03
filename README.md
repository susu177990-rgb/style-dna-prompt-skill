<p align="right">
  <strong>语言 / Language:</strong>
  <a href="#中文">中文</a> ·
  <a href="#english">English</a>
</p>

<a id="中文"></a>

# Style DNA Prompt Skill

这个 skill 用来做一件很具体的事：把一组风格参考图，提炼成一个可复用、可迁移、可继续出新图的 `Style DNA`。它不是普通“反推提示词”，也不是照抄原图内容，而是帮你锁住风格系统本身。

## 它适合什么场景

- 你已经有 `3x3`、`4x4`、拼贴板或一组同风格参考图
- 你想保留风格、情绪、氛围，但不想复制原图人物和道具
- 你需要后续持续换主体、换场景、换动作，但风格不乱
- 你要给 GPT Image、Nano Banana 或别的黑盒模型喂稳定风格合同

## 这个 skill 会给你什么

- `style_dna.md`：给人看的中文风格说明
- `style_dna.json`：结构化风格合同
- `execution_prompt.txt`：可以直接喂给模型执行的提示词
- `scene_request_template`：后续换主体和场景时继续沿用

## 功能亮点

- 从参考板里提取重复风格信号
- 自动区分“风格机制”和“源图内容”
- 适合长期复用，不是一次性 prompt
- 输出同时适合人审阅和模型执行
- 对 GPT Image、Nano Banana 这类黑盒模型尤其有用

## 最核心的价值

不是“这张图像什么”，而是“这组图为什么看起来像同一个视觉体系”。

这个 skill 会把：

- 可以迁移的风格机制保留下来
- 不能迁移的源图内容清出去
- `STYLE_DNA` 固定住
- 把后续变化留给 `SCENE_REQUEST`

## Installation / 安装

放进全局 skills 目录：

```bash
$ cp -R "style dna prompt skill" ~/.codex/skills/style-dna
```

如果你使用项目本地 skills：

```bash
$ cp -R "style dna prompt skill" ./.codex/skills/style-dna
```

## Usage / 用法

最短使用方式：

1. 准备一张主风格板，或一组明确同风格的参考图
2. 调用 skill 提取 `Style DNA`
3. 以后只改 `SCENE_REQUEST`，不要反复改 `STYLE_DNA`

示例调用：

```text
$ 请用这张风格参考板提取可迁移的 Style DNA，返回 style_dna.md、style_dna.json 和 execution_prompt.txt。
```

## 输入要求

输入结构定义在 [schemas/input.schema.json](./schemas/input.schema.json)。

最常用字段：

- `style_board_image_url`：主参考板图片，必填
- `reference_images`：补充参考图，可选
- `target_model`：目标模型类型
- `output_language`：输出语言模式
- `analysis_depth`：分析深度
- `scene_request_hint`：可选场景请求示例

## 最常见的工作流

### 1. 先提取固定风格合同

适合已有稳定风格板的情况：

```json
{
  "style_board_image_url": "https://example.com/style-grid.jpg",
  "target_model": "gpt_image_or_nano_banana",
  "output_language": "zh_review_en_contract",
  "analysis_depth": "standard"
}
```

### 2. 后续只换场景，不换风格

```json
{
  "SCENE_REQUEST": {
    "subject": "a small silver perfume bottle",
    "environment": "an empty tiled bathroom at dusk",
    "action": "resting near a fogged mirror",
    "shot_type": "close medium product shot",
    "composition": "off-center subject with negative space",
    "aspect_ratio": "4:5",
    "output_goal": "generate a new subject while preserving the locked Style DNA"
  }
}
```

## 它特别适合这些人

- 做品牌视觉统一的人
- 做一套持续更新内容的人
- 需要把参考图变成长期生成规则的人
- 讨厌“同一个风格每次都要重新解释一遍”的人

## 仓库结构

```text
.
├── README.md
├── SKILL.md
├── agents/
├── examples/
├── references/
├── schemas/
└── tests/
```

## 推荐先看哪里

- [SKILL.md](./SKILL.md)：skill 入口
- [references/workflow.md](./references/workflow.md)：完整流程
- [references/output-contract.md](./references/output-contract.md)：输出约束
- [examples/style_dna.example.json](./examples/style_dna.example.json)：结果示例
- [examples/scene_request.example.json](./examples/scene_request.example.json)：后续场景请求示例

## 使用规则，尽量记住这三条

- `STYLE_DNA` 要稳定
- `SCENE_REQUEST` 才是后续可变部分
- 不要把源图里的人、衣服、道具、事件误锁进风格合同

---

<a id="english"></a>

## English

`Style DNA Prompt Skill` extracts a transferable style contract from a style board or a same-style reference set. It is built for teams who want to keep the visual system stable while changing subject, scene, action, or framing later.

## Best for

- style boards
- collage references
- repeatable brand visuals
- long-running image systems
- GPT Image / Nano Banana style locking

## Main outputs

- `style_dna.md`
- `style_dna.json`
- `execution_prompt.txt`
- `scene_request_template`

## Core rule

Keep `STYLE_DNA` fixed. Change future content through `SCENE_REQUEST`.

## License / 许可

仓库内如有单独许可文件，以仓库实际文件为准；当前 README 不额外重定义许可。
