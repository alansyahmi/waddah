# Codex and AI Agent Instructions

This file defines the working contract for coding agents in this repository.

## Mission

Build Waddah: an Arabic-first browser-based caption and lyric video editor. The product combines Arabic text editing, audio playback, phrase/word synchronisation, timeline editing, visual templates, preview, and browser-based export.

Read the relevant documents in `docs/` before implementing a feature. The PRD defines product scope; architecture and domain documents define intended boundaries.

## Non-negotiable engineering principles

- TypeScript strict mode. Avoid `any`; use runtime validation at untrusted boundaries.
- Keep domain logic independent of React components and browser UI state.
- Store timeline time as integer milliseconds. Avoid floating-point time as the canonical persisted representation.
- Keep phrase segments and their optional word timings in one coherent model.
- Preserve original Arabic Unicode text and diacritics. Never destructively strip tashkeel, Quranic marks, or punctuation.
- Any normalised text must be a separate derived representation with a documented purpose.
- Do not silently alter Quranic, Hadith, or other authoritative religious text. AI output is a draft requiring human verification.
- Do not claim that a text is authenticated merely because it was transcribed or aligned.
- Preview and export must use the same scene/timeline evaluation rules.
- Keep browser capability detection explicit. Do not promise MP4 or WebCodecs support without checking the runtime.
- Prefer local-first functionality. Do not require accounts or cloud services for the initial manual editor.
- Avoid adding infrastructure, dependencies, or abstractions without a demonstrated need.
- Do not commit secrets, credentials, private user media, or large test recordings.

## Implementation workflow

1. Inspect the current repository and existing code before changing anything.
2. Read the relevant PRD/architecture sections and identify the acceptance criteria.
3. State a short implementation plan for non-trivial tasks.
4. Implement the smallest coherent vertical slice.
5. Add or update unit, integration, and browser tests as appropriate.
6. Run formatting, linting, type checking, and tests. Report commands and actual outcomes.
7. Update documentation when behaviour, architecture, or scope changes.
8. Summarise files changed, decisions, limitations, and next steps.

Do not claim tests passed unless they were actually run. Do not implement future roadmap items merely because they appear in the architecture.

## Initial build order

Follow the phases in `docs/ROADMAP.md`. Start with a runnable React + TypeScript + Vite application, quality tooling, and a minimal shell. Then implement project persistence, audio loading/playback, Arabic caption editing, timeline interaction, visual preview, and export.

## Architecture boundaries

- UI: React pages, panels, controls, and dialogs.
- State: Zustand stores and explicit commands/history.
- Domain: project, caption, track, template, and render types.
- Arabic engine: directionality, Unicode-safe text handling, segmentation helpers, and font test fixtures.
- Audio engine: decode/playback, waveform data, and transport.
- Timeline engine: time mapping, clip operations, snapping, and scene evaluation.
- Rendering engine: deterministic scene description, frame composition, and export adapters.
- Storage: IndexedDB/local project persistence; cloud adapters only in later phases.

These are logical boundaries first. Do not create a complex package/workspace structure before the code needs it.

## Religious-content safeguards

For Quranic and Hadith workflows:
- Keep supplied source text intact and record source/provenance metadata where available.
- Distinguish the text's written orthography from the recitation audio.
- Distinguish qira'ah and riwayah; do not treat them as interchangeable pronunciation presets.
- AI transcription, tashkeel suggestions, and alignment are assistive outputs, not verification.
- Make human correction and source comparison possible.
- Never silently auto-correct authoritative text.

## Definition of done

A feature is done only when its acceptance criteria are met, relevant tests are added, errors and unsupported browser capabilities are handled, and documentation is updated where needed.
