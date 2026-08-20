# Legend's Math Dojo — v1 Plan

## Status

Initial v1 implementation is complete and browser-tested. The single-page game includes idle and action photo cutouts, fixed fifteen-second recall, streak attacks, untimed no-reveal correction, delayed retries, realistic belt/stripe progression, reward ceremonies, sound, and local persistence. The player is labeled Legend throughout the public project. Public GitHub Pages testing with the processed cutouts was approved on August 19, 2026; raw family photos remain local and excluded from git.

An optional first-visit opening sequence is being prototyped separately on `codex/opening-sequence`. It is intentionally excluded from the live `main` deployment pending review.

## Goal

Help the player memorize multiplication facts through 9 × 9 using short timed recall, required error correction, adaptive repetition, and a funny sibling karate theme.

The game succeeds if the player wants to keep playing and her accurate response speed improves on facts she initially misses.

## V1 experience

Legend faces one sibling at a time in friendly, continuous cartoon-dojo play. She chooses her sister or brother as the opponent when starting a play session. Each multiplication question is one dojo exchange; v1 has no health, winner, loser, or match-ending state.

### Timed attempt

1. Finish any preceding feedback animation, then show a multiplication fact and enable/focus the answer input.
2. Start the 15-second power bar only when the full question is visible and input is enabled.
3. Accept answers from the physical keyboard or the on-screen number pad. Digits may be freely changed with Backspace before submission.
4. Submit only with Enter or the on-screen submit button; never infer submission from digit count.
5. If time expires before submission, treat the attempt as a timeout even when digits are present in the input.
6. If the submitted answer is correct before time expires:
   - play brief positive feedback;
   - advance the visible streak by one;
   - immediately continue to the next fact, except when the streak reaches five.
7. When the streak reaches five:
   - Legend performs a random exaggerated karate attack on the sibling;
   - award one dojo stripe;
   - reset the streak to zero;
   - continue playing.

### Wrong answer or timeout

1. Reset the current streak to zero.
2. The sibling performs a funny counterattack on Legend.
3. Keep showing the original multiplication fact without revealing its answer.
4. Require the player to keep guessing until she enters the correct answer, with no time limit.
5. Do not count the correction toward her streak or timed accuracy.
6. Reinsert that fact after 2–4 other timed questions.
7. Keep it in the priority-review queue until she later answers it correctly within the time limit.

If the player enters another wrong answer during correction, keep the untimed correction screen active with neutral encouragement and without another attack or answer reveal.

A delayed retry uses the same displayed orientation that the player missed. When she later answers it correctly under time, it counts toward the current streak like any other timed answer, clears that unresolved review item, and receives a distinct “fact defeated” celebration.

## Play structure and progression

- V1 is continuous play rather than a complicated match or lives system.
- Provide a clear pause/finish control so a session can end at any time.
- Every successful five-question streak awards one stripe.
- Five stripes promote Legend to the next belt and clear the stripe row.
- Proposed belt order: White, Yellow, Orange, Green, Blue, Purple, Red, Brown, Black.
- Black is the v1 belt cap. Additional stripes may continue accumulating cosmetically without adding ranks.
- Persist total successful streaks, belt, stripes, and per-fact learning data between sessions.
- After the Legend's attack finishes, pause play for a full reward ceremony showing either “Stripe Earned!” or “New Belt Earned!”, the updated belt, and progress toward the next belt. The next timed fact starts only after “Keep Fighting!” is pressed.
- A later play session begins with a small number of unresolved missed facts mixed into the opening questions.

The belt thresholds and presentation are tunable during testing; the five-correct attack rule is the central mechanic.

## Fact selection

- Cover multiplication facts with factors from 0 through 9.
- Store commutative pairs under one canonical key (for example, `6x7`) while presenting both `6 × 7` and `7 × 6`.
- Do not use a purely uniform random draw.
- Allow at most one ×0 or ×1 fact in any five-question window so easy facts cannot dominate streaks.
- Prioritize, in order:
  1. unresolved facts missed in the previous session;
  2. a missed fact due for its delayed retry;
  3. facts with low timed accuracy or slow correct responses;
  4. facts not seen recently;
  5. already-strong facts for mixed review.
- Prevent immediate duplicates unless the player is on the required correction screen.
- Schedule a delayed retry into an exact slot 2–4 timed questions after the miss. If multiple retries become due together, present them FIFO by original miss time.
- If a delayed retry is missed again, restart its 2–4-question delay from that new miss.
- Bias the questions between a miss and its delayed retry toward facts the player has previously answered well, helping her rebuild momentum without changing the retry rule.

V1 may expose a parent-only fact-family selector if testing shows that practicing all families at once is overwhelming. The default scope can be adjusted without changing the core game loop.

## Feedback and animation

- Treat attacks as affectionate comic slapstick, not realistic fighting.
- Use quick animations so learning flow is not interrupted for more than about two seconds.
- Rotate multiple Legend attacks, sibling counters, comic words, and sound effects to reduce repetition.
- A fifth-streak question should feel special: visually charge Legend's move before the answer.
- The fifth-streak charge occurs before the question appears and before its timer starts. If the player misses or times out, the charge fizzles comically and the sibling counterattacks normally. Whether this advance warning adds too much pressure is explicitly tunable after watching the player play.
- Wrong feedback should remain neutral and encouraging; avoid shame language or a harsh game-over state.
- Include a sound toggle. Under reduced-motion preferences, replace spins and large knockbacks with a simpler lunge, recoil, and impact flash so the core attack remains legible on phones.
- V1 needs only two Legend attack animations and two sibling counterattack animations; more variety is a later enhancement.

## Saved progress

Use one versioned `localStorage` document under `legendsMathDojo.v1`.

Save:

- schema version;
- current belt and stripe count;
- total timed questions and successful streaks;
- per canonical fact: attempts, timed correct answers, misses, timeouts, up to the five most recent response times, last seen time, and review priority;
- unresolved missed-fact queue;
- sound preference.

Do not save a partial correction as though the fact were successfully recalled. If a session closes during correction, keep that fact in the next-session review queue.

If the page reloads or closes while a timed question is active, reset the live streak to zero and add that fact to the unresolved review queue. Reloading must never become a way to skip a difficult fact.

## Controls and diagnostics

- V1 uses a fixed fifteen-second timer with no visible parent/settings screen, preventing the player from changing the difficulty.
- The child-facing controls are limited to sound, number entry, submit, and Finish.
- Per-fact accuracy, response time, and review data are still saved internally so they can be inspected or exposed in a later parent-only design.
- Timer adjustment, progress reset, and focused fact-family selection are deferred until there is an adult-only access method worth adding.

## Visual assets

Expected raw uploads:

- `assets/raw/player.*`
- `assets/raw/sister.*`
- `assets/raw/brother.*`

Raw photos remain local and ignored by git. After the visual direction is chosen, create approved transparent cutouts or cartoon avatars in `assets/processed/` for the game.

Public deployment of the processed child cutouts and sibling relationships was approved for phone testing on August 19, 2026. This approval does not include the raw source photos, which must remain local and ignored.

## V1 implementation sequence

1. Receive and inspect the three source photos.
2. Create real-photo idle cutouts plus one clear action pose for Legend and each sibling.
3. Build the question, timer, input, correction, streak, and adaptive-review state machine.
4. Add realistic belt/stripe rendering and persistence.
5. Add attacks, counters, sound, and reduced-motion alternatives.
6. Test keyboard, touch, refresh/resume, missed-fact scheduling, and corrupted/old saved data.
7. Watch the player play; tune timer, question mix, animation length, and belt pacing based on observation.
8. Prepare the GitHub repository and Pages deployment after approval. The first commit must already contain the raw-photo `.gitignore` rule; never add and later remove a raw photo.

## V1 acceptance checks

- Physical digits, Backspace, and Enter work without extra clicks.
- On-screen keypad works comfortably on a phone-sized viewport.
- Answers submit only through Enter or the on-screen submit control; a partial or complete unsubmitted input at expiry is a timeout.
- A correct answer inside fifteen seconds advances the streak exactly once.
- The fifth consecutive timed correct answer triggers exactly one Legend attack and one stripe.
- Every earned stripe or belt opens a clear post-attack reward ceremony before the next question begins.
- Wrong answers and timeouts reset the streak and trigger exactly one sibling counterattack.
- Correction is untimed, mandatory, cannot advance the streak, and never reveals the answer.
- Additional wrong entries during correction keep the correction active without causing extra counterattacks.
- A missed fact returns after 2–4 intervening questions and remains prioritized next session until recalled correctly under time.
- Refreshing during a live timed question resets the streak and queues that fact for review rather than skipping it.
- Refreshing or reopening preserves belts, stripes, learning history, and unresolved review facts.
- The app remains usable with sound off and reduced motion enabled; reduced-motion mode still provides a clear lower-motion attack and streak celebration.
- Raw photos are absent from git history and the deployed site, including as base64 or other embedded data inside HTML, CSS, or JavaScript.

## Deferred beyond v1

- Cloud accounts, SQL, or cross-device synchronization
- Multiple child profiles
- Competitive leaderboards
- Elaborate matches, health bars, or game-over mechanics
- Additional minigames
- Online sharing of scores
