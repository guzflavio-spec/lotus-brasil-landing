# Prompt playbook

The agency's own rules for AI image and video prompts. Distilled from the
community libraries in `sources/` plus hands-on analysis of a 15 s vertical ad.

## Formula (video)

`[Shot/camera] + [Subject] + [Action] + [Setting] + [Lighting/style] + [Audio] + [Constraints]`

1. **One action and one camera move per shot.** Five to eight seconds per clip.
2. **Name the format**: `9:16`, duration, "handheld selfie, front phone camera at arm's length".
3. **Lock identity**: reuse the same reference image and the same subject sentence in every shot.
4. **Camera vocabulary** the models understand: POV, eye-level, handheld sway, whip pan
   (give direction and "motion blur at midpoint"), low-angle, push-in, orbit.
5. **Audio line**: ambient sounds, dialogue as `She says: "..."`, and `no music` when you add it later.
6. **Constraints at the end**: "no text, no logos, no morphing, same clothing and layout".
7. **Negative prompts**: list what you don't want ("wall, frame"), not "no walls".
8. Veo takes **English prompts only**. Write the dialogue in the language you need inside quotes.

## Structure of a 15 s social ad

| Time | Beat | Made with |
|---|---|---|
| 0-3 s | Hook: expressive face or POV selfie | AI video clip |
| 3-9 s | Reveal or proof: whip pan to the key visual | AI video clip |
| 9-12 s | Payoff: close, reaction, energy | AI video clip |
| 12-15 s | End card: one line, one CTA | Editor (not AI) |

## Workflow

1. Keyframe image first (9:16), approve it.
2. Image-to-video per beat, 2-3 takes each, pick the best.
3. Stitch with hard cuts on the whip pan. Add captions and the end card in the editor.
4. Export 9:16 1080p. Upscale only if the platform needs it.

## Pipeline for event recaps ("postcards")

Use real event photos as the first frame (image-to-video), 3-4 s per clip, light
camera moves, shared music bed, one caption card at the end. This keeps it authentic
and cheaper than generating people.

## QA checklist

- Face and wardrobe identical across clips
- Readable on-screen text only where you added it in the editor
- No invented logos or brand marks
- Audio levels consistent, captions on
- Rights: licence of any source prompt respected (see `ATTRIBUTION.md`)
