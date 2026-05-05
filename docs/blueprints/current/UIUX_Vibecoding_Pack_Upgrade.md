# UI/UX Vibecoding Pack Upgrade

Date: 2026-05-03
Status: Applied to local `ui-ux-design` skill

## Why The First Front Felt Weak

The first Eden Front MVP proved the technical path, but the visual result was disappointing because the design judgment happened inside the implementation step.

The failure was not mainly React, Three.js, or component choice. The failure was the absence of:

- reference teardown
- visual position
- lookdev before code
- strong design tokens
- motion quality gates
- screenshot-based critique before declaring completion

Codex can implement high-quality UI, but it needs a better operating contract.

## New Working Rule

For high-fidelity UI, Codex should not begin by coding the final screen.

It should first produce:

1. visual intent
2. reference teardown
3. stack choice
4. design tokens
5. motion system
6. QA gates

Only then should it implement.

## Recommended Stack

Core app UI:

- React / Vite or Next.js
- Tailwind CSS or tokenized CSS
- shadcn/ui for accessible app primitives
- Radix primitives when building lower-level controls
- lucide-react for icon consistency

Animated interface layer:

- Magic UI for selected high-polish effects
- SmoothUI, Aceternity, React Bits, or 21st.dev as references or copy-paste component sources
- Motion for React UI transitions and micro-interactions
- GSAP for timeline and scroll orchestration

Overlay Pet / cinematic motion layer:

- Three.js / React Three Fiber / GLSL for real-time visuals
- Theatre.js for keyframed Three.js or complex variable animation
- Blender or TouchDesigner for lookdev and prerendered high-fidelity motion
- Spline for fast 3D scene prototyping
- Rive or dotLottie for small stateful vector animations; use one Overlay Pet identity rather than multiple route-specific variants

## Magic UI Positioning

Magic UI is useful, but it is not the whole design strategy.

Use it for:

- one signature effect
- one supporting effect
- text reveal or subtle background detail
- component source-code reference

Do not use it for:

- entire app visual identity
- Overlay Pet surface replacement
- heavy operational panels
- multiple simultaneous high-motion effects

Important Magic UI candidates:

- Orbiting Circles: integration/ecosystem visual
- Animated Beam: flow/automation visual
- Magic Card, Glare Hover, Shine Border, Border Beam: subtle premium panel treatment
- Particles, Light Rays, Noise Texture: background atmosphere with restraint
- Blur Fade, Text Animate, Typing Animation: controlled text motion

## Overlay Pet-Specific Recommendation

The Overlay Pet should be handled as a separate motion product.

Best path:

```txt
Reference lock
-> Blender/TouchDesigner/Spline lookdev
-> prerendered or realtime prototype
-> WebGL overlay/state system
-> screenshot/FPS/mobile QA
-> integrate into Eden Front
```

Default target:

```txt
Overlay Pet = one lookdev-matched base identity + runtime state animation
```

This gives better odds of Dribbble-level optical quality than code-only shader exploration.

## Updated Skill Pack Gates

The local `ui-ux-design` skill now requires these gates for high-fidelity UI:

1. Design Intent Gate
2. Reference Teardown Gate
3. Stack Selection Gate
4. Design System Gate
5. Composition Gate
6. Implementation Gate
7. Screenshot QA Gate
8. Red Team Gate

## Eden Front Next Design Direction

Before redesigning the front:

- collect 5-10 references
- choose one Overlay Pet visual family: companion core, living membrane, soft machine, energy creature, or orbital intelligence
- define what Eden should feel like in the first 3 seconds
- decide whether the first version uses real-time WebGL, prerendered video, or hybrid
- rebuild the shell using fewer panels, stronger hierarchy, better spacing, and a dedicated visual centerpiece

## Source Notes

- Magic UI: https://magicui.design/
- Magic UI GitHub: https://github.com/magicuidesign/magicui
- Magic UI MCP: https://magicui.design/docs/mcp
- shadcn/ui components: https://ui.shadcn.com/docs/components
- Motion React docs: https://motion.dev/docs/react-motion-component
- Rive state machines: https://rive.app/docs/runtimes/web/state-machines
- Spline: https://spline.design/
- GSAP docs: https://gsap.com/docs/v3/
- Theatre.js: https://www.theatrejs.com/
- dotLottie Web: https://developers.lottiefiles.com/docs/dotlottie-player/dotlottie-web/
- Blender command line: https://docs.blender.org/manual/en/dev/advanced/command_line/arguments.html
- Shader Park: https://docs.shaderpark.com/
- Dribbble motion references: https://dribbble.com/tags/orb
