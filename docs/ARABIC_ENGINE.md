# Arabic Text Engine

## 1. Purpose

Arabic text correctness is central to Waddah. The editor must treat Arabic as structured Unicode text with bidirectional layout, shaping, diacritics, and orthographic conventions—not as ordinary left-to-right strings with a CSS direction flag.

## 2. Requirements

- Correct RTL paragraph and inline direction.
- Correct Unicode bidirectional behaviour when Arabic is mixed with Latin text, numerals, timestamps, or punctuation.
- Preserve tashkeel and Quranic annotation marks.
- Preserve original letters, hamza forms, alif variants, punctuation, and source spelling.
- Support copy/paste without corrupting combining marks.
- Support phrase and word segmentation while retaining source offsets where practical.
- Test Arabic font rendering and fallback.
- Avoid destructive normalisation.

## 3. Source text and derived text

Maintain the original supplied text as the authoritative editable source. Any transformed representation must be separate and explicitly named, for example:
- displayText
- alignmentText
- searchNormalisedText

Normalisation may be useful for matching audio to text, but must never overwrite source text. Every normalisation rule should be documented and tested.

## 4. Typography

Test at minimum:
- Noto Naskh Arabic
- Amiri
- Noto Sans Arabic

Evaluate shaping, ligatures, diacritics positioning, line height, punctuation, mixed-direction runs, and browser consistency. Do not assume one font is best for all content.

Use DOM/SVG for editable text and text shaping wherever browser layout gives the desired fidelity. Canvas may be used for final composition, but test the exact export path because text rasterisation and font loading differ from normal DOM preview.

## 5. Segmentation

Do not assume splitting on spaces is always sufficient. Arabic clitics, punctuation, diacritics, Quranic marks, and recitation-specific orthography can complicate segmentation.

A segmentation operation should preserve the original string and provide a mapping between visible units and source ranges where feasible. Avoid silently changing token order or removing combining marks.

## 6. Religious text safeguards

- Distinguish written orthography from recited pronunciation.
- Distinguish qira'ah and riwayah; do not treat them as interchangeable presets.
- Preserve supplied Quranic text and source edition information.
- AI transcription and tashkeel suggestions are drafts, not authenticated text.
- Never silently auto-correct authoritative Quranic or Hadith text.
- Make provenance and human review status visible where relevant.

## 7. Test corpus

Create a small, licensed or public-domain test fixture set that covers:
- Arabic with and without tashkeel.
- Quranic annotation marks.
- Long and short phrases.
- Mixed Arabic/Latin text.
- Arabic-Indic and Western digits.
- Punctuation at phrase boundaries.
- Diacritics on edge cases and combining marks.
- Copy/paste and edit round-trips.

Do not add copyrighted or restricted corpus material without checking its licence and provenance.
