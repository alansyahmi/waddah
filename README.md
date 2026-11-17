# Waddah | وَضَّاح

**Arabic-first caption and lyric video editor.**

Waddah turns Arabic audio and text into beautifully synchronised, typographically rich videos. It is designed for recitation, nasheeds, poetry, lectures, educational media, and other Arabic audio-first content.

> The art of Arabic audio visualisation.

## Product direction

Waddah is a browser-based editor with a timeline workflow, supporting manual and AI-assisted caption creation, phrase-level and word-level synchronisation, and optional karaoke-style highlighting. Its visual identity combines minimal contemporary design with cinematic and heritage-inspired templates.

Waddah is not intended to be a general-purpose nonlinear video editor. Its core strength is Arabic text, audio synchronisation, and elegant caption-led visualisation.

## Current status

This repository contains the product and engineering blueprint. The application is not yet implemented. Architecture and roadmap documents describe intended direction, not completed features.

## Documentation

- [Product requirements](docs/PRD.md)
- [Architecture](docs/ARCHITECTURE.md)
- [Data model](docs/DATA_MODEL.md)
- [Arabic text engine](docs/ARABIC_ENGINE.md)
- [Audio and synchronisation](docs/SYNCHRONISATION.md)
- [Rendering and export](docs/RENDERING.md)
- [Roadmap](docs/ROADMAP.md)
- [Testing strategy](docs/TESTING.md)
- [UX and visual design](docs/UX_SPEC.md)
- [Decision log](docs/DECISIONS.md)
- [Codex implementation guide](AGENTS.md)

## Planned technology

React, TypeScript, Vite, Tailwind CSS, Zustand, IndexedDB/Dexie, Web Audio API, WaveSurfer.js or a custom waveform renderer, Canvas/SVG/DOM text rendering, and browser-native video encoding with WebCodecs/Mediabunny where supported.

Cloudflare Pages, Workers, D1, and R2 are candidates for the later hosted product. The first milestone is local-first and browser-based.

## Guiding principles

1. Arabic text integrity is a first-class requirement.
2. Preserve source text; never silently normalise or rewrite religious text.
3. Manual editing must remain useful without AI.
4. Phrase and word timing are two levels of one coherent caption model.
5. Preview and export must share the same timeline evaluation and rendering logic.
6. Prefer a small, testable MVP over premature infrastructure.
7. Clearly disclose browser capability and export-format limitations.

## Development

The initial implementation should begin with the browser application and a small number of well-defined core modules. Do not create every proposed package as a separately buildable workspace until real code boundaries justify it.

See [AGENTS.md](AGENTS.md) before asking an agent to implement a milestone.
