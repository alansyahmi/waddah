# Product and Technical Decisions

This is a lightweight decision log. Update it when a meaningful product or architecture decision changes.

## D-001 — Arabic-first, not religious-only

**Decision:** Waddah is Arabic-first and supports religious and non-religious audio content.

**Reason:** The core technology—Arabic typography, transcription, alignment, and visualisation—also applies to poetry, lectures, spoken word, and educational media.

## D-002 — Manual and AI-assisted workflows

**Decision:** Both workflows are first-class. Manual editing must work without an AI service.

**Reason:** Users may already possess authoritative text, and AI transcription may be inaccurate or unavailable.

## D-003 — Browser-based editing and rendering

**Decision:** The editor is browser-based, with local-first functionality for the initial MVP.

**Reason:** Fast distribution and low operational complexity. Export capabilities must be detected rather than assumed.

## D-004 — Hybrid visual style

**Decision:** Support both minimal and cinematic template directions.

**Reason:** The use cases range from quiet educational captions to expressive recitation and poetry videos.

## D-005 — Phrase and word timing

**Decision:** Support phrase-level and word-level synchronisation, with optional karaoke highlighting.

**Reason:** Phrase timing is an efficient baseline; word timing enables precise highlighting. Karaoke is a presentation mode driven by word timings.

## D-006 — Timeline-based editor

**Decision:** Use a timeline as the primary editing model.

**Reason:** Audio synchronisation requires precise temporal control, playback, waveform inspection, and direct manipulation of caption intervals.

## D-007 — Local-first MVP

**Decision:** Do not require an account, cloud database, or hosted media storage for the first manual editor.

**Reason:** Validate the editing experience before adding SaaS complexity.

## D-008 — Preserve authoritative source text

**Decision:** Never destructively normalise or silently rewrite Arabic source text, especially Quranic and Hadith text.

**Reason:** Orthography, diacritics, annotation marks, and source editions can be meaningful. Derived text must remain separate.

## D-009 — Shared preview/export scene evaluation

**Decision:** Preview and export use the same timeline evaluator and scene description.

**Reason:** Prevent visual and timing discrepancies between what the user edits and the exported file.

## D-010 — Incremental package extraction

**Decision:** Begin with one browser app and logical internal modules. Extract packages only when boundaries and reuse are real.

**Reason:** Avoid premature monorepo complexity and allow Codex to implement a coherent vertical slice.
