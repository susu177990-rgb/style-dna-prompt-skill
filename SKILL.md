---
name: style-dna
description: Use this skill when the user provides a 3x3 or 4x4 style grid, collage, reference board, or multiple same-style images and asks to extract Style DNA, visual DNA, 风格DNA, 风格锁定, style consistency, Nano Banana / GPT Image style prompt, or a reusable style rule set. The skill turns reference images into a three-part output: human-readable style_dna.md, machine-readable style_dna.json, and execution_prompt.txt for GPT Image / Nano Banana style-consistent generation.
---

# Style DNA Compiler

This skill extracts transferable visual style mechanisms from a style board. It is not a captioner, reverse prompt tool, or template filler. The goal is to compile image references into a reusable style-lock rule set for black-box image models.

The central extraction target is not "what is in the image". It is the transferable combination of `style`, `emotion`, and `atmosphere` after source subjects, props, identities, locations, logos, and one-off story events have been removed.

## Commands

| Command | Action |
|---|---|
| `/start` | Explain what the skill does, what inputs it needs, and what the three default outputs are |
| `/analyze` | Run the default Style DNA extraction workflow |
| `/json` | Return only the analysis result |
| `/prompt` | Return only `execution_prompt.txt` |
| `/help` | Show the command table and a short usage guide |

## Default Interaction

- This skill now uses slash commands as the primary entry mode.
- The user should first send one style board or a same-style image set, then run `/analyze`.
- If the user sends images first, acknowledge them as style references and wait for `/analyze` unless the request already clearly asks to start.
- `/json` and `/prompt` are narrower output variants of the same analysis, not separate workflows.

## Default Output

Always produce three outputs unless the user explicitly asks for a narrower format:

- `style_dna.md`: Chinese human review document.
- `style_dna.json`: the main analysis result plus generation rules.
- `execution_prompt.txt`: copy-ready prompt for GPT Image / Nano Banana.

Also include a `scene_request_template` inside the main analysis result so future generations keep `STYLE_DNA` fixed and only change the scene request.

## Workflow

1. Intake the input as one of: `single_style_grid`, `multi_image_reference_set`, `collage_reference_board`, `low_information_reference`, or `mixed_uncertain_set`.
2. Decompose the grid or image set into cells/items before synthesizing style.
3. Observe each cell with only visible facts. Do not summarize first.
4. Rank repeated visual signals by frequency, visual control power, and transfer value.
5. Route to the relevant style modules only after inspecting the images.
6. Separate retained signals from ignored source content.
7. Translate repeated concrete content into abstract style / emotion / atmosphere mechanisms only when justified.
8. Compile the three outputs.
9. Run self-checks for template leakage, content copying, missing negative constraints, and missing verification rules.

## Resource Loading

Load only what is needed:

- Core process: `references/workflow.md`.
- Dynamic field choice: `references/style-signal-routing.md`.
- Ignore/retain rules: `references/ignore-retain-rules.md`.
- Output writing guide: `references/output-contract.md`.
- Failure prevention: `references/failure-cases.md`.
- JSON structure: `schemas/style_dna.schema.json`.
- Internal validation only: `schemas/input.schema.json` and `schemas/output.schema.json`.

## Hard Rules

- Do not use a fixed template to decide what matters. Inspect first, then choose fields.
- Do not describe image content as style.
- Ignore specific people, clothing, props, locations, text, logos, brands, and story events by default.
- Retain only transferable `style`, `emotion`, and `atmosphere` mechanisms.
- A feature appearing once is content by default. If visually important, translate it into an abstract mechanism instead of copying it.
- Do not keep example field names inside `locked_style`, `strong_style`, `soft_style`, or `style_modules` unless they fit the actual image. These are adaptive containers, not templates.
- Use frequency thresholds as guidance, not blind automation:
  - 70%+ repeated: `locked_style`
  - 40%-70% repeated: `strong_style`
  - 20%-40% repeated: `soft_style`
  - one-off: `content_removed`
- JSON execution fields must be in English.
- Chinese explanation belongs in `style_dna.md` and `quality_report`.
- If the user requests JSON-only or web-agent output, wrap the JSON in a `json` code block and target 2000-4000 characters: enough detail to preserve style, emotion, and atmosphere, but not a full per-cell transcript.
- Avoid vague words such as `beautiful`, `cinematic`, `dreamy`, `high quality`, `aesthetic`, or `premium` unless paired with concrete visual mechanisms.
- Never claim this trains a real LoRA. Describe it as a style-lock rule set for GPT Image / Nano Banana style consistency.

## Completion Checks

Before final output, verify:

- The chosen style category modules match the actual images.
- `style_dna.json` contains `analysis_trace`, `generation_contract`, `content_removed`, `forbidden`, and `verification`.
- `generation_contract.STYLE_DNA` preserves style, emotion, and atmosphere while excluding source subjects and props.
- `execution_prompt.txt` contains `<visual_dna>`, `<consistency_backbone>`, `<allowed_variation>`, `<forbidden>`, and `<verify>`.
- Scene changes are isolated in `SCENE_REQUEST`; `STYLE_DNA` remains stable.
- The output can transfer to a new subject without copying source content.
