# Product Requirements Document

## 1. Product summary

Waddah (وَضَّاح) is an Arabic-first, browser-based caption and lyric video editor. It transforms Arabic audio and text into synchronised visual media with careful typography and a creator-friendly editing workflow.

The product's distinctive value is not generic video editing. It is the combination of Arabic text handling, audio-to-text synchronisation, phrase and word timing, optional karaoke highlighting, and reusable visual styles.

## 2. Problem

Creators publishing Arabic recitations, nasheeds, poetry, lectures, dhikr, salawat, and educational audio often assemble captions and visualisations manually across several tools. Generic subtitle editors may not provide a comfortable Arabic-first workflow, precise word timing, appropriate typography, or reliable preservation of diacritics and orthographic marks.

Waddah aims to make this workflow coherent in one browser-based editor.

## 3. Target users and use cases

- Creators producing Arabic recitation and devotional content.
- Nasheed, poetry, and spoken-word publishers.
- Educators and lecturers creating captioned clips.
- Arabic-language media creators who need RTL typography and synchronised text.
- Users who already have authoritative text and want to align it to audio.

Religious content is an important initial use case, but the product should not be branded or architected as exclusively religious software.

## 4. Product principles

1. Arabic-first, not Arabic-as-an-afterthought.
2. Manual workflow is a complete product capability, not merely an AI fallback.
3. AI assists; the user remains in control of text and timing.
4. Preserve source text and provenance.
5. Make phrase-level editing fast; allow word-level precision when needed.
6. A creator should be able to produce a useful video without a cloud account.
7. Templates should support both restrained minimalism and cinematic expression.
8. Editing and export should produce consistent results.

## 5. Core workflow

### Manual workflow
1. Create a project and upload audio.
2. Paste or enter Arabic text.
3. Edit text and split it into phrases/verses/segments.
4. Play audio and mark or adjust phrase boundaries.
5. Optionally create word timings and karaoke highlighting.
6. Choose a template, aspect ratio, typography, and background.
7. Preview and export.

### AI-assisted workflow
1. Upload audio and choose a language/context profile.
2. Request transcription from a replaceable provider.
3. Review and correct the draft transcript.
4. Optionally supply authoritative reference text.
5. Generate preliminary phrase timings and, when supported, word alignment.
6. Correct text and timing manually.
7. Continue through the same editor, template, preview, and export workflow.

Both workflows must converge on the same project and caption data model.

## 6. Functional requirements

### Projects
- Create, rename, duplicate, open, and delete local projects.
- Persist project metadata and editable state locally.
- Autosave with visible save status.
- Recover gracefully from interrupted sessions where feasible.
- Track imported media references and handle missing media.

### Audio
- Import supported browser-decodable audio files.
- Display duration and waveform.
- Play, pause, seek, and adjust playback volume.
- Keep transport/playhead state consistent with timeline time.
- Handle decode errors and unsupported formats clearly.

### Arabic text
- Correct RTL and bidirectional text behaviour.
- Preserve Arabic Unicode, tashkeel, Quranic annotation marks, punctuation, and source spelling.
- Support editing, copy/paste, phrase segmentation, and word-level segmentation.
- Offer selectable Arabic fonts and robust fallback behaviour.
- Never silently remove diacritics or rewrite source text.
- Keep raw source text distinct from derived normalised text used for search or alignment.

### Synchronisation and timeline
- Phrase-level timing is required for the first useful release.
- Word-level timing is supported by the domain model and added progressively.
- Karaoke highlighting is optional and uses word timing.
- Allow users to create, edit, move, resize, split, merge, and delete caption segments.
- Support playback-based manual marking.
- Provide zoom, horizontal scrolling, scrubbing, snapping, selection, and undo/redo.
- Use integer milliseconds as canonical time units.

### Visual design
- Provide a live preview canvas.
- Support 9:16, 16:9, and 1:1 output compositions.
- Allow caption position, alignment, size, colour, background, and style changes.
- Support minimal and cinematic template families.
- Preview should reflect the same rendering logic used by export.

### Export
- Initial target: browser-based WebM export where supported.
- Detect available codecs and explain format limitations.
- Keep audio/video synchronisation.
- Provide export progress, error handling, and cancellation where practical.
- Initial presets: 1080×1920, 1920×1080, 1080×1080 at 30 FPS.
- MP4 and 60 FPS are later capabilities, not assumed MVP guarantees.

### AI assistance (later MVP increment)
- Provider abstraction for transcription and alignment.
- Transcript confidence and alignment confidence where available.
- Editable output and explicit human review.
- Do not bind the product to a single AI vendor.

## 7. Editor experience

The editor is timeline-based and contains five principal regions:

1. **Top toolbar:** project name, undo/redo, save state, preview quality, aspect ratio, export.
2. **Left tool panel:** Text, Audio, Styles, Media, Effects.
3. **Preview canvas:** current composition with direct positioning/resizing where practical.
4. **Inspector:** context-sensitive text, typography, alignment, colour, animation, background, and audio controls.
5. **Timeline:** audio track, caption track, and visual/background track. Caption phrases may expose nested word timing.

A dedicated synchronisation mode should prioritise playback, waveform visibility, and fast keyboard marking.

## 8. Template directions

Initial template concepts:
- Naskh Classic
- Minimal Ivory
- Midnight Gold
- Andalusian
- Sufi Heritage
- Modern Kinetic

These are visual directions, not claims of religious authenticity or historical reconstruction. Templates should be editable rather than hard-coded compositions.

## 9. MVP scope

### MVP 0.1 — Manual Caption Studio
- Audio upload and playback.
- Paste/edit Arabic text with RTL support.
- Phrase segmentation and manual timing.
- Waveform and timeline.
- Phrase-level synchronisation.
- Preview with background colour/image.
- Arabic font selection and basic typography controls.
- 9:16, 16:9, and 1:1 compositions.
- Local autosave.
- WebM export where browser capabilities permit.

### MVP 0.2 — Assisted Synchronisation
- Arabic ASR provider integration.
- Transcript correction workflow.
- Preliminary phrase timestamps.
- Reference-text alignment.
- Word alignment experiments and confidence display.
- Optional karaoke highlighting.
- Additional text styling and animation.

### MVP 0.3 — Creator SaaS
- Accounts and cloud project storage.
- Custom templates and brand kits.
- MP4 export where supported by the selected processing path.
- Usage limits and subscriptions.
- More export controls and collaboration only if validated by demand.

## 10. Explicit non-goals for initial MVP

- Full nonlinear video editing suite.
- AI voice generation or AI Quran recitation.
- Automatic religious-text authentication.
- Extensive built-in Quran/Hadith database.
- Automatic translation as a core dependency.
- Native mobile application.
- Social network publishing integrations.
- Real-time collaboration.
- Custom ASR model training.
- Server-side rendering infrastructure before browser export is validated.

## 11. Success criteria

The first release is useful when a user can load an audio recording, paste Arabic text, segment it, synchronise phrases against the waveform, style the captions, preview the composition, export a video with aligned audio, refresh the browser, and reopen the project without losing work.

Quality gates include correct Arabic shaping/diacritics, stable timeline interaction, consistent preview/export, and clear handling of unsupported browser capabilities.
