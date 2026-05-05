# Overlay Pet Image Prompt Pack

Date: 2026-05-06

## Use

This prompt pack is for GPT Image concept exploration.

The goal is not final runtime animation. The goal is to discover the Pet's silhouette, face language, material, and emotional baseline.

## Global Rules

```txt
One AI companion identity only.
No Eden/Jarvis/Hybrid labels.
No separate route colors.
No text, captions, logos, watermarks, UI panels, or speech bubbles.
No orb-only design.
Must read as a small always-on desktop overlay companion.
Premium, calm, intelligent, alive.
```

## Prompt 01: First Concept Sheet

```txt
Use case: stylized-concept
Asset type: early concept sheet for a Swift-native always-on desktop overlay AI companion
Primary request: Create a 4x4 concept sheet of sixteen compact floating AI companion pet designs. Each candidate should be a small premium desktop assistant character, not a full robot and not an orb. The design should feel like quiet intelligence, soft machine, living glow, calm readiness, and trustworthy execution.
Scene/backdrop: dark neutral studio background, evenly spaced candidates, no captions, no labels, no UI.
Subject: one small floating AI companion pet per cell, rounded head or core, tiny body or lower capsule mass, readable luminous eyes, subtle blue-violet inner glow, deep graphite or dark translucent shell, soft rim light, premium 3D stylized render.
Composition: 4x4 grid, each candidate centered, generous spacing, front or slight 3/4 view, no text.
Style: high-end 3D icon concept art, polished, soft glass, luminous core, gentle bloom, clean silhouette, desktop overlay friendly.
Constraints: one external identity direction only; no route labels; no Eden/Jarvis/Hybrid marks; no badges; no speech bubbles; no human face; no toy plastic; no aggressive robot; no existing branded character; no pure orb.
Quality bar: each candidate must be recognizable at 72px, 96px, and 128px.
```

## Prompt 02: Chosen Candidate Refinement

```txt
Use case: stylized-concept
Asset type: refined character design for a Swift-native desktop overlay AI companion
Primary request: Refine the selected Overlay Pet candidate into one cohesive character. Keep it compact, floating, premium, calm, and alive.
Scene/backdrop: dark neutral studio background, no UI, no text.
Subject: one small floating AI companion pet, rounded translucent graphite shell, blue-violet inner light, readable tiny luminous eyes, subtle soft-machine body, minimal appendages only if they improve gesture readability.
Composition: one front view, one 3/4 view, and one small-size preview at 72px/96px/128px shown visually without labels.
Style: premium 3D stylized render, soft glass, inner glow, mild bloom, crisp silhouette.
Constraints: no route-specific design, no costumes, no badges, no captions, no orb-only form, no toy-like plastic.
```

## Production Direction

The production path is:

```txt
1. Choose and lock one Pet appearance.
2. Generate state-specific still images with GPT Image.
3. Use those state stills as image-to-video sources.
4. Generate short state loops with Grok/Veo/Sora-class video models.
5. Convert approved loops into runtime assets for the Swift overlay.
```

Do not generate state videos from text alone. The video model should receive the locked Pet still image for the target state so identity drift is reduced.

## State Set

Canonical state stills:

```txt
idle
listening
thinking
speaking-texting
working
approval
blocked-error
done
```

Runtime may split `speaking-texting` later if voice and text need different motion timing. For the first visual pass, keep them together.

## Prompt 03: State Still Sheet

```txt
Use case: stylized-concept
Asset type: expression and state sheet for one Overlay Pet character
Primary request: Create a state still sheet for the same compact floating AI companion pet across eight states: idle, listening, thinking, speaking/texting, working, approval, blocked/error, done. The same body and identity must remain consistent in every pose.
Scene/backdrop: dark neutral studio background, no text, no labels.
Subject: the same small floating AI companion pet in each state, with state changes expressed only through eyes, posture, glow intensity, subtle halo/orbit energy, and body compression.
Composition: 2x4 grid, consistent scale, no captions.
Style: premium 3D stylized render, soft glass, luminous blue-violet core, restrained glow.
Constraints: no route labels, no different costumes, no different color families, no UI bubbles, no speech bubbles, no exaggerated cartoon emotion.
```

## Prompt 04: Individual State Still

Use this after one Pet appearance is locked. Replace `<STATE>` and `<STATE_DIRECTION>`.

```txt
Use case: stylized-concept
Asset type: state still source for image-to-video generation
Primary request: Create the locked Overlay Pet character in the <STATE> state. Preserve the exact same character identity, silhouette, material, face language, and color system from the chosen reference. Express the state only through eyes, posture, glow intensity, small halo/orbit energy, and body compression.
State direction: <STATE_DIRECTION>
Scene/backdrop: dark neutral studio background, no text, no UI, no labels.
Subject: one small floating AI companion pet, dark translucent shell, blue-violet inner glow, readable tiny luminous eyes, crisp silhouette, generous padding.
Composition: centered full body, front view, no crop.
Style: premium 3D stylized render, soft glass, luminous core, restrained bloom, desktop overlay friendly.
Constraints: no route labels, no different costume, no badge, no speech bubble, no captions, no watermark, no human face, no pure orb, no exaggerated cartoon emotion.
```

State directions:

```txt
idle: calm breathing posture, neutral eyes, soft steady glow, relaxed readiness
listening: attentive eyes, slight forward posture, gentle outward pulse, receptive presence
thinking: inward-focused eyes, glow gathers toward core, subtle halo/orbit tension, quiet concentration
speaking/texting: face light rhythm, eyes engaged, small waveform-like glow motion implied, clear communication energy
working: stronger internal light, compressed focus posture, precise tool-like cadence implied, active execution
approval: warm amber edge attention, still calm, waiting for user decision without alarm
blocked/error: reduced motion posture, red-orange tension at edges, constrained but not panicked
done: relaxed release glow, softened eyes, subtle completion sparkle, return-to-idle readiness
```

## Prompt 05: Chroma-Key State Still Export

Use this only after a state still is approved and a transparent-ready source is needed.

```txt
Use case: stylized-concept
Asset type: transparent-ready state still source for a desktop overlay companion asset
Primary request: Create the locked Overlay Pet character in the <STATE> state as a single centered asset on a perfectly flat solid #00ff00 chroma-key background for background removal. Preserve the exact same character identity, silhouette, material, face language, and state treatment from the approved state still.
Scene/backdrop: perfectly flat solid #00ff00 background with no shadows, no gradients, no floor plane, no texture, no reflection, and no lighting variation.
Subject: one small floating AI companion pet, crisp edges, generous padding, no crop.
Composition: centered full body, front view.
Style: premium 3D stylized render, crisp silhouette, restrained bloom that does not contaminate the green background.
Constraints: do not use #00ff00 anywhere in the subject; no text, no watermark, no UI, no cast shadow, no contact shadow, no reflection.
```

## Prompt 06: Image-To-Video State Loop

Use this in Grok/Veo/Sora-class video generation after a state still is approved.

```txt
Use case: image-to-video
Asset type: short seamless state loop for a Swift-native desktop overlay AI companion
Input image: approved Overlay Pet <STATE> still
Primary request: Animate this exact Overlay Pet in the <STATE> state as a short seamless loop. Preserve the same identity, silhouette, material, face, colors, and camera angle. The motion should feel organic, premium, and alive while remaining subtle enough for an always-on desktop overlay.
Motion direction: <MOTION_DIRECTION>
Camera: locked camera, no zoom, no pan, no rotation.
Background: keep the same clean background or transparent/chroma-key-ready background if supported.
Duration: 4-8 seconds for first pass; later normalize runtime loops to a consistent duration if needed.
Style: high-end soft-machine motion, gentle glow, smooth easing, no jitter, no sudden cuts.
Constraints: no new objects, no text, no UI, no speech bubble, no route labels, no costume change, no camera movement, no identity drift, no full-body transformation.
Loop requirement: first and last frame should be visually close enough for a seamless loop or crossfade loop.
```

Motion directions:

```txt
idle: slow breathing, tiny hover drift, steady soft glow
listening: gentle outward listening pulse, tiny head/core tilt, attentive eye blink
thinking: inward glow accumulation, slow orbit/halo drift, focused micro-compression
speaking/texting: rhythmic face light and subtle waveform-like glow, conversational cadence without mouth realism
working: precise stronger pulse, small energetic compression/release, controlled execution rhythm
approval: calm amber attention pulse, held posture, waiting tension without alarm
blocked/error: restrained red-orange edge tension, small stutter-like resistance, no panic
done: brief release shimmer, relaxed exhale, settles back toward idle
```

## Initial Generation Prompt

Use Prompt 01 first.
