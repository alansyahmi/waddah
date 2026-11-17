# UX and Visual Design Specification

## Product character

Waddah should feel like a focused creative instrument: Arabic calligraphic elegance combined with modern creator software. It should be calm and legible during detailed timing work, while allowing expressive cinematic output.

The product itself should not be visually overloaded with ornamental motifs. Heritage-inspired decoration belongs primarily in optional templates.

## Brand direction

- Working name: Waddah / وَضَّاح.
- Root: و-ض-ح, associated with clarity and becoming clear.
- The name is a brand identity, not a literal Arabic translation of caption or subtitle.
- Product scope remains Arabic-first but is not restricted to religious media.
- Tagline direction: “The Art of Arabic Audio Visualisation.”

Suggested palette direction: parchment/ivory, midnight, muted sage, antique gold, and bronze. Establish accessible contrast tokens during implementation rather than hard-coding decorative colours.

## Editor layout

Five functional regions:

1. **Top toolbar:** project name, undo/redo, save state, preview quality, aspect ratio, export.
2. **Left tool panel:** Text, Audio, Styles, Media, Effects.
3. **Preview canvas:** composition at the selected output ratio; direct caption positioning and resizing where practical.
4. **Inspector:** contextual controls for typography, alignment, colour, animation, audio, background, and selected timeline object.
5. **Timeline:** audio track, caption track, visual/background track; phrase segments can reveal nested word timings.

The timeline is a primary editing surface, not a decorative strip. It should support zoom, scroll, scrubbing, drag/resize, split/merge, snapping, multi-select, and keyboard shortcuts over time.

## Synchronisation workspace

Provide a focused mode that makes audio playback, waveform, selected phrase, and marking controls prominent. Users should be able to mark phrase boundaries without navigating a complex inspector. Word timing can be expanded when needed.

## Templates

Initial template directions:
- **Naskh Classic:** readable traditional Arabic typography.
- **Minimal Ivory:** restrained, bright, editorial composition.
- **Midnight Gold:** dark cinematic palette with gold accents.
- **Andalusian:** geometric/architectural influence used sparingly.
- **Sufi Heritage:** contemplative, restrained visual language.
- **Modern Kinetic:** contemporary motion and progressive word highlighting.

These are design directions, not historical or religious authenticity claims. All templates should be editable configurations.

## Output presets

- Vertical: 1080×1920, for short-form video.
- Landscape: 1920×1080, for YouTube and widescreen.
- Square: 1080×1080, for square social posts.
- Start with 30 FPS. 60 FPS can follow after export stability.

## Accessibility and usability

- Strong contrast and readable control labels.
- Keyboard-accessible editing and timeline operations.
- Do not communicate state by colour alone.
- Respect reduced-motion preferences in the editor UI.
- Keep Arabic text direction explicit and avoid ambiguous mixed-direction controls.
- Provide tooltips for less familiar timeline actions.
- Make save status, export status, and unsupported media errors visible.
