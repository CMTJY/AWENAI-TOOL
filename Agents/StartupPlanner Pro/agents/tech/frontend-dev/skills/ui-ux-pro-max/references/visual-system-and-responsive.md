# Visual system and responsive behavior

## Token system

Define semantic tokens for:

- foreground, background, surface, primary, secondary, border, focus, danger, warning, and success;
- typography roles rather than ad hoc font sizes;
- spacing, radius, elevation, icon sizes, motion duration, and easing;
- component states in both light and dark themes.

Avoid raw values scattered across components. Verify that theme variants preserve hierarchy and contrast rather than merely invert colors.

## Layout

- Start with the smallest supported viewport and expand by content pressure, not device marketing names.
- Prevent horizontal overflow and hidden content.
- Set readable line lengths and adaptive gutters.
- Reserve space for media and asynchronous content to avoid layout shifts.
- Keep fixed headers, bottom bars, and calls to action from covering scroll content.
- Test portrait, landscape, large text, long localization strings, empty data, and dense data.

## Typography and icons

- Use a clear type hierarchy with consistent line height and weight.
- Prefer wrapping to destructive truncation; expose full content when truncation is necessary.
- Use tabular figures for aligned numeric data.
- Use one coherent icon family and official brand assets.
- Do not use emoji as structural icons when a controllable vector or native symbol is available.

## Performance

- Set media dimensions and use responsive formats.
- Lazy-load non-critical media and code without delaying the primary task.
- Virtualize genuinely long lists and measure before optimizing smaller ones.
- Avoid excessive third-party scripts, synchronous main-thread work, repeated layout reads/writes, and unbounded animations.
- Test interaction latency and layout stability on realistic low-end devices or throttled conditions when performance is a requirement.
