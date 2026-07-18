---
name: frontend-design
description: Create distinctive visual direction and production-quality frontend presentation for web pages, components, applications, and interface redesigns. Use when a UI needs intentional art direction, typography, layout, motion, brand expression, or relief from generic template aesthetics.
---

# Frontend Design

This is a locally modified derivative of Anthropic's `frontend-design` skill. See `LICENSE.txt` and the collection `SOURCES.md`.

Create an interface whose visual choices come from the product's subject, audience, content, and purpose.

## Direction brief

Before implementation, define:

```yaml
design_direction:
  subject:
  audience:
  page_job:
  desired_feeling:
  palette: []
  typography_roles: []
  layout_thesis:
  signature_element:
  deliberate_risk:
  constraints: []
```

Use real product content. If the brief leaves a material choice open, select a coherent direction and state it rather than generating a neutral collage of popular styles.

## Design principles

- Make the hero or primary view express the product's central idea.
- Let typography carry personality through deliberate role, scale, weight, width, and rhythm.
- Use dividers, labels, numbering, and structure only when they encode real information.
- Spend boldness on one signature element; keep supporting elements disciplined.
- Match implementation complexity to the direction. Minimalism demands precision; maximalism demands coherent systems.
- Use motion to explain cause, hierarchy, or continuity, not to decorate every element.
- Write interface copy from the user's perspective with consistent action names and recoverable error states.

## Anti-template critique

Before building, ask:

1. Could the same palette, type, hero, and card layout fit an unrelated product?
2. Does each visual device express something true about this subject?
3. Is the signature element memorable without harming comprehension?
4. Are current trends being used because they fit, or because they are defaults?

Revise generic choices, then implement the approved direction consistently through tokens and reusable components.

## Quality floor

Distinctive design does not replace engineering quality. Deliver responsive behavior, visible focus, semantic controls, readable contrast, reduced-motion support, stable states, and tested empty/error/loading views. Use `ui-ux-pro-max` for systematic usability and accessibility review.

## StartupPlanner Pro Integration

This is an independently maintained local copy imported from baseline `superpowers-portable-2026-07-18`.

- Local owner: `tech-frontend-dev`
- Role contract: read [../../frontend-dev.md](../../frontend-dev.md) before using this skill.
- Input: the assigned Task Packet, approved upstream artifacts, declared file scope, and acceptance criteria.
- Boundary: never read or depend on the repository-level `Skills/superpowers` source at runtime.
- Handoff: 输出包含渲染、可访问性和测试证据的 implementation_result，交给 tech-code-reviewer。
- Evidence: include changed files, focused and regression checks, failures, and known gaps.
