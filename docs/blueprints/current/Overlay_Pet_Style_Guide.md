# Overlay Pet Style Guide

Date: 2026-05-06

## Purpose

The Overlay Pet is the single visible identity of Eden Agent.

It should feel like a small always-present AI companion that can think, listen, work, warn, and recover without becoming a full chat window or a decorative mascot.

## Non-Negotiables

```txt
1. One external appearance only.
2. Eden, Jarvis, and Hybrid are internal routes, not visual identities.
3. No separate bodies, skins, costumes, route colors, badges, or mode labels.
4. The Pet must read clearly at 72px, 96px, and 128px.
5. It must look good as a still image before any animation is added.
6. It must support animation through posture, glow, expression, breathing, and small accessory motion.
7. It should feel alive, but not childish, noisy, or game-like.
```

## Desired Essence

```txt
quiet intelligence
compact presence
soft machine
living glow
calm readiness
premium desktop companion
trustworthy executor
```

The Pet should sit between these references:

- not a generic chatbot avatar
- not a toy robot
- not a corporate assistant logo
- not a fantasy creature
- not an orb
- not a full humanoid

## Form Direction

Preferred base form:

- compact floating body
- rounded head/core
- tiny body or lower capsule mass
- clear face plane or expression zone
- subtle ear/halo/cloud/collar silhouette only if it improves recognition
- no hands unless they are tiny, simple, and useful for readable gestures

The silhouette should remain recognizable when reduced to a small overlay.

## Face Language

The face is the main social interface.

Allowed:

- two small luminous eyes
- minimal mouth only if needed
- eyelid changes
- blink
- gaze shift
- calm attention expression
- working concentration expression

Avoid:

- human mouth realism
- exaggerated cartoon emotion
- emoji face
- aggressive robot eyes
- text inside the face

## Material

The material should imply an AI-native object, not a physical toy.

Preferred:

- soft glass
- translucent shell
- velvet dark core
- inner blue-violet light
- rim glow
- mild bloom
- subtle pixel or panel detail only if it stays premium

Avoid:

- plastic toy finish
- heavy metallic robot armor
- flat sticker icon style
- excessive gradients that blur the silhouette
- noisy surface detail

## Color

The default identity should use a narrow but not one-note palette.

Base:

- deep graphite or black core
- electric blue inner light
- soft violet secondary glow
- tiny cyan highlights

Accent:

- warm amber only for approval/attention
- red-orange only for blocked/error pressure

Color must not imply Eden/Jarvis/Hybrid route selection.

## State Mapping

The same Pet changes state through animation and expression.

| State | Visual Treatment |
| --- | --- |
| idle | slow breathing, calm glow, neutral eyes |
| listening | eyes attentive, slight forward posture, soft pulse |
| thinking | gaze narrows, glow gathers inward, micro-orbit or halo drift |
| speaking/texting | face brightens, eye rhythm or light waveform, communication cadence |
| working | stronger internal light, subtle body compression, tool-like cadence |
| approval | amber edge attention, still calm, no modal-looking badge |
| blocked/error | reduced motion, red-orange tension, visible constraint without alarmism |
| done | short release glow, relaxed return to idle |

## Scale Rules

At 72px:

- silhouette must be clear
- eyes must be readable
- glow cannot swallow the body
- no fine line details should be required

At 96px:

- expression should be readable
- body/core material should be visible

At 128px:

- premium surface quality should become visible
- animation detail can appear without changing identity

## Prompting Direction

Start with concept sheets instead of final production assets.

Generate:

- 12-20 still candidates
- dark neutral background for review
- no text labels
- consistent scale and spacing
- premium 3D/stylized rendering

Then select 1 candidate and generate:

- front view
- 3/4 view
- expression sheet
- idle/listening/thinking/speaking-texting/working/approval/blocked-error/done stills
- transparent-background export candidates

After state stills are approved:

- use each approved state still as the source image for image-to-video generation
- generate short state loops
- reject loops that drift from the locked Pet identity
- export approved loops for the Swift overlay runtime

## Rejection Criteria

Reject any candidate that:

- looks like a generic orb
- looks like a cheap mobile game mascot
- needs a label to be understood
- cannot be recognized at 72px
- uses separate route colors or route costumes
- has too much facial emotion for a work assistant
- looks too much like an existing branded character
- cannot plausibly animate through small state changes

## First Concept Target

```txt
A compact floating AI companion pet with a dark translucent core, blue-violet inner glow, tiny luminous eyes, soft machine body language, premium desktop overlay presence, readable at small sizes, calm but alive.
```
