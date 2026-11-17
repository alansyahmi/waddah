# Technical Architecture

## 1. Architecture goals

- Browser-first and local-first for the initial manual editor.
- Clear separation between UI, domain logic, audio, timeline, Arabic text, rendering, and persistence.
- Deterministic scene evaluation shared by preview and export.
- Provider-neutral AI integration.
- Incremental architecture: logical modules first, separately deployed services/packages only when justified.

## 2. Proposed stack

### Frontend
- React + TypeScript + Vite.
- Tailwind CSS and shadcn/ui.
- Zustand for application/editor state.
- Zod for runtime validation.
- Lucide icons.
- Dexie over IndexedDB for local persistence.
- WaveSurfer.js or a purpose-built Canvas waveform.

### Browser media
- Web Audio API for audio decoding/playback and audio graph operations.
- DOM/SVG for editable text and accurate browser text shaping.
- Canvas for waveform/timeline/compositing where appropriate.
- WebCodecs with a muxing library such as Mediabunny for advanced export where supported.
- MediaRecorder as a capability-dependent fallback, not a universal MP4 solution.
- Web Workers for expensive processing when useful.

### Hosted services (later)
- Cloudflare Pages for frontend hosting.
- Cloudflare Workers for API endpoints.
- D1 for relational metadata.
- R2 for user media and exports.
- Resend for transactional email.
- Turnstile for abuse prevention.
- Stripe for subscriptions when monetisation is introduced.

Avoid introducing Postgres, Redis, Kubernetes, or server-side video rendering for the initial MVP without a clear requirement.

## 3. Logical system boundaries

### Application/UI
React pages, editor layout, panels, controls, dialogs, accessibility, and routing.

### Domain model
Projects, assets, tracks, captions, word timings, templates, export settings, and validation rules.

### Arabic engine
RTL/bidi helpers, Unicode-safe text operations, segmentation utilities, font fixtures, and separate normalisation functions.

### Audio engine
Audio import/decode, playback transport, waveform generation, volume, and audio timing.

### Timeline engine
Time mapping, track/clip operations, snapping, selection, split/merge, and deterministic evaluation at a given time.

### Rendering engine
Scene description, caption composition, background/overlay rendering, frame generation, audio composition, encoding, and export adapters.

### Storage
Local project persistence, media references, autosave, migrations, and later cloud adapters.

### AI provider adapters
Transcription and forced-alignment interfaces. Vendor-specific code must remain behind adapters.

## 4. State management

Use Zustand stores with separated responsibilities:
- Project store: project metadata, active project, save state.
- Timeline store: tracks, clips, playhead, zoom, selection.
- Audio store: loaded media, transport, volume, waveform state.
- Visual store: typography, backgrounds, animation, template selection.
- History/command layer: undo/redo and domain operations.

Avoid making every playback tick re-render the entire editor. Keep high-frequency playhead updates isolated and throttle visual updates where appropriate.

## 5. Editing commands and history

Represent meaningful edits as commands, for example:
- CreateCaption
- UpdateCaptionText
- MoveCaption
- ResizeCaption
- SplitCaption
- MergeCaptions
- SetWordTiming
- ApplyTemplate
- UpdateStyle

Commands should validate invariants and support undo/redo. Avoid storing a full project snapshot for every keystroke or tiny timing change. Coalesce text input and drag operations where appropriate.

## 6. Rendering pipeline

Project data → timeline evaluator at time T → RenderScene → visual compositor + audio graph → frame/audio synchronisation → encoder/muxer → export.

Preview and export must consume the same scene description and timeline evaluation rules. React lifecycle should not own the rendering engine.

Illustrative contract:

```ts
interface RenderContext {
  currentTimeMs: number;
  width: number;
  height: number;
  frameRate: number;
}

interface RenderScene {
  background: BackgroundLayer;
  captions: CaptionLayer[];
  overlays: OverlayLayer[];
}

function evaluateScene(
  project: Project,
  context: RenderContext
): RenderScene;
```

The rendering engine should be testable independently of React. Browser-specific APIs belong behind adapters.

## 7. Persistence

Initial local-first design:
- IndexedDB via Dexie for project records and structured state.
- Store imported binary assets in IndexedDB only after evaluating storage limits and expected file sizes.
- Consider object URLs ephemeral; do not persist blob URLs as durable asset references.
- Persist asset blobs or explicit user-managed file handles where supported, with fallback import/relink flow.
- Version project schemas and implement migrations.
- Autosave with debouncing and a visible status indicator.
- Handle quota errors and missing assets.

Later cloud design:
- Worker API for auth/project metadata.
- D1 for structured metadata.
- R2 for uploaded assets and exports.
- Signed or scoped access to private media.
- Explicit usage and retention limits.

## 8. AI service boundary

Define interfaces for transcription and alignment; do not couple domain logic to one provider. AI tasks should be asynchronous and return provenance, model/provider metadata, confidence where available, and editable draft results.

## 9. Security and privacy

- Validate file types, sizes, and metadata.
- Treat uploaded media and transcripts as untrusted input.
- Avoid logging user audio or full religious/private transcripts by default.
- Do not expose provider API keys in browser code.
- Apply rate limits and abuse prevention to hosted AI endpoints.
- Use least-privilege storage access and explicit retention policies.
- Do not send user media to external providers without clear user action and disclosure.

## 10. Initial repository structure

The proposed structure is a destination, not a mandate to implement every module immediately:

```text
waddah/
├── apps/
│   └── web/
│       ├── public/
│       └── src/
│           ├── app/
│           ├── pages/
│           ├── features/
│           ├── components/
│           ├── stores/
│           ├── hooks/
│           ├── core/
│           ├── assets/
│           └── styles/
├── packages/
│   ├── shared-types/
│   ├── arabic-engine/
│   ├── audio-engine/
│   ├── timeline-engine/
│   ├── rendering-engine/
│   └── editor-core/
├── services/
│   ├── api/
│   └── transcription/
├── infrastructure/
│   ├── cloudflare/
│   └── database/
├── tests/
│   ├── unit/
│   ├── integration/
│   ├── arabic/
│   └── rendering/
└── docs/
```

Begin with `apps/web` and a small set of internal modules. Extract packages when boundaries become stable and independently useful.
