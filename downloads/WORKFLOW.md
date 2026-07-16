# The Last Lantern — Replication Workflow

How a 45-second AI-animated short gets made, start to finish. Seven phases, in order. The single rule that makes it all work: **lock your references before generating a single shot**, then pass those same references into every image and every video.

## Tools

- **GPT Image 2** — reference sheets and keyframes (2K, 16:9, image references locked)
- **Seedance 2.0** — 15s multishot video generation with start-image + reference images
- **A TTS voice** — narrator voiceover (any quality storyteller voice)
- **ffmpeg** — assembly, audio mixing, captions, final encode

## Phase 1 — Story lock

1. Write the story as a 12-shot list with timecodes: 3 acts x 4 shots x ~3.75s = three 15s sequences.
2. Give each shot ONE action and ONE camera move. If a shot needs two, split it.
3. Fix screen geography now: pick a left-to-right route through your world and never violate it.
4. Freeze this. Everything downstream quotes it.

## Phase 2 — Environment sheet

1. Generate a single 16:9 ENVIRONMENT MODEL SHEET: 5-6 labeled views of the world, material studies, a color swatch strip, and a route/landmark plan.
2. No characters on it — world only.
3. Generate 2-4 variations, pick one, and that image becomes canon (WHERE).

## Phase 3 — Object sheet

1. Same treatment for the hero prop: turnaround views, functional states (off -> partial -> on), component callouts, a power/causality diagram.
2. The states matter most — video models need to see what "broken" vs "working" looks like.
3. Pick one variation. That image becomes canon (WHAT). Character sheets, if not already made, get the same process (WHO).

## Phase 4 — 12 keyframes with locked refs

1. Build one reusable style prefix: art style, aspect ratio, palette, plus verbatim character identity blocks. Repeat it in EVERY keyframe prompt — never paraphrase it.
2. Append a short per-shot insert: one action, framing, the camera move the frame must support, lighting state.
3. Attach ALL reference sheets (characters, environment, object) to every generation.
4. Generate 2-4 variations per keyframe. Audit each against a continuity checklist (hair, outfit, prop design, geography direction, light state) before approving.
5. You need 3 approved anchors minimum — one per 15s sequence — but approving all 12 keeps the edit honest.

## Phase 5 — 3x15s Seedance multishot

1. One prompt per 15s sequence: 4 timed camera segments with hard cuts, a SUBJECT block restating character identity, and an SFX block (diegetic only, no music).
2. Pass `--start-image` = the approved keyframe that opens the sequence, plus all reference sheets as `--image` inputs.
3. Preview in fast mode first. Only re-render in std 1080p once the fast pass survives the continuity audit.
4. If identity or geography drifts: regenerate with the identity block strengthened, or re-anchor from a cleaner keyframe. Don't try to fix drift in the edit.

## Phase 6 — Edit + diegetic sound

1. Assemble the three sequences in ffmpeg; trim dead frames at the joins so motion carries across cuts.
2. Keep the generated diegetic audio as the base layer. Patch weak moments with foley; keep it music-free so the VO owns the emotional register (score is optional, added last, low).

## Phase 7 — VO + captions

1. Generate the narrator lines with TTS; keep the middle chase silent — sparse VO reads as confidence.
2. Place each line at its scripted timestamp; sidechain-duck the diegetic bed under the voice.
3. Burn or sidecar captions matched to the VO windows. Export final master.

## Batching tips

- **2-4 variations per image, always.** The first render is a draft, not a decision.
- **Audit against a written continuity checklist** after every generation — invariants like hair color, scarf, prop mechanism, route direction, lighting state. Drift compounds; catch it at the frame, not in the film.
- **Fast mode before std.** Preview every video prompt cheap, then pay for 1080p only on prompts that already work.
- **Never regenerate references.** If a sheet is canon, it stays canon for the whole production.
