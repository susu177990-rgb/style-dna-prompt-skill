# Test: content trap

Input: a 3x3 board where only one image contains a red umbrella, one contains a cat, and one contains a yacht, while all images share muted cyan shadows and milky highlights.

Expected:

- Red umbrella, cat, and yacht go to `content_removed`.
- Locked style preserves muted cyan shadows and milky highlights.
- If the red umbrella is mentioned, it is only translated as `isolated high-saturation accent object`, not copied literally.
- The exact subject, prop, location, and event do not appear in `locked_style`.
- Emotion and atmosphere are retained through abstract mechanisms, not through the original person or prop.
