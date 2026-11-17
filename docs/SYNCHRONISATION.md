# Audio and Synchronisation

## 1. Modes

- **Phrase sync:** one interval per phrase, verse, or caption segment. This is the first MVP timing mode.
- **Word sync:** each word has its own start/end interval.
- **Karaoke sync:** progressive highlighting driven by word timing. It is a presentation mode over word-level timing, not a separate timing data model.

## 2. Manual workflow

A synchronisation workspace should provide:
- Audio playback and pause.
- Visible waveform and playhead.
- Phrase list and selected phrase.
- Mark-start/mark-end keyboard actions.
- Fine adjustment and snapping.
- Seek to selected phrase.
- Optional word-level timing controls.
- Undo/redo.

The manual workflow must remain available even if AI services are unavailable.

## 3. Alignment model

Phrase timing is required first. Word-level forced alignment should be introduced only after testing representative Arabic recordings. Alignment quality may vary with recitation style, repetition, melisma, pauses, background noise, and differences between supplied orthography and spoken audio.

AI alignment results must be editable and should expose confidence where the provider supplies it.

## 4. Provider abstraction

```ts
interface ArabicTranscriptionProvider {
  transcribe(audio: Blob): Promise<TranscriptionResult>;
}

interface ArabicAlignmentProvider {
  align(
    audio: Blob,
    referenceText: string
  ): Promise<AlignmentResult>;
}
```

Keep provider-specific request/response formats out of the domain model. Normalise provider output into a stable internal result and retain provider/model provenance.

## 5. Timing rules

- Canonical unit: integer milliseconds.
- Use one documented interval convention throughout the application.
- Validate positive durations and parent/child boundaries.
- Avoid accumulating floating-point drift during frame/time conversion.
- Define snapping tolerance and drag behaviour centrally.
- Playback time should be derived from the audio transport; the timeline playhead should reflect it without excessive React re-rendering.

## 6. Data integrity

- Editing phrase boundaries should not silently destroy word timings. Define whether child timings move, clamp, or require confirmation.
- Splitting a phrase should have an explicit word reassignment strategy.
- Merging phrases should preserve word order and timing.
- Text edits must not silently rewrite word timing text.
- When alignment is rerun, preserve the prior result or provide undo/restore.

## 7. Test recordings

Use short representative recordings first, then longer recordings. Include varied reciters/speakers, speeds, pauses, repeated phrases, and recordings with background sound. Ensure all test media is lawfully obtained and suitable for development use.
