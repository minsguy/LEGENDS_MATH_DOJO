# Legend's Math Dojo

## Purpose

Build a small, personalized multiplication-fluency game for the player character, Legend. The game should feel like the family's existing one-page browser games: immediately understandable, playful, mobile-friendly, and easy to publish with GitHub Pages.

## Canonical product plan

Read `PLAN.md` before changing game behavior. Keep it updated when product decisions change.

## Technical direction

- Prefer one self-contained `index.html` containing the HTML, CSS, and JavaScript.
- Use no build process or runtime dependencies unless a later requirement clearly justifies them.
- Support physical keyboard input and a large on-screen number pad.
- Design mobile-first and test desktop keyboard behavior too.
- Persist progress in namespaced `localStorage`; do not introduce a database for v1.
- Keep raw family photos in `assets/raw/`. That directory is intentionally gitignored and must never be deployed.
- Put only approved, web-ready artwork in `assets/processed/`.

## Learning rules that must remain true

- A normal first attempt has a 12-second limit.
- Five timed correct answers in a row earn the player character, labeled Legend, an attack and a progression reward.
- A wrong answer or timeout resets the streak and triggers the sibling's counterattack.
- After a wrong answer or timeout, the player must keep guessing until she enters the correct answer without a time limit; do not reveal it first.
- A correction never advances the streak.
- Missed facts return after a short delay and are prioritized in the next play session.
- V1 has a fixed 12-second timer and no child-accessible parent/settings panel.

## Safety and tone

- Fighting is affectionate cartoon slapstick: exaggerated reactions, comic effects, no injuries, weapons, blood, or realistic violence.
- Do not publish, embed, or commit raw photos without explicit approval.

## Project instruction files

`AGENTS.md` is canonical. `CLAUDE.md` must contain only `@AGENTS.md`.
