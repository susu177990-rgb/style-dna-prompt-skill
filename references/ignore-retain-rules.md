# Ignore / Retain Rules

This is the most important quality gate for Style DNA.

## Retain

Only retain transferable mechanisms that can survive a subject or scene swap:

- `style`: palette, lighting, value structure, camera/layout, composition, material, texture, rendering finish, detail density.
- `emotion`: how emotion is visually expressed through distance, posture energy, expression intensity, exposure, color temperature, contrast, framing pressure, or viewer distance.
- `atmosphere`: how atmosphere is visually built through air density, haze, environmental softness, temporal feeling, space density, light diffusion, material aging, or background treatment.

Emotion and atmosphere are mandatory. They must be concrete visual mechanisms, not just words like lonely, dreamy, sad, warm, or nostalgic.

Good:

- `restrained emotional distance created by off-center framing and low expression intensity`
- `humid memory-like atmosphere built from cyan-green shadows, milky highlights, and soft focus drift`

Bad:

- `sad girl`
- `dreamy vibe`
- `nice atmosphere`

## Ignore

Ignore these by default, even if they dominate the reference image:

- exact person or character identity
- age, gender, or body identity as content, unless the treatment is a style mechanism
- exact clothing item
- exact prop
- exact location
- exact room, vehicle, building, landscape, or product
- readable text, logo, brand, watermark
- one-off event or story action
- exact pose if it is not repeated as a composition or emotional-treatment rule

Ignored content belongs in `content_removed`, not in `STYLE_DNA`.

## Translate

Translate source content only when it becomes a reusable visual mechanism:

- red umbrella -> isolated high-saturation accent object
- crying girl -> restrained emotional realism, low expression intensity, vulnerable viewer distance
- rainy rooftop -> wet reflective surfaces plus overcast diffused light
- old TV -> analog screen glow plus low-resolution electronic texture
- yacht pool -> reflective luxury surfaces plus hard sun specular highlights
- candy carriage -> glossy pastel materials plus dense whimsical prop rhythm
- space capsule -> silver-white reflective material plus transparent acrylic and high-tech product lighting

Translation must not preserve exact content. If the abstract rule would still force the same prop, person, or scene, it is not abstract enough.

## Retention Test

Before finalizing, ask:

1. If the subject changes to a product, animal, room, vehicle, or landscape, does the DNA still work?
2. Are emotion and atmosphere still present without the original person or story?
3. Did any exact prop, outfit, room, logo, or character leak into `locked_style`?
4. Are forbidden constraints specific enough to prevent style drift and source copying?
