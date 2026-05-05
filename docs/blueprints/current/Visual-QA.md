# Visual QA

Date: 2026-05-03
Status: Organic glow pass checked

## Required Checks

Before claiming a UI redesign is complete:

- desktop screenshot at 1440px width
- tablet screenshot at 768px width
- mobile screenshot at 390px width
- console error check
- no horizontal scroll
- no clipped Korean text
- no overlapping buttons/cards/panels
- no hidden approval queue
- no blank WebGL/canvas area
- reduced-motion behavior exists

## Premium Visual Checks

Ask:

- Does the still frame look intentional without animation?
- Does motion make the product easier to understand?
- Is there one visual protagonist?
- Is the Overlay Pet more than decoration?
- Are panel density, type, and spacing controlled?
- Does it avoid default AI/SaaS visual tropes?

## Evidence To Save

Save screenshot evidence under:

```txt
docs/ai/current/qa/
```

or a clearly named local QA folder.

Each QA note should include:

- viewport
- screenshot path
- observed issue
- fix decision
- residual risk

## Current QA Note

Viewport checked:

- 1440 x 1000 desktop via Playwright MCP.

Result:

- WebGL canvas is nonblank.
- activity comparison controls are visible.
- Previous broad shell UI remains removed.
- Previous custom ring, CSS voice ring, ElevenLabs blob, torus, and old particle directions remain removed.
- Current Overlay Pet uses the locally owned `ReferenceSphereOrb` shader.
- Default idle, responding, and blocked samples were checked in the browser.
- Responding is driven by synthetic speech-like audio modulation.
- `Idle`, `Responding`, and `Blocked` were visually checked on the same Pet identity.
- The page should expose activity state controls, not route-specific Pet variants.
- Screenshots saved:
  - `docs/ai/current/qa/eden-reference-sphere-idle.png`
  - `docs/ai/current/qa/eden-reference-sphere-responding.png`
  - `docs/ai/current/qa/eden-reference-sphere-blocked.png`
  - `docs/ai/current/qa/eden-layered-overlay-pet-idle-a.png`
  - `docs/ai/current/qa/eden-layered-overlay-pet-idle-b.png`
  - `docs/ai/current/qa/eden-layered-overlay-pet-responding.png`
- Idle animation was checked with two screenshots captured 1.6s apart; their SHA-256 hashes differed, confirming live frame changes.

Residual risk:

- Not all activity states have been visually tuned one by one.
- Not every state has a unique polished motion language yet; `Approval` and `Responding` need another fine-tuning pass against the speaking/texting video.
- Earlier state comparison used keyed R3F remounts plus a short canvas fade. This was replaced by a persistent canvas and shader uniform interpolation in the Motion Bible bridge pass.
- The diagonal wave and external cilia are intentionally visible to match `original-6433...`, but brightness/speed may need adjustment after user review.

## Organic Glow QA Note

Viewport checked:

- 1440 x 900 desktop via Playwright MCP.

Result:

- `npm run build` passes.
- Browser console errors: 0 after Vite dev server restart with dependency re-optimization.
- WebGL canvas is nonblank.
- Activity comparison controls were clicked successfully.
- Canvas measured approximately 534 x 534 CSS pixels.
- The temporary `EffectComposer/Bloom` approach was rejected because it produced a visible rectangular canvas boundary.
- Final approach uses shader fake-bloom, CSS glow, living membrane deformation, irregular cilia, and volumetric corona.
- Screenshots saved:
  - `docs/ai/current/qa/eden-organic-overlay-pet-idle.png`
  - `docs/ai/current/qa/eden-organic-overlay-pet-working.png`
  - `docs/ai/current/qa/eden-organic-overlay-pet-blocked.png`

## Motion Bible Bridge QA Note

Viewport checked:

- 1463 x 861 desktop via Playwright MCP.

Result:

- `npm run build` passes.
- Browser console errors: 0.
- Activity comparison controls were clicked successfully.
- Each control mapped to the expected `data-pet-activity`; route metadata is debug-only.
- Canvas remained the same DOM node across transitions, confirming state changes no longer remount the WebGL canvas.
- Canvas measured approximately 534 x 534 CSS pixels.
- Screenshot saved:
  - `docs/ai/current/qa/eden-overlay-pet-motion-bible-continuous.png`

Residual risk:

- The current shader still receives a legacy adapted state instead of the full `PetSignal`.
- The true high-end lookdev asset is not created yet; the current WebGL Overlay Pet remains a prototype renderer under the new signal and asset pipeline.
