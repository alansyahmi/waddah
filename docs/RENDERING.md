# Rendering and Export

## 1. Shared scene model

Preview and export must use the same timeline evaluator and scene description. Avoid implementing one rendering path for preview and a separate set of timing/layout rules for export.

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

The exact layer types should be defined when implementation begins.

## 2. Pipeline

1. Load validated project data and referenced assets.
2. Evaluate active timeline elements at time T.
3. Resolve caption text, typography, position, and animation.
4. Render background, captions, and overlays.
5. Mix or route audio.
6. Synchronise frames and audio timestamps.
7. Encode and mux.
8. Produce an export file and report actual format/codec.

## 3. Arabic text rendering

DOM/SVG may be preferable for Arabic shaping and typography. Canvas can composite final visual layers, but do not assume Canvas text output will match DOM preview. Test fonts, ligatures, diacritics, mixed-direction text, and line wrapping on the actual export path.

Wait for fonts and images to load before rendering export frames. Avoid changing text shaping or fallback fonts between preview and export.

## 4. Browser encoding strategy

Preferred advanced path: WebCodecs plus a muxing library such as Mediabunny, subject to runtime support and testing.

Fallback: MediaRecorder when supported. Its output format and codec availability vary by browser; it must not be presented as universally capable of MP4 export.

Perform capability detection for:
- WebCodecs availability.
- Supported video/audio codecs.
- Muxing support.
- MediaRecorder MIME types.
- Browser-specific limitations.

Show the user which format will actually be produced before export. Keep a future server-side export adapter possible, but do not build it for the initial MVP.

## 5. Initial export presets

| Preset | Dimensions | Initial frame rate |
|---|---:|---:|
| Vertical | 1080 × 1920 | 30 FPS |
| Landscape | 1920 × 1080 | 30 FPS |
| Square | 1080 × 1080 | 30 FPS |

60 FPS, MP4 guarantees, advanced audio effects, and high-resolution export can follow after a stable MVP.

## 6. Performance

- Move expensive encoding to a Web Worker where supported.
- Avoid recomputing static backgrounds and unchanged layers.
- Cache waveform and reusable visual assets.
- Provide progress and cancellation where possible.
- Test long recordings and memory use.
- Avoid blocking editor interactions during export.

## 7. Export correctness

Verify:
- Audio and video start/end alignment.
- Frame timestamps and duration.
- No missing first/last frames.
- Fonts and diacritics render correctly.
- Preview and exported frame match at sampled timestamps.
- Export failure leaves the project intact.
- Unsupported codecs produce a clear actionable message.
