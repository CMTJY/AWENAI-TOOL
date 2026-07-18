# Platform and data interfaces

## Mobile platforms

- Respect safe areas, system bars, notches, gesture regions, and keyboard insets.
- Preserve platform back behavior and navigation-stack state.
- Use top-level tabs or bottom navigation only for a small stable set of destinations.
- Avoid gesture conflicts and always expose a visible alternative for critical gesture actions.
- Support platform text scaling, screen-reader traits, permissions, offline states, and lifecycle interruptions.
- Test real touch behavior and at least one small and one large device class.

## Navigation

- Keep the current location visible.
- Preserve filters, input, and scroll position when users navigate back where expected.
- Provide a clear exit from dialogs and multi-step flows.
- Keep dangerous actions spatially separate from normal navigation.
- Do not use modal surfaces as a substitute for primary navigation.

## Charts and tables

- Choose chart types by the question: trend, comparison, distribution, relationship, or composition.
- Label units, time grain, axes, and legends clearly.
- Do not rely on color alone; use labels, shapes, patterns, or direct annotation.
- Provide a table or textual summary for screen readers and precise values.
- Make tooltips and series controls keyboard and touch accessible.
- Reflow or simplify charts at narrow widths; avoid unreadable rotated labels.
- Use locale-aware number, date, and currency formatting.
- Show loading, empty, error, and stale-data states.

## Pre-delivery check

- Primary journey works by keyboard and touch.
- Focus order and accessible names were inspected.
- Light/dark contrast and large text were checked.
- Small viewport, landscape, and long content were checked.
- Loading, empty, error, disabled, and destructive states exist.
- Fixed elements do not cover content.
- Motion respects reduced-motion settings.
- Claims are backed by screenshots, automated checks, or documented manual evidence.
