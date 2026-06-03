# Output Contract

The skill returns three artifacts.

## style_dna.md

Chinese human review version. Keep it concise and useful:

- style name and one-sentence definition
- selected style category and why
- locked / strong / soft Style DNA
- emotion and atmosphere mechanisms
- content removed
- allowed variation
- forbidden drift
- confidence and risks
- usage note for changing subjects/scenes

## style_dna.json

Strict JSON. Top-level key: `style_dna_compiler`.

Required sections:

- `metadata`
- `analysis_trace`
- `generation_contract`
- `scene_request_template`
- `quality_report`

`analysis_trace` contains evidence and reasoning. `generation_contract` is the reusable part for image generation.

Keep execution values in English. Chinese can appear in review notes and quality report.

`generation_contract.STYLE_DNA` must include `emotion_and_atmosphere`. Do not rely only on color, camera, or texture; the DNA must preserve how the style feels after source subjects and props are removed.

## execution_prompt.txt

Use this block structure:

```xml
<visual_dna>
...
</visual_dna>

<consistency_backbone>
...
</consistency_backbone>

<allowed_variation>
...
</allowed_variation>

<forbidden>
...
</forbidden>

<verify>
...
</verify>
```

The execution prompt should be shorter than the analysis JSON. It should contain only stable style mechanisms, allowed variation, forbidden drift, and verification checks.

For JSON-only web-agent use, output one `json` fenced code block and no surrounding text. Target 2000-4000 characters: keep compressed evidence plus `STYLE_DNA`, `emotion_and_atmosphere`, `SCENE_REQUEST_TEMPLATE`, `NEGATIVE_CONSTRAINTS`, and `VERIFY`; omit full per-cell transcripts.

## Scene Request Rule

Future generation should keep `STYLE_DNA` unchanged and only edit:

- subject
- environment
- action
- shot type or composition request
- aspect ratio
- output goal

If a scene request conflicts with locked style, locked style wins unless the user explicitly asks to revise the Style DNA.

Changing `SCENE_REQUEST` must never require preserving the source board's original subject, prop, outfit, location, or story event.
