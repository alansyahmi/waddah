# Product and Engineering Roadmap

Roadmap is ordered by dependency and risk, not a promise of calendar dates.

## Phase 0 — Foundation
- [ ] Initialise React + TypeScript + Vite.
- [ ] Add formatting, linting, type checking, and test tooling.
- [ ] Establish app shell, routing, and responsive desktop-first layout.
- [ ] Add Zod and baseline domain types.
- [ ] Add Zustand stores with clear ownership.
- [ ] Add IndexedDB/Dexie persistence spike.
- [ ] Add error boundaries and basic diagnostics.

**Exit:** runnable app, repeatable quality checks, documented developer setup.

## Phase 1 — Project management
- [ ] Dashboard and create project.
- [ ] Rename, duplicate, delete, and reopen local projects.
- [ ] Project schema versioning.
- [ ] Local autosave and save-state indicator.
- [ ] Asset import/relink model.

**Exit:** a project survives refresh and can be reopened.

## Phase 2 — Audio engine
- [ ] Audio import and decode.
- [ ] Playback, pause, seek, and volume.
- [ ] Duration and transport state.
- [ ] Waveform generation and caching.
- [ ] Error handling for unsupported/corrupt files.

**Exit:** stable audio transport and waveform for reference recordings.

## Phase 3 — Arabic caption editor
- [ ] RTL text input and editing.
- [ ] Font selection and font loading.
- [ ] Unicode-safe text operations.
- [ ] Phrase creation/edit/delete.
- [ ] Word segmentation model and UI groundwork.
- [ ] Arabic typography test fixtures.

**Exit:** reliable Arabic text editing without corruption.

## Phase 4 — Timeline and manual synchronisation
- [ ] Ruler, tracks, playhead, and scrubbing.
- [ ] Caption clips and selection.
- [ ] Manual phrase start/end marking.
- [ ] Drag/resize, zoom, and scroll.
- [ ] Split/merge and snapping.
- [ ] Command-based undo/redo.
- [ ] Word timing controls.

**Exit:** a user can manually synchronise an entire short recording.

## Phase 5 — Visual engine and templates
- [ ] Shared scene evaluator.
- [ ] Live preview.
- [ ] Typography, alignment, colour, and positioning.
- [ ] Background image/colour support.
- [ ] Template system and initial six style directions.
- [ ] Optional phrase/word animation and karaoke highlighting.

**Exit:** stable preview from project/timeline state.

## Phase 6 — Browser export
- [ ] Browser capability detection.
- [ ] Frame compositor.
- [ ] Audio/video synchronisation.
- [ ] WebM export path where supported.
- [ ] Progress/error/cancel states.
- [ ] Preview/export visual regression tests.

**Exit:** repeatable export of short projects with correct timing.

## Phase 7 — AI assistance
- [ ] Provider-neutral Arabic transcription adapter.
- [ ] Transcript review/edit flow.
- [ ] Phrase-level timestamp generation.
- [ ] Reference-text alignment.
- [ ] Evaluate Arabic word-level forced alignment.
- [ ] Confidence/provenance display.
- [ ] Karaoke highlighting driven by verified word timings.

**Exit:** AI output is editable, traceable, and clearly marked as unverified until reviewed.

## Phase 8 — Hosted product
- [ ] Authentication.
- [ ] Worker API and D1 metadata.
- [ ] R2 asset storage.
- [ ] Cloud project sync.
- [ ] Usage limits and abuse controls.
- [ ] Billing and subscription plans.
- [ ] Custom templates and brand kits.

**Exit:** hosted accounts and paid features are reliable and secure.

## Risk-first technical spikes

Test these early rather than discovering them after building the editor:
1. Arabic font shaping, diacritics, and export fidelity.
2. Browser audio/video export and codec support.
3. Timeline interaction performance on longer recordings.
4. Persistence of large audio assets and recovery from browser storage limits.

## Suggested one-developer effort ranges

These are rough planning estimates, not commitments:
- Foundation and dashboard: 1 week.
- Audio engine: 1 week.
- Arabic editor: 1–2 weeks.
- Timeline: 1–2 weeks.
- Visual engine: 1–2 weeks.
- Export: 1–2 weeks.
- Testing and polish: 1 week.
- AI integration: 1–2 weeks.

Actual effort depends heavily on browser media edge cases and the quality target.
