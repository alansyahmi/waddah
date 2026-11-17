# Testing Strategy

## 1. Quality objectives

Test correctness at domain boundaries before relying on visual manual inspection. Arabic text integrity, time arithmetic, timeline operations, preview/export consistency, and local persistence are high-risk areas.

## 2. Test layers

### Unit tests
- Time interval validation and conversions.
- Caption split/merge/move/resize commands.
- Word timing parent-child invariants.
- Timeline scene evaluation at selected timestamps.
- Arabic text preservation and segmentation helpers.
- Project schema validation and migrations.
- Export capability selection logic.

### Integration tests
- Import audio → waveform → playback transport.
- Create captions → edit timings → persist → reload.
- Apply template → preview scene evaluation.
- Export pipeline with deterministic test fixtures.
- Asset relinking and missing-file handling.

### Browser/end-to-end tests
- Create a project.
- Import an audio fixture.
- Paste Arabic text.
- Create and time phrase captions.
- Change aspect ratio and template.
- Refresh and reopen.
- Export where the browser test environment supports it.

### Visual regression tests
- Arabic shaping and diacritics.
- RTL mixed-direction content.
- Preview and exported frame comparisons at fixed timestamps.
- Template rendering at each target aspect ratio.

## 3. Arabic fixture coverage

Include:
- Arabic with full and partial tashkeel.
- Quranic annotation marks.
- Mixed Arabic/Latin runs.
- Arabic-Indic and Western digits.
- Punctuation and brackets.
- Long phrases and line wrapping.
- Combining mark edge cases.
- Copy/paste and edit round-trips.

Use properly licensed fixtures. Avoid placing private user recordings or copyrighted content in the repository.

## 4. Audio and timeline fixtures

Test short and longer recordings, silence, pauses, repeated phrases, varied speech rates, and background noise. Use deterministic generated tones/silence for low-level timing tests and lawful reference recordings for realistic alignment evaluation.

## 5. Export checks

- Audio/video duration and synchronisation.
- Frame timestamps and frame count.
- First and last frame.
- Font loading and Arabic rendering.
- Supported MIME type/codec reporting.
- Failure and cancellation handling.
- Project remains usable after failed export.

## 6. Performance checks

Measure:
- Waveform generation time.
- Timeline responsiveness with many caption segments.
- Memory use during playback and export.
- Export time relative to recording duration.
- Behaviour on long recordings and lower-powered devices.

## 7. Definition of done

A change is complete when relevant tests pass, type checking/linting pass, browser limitations are documented, and the project remains editable after the operation.
