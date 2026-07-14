# The Last Lantern — Kai &amp; Miko

A 45-second AI-produced animated short. A boy chases a fox for a stolen ember, and finds a friend trying to relight the village's last dark beacon. A wordless story of misread intentions and belonging, above the clouds.

**▶ Watch + full breakdown:** https://atefiqbal.github.io/kai-and-miko-the-last-lantern/

This single-page site contains everything: the film (four cuts — narrated+captioned, wordless, scored), the environment &amp; beacon reference sheets, the 12 storyboard keyframes, the voiceover script, the production pipeline, and the complete prompt archive.

## The film
- 45s · 1080p · 16:9 · three 15-second Seedance 2.0 sequences (The Theft / The Revelation / The Light)
- Kai — cheerful ~10yo boy; Miko — a small, clever fox. Both preserved on-model across every frame.

## How it was made (storyboard-first)
1. Locked the story around one readable conflict — a "theft" that's really a rescue.
2. Built an **environment sheet** and a **beacon object sheet** so world + prop logic were fixed before animation.
3. Generated **12 keyframes in GPT Image 2** (2K), each referencing the locked character/world/prop sheets.
4. Animated **three 15-second Seedance 2.0 multishot clips** from those keyframes (diegetic sound).
5. Edited, sound-designed, then added a spare narrator voiceover + on-screen script; a HyperFrames composition rendered the captioned master.

Tools: GPT Image 2 · Seedance 2.0 · Seed Audio (TTS) · HyperFrames · ffmpeg.

Made for the $100 weekly animation challenge — "Kai &amp; Miko, An Animated Short."

_Site pattern adapted from github.com/thariqs/html-effectiveness._
