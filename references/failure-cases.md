# Failure Cases

Use these as regression checks while extracting Style DNA.

## Template Filling

Bad: every output has the same long list of fields, even when the board is a poster, watercolor illustration, or live-action photo set.

Fix: choose modules after visual inspection and omit irrelevant fields.

## Content Leakage

Bad: "young woman in bedroom", "red umbrella", "yacht", or "cat" appears in `locked_style`.

Fix: move one-off objects to `content_removed`. Translate only repeated or style-defining mechanisms.

## Subject-as-Style Leakage

Bad: the source board is full of girls, cats, cars, food, or products, and the output makes those subjects mandatory.

Fix: preserve only the treatment: viewer distance, pose energy, expression intensity, material behavior, framing pressure, or environmental relationship.

## Missing Emotion / Atmosphere

Bad: the output locks palette and camera, but loses the emotional distance or atmosphere that made the board recognizable.

Fix: add concrete mechanisms such as restrained expression range, lonely viewer distance, humid haze, dense playful clutter, sterile showroom calm, or oppressive negative space.

## Vague Style Words

Bad: "cinematic, dreamy, beautiful, high quality".

Fix: write mechanisms such as low-contrast milky highlights, shallow depth of field, cyan-green shadow bias, soft focus drift, or off-center negative-space framing.

## Over-Locking

Bad: a mixed board produces a huge `locked_style` that cannot transfer.

Fix: lower confidence, shorten locked fields, and move uncertain signals to `soft_style` or `quality_report.risks`.

## Wrong Module

Bad: illustration board gets focal length and film stock fields with no evidence.

Fix: use line, edge, brush, shape, color blocking, shading, and detail-density signals.

## Missing Negative DNA

Bad: output only says what to include.

Fix: always include forbidden constraints such as modern HDR, glossy AI default, exact content copying, commercial beauty light, clean digital sharpness, or any drift relevant to the style.
