# Workflow

Use this process for every Style DNA extraction.

## 1. Intake

Classify the input:

- `single_style_grid`: one 3x3/4x4 or similar grid.
- `multi_image_reference_set`: separate images intended to share a style.
- `collage_reference_board`: mixed layout with uncertain cell boundaries.
- `low_information_reference`: too few images or too little visible evidence.
- `mixed_uncertain_set`: references do not clearly share one visual system.

If the input is low-information, still produce the three outputs, but lower confidence and avoid over-locking.

## 2. Cell Observation

Analyze each cell/item separately before any synthesis. Record only visible facts:

- medium/render type
- palette, accent behavior, highlight/shadow bias
- lighting source, direction, hardness, exposure behavior
- camera/viewpoint or design layout
- composition, subject placement, negative space, foreground use
- texture, grain/noise, sharpness, material finish
- subject and environment treatment
- emotion as visible behavior, not abstract feeling
- atmosphere as visible behavior, not generic mood words
- obvious non-style content to remove

Do not force every field. If a field is not visually relevant, omit it or mark it low-confidence.

## 3. Signal Ranking

Rank candidate style signals by three factors:

- frequency: how often it appears across cells/images
- control power: how strongly it changes generated results
- transfer value: whether it survives subject/scene changes
- ignore risk: whether the signal is actually source content

Frequency mapping:

- 70%+ -> `locked_style`
- 40%-70% -> `strong_style`
- 20%-40% -> `soft_style`
- one-off -> `content_removed`

Override only when a one-off element is clearly a visual mechanism. Example: a single red umbrella should not become "red umbrella"; it may become "isolated high-saturation accent object" if the board otherwise supports accent-color logic.

## 4. Dynamic Module Routing

Choose modules from `style-signal-routing.md` after observation. A style can use multiple modules, but each selected module must be justified by visible evidence.

Do not output empty module fields. Better to output fewer high-signal fields than many generic ones.

## 5. Ignore / Retain Filter

Load `ignore-retain-rules.md` when the input includes strong subjects, props, clothing, locations, or story events.

Move source-specific details into `content_removed`:

- exact people or character identities
- apparent age/gender/body identity when it is only subject content
- clothing items unless repeated as a styling system
- props unless repeated as motif logic
- exact locations unless repeated as environment treatment
- readable text, logos, brands, watermarks
- one-off scene events

Retain only:

- transferable visual style mechanisms
- emotion mechanisms visible through composition, expression intensity, color, lighting, or distance
- atmosphere mechanisms visible through air, texture, space, temporal feeling, environment treatment, or light behavior

Translate only when useful:

- red umbrella -> isolated high-saturation accent object
- rainy rooftop -> wet reflective surfaces plus overcast diffused light
- old TV -> analog screen glow plus low-resolution electronic texture
- yacht pool -> reflective luxury surfaces plus hard sun specular highlights

Never translate in a way that still forces the original prop, person, or location.

## 6. Compile

Create:

- `style_dna.md`: Chinese review version with reasoning and risks.
- `style_dna.json`: strict JSON with analysis trace and generation contract.
- `execution_prompt.txt`: structured prompt block for image generation.

The JSON should be the source of truth. The MD and execution prompt must not contradict it.

If the user asks for JSON-only or web-app agent behavior, output only one `json` fenced code block. Target 2000-4000 characters; reduce `analysis_trace` first and preserve `STYLE_DNA`, `emotion_and_atmosphere`, `NEGATIVE_CONSTRAINTS`, and `VERIFY`.

## 7. Self-Check

Reject or revise output if:

- it could apply to almost any image style
- it copies source content
- it preserves subject, prop, outfit, or location as locked style
- it lacks concrete emotion or atmosphere mechanisms
- it contains generic praise words without mechanisms
- it overuses fields from the wrong style category
- it lacks forbidden constraints
- it lacks verification rules
- it cannot survive a subject or scene swap
