# Accessibility and interaction

## Controls and focus

- Use native semantic controls before generic containers with click handlers.
- Provide an accessible name for every control and meaningful image.
- Keep keyboard and screen-reader order aligned with visual order.
- Preserve visible focus and move focus intentionally after dialogs, route changes, and validation failures.
- Provide keyboard alternatives for drag, hover, gesture, or pointer-only interactions.
- Do not disable user zoom.

## Targets and feedback

- Aim for at least 44 by 44 CSS pixels/points on touch interfaces; follow stricter platform requirements where applicable.
- Separate adjacent targets enough to avoid accidental activation.
- Show pressed, selected, disabled, busy, success, and error states without shifting layout.
- Give immediate feedback for input; use progress or skeleton states for longer waits.
- Keep actions idempotent or disabled while an irreversible request is pending.

## Forms and recovery

- Use persistent labels; placeholders are examples, not labels.
- Validate at a useful time and place errors next to affected fields.
- State what failed and how to recover; focus the first invalid field when appropriate.
- Preserve entered data after recoverable errors.
- Confirm destructive actions or offer a reliable undo path.
- Announce asynchronous errors and status changes through appropriate accessibility semantics without stealing focus.

## Color, text, and motion

- Meet the project's WCAG target; do not infer contrast from appearance alone.
- Never encode status by color alone.
- Support text enlargement and reflow without clipping controls or hiding content.
- Respect reduced-motion preferences.
- Animate transform and opacity when possible; avoid motion that blocks input or causes layout shift.
- Make motion interruptible and use it to express cause, hierarchy, or continuity.
