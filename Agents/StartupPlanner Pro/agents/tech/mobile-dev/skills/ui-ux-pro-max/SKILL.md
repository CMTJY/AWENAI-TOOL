---
name: ui-ux-pro-max
description: Design, implement, or review web and mobile interfaces for usability, accessibility, responsive behavior, interaction feedback, visual-system consistency, and platform conventions. Use for UI components, pages, forms, navigation, charts, design systems, or pre-delivery experience audits.
---

# UI/UX Pro Max

This is a locally modified, self-contained derivative of `nextlevelbuilder/ui-ux-pro-max-skill`. The upstream search database and CLI are not bundled. See `LICENSE.txt` and the collection `SOURCES.md`.

## Workflow

1. Identify product type, target users, primary task, device contexts, content density, and implementation stack.
2. Define a compact design system: semantic colors, typography roles, spacing, radius/elevation, interaction states, motion, and responsive rules.
3. Design the information hierarchy and primary path before polishing individual components.
4. Implement with semantic controls and reusable tokens.
5. Test loading, empty, error, disabled, permission, destructive, and offline states relevant to the product.
6. Run accessibility, interaction, responsive, platform, performance, and visual-consistency checks.

Use `frontend-design` first when the task needs distinctive art direction. This skill owns systematic usability and quality controls.

## Priority order

| Priority | Area | Required outcome |
|---|---|---|
| 1 | Accessibility | Operable and understandable without relying on color, pointer, or animation alone |
| 2 | Interaction | Adequate targets, clear states, immediate feedback, recoverable errors |
| 3 | Information and navigation | Predictable hierarchy, orientation, back path, and primary action |
| 4 | Responsive and platform | No clipped content; correct safe areas, input modes, and platform conventions |
| 5 | Performance | Stable layout, responsive input, optimized media and long lists |
| 6 | Visual system | Consistent tokens, typography, icon language, spacing, and themes |
| 7 | Motion and data | Meaningful, interruptible motion and accessible data alternatives |

## Load references as needed

- Read [accessibility-and-interaction.md](references/accessibility-and-interaction.md) for controls, forms, focus, feedback, and motion.
- Read [visual-system-and-responsive.md](references/visual-system-and-responsive.md) for tokens, layout, typography, themes, icons, and performance.
- Read [platform-and-data.md](references/platform-and-data.md) for mobile safe areas, navigation, charts, tables, and final checks.

## Deliverables

Return the design-system decisions, component/state inventory, responsive behavior, accessibility decisions, implementation notes, verification performed, and known gaps. Do not claim checks that were not run on the rendered interface.

## StartupPlanner Pro Integration

This is an independently maintained local copy imported from baseline `superpowers-portable-2026-07-18`.

- Local owner: `tech-mobile-dev`
- Role contract: read [../../mobile-dev.md](../../mobile-dev.md) before using this skill.
- Input: the assigned Task Packet, approved upstream artifacts, declared file scope, and acceptance criteria.
- Boundary: never read or depend on the repository-level `Skills/superpowers` source at runtime.
- Handoff: 输出包含平台、设备或模拟器边界的 implementation_result，交给 tech-code-reviewer。
- Evidence: include changed files, focused and regression checks, failures, and known gaps.
