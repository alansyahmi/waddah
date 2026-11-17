# Domain Data Model

This document proposes the initial persisted domain model. It is a design contract to refine during implementation, not a claim that these types already exist in code.

## 1. Core entities

- Project: editable composition and metadata.
- Asset: imported audio, image, or other media.
- Track: ordered timeline lane.
- CaptionSegment: phrase/line with start/end and optional nested word timings.
- WordTiming: word-level interval and optional confidence.
- Template: reusable visual configuration.
- Style: typography, colour, position, and animation configuration.
- ExportSettings: target dimensions, frame rate, and output format.

## 2. Time representation

Use integer milliseconds as the canonical persisted unit. The project must define a consistent convention for interval boundaries. Recommended convention: start-inclusive, end-exclusive intervals `[startMs, endMs)`. Enforce `startMs >= 0` and `endMs > startMs`.

## 3. Illustrative TypeScript types

```ts
type SyncMode = "phrase" | "word" | "karaoke";
type AspectRatioPreset = "9:16" | "16:9" | "1:1";

interface WordTiming {
  id: string;
  text: string;
  startMs: number;
  endMs: number;
  confidence?: number;
}

interface CaptionSegment {
  id: string;
  text: string;
  startMs: number;
  endMs: number;
  words: WordTiming[];
  syncMode: SyncMode;
  styleId?: string;
  sourceText?: string;
}

interface ProjectAsset {
  id: string;
  kind: "audio" | "image" | "video" | "font";
  name: string;
  mimeType: string;
  sizeBytes: number;
  durationMs?: number;
  storageKey: string;
  checksum?: string;
}

interface TimelineTrack {
  id: string;
  kind: "audio" | "captions" | "visual";
  name: string;
  muted?: boolean;
  locked?: boolean;
  order: number;
}

interface Project {
  id: string;
  schemaVersion: number;
  title: string;
  createdAt: string;
  updatedAt: string;
  durationMs: number;
  aspectRatio: AspectRatioPreset;
  width: number;
  height: number;
  frameRate: number;
  assets: ProjectAsset[];
  tracks: TimelineTrack[];
  captions: CaptionSegment[];
  templateId?: string;
  metadata?: ProjectMetadata;
}

interface ProjectMetadata {
  language?: string;
  contentType?: string;
  sourceTextReference?: string;
  sourceEdition?: string;
  qiraah?: string;
  riwayah?: string;
  reciter?: string;
  performer?: string;
  verificationStatus?: "unverified" | "user-reviewed" | "source-checked";
}
```

## 4. Important modelling rules

- Phrase and word timing are two levels of one caption representation, not competing independent data systems.
- A phrase may have no word timings, partial word timings, or complete word timings.
- Word text should be traceable to the parent caption text, but editing operations must define how parent/child text stays consistent.
- Preserve source text separately when edits or derived text are required.
- Never assume whitespace tokenisation is sufficient for all Arabic segmentation needs.
- Do not embed large binary media in JSON project exports. Use asset references and a separate asset storage mechanism.
- Use stable IDs for entities and version the project schema.
- Confidence is optional metadata, not a substitute for validation.
- Store source/provenance for externally supplied authoritative text where available.

## 5. Religious content provenance

Where applicable, metadata may include collection/book, chapter/verse or hadith reference, edition/source, qira'ah, riwayah, reciter, and human verification status. These fields should be optional and extensible. Do not infer religious authenticity from transcription confidence or successful alignment.

## 6. Validation invariants

- IDs are unique within their entity collections.
- All times are finite integers.
- Segment start is non-negative and end is greater than start.
- Word intervals lie within their parent phrase unless a documented exception is introduced.
- Captions and assets reference existing entities.
- Project dimensions and frame rate are positive and supported by the export profile.
- Schema migrations preserve source text and timing semantics.
