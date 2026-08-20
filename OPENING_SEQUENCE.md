# Opening Sequence Prototype

## Status

This work exists only on the `codex/opening-sequence` branch. GitHub Pages continues to deploy `main`, so none of the intro code or preview media is part of the live game.

## Sequence

1. Legend enters already talking on a chunky pink-and-purple retro corded phone, inspired loosely by the playful shape and colors of a Tin Can kids' phone but drawn as an original prop with no branding.
2. The conversation is split into four readable beats:
   - “Ugh. My dad is the WORST.”
   - “I can't do ANYTHING until I beat up my siblings…”
   - The existing sentence remains visible and “…with MATH.” appears beneath it as the punchline.
   - “See ya!”
3. Each line waits for a tap. A generous 5–9 second automatic fallback keeps the scene moving if the player does not tap.
4. Legend hangs up with a visible “CLICK!”, switches into her kick pose, and performs two warm-up moves against a breakable practice board.
5. “LET'S DO THIS!” fills the screen before the normal opponent-selection menu appears.

The phone pose has only a slow, slight sway while the player reads. The player may always use **Skip Intro**, and the start screen includes **Replay Intro**. The opening automatically plays only for a player who has not seen it before.

## Design review

Fable recommended replacing a fixed rapid timeline with tap-to-continue dialogue and isolating “…with MATH.” as its own comic beat. The implemented version follows that recommendation while preserving automatic fallbacks for a hands-off first viewing.

## Review questions

- Is the dad joke funny to Reagan, or should it be more mischievous/less negative?
- Is “beat up my siblings… with MATH” the right punchline?
- Should the intro stay as a cold open, or play after she chooses which sibling to face?
- Does the warm-up need a second distinct action sprite later?

## Preview

See `preview/legend-opening-sequence.gif` for the phone-sized prototype recording.
