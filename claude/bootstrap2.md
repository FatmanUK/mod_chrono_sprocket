# Chrono Sprocket: Project Bootstrap File (Updated — Composition Complete, Pre-Compile)

**Project:** Chrono Sprocket
**Status:** All 8 patterns written and refined; order list finalized; ready to compile and test in MilkyTracker
**Tracker:** MilkyTracker
**Platform:** Linux / PikaOS
**Target format:** 4-channel ProTracker MOD

---

## 1. Current Goal

Compile the pattern data below via the custom external compiler into a working `.mod` file, then load and test it in MilkyTracker on PikaOS. No further composition is expected unless testing reveals a problem.

---

## 2. State of Play

### Source-of-Truth Hierarchy (unchanged)
1. Auditioned project files are authoritative for: exact sample loop points, exact sample volumes, exact per-row volume edits, exact finetune values, any last by-ear edits.
2. This bootstrap file is authoritative for: project architecture, pattern roles, order list, note/rhythm/effect structure, final sample identities, tested status.
3. Sample archives (ST-01, ST-02) are only the source of the sample files.

### Title & Tempo (CONFIRMED)
- Title: **Chrono Sprocket**
- Speed: **06**, Tempo: **7D (125)** — deliberately laid-back, not punchy/arcade.
- Runtime and file-size targets (85–105s, <40KB) remain loose guidelines only; creativity took priority throughout and no pattern was cut or padded to hit them.

### Instrument Set (CONFIRMED, includes latest volume change)

| ID | Role | Source | Sample | Volume | Finetune | Loop (start/length) | Note range |
|----|------|--------|--------|--------|----------|----------------------|------------|
| 1 | Main melody (piano, two-handed: R.H. lead + L.H. sustained root notes) | ST-02 | **Pizza2** | 0x17 | 0xD (−3) | none | 3–5 (unrestricted) |
| — | *backup for #1, inactive* | ST-01 | RingPiano | 0x10 | 0x0 (TBD if activated) | none | — |
| 2 | Haunting woodwind solo | ST-01 | **PanFlute** | 0x21 | 0xE (−2) | 0x1FE5 + 0x0051 | 3–4 (high) |
| 3 | Heartbeat kick | ST-01 | **BassDrum1** | 0x40 | — | none | C-4 only |
| 4 | Snare (debuts Pattern 01) | ST-01 | **Snare2** | 0x22 | — | none | C-4 only |
| 5 | Hi-hat | ST-01 | **HiHat1** | 0x1C | — | none | C-4 only |
| 6 | Bass — root-tracking pulse (was static D-4 drone; revised to move with each bar's chord root during "away" harmony, home to D-4 on tonic bars) | ST-01 | **MonoBass** | **0x10** (lowered from 0x20 this session) | 0xB (−5) | 0x0AC2 + 0x0181 | 4–5 (low-to-medium) |
| 7 | Pad (solo section only — Patterns 03/04) | ST-01 | **RichString** | 0x12 | 0xE (−2) | 0x09F6 + 0x10FC | 3–4 (medium-to-high) |
| 8 | Metallic chime accents | ST-02 | **Glockenspiel** | 0x28 | 0xD (−3) | none | 3–4 (high) |

**Decision history:**
- Instrument #1 was originally "Steinway" (ST-01), wrongly assumed to be a piano sample — corrected to **ST-02/Pizza2**, with **ST-01/RingPiano** kept as an explicit inactive backup.
- Instrument #2: ST-02/Blower was considered, PanFlute confirmed as the final choice.
- Instrument #6 (MonoBass): originally a static D-4 pedal for the entire piece (flagged by user as making Channel 3 "boring"). Fixed by making it track each bar's chord root during non-tonic ("away") harmony, returning to D-4 on tonic bars — Motif A's pulse identity is preserved on home bars, motion is added elsewhere. An earlier attempt to solve this by swapping Channel 3 to RichString (instrument 7) was explicitly rejected by the user and reverted. Volume subsequently lowered 0x20→0x10 to suit its new, busier role.
- Instrument #7 (RichString) is real and in use (Ch2 pad, Patterns 03/04 only) — flagging that this was briefly and mistakenly thought to be unused mid-session; confirmed present, not dropped.
- Left-hand piano technique: an arpeggio effect (`047`/`037`, cycling triad notes to fake a chord) was tried for Pizza2's left hand and **rejected by the user** — replaced with simple sustained/retriggered single root notes. This is the standing left-hand convention.

### Effects Used (glossary, first-use-per-effect already explained in pattern commentary)
- `047` / `037` — arpeggio (rejected/removed from final patterns; historical only)
  - `436` — vibrato, moderate speed/depth, repeated across rows to sustain a continuous wobble on held solo notes (Patterns 03, 04, 07)
  - `108` — portamento up, speed 08, used once in the Coda (Pattern 07) for a rising pitch-smear into the final landing

### Structural Arc (as composed)
Wind-up → Engagement (question/answer) → Inner Mechanism (PanFlute/RichString solo) → Re-engagement (denser reprise) → Release (coda). **Note:** the final order list (below) places the solo *after* the midpoint rather than immediately following the first Engagement statement, per later user direction — the pattern content itself is unchanged from the original arc description, only its position in the sequence moved.

### Motif Map (as composed)
- **Motif A — "Ratchet Pulse":** BassDrum1 + MonoBass. Now includes root-tracking motion on away-chords (see instrument #6 history above), still returns to a static D-4 pulse on tonic bars.
- **Motif B — "Drive Theme":** Pizza2 R.H. melody. Deliberately kept to quarter-note-plus-occasional-syncopated-pickup phrasing throughout, including in the "denser" reprise — an earlier reprise draft used continuous 8th notes and was rejected by the user as too mechanical/staccato. "Denser/more confident" in the reprise is instead conveyed by the walking (root–fifth) left hand and more frequent Glockenspiel accents, not by a busier melody.
- **Motif C — "Sprocket Glint":** Glockenspiel, sparse accents, more frequent in the reprise (every bar vs. every other bar in the first Engagement statement).
- **Motif D — "Inner Drift":** PanFlute solo over RichString pad, Patterns 03/04 only, untouched by the Channel 3 fix (explicitly excluded per user instruction).

### Order List (CONFIRMED — 17 slots, 8 unique patterns)
```yaml
orderList:
  - 0   # Wind-up
  - 1   # Engagement Q
  - 2   # Engagement A
  - 5   # Re-engagement Q (denser)
  - 6   # Re-engagement A (denser)
  - 1   # Engagement Q (reuse)
  - 2   # Engagement A (reuse)
  - 5   # Re-engagement Q (reuse)
  - 6   # Re-engagement A (reuse)
  - 1   # Engagement Q (reuse)
  - 2   # Engagement A (reuse)
  - 3   # Inner Mechanism I (solo)
  - 4   # Inner Mechanism II (solo)
  - 1   # Engagement Q (reuse)
  - 2   # Engagement A (reuse)
  - 6   # Re-engagement A (final confident restatement)
  - 7   # Coda: Release
```
Solo (3, 4) lands at positions 12–13 of 17 — after the midpoint, per user direction. Patterns 0,3,4,7 appear once each; 1,2 appear four times each; 5,6 appear twice each (6 appears a third time as the final pre-coda restatement).

---

## 3. Dependency Map
- Tracker (testing only): MilkyTracker, on PikaOS
- Target format: ProTracker 2 (PT2) `.mod`, 4-channel
- Pattern authoring: custom external compiler, consumes MarkDown-table pattern data (format below)
- Sample archives: ST-01, ST-02 (raw 8-bit signed PCM, headerless; extracted and analyzed directly from user-supplied tarballs)

---

## 4. Open Issues
- RingPiano backup's finetune remains an undetermined placeholder — only relevant if it's ever activated in place of Pizza2.
- PanFlute is a substitution for the originally-envisioned oboe; accepted, but noted as a compromise.
- Nothing has been compiled or loaded into MilkyTracker yet — no playback testing has occurred. All correctness checks so far have been arithmetic/structural (loop bounds, finetune decode, note-range compliance), not by-ear.

---

## 5. "Golden" Code Blocks

### Instrument definitions (`song.yml`, current state)
```yaml
title: Chrono Sprocket
speed: 6
bpm: 125
orderList:
  - 0
  - 1
  - 2
  - 5
  - 6
  - 1
  - 2
  - 5
  - 6
  - 1
  - 2
  - 3
  - 4
  - 1
  - 2
  - 6
  - 7
instruments:
  - id: 1
    source: st02
    name: ST-02/Pizza2
    volume: 0x17
    finetune: 0xd  # -3
  - id: 2
    source: st01
    name: ST-01/PanFlute
    volume: 0x21
    finetune: 0xe  # -2
    start: 0x1fe5
    length: 0x0051
  - id: 3
    source: st01
    name: ST-01/BassDrum1
    volume: 0x40
  - id: 4
    source: st01
    name: ST-01/Snare2
    volume: 0x22
  - id: 5
    source: st01
    name: ST-01/HiHat1
    volume: 0x1c
  - id: 6
    source: st01
    name: ST-01/MonoBass
    volume: 0x10
    finetune: 0xb  # -5
    start: 0xac2
    length: 0x181
  - id: 7
    source: st01
    name: ST-01/RichString
    volume: 0x12
    finetune: 0xe  # -2
    start: 0x09f6
    length: 0x10fc
  - id: 8
    source: st02
    name: ST-02/Glockenspiel
    volume: 0x28
    finetune: 0xd  # -3
```

### Pattern Format (compiler input spec)
```
| RR | NNN II EEE | NNN II EEE | NNN II EEE | NNN II EEE |
```
`RR` = row number (**decimal**, not hex — compiler bug workaround). `NNN` = note. `II` = instrument slot. `EEE` = effect. MarkDown table headers: `Row`, `Ch1`, `Ch2`, `Ch3`, `Ch4`. No instrument = `--`. No effect = `---`. No note = `---`. Omit entirely empty lines.

### Pattern 00 — "Intro / Wind-up"
| Row | Ch1 | Ch2 | Ch3 | Ch4 |
|---|---|---|---|---|
| 0 | --- -- --- | C-4 03 --- | D-4 06 --- | --- -- --- |
| 4 | --- -- --- | --- -- --- | D-4 06 --- | --- -- --- |
| 8 | --- -- --- | C-4 03 --- | D-4 06 --- | --- -- --- |
| 12 | --- -- --- | --- -- --- | D-4 06 --- | --- -- --- |
| 16 | --- -- --- | C-4 03 --- | D-4 06 --- | --- -- --- |
| 18 | --- -- --- | C-4 05 --- | --- -- --- | --- -- --- |
| 20 | --- -- --- | C-4 05 --- | D-4 06 --- | --- -- --- |
| 22 | --- -- --- | C-4 05 --- | --- -- --- | --- -- --- |
| 24 | --- -- --- | C-4 03 --- | D-4 06 --- | --- -- --- |
| 26 | --- -- --- | C-4 05 --- | --- -- --- | --- -- --- |
| 28 | --- -- --- | C-4 05 --- | D-4 06 --- | --- -- --- |
| 30 | --- -- --- | C-4 05 --- | --- -- --- | --- -- --- |
| 32 | D-4 01 --- | C-4 03 --- | D-4 06 --- | D-3 01 --- |
| 34 | --- -- --- | C-4 05 --- | --- -- --- | --- -- --- |
| 36 | E-4 01 --- | --- -- --- | D-4 06 --- | D-3 01 --- |
| 38 | --- -- --- | C-4 05 --- | --- -- --- | --- -- --- |
| 39 | F#4 01 --- | --- -- --- | --- -- --- | --- -- --- |
| 40 | --- -- --- | C-4 03 --- | D-4 06 --- | D-3 01 --- |
| 42 | --- -- --- | C-4 05 --- | --- -- --- | --- -- --- |
| 44 | A-4 01 --- | C-4 05 --- | D-4 06 --- | D-3 01 --- |
| 46 | --- -- --- | C-4 05 --- | --- -- --- | --- -- --- |
| 48 | G-4 01 --- | C-4 03 --- | A-4 06 --- | A-3 01 --- |
| 50 | --- -- --- | C-4 05 --- | --- -- --- | --- -- --- |
| 52 | F#4 01 --- | C-4 05 --- | A-4 06 --- | A-3 01 --- |
| 54 | --- -- --- | C-4 05 --- | --- -- --- | --- -- --- |
| 56 | E-4 01 --- | C-4 03 --- | D-4 06 --- | D-3 01 --- |
| 58 | --- -- --- | A-4 08 --- | --- -- --- | --- -- --- |
| 60 | D-4 01 --- | C-4 05 --- | D-4 06 --- | D-3 01 --- |
| 62 | --- -- --- | C-4 05 --- | --- -- --- | --- -- --- |

### Pattern 01 — "Engagement" (question half)
| Row | Ch1 | Ch2 | Ch3 | Ch4 |
|---|---|---|---|---|
| 0 | D-4 01 --- | C-4 03 --- | D-4 06 --- | D-3 01 --- |
| 2 | --- -- --- | C-4 05 --- | --- -- --- | --- -- --- |
| 4 | --- -- --- | C-4 04 --- | D-4 06 --- | D-3 01 --- |
| 6 | F#4 01 --- | C-4 05 --- | --- -- --- | --- -- --- |
| 8 | --- -- --- | C-4 03 --- | D-4 06 --- | D-3 01 --- |
| 10 | A-4 01 --- | C-4 05 --- | --- -- --- | --- -- --- |
| 12 | --- -- --- | C-4 04 --- | D-4 06 --- | D-3 01 --- |
| 14 | --- -- --- | C-4 05 --- | --- -- --- | --- -- --- |
| 16 | G-4 01 --- | C-4 03 --- | G-4 06 --- | G-3 01 --- |
| 18 | --- -- --- | C-4 05 --- | --- -- --- | --- -- --- |
| 20 | --- -- --- | C-4 04 --- | G-4 06 --- | G-3 01 --- |
| 22 | F#4 01 --- | C-4 05 --- | --- -- --- | --- -- --- |
| 24 | --- -- --- | C-4 03 --- | G-4 06 --- | G-3 01 --- |
| 26 | E-4 01 --- | C-4 05 --- | --- -- --- | --- -- --- |
| 28 | --- -- --- | C-4 04 --- | G-4 06 --- | G-3 01 --- |
| 30 | D-4 01 --- | C-4 05 --- | --- -- --- | --- -- --- |
| 32 | G-4 01 --- | C-4 03 --- | E-4 06 --- | E-3 01 --- |
| 34 | --- -- --- | C-4 05 --- | --- -- --- | --- -- --- |
| 36 | --- -- --- | C-4 04 --- | E-4 06 --- | E-3 01 --- |
| 38 | A-4 01 --- | C-4 05 --- | --- -- --- | --- -- --- |
| 40 | --- -- --- | C-4 03 --- | E-4 06 --- | E-3 01 --- |
| 42 | B-4 01 --- | C-4 05 --- | --- -- --- | --- -- --- |
| 44 | --- -- --- | C-4 04 --- | E-4 06 --- | E-3 01 --- |
| 46 | A-4 01 --- | C-4 05 --- | --- -- --- | --- -- --- |
| 48 | G-4 01 --- | C-4 03 --- | D-4 06 --- | D-3 01 --- |
| 50 | --- -- --- | C-4 05 --- | --- -- --- | --- -- --- |
| 52 | --- -- --- | C-4 04 --- | D-4 06 --- | D-3 01 --- |
| 54 | F#4 01 --- | C-4 05 --- | --- -- --- | --- -- --- |
| 56 | --- -- --- | C-4 03 --- | D-4 06 --- | D-3 01 --- |
| 58 | E-4 01 --- | C-4 05 --- | --- -- --- | --- -- --- |
| 60 | --- -- --- | C-4 04 --- | D-4 06 --- | D-3 01 --- |

### Pattern 02 — "Engagement" (answer half)
| Row | Ch1 | Ch2 | Ch3 | Ch4 |
|---|---|---|---|---|
| 0 | G-4 01 --- | C-4 03 --- | G-4 06 --- | G-3 01 --- |
| 2 | --- -- --- | C-4 05 --- | --- -- --- | --- -- --- |
| 4 | A-4 01 --- | C-4 04 --- | G-4 06 --- | G-3 01 --- |
| 6 | --- -- --- | C-4 05 --- | --- -- --- | --- -- --- |
| 8 | B-4 01 --- | C-4 03 --- | G-4 06 --- | G-3 01 --- |
| 10 | --- -- --- | C-4 05 --- | --- -- --- | --- -- --- |
| 12 | A-4 01 --- | C-4 04 --- | G-4 06 --- | G-3 01 --- |
| 14 | --- -- --- | C-4 05 --- | --- -- --- | --- -- --- |
| 16 | A-4 01 --- | C-4 03 --- | A-4 06 --- | A-3 01 --- |
| 18 | --- -- --- | C-4 05 --- | --- -- --- | --- -- --- |
| 20 | B-4 01 --- | C-4 04 --- | A-4 06 --- | A-3 01 --- |
| 22 | --- -- --- | C-4 05 --- | --- -- --- | --- -- --- |
| 24 | A-4 01 --- | C-4 03 --- | A-4 06 --- | A-3 01 --- |
| 26 | --- -- --- | C-4 05 --- | --- -- --- | --- -- --- |
| 28 | --- -- --- | C-4 04 --- | A-4 06 --- | A-3 01 --- |
| 30 | C#5 01 --- | C-4 05 --- | --- -- --- | --- -- --- |
| 32 | B-4 01 --- | C-4 03 --- | B-4 06 --- | B-3 01 --- |
| 34 | --- -- --- | C-4 05 --- | --- -- --- | --- -- --- |
| 36 | A-4 01 --- | C-4 04 --- | B-4 06 --- | B-3 01 --- |
| 38 | --- -- --- | C-4 05 --- | --- -- --- | --- -- --- |
| 40 | G-4 01 --- | C-4 03 --- | B-4 06 --- | B-3 01 --- |
| 42 | --- -- --- | C-4 05 --- | --- -- --- | --- -- --- |
| 44 | F#4 01 --- | C-4 04 --- | B-4 06 --- | B-3 01 --- |
| 46 | --- -- --- | C-4 05 --- | --- -- --- | --- -- --- |
| 48 | E-4 01 --- | C-4 03 --- | G-4 06 --- | G-3 01 --- |
| 50 | --- -- --- | C-4 05 --- | --- -- --- | --- -- --- |
| 52 | --- -- --- | C-4 04 --- | G-4 06 --- | G-3 01 --- |
| 54 | F#4 01 --- | C-4 05 --- | --- -- --- | --- -- --- |
| 56 | D-4 01 --- | C-4 03 --- | D-4 06 --- | D-3 01 --- |
| 58 | --- -- --- | A-4 08 --- | --- -- --- | --- -- --- |
| 60 | --- -- --- | C-4 04 --- | D-4 06 --- | D-3 01 --- |

### Pattern 03 — "Inner Mechanism I" (solo, untouched by Ch3 fix)
| Row | Ch1 | Ch2 | Ch3 | Ch4 |
|---|---|---|---|---|
| 0 | B-3 02 436 | B-3 07 --- | --- -- --- | --- -- --- |
| 4 | --- -- 436 | --- -- --- | --- -- --- | --- -- --- |
| 8 | --- -- 436 | --- -- --- | --- -- --- | --- -- --- |
| 12 | --- -- 436 | --- -- --- | --- -- --- | --- -- --- |
| 16 | D-4 02 436 | G-3 07 --- | --- -- --- | --- -- --- |
| 20 | --- -- 436 | --- -- --- | --- -- --- | --- -- --- |
| 24 | --- -- 436 | --- -- --- | --- -- --- | --- -- --- |
| 28 | --- -- 436 | --- -- --- | --- -- --- | --- -- --- |
| 32 | F#4 02 436 | D-3 07 --- | --- -- --- | --- -- --- |
| 36 | --- -- 436 | --- -- --- | --- -- --- | --- -- --- |
| 40 | E-4 02 436 | --- -- --- | --- -- --- | --- -- --- |
| 44 | --- -- 436 | --- -- --- | --- -- --- | --- -- --- |
| 48 | F#4 02 436 | F#3 07 --- | --- -- --- | --- -- --- |
| 52 | --- -- 436 | --- -- --- | --- -- --- | --- -- --- |
| 56 | --- -- 436 | --- -- --- | --- -- --- | --- -- --- |
| 60 | --- -- 436 | --- -- --- | --- -- --- | --- -- --- |

### Pattern 04 — "Inner Mechanism II" (solo, untouched by Ch3 fix)
| Row | Ch1 | Ch2 | Ch3 | Ch4 |
|---|---|---|---|---|
| 0 | A-4 02 436 | B-3 07 --- | --- -- --- | --- -- --- |
| 4 | --- -- 436 | --- -- --- | --- -- --- | --- -- --- |
| 8 | F#4 02 436 | --- -- --- | --- -- --- | --- -- --- |
| 12 | --- -- 436 | --- -- --- | --- -- --- | --- -- --- |
| 16 | E-4 02 436 | A-3 07 --- | --- -- --- | --- -- --- |
| 20 | --- -- 436 | --- -- --- | --- -- --- | --- -- --- |
| 24 | D-4 02 436 | --- -- --- | --- -- --- | --- -- --- |
| 28 | --- -- 436 | --- -- --- | --- -- --- | --- -- --- |
| 32 | B-3 02 436 | G-3 07 --- | --- -- --- | --- -- --- |
| 36 | --- -- 436 | --- -- --- | --- -- --- | --- -- --- |
| 40 | --- -- 436 | --- -- --- | --- -- --- | --- -- --- |
| 44 | --- -- 436 | --- -- --- | --- -- --- | --- -- --- |
| 48 | F#4 02 436 | F#3 07 --- | --- -- --- | --- -- --- |
| 52 | --- -- 436 | --- -- --- | --- -- --- | --- -- --- |
| 56 | --- -- 436 | --- -- --- | --- -- --- | --- -- --- |
| 60 | --- -- 436 | --- -- --- | --- -- --- | --- -- --- |

### Pattern 05 — "Re-engagement I" (reprise, question half)
| Row | Ch1 | Ch2 | Ch3 | Ch4 |
|---|---|---|---|---|
| 0 | D-4 01 --- | C-4 03 --- | D-4 06 --- | D-3 01 --- |
| 4 | --- -- --- | C-4 04 --- | D-4 06 --- | A-3 01 --- |
| 6 | F#4 01 --- | A-4 08 --- | --- -- --- | --- -- --- |
| 8 | --- -- --- | C-4 03 --- | D-4 06 --- | D-3 01 --- |
| 12 | A-4 01 --- | C-4 04 --- | D-4 06 --- | --- -- --- |
| 14 | --- -- --- | C-4 05 --- | --- -- --- | --- -- --- |
| 16 | G-4 01 --- | C-4 03 --- | G-4 06 --- | G-3 01 --- |
| 20 | --- -- --- | C-4 04 --- | G-4 06 --- | D-3 01 --- |
| 22 | F#4 01 --- | D-4 08 --- | --- -- --- | --- -- --- |
| 24 | --- -- --- | C-4 03 --- | G-4 06 --- | G-3 01 --- |
| 28 | E-4 01 --- | C-4 04 --- | G-4 06 --- | --- -- --- |
| 30 | C#4 01 --- | C-4 05 --- | --- -- --- | --- -- --- |
| 32 | E-4 01 --- | C-4 03 --- | E-4 06 --- | E-3 01 --- |
| 36 | --- -- --- | C-4 04 --- | E-4 06 --- | B-3 01 --- |
| 38 | G-4 01 --- | G-4 08 --- | --- -- --- | --- -- --- |
| 40 | --- -- --- | C-4 03 --- | E-4 06 --- | E-3 01 --- |
| 44 | F#4 01 --- | C-4 04 --- | E-4 06 --- | --- -- --- |
| 46 | --- -- --- | C-4 05 --- | --- -- --- | --- -- --- |
| 48 | E-4 01 --- | C-4 03 --- | D-4 06 --- | D-3 01 --- |
| 52 | --- -- --- | C-4 04 --- | D-4 06 --- | A-3 01 --- |
| 54 | D-4 01 --- | F#4 08 --- | --- -- --- | --- -- --- |
| 56 | E-4 01 --- | C-4 03 --- | D-4 06 --- | D-3 01 --- |
| 60 | --- -- --- | C-4 04 --- | D-4 06 --- | --- -- --- |

### Pattern 06 — "Re-engagement II" (reprise, answer half)
| Row | Ch1 | Ch2 | Ch3 | Ch4 |
|---|---|---|---|---|
| 0 | G-4 01 --- | C-4 03 --- | G-4 06 --- | G-3 01 --- |
| 4 | A-4 01 --- | C-4 04 --- | G-4 06 --- | D-4 01 --- |
| 6 | --- -- --- | E-4 08 --- | --- -- --- | --- -- --- |
| 8 | B-4 01 --- | C-4 03 --- | G-4 06 --- | G-3 01 --- |
| 12 | A-4 01 --- | C-4 04 --- | G-4 06 --- | --- -- --- |
| 14 | --- -- --- | C-4 05 --- | --- -- --- | --- -- --- |
| 16 | A-4 01 --- | C-4 03 --- | A-4 06 --- | A-3 01 --- |
| 20 | B-4 01 --- | C-4 04 --- | A-4 06 --- | E-4 01 --- |
| 22 | --- -- --- | A-4 08 --- | --- -- --- | --- -- --- |
| 24 | A-4 01 --- | C-4 03 --- | A-4 06 --- | A-3 01 --- |
| 28 | --- -- --- | C-4 04 --- | A-4 06 --- | --- -- --- |
| 30 | C#5 01 --- | C-4 05 --- | --- -- --- | --- -- --- |
| 32 | B-4 01 --- | C-4 03 --- | B-4 06 --- | B-3 01 --- |
| 36 | A-4 01 --- | C-4 04 --- | B-4 06 --- | F#4 01 --- |
| 38 | --- -- --- | D-4 08 --- | --- -- --- | --- -- --- |
| 40 | G-4 01 --- | C-4 03 --- | B-4 06 --- | B-3 01 --- |
| 44 | F#4 01 --- | C-4 04 --- | B-4 06 --- | --- -- --- |
| 46 | --- -- --- | C-4 05 --- | --- -- --- | --- -- --- |
| 48 | E-4 01 --- | C-4 03 --- | G-4 06 --- | G-3 01 --- |
| 52 | --- -- --- | C-4 04 --- | G-4 06 --- | D-4 01 --- |
| 54 | F#4 01 --- | A-4 08 --- | --- -- --- | --- -- --- |
| 56 | D-4 01 --- | C-4 03 --- | D-4 06 --- | D-3 01 --- |
| 60 | --- -- --- | C-4 04 --- | D-4 06 --- | A-3 01 --- |

### Pattern 07 — "Coda: Release"
| Row | Ch1 | Ch2 | Ch3 | Ch4 |
|---|---|---|---|---|
| 0 | D-4 01 --- | C-4 03 --- | D-4 06 --- | D-3 01 --- |
| 2 | F#4 01 --- | C-4 05 --- | --- -- --- | --- -- --- |
| 4 | A-4 01 --- | C-4 04 --- | D-4 06 --- | D-3 01 --- |
| 6 | G-4 01 --- | A-4 08 --- | --- -- --- | --- -- --- |
| 8 | F#4 01 --- | C-4 03 --- | G-4 06 --- | G-3 01 --- |
| 10 | E-4 01 --- | C-4 05 --- | --- -- --- | --- -- --- |
| 12 | D-4 01 --- | C-4 04 --- | G-4 06 --- | G-3 01 --- |
| 14 | --- -- --- | D-4 08 --- | --- -- --- | --- -- --- |
| 16 | G-4 01 --- | C-4 03 --- | E-4 06 --- | E-3 01 --- |
| 18 | A-4 01 --- | C-4 05 --- | D-4 06 --- | --- -- --- |
| 20 | B-4 01 --- | C-4 04 --- | E-4 06 --- | E-3 01 --- |
| 22 | A-4 01 --- | G-4 08 --- | D-4 06 --- | --- -- --- |
| 24 | G-4 01 --- | C-4 03 --- | D-4 06 --- | D-3 01 --- |
| 26 | F#4 01 --- | C-4 05 --- | D-4 06 --- | --- -- --- |
| 28 | E-4 01 --- | C-4 04 --- | D-4 06 --- | D-3 01 --- |
| 30 | D-4 01 --- | F#4 08 --- | D-4 06 --- | --- -- --- |
| 32 | D-4 02 436 | C-4 03 --- | D-4 06 --- | D-3 01 --- |
| 36 | --- -- 436 | C-4 04 --- | A-4 06 --- | A-3 01 --- |
| 38 | --- -- 436 | A-4 08 --- | --- -- --- | --- -- --- |
| 40 | F#4 02 436 | C-4 03 --- | D-4 06 --- | D-3 01 --- |
| 44 | --- -- 436 | C-4 04 --- | G-4 06 --- | G-3 01 --- |
| 46 | --- -- 436 | D-4 08 --- | --- -- --- | --- -- --- |
| 48 | A-4 01 --- | C-4 03 --- | A-4 06 --- | A-3 01 --- |
| 50 | B-4 01 --- | C-4 05 --- | --- -- --- | --- -- --- |
| 52 | C#5 01 --- | C-4 04 --- | A-4 06 --- | A-3 01 --- |
| 54 | A-4 01 108 | C-4 05 --- | D-4 06 --- | --- -- --- |
| 56 | --- -- 108 | C-4 04 --- | --- -- --- | --- -- --- |
| 58 | --- -- 108 | C-4 04 --- | D-4 06 --- | --- -- --- |
| 60 | D-5 01 --- | C-4 03 --- | D-4 06 --- | D-3 01 --- |

### Compatibility Rules (unchanged)
```text
4 channels only
ProTracker-compatible effects only
No XM-only composition features
No notes below C-3
No notes above B-5
Forward sample loops only
No ping-pong loops
Pattern reuse preferred
Exact final runtime is unimportant
```
Bonus points if final `.mod` is under 40KB.

### Arbitrary Guidelines (unchanged)
- All unpitched percussion hits written as note `C-4`.
- Lone numbers output in hex format (e.g. "3f") unless otherwise specified.
- Effects explained on first use.

---

## 6. Testing State

**Not yet tested.** No `.mod` has been compiled from the pattern data above, and nothing has been loaded into MilkyTracker. All verification performed so far has been structural/arithmetic (loop-point bounds checked against real sample lengths, finetune nibbles decoded and cross-checked, note ranges checked against the stated per-instrument octave rules) — none of it is a substitute for actually hearing the piece play.

---

## 7. Next Steps

- Run the pattern data above through the custom compiler to produce the `.mod` file.
- Load the compiled `.mod` into MilkyTracker on PikaOS and audition the full 17-slot order list start to finish.
- Report back with any by-ear corrections needed (per the Source-of-Truth Hierarchy, these — not this bootstrap file — will be authoritative for loop points, volumes, per-row edits, and finetune).
