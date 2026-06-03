# Style Signal Routing

The skill must choose extraction fields dynamically. Start with broad observation, then activate only the modules that are visually relevant.

## Universal Signals

Always consider these, but do not force all into the final output:

- palette and color hierarchy
- lighting or value structure
- contrast and exposure behavior
- composition and visual balance
- texture, sharpness, grain, noise, finish
- subject treatment
- environment treatment
- mood mechanisms
- emotion mechanisms
- atmosphere mechanisms
- forbidden style drift
- verification checks

## Photography / MV / Short Drama

Use when the board looks photographic, live-action, filmic, documentary, editorial, or AI+real-shot.

Prioritize:

- lens feel and camera distance
- camera height and angle
- exposure behavior and white balance
- highlight and shadow behavior
- skin/surface rendering
- depth of field and focus drift
- motion blur or handheld stability
- grain, compression, film stock feel

Avoid forcing illustration terms such as line quality or brushwork.

## Illustration / Anime / Picture Book

Use when the board relies on drawn or painted construction.

Prioritize:

- line quality
- brush texture
- edge treatment
- shape language
- color blocking
- shading method
- facial simplification
- detail density
- background simplification

Avoid forcing focal length or film stock unless the illustration clearly imitates camera language.

## CG / 3D / Product Advertising

Use when the board relies on rendered assets, shaders, product surfaces, game CG, toy-like worlds, or fantasy product scenes.

Prioritize:

- material system
- surface reflection
- shader behavior
- transparency and subsurface scattering
- volumetric light
- asset density
- product scale logic
- render cleanliness

Avoid vague "3D quality"; name the material and lighting behavior.

## Graphic Design / Poster / KV / Cover

Use when layout, typography, figure scale, or visual hierarchy controls the style.

Prioritize:

- layout grid
- title placement
- typography style
- visual hierarchy
- negative space rule
- figure scale
- graphic motifs
- text density
- poster energy

Do not copy exact text, logos, or brand marks into the generation contract.

## Mixed or Uncertain Style

Use when references include multiple media or inconsistent sources.

Rules:

- lower confidence
- extract only cross-image mechanisms
- avoid over-locking camera or rendering fields
- mark conflicting signals in `quality_report`
- keep `locked_style` short

## Nonstandard Styles

If the image does not fit the common categories, use `mixed_uncertain` for the category and create precise adaptive fields inside `style_modules`.

Examples:

- `embroidery_stitch_logic`
- `clay_surface_imperfection`
- `risograph_misalignment`
- `surreal_scale_logic`
- `museum_display_language`
- `found_object_arrangement`

Only create fields that are supported by visible evidence. The field name should describe the visual mechanism, not the source subject.
