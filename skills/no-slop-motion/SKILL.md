---
name: no-slop-motion
description: "Launch, brand and promo films that look directed, not AI-generated, built gate by gate (pain research, script, voiceover, style frames, animatic, HyperFrames + GSAP build, music, QA, export). Use when asked for a launch or product video, for one of those layers of one, or when an AI-made video looks like slop, vibe coded or a slideshow."
---

# No-slop motion

**The agent's defaults are the slop.** Any choice the agent makes on its own (a track, a transition, a shadow, a font, where to cut the voice) looks like every other AI video. A film feels directed when every choice is **grounded**: traced to the customer's own words, the brand's own assets, the music's structure, the narrator's take, or a named reference. The gates decide where each choice comes from; the scripts enforce it.

## What makes a film work

1. **Customer truth.** Who buys (the ICP), what hurts them in their own words, and the one thing only this product does (the USP). The film sells one before and after, not a feature list.
2. **One story thread**: effect, then cause, then fix. A small mystery pulls people through a film; a feature tour doesn't ([02-story.md](references/02-story.md)).
3. **A world with its own rules**, taken from the story's feeling, so every texture, colour and transition has a reason ([04-world.md](references/04-world.md)).
4. **Brand motifs**: three to five things only this brand owns. No mascot is fine: the film follows a hero object ([05-hero.md](references/05-hero.md)).
5. **The voice sets the clock.** Narration first, one continuous take per act; picture timed to the voice; music last, edited so it still sounds like one performance.

## Before you start

Check the tools in the first session, before Gate 0. Done when every row works or its gap is reported to the decision maker (the person who approves the film).

| Need | Default | Notes |
| --- | --- | --- |
| Motion and render | [HyperFrames](https://hyperframes.heygen.com) (HTML + GSAP to MP4) | `npx hyperframes skills` installs its agent skills. Read `/hyperframes-core` before writing composition HTML. |
| Voice | [Cartesia](https://cartesia.ai) Sonic (`scripts/audio/tts-cartesia.ts`) | ElevenLabs works too. The key goes in an env var. Record a scratch voice in the first pass. |
| Music | [Suno](https://suno.com) or a licensed track | Once a track is liked, ask for continuations of it, not a fresh batch. |
| Transcription | faster-whisper or `npx hyperframes transcribe` | Word timestamps feed captions and voice splitting. |
| Audio and video tools | ffmpeg, Python 3.10+ | One `requirements.txt` per `scripts/` folder. |
| Real UI | Access to the live product, marketing site and brand files | UI gets rebuilt as HTML from the product's real CSS and copy. |

Start the project from [starter/](starter/): a HyperFrames project with a film engine (one timeline, a timing table, actors, cameras, captions, sound cues). Copy it, then read `starter/README.md`.

## Where to enter

- **A new film**: start at Gate 0.
- **Rescuing a film that exists** (it looks like slop, or keeps getting rejected): diagnose before rebuilding. Seed `LOVES-HATES.md` from every past rejection, run the Gate 9 gauntlet ([09-qa-render.md](references/09-qa-render.md)) on the current render, and sort every failure by layer: story, voice, style, motion, sound. Reopen at the earliest gate with a failure and relock forward from there.
- **One layer only** (a script, a voice, a music edit): run that gate, treating the earlier layers as locked inputs. Ask for any that are missing.

## The gates

Work in order. A gate opens when the decision maker has signed off the lock before it, and each lock uses the artefact they can judge fastest: a page of text, five stills, a rough animatic. **Lock story and style before motion.** They take the most rounds, and far more when attempted at the same time as everything else; the usual failure is a beautiful animatic of the wrong story.

| Gate | What you make | Lock | Reference |
| --- | --- | --- | --- |
| 0. Inputs | Input pack: brand truth from production, product surfaces, claims list, platform and length, 2 to 4 references with what to take from each | Pack exists; `BRIEF.md` has platform, length and references; `LOVES-HATES.md` started | [01-inputs.md](references/01-inputs.md) |
| 1. Pain and positioning | Pain bank from real customer words, one villain, 2 or 3 felt numbers, one-page brief | Brief approved | [02-story.md](references/02-story.md) |
| 2. Script | The film as spoken paragraphs per act | Words approved when read aloud | [02-story.md](references/02-story.md) |
| 3. Voice | Cast, record one take per act in 2 or 3 readings, score, split in silences | Every piece placed in `plan.js` and `vo-data.js`, whole narration heard in order. From here the voice sets the clock | [03-voice.md](references/03-voice.md) |
| 4. World and style frames | 2 or 3 world concepts, then 5 still frames for the chosen one, plus `DESIGN.md` with a banned list | Contact sheet and `DESIGN.md` approved | [04-world.md](references/04-world.md) |
| 5. Hero (parallel lane) | Mascot rig or hero object, with an expression or state sheet | Rig and sheet approved at display and thumbnail size | [05-hero.md](references/05-hero.md) |
| 6. Animatic | Every shot blocked on the VO timeline with temp music | Animatic approved and every `SHOTLIST.md` cut has a named transition. Story and timing frozen | [06-motion.md](references/06-motion.md), [07-build.md](references/07-build.md) |
| 7. Build | Scenes split into files, built by parallel agents, one owner per scene file | Picture lock: the handover checks in `07-build.md` clean, picture approved | [07-build.md](references/07-build.md) |
| 8. Sound | Cue sheet, music edited on downbeats, few SFX tuned to the key, mix | One full listen with no audible splice and every must-hit landing | [08-sound.md](references/08-sound.md) |
| 9. Final gauntlet | Independent review of every frame, sound on and muted, exports | Every gauntlet box ticked | [09-qa-render.md](references/09-qa-render.md) |

Fill the templates in [templates/](templates/) as you go: `BRIEF.md`, `PAIN-BANK.md`, `SCRIPT.md`, `DESIGN.md`, `SHOTLIST.md`, `CUE-SHEET.md`, `LOVES-HATES.md`. Each script in `scripts/` is named in the gate reference that uses it and prints its usage with `--help`.

## Standing rules

These apply at every gate.

- **Keep a loves and hates file.** After every message from the decision maker, add what they loved and what they hated to `LOVES-HATES.md`, in their words, with the fix. Re-read it before every render; it is what stops the same complaints coming back round after round.
- **Ground every choice.** Before building anything, name its source: customer words, the live brand, the music's structure, the narrator's take, or a named reference. Replace any choice that has no source with one that does.
- **Claims come from the whitelist.** A launch film is a public claim. Every spoken or written line matches the marketing site or an approved claims list. Watch for lines that promise more autonomy or speed than the product has.
- **When the feedback is "too much", cut elements and keep the life.** Corrections overshoot: "too busy" easily turns into "too minimal and dry" in one round. Keep the texture, colour and motion; remove things.
- **Batch follow-ups.** Notes arrive mid-render. Fold them all into one pass, and say which layer each one touches.
- **Name a locked layer before changing it.** If a picture change needs a new voice line, or a music edit needs a picture retime, say so first.

## Banned by default

The fingerprints of AI motion slop, each with its replacement. `DESIGN.md` copies this list and `scripts/qa/lint-slop.ts` checks it. Lift a ban only when the decision maker asks.

| Banned | Instead |
| --- | --- |
| Hard offset shadows and drop shadows on containers | A 1px border on containers; depth only on buttons |
| Radial gradients, glows, vignettes, coloured world backgrounds, checkerboard floors, corner labels | The authored palette and moving grain from `DESIGN.md` |
| Card grids and icon lists standing in for an explanation | One object, built piece by piece, marked where it matters |
| Static UI screens with no camera move, build or morph (a slide) | A camera move, build or morph in every shot |
| Text parked at the top of the frame while something else happens below | Type where the eye already is, or type that becomes the object it names |
| Hard pops: anything that appears, vanishes or flashes in one or two frames; black dips between shots | Animated entrances and exits; a named transition on every cut |
| Shader transitions that drop colour on capture; glitch transitions picked for "energy" | Match cut, camera through, morph, or the world's native transition |
| Linear moves; overshoot (`back.out`, `elastic`) on UI | `expo.out` or `power3.out` in, `power2.inOut` moves; squash and stretch for a character only |
| CSS filters (`grayscale`, `sepia`, `saturate`) faking a colour world | Authored colours |
| Customer quotes as tweet or Slack cards | The narrator says the pain; the picture shows the object |
| More than one brand-coloured call to action in a frame | Exactly one |
| A sound on every landing | Sounds only where they help a beat land, tuned to the key |
| Stitched one-line TTS clips; voice cut in the middle of a word or a sentence | One continuous take per act, split only in real silences |

## Handing over a cut

1. **Review it first.** Run the QA scripts, then have an independent subagent review the cut adversarially against `LOVES-HATES.md` and the banned list (commands in [07-build.md](references/07-build.md)). You find the pops, the mistimed captions and the cursor that misses, before the decision maker does.
2. **Send a review page or a Studio link**, not only a file: the video, a frame grid, and a short message:
   - What changed, one line per note, in the decision maker's words.
   - What to judge this round (for example "only the style frames, not the timing").
   - Anything you could not do, and why.

Time a full render in the first pass and plan review loops around it: long renders near a deadline are the most common way to run out of time ([09-qa-render.md](references/09-qa-render.md) makes them fast).
