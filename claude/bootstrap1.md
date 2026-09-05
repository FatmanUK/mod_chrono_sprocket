# Chrono Sprocket: Project Bootstrap File (Updated)

**Project:** Chrono Sprocket
**Status:** In Progress — Step 3 complete, pattern data not yet written
**Tracker:** MilkyTracker
**Platform:** Linux / PikaOS
**Target format:** 4-channel ProTracker MOD

---

## 1. Current Goal

Write actual pattern data (Step 4) for "Chrono Sprocket" — an original, polished, 1990s-Amiga-game-style attract-mode `.mod`, built from the finalized 8-instrument sample set, structural arc, and motif map below. Patterns are authored in the compiler-input MarkDown table format (see Pattern Format), not entered directly into MilkyTracker.

---

## 2. State of Play

### Source-of-Truth Hierarchy (unchanged from original bootstrap)
1. **Auditioned project files** are authoritative for: exact sample loop points, exact sample volumes, exact per-row volume edits, exact finetune values, any last by-ear edits.
2. **This bootstrap file** is authoritative for: project architecture, pattern roles, order list, note/rhythm/effect structure, final sample identities, tested status.
3. **Sample archives** (ST-01, ST-02) are only the source of the sample files.

### Primary Goal / Character (unchanged)
- Jaunty, cheerful, engaging game-title "attract" tune
- Main melody instrument: piano-type (see Instrument Set — Pizza2)
- Piano should sound human-played: not too fast or staccato
- Haunting oboe-type solo (substituted with PanFlute) over two patterns
- Heavy pattern reuse; interesting pattern order list
- Inspirations: Tim Wright / David Whittaker
- Unmistakably early-1990s tracker construction
- 4 channels, 64 rows per pattern
- Runtime 85–105s as a loose guideline only — **not a hard constraint; creativity takes priority over hitting an exact runtime** (per user direction)
- No XM-only features; strict PT2 compatibility

### Title & Tempo (Step 1 — CONFIRMED)
- **Title:** Chrono Sprocket
- **Speed:** 06
- **Tempo (BPM):** 7D (125 decimal)
- Chosen deliberately for a **laid-back feel** (user preference) over a punchier arcade pulse (Speed 05 was considered and rejected).

### Instrument Set (Step 2 — CONFIRMED, sample audition passed)

All sample stats below were measured directly from the raw 8-bit signed PCM sample data (no header/metadata present in the archives — sample rate and original recorded pitch are not recoverable from the files themselves).

| ID | Role | Source | Sample | Volume | Finetune | Loop (start/length) | Note range |
|----|------|--------|--------|--------|----------|----------------------|------------|
| 1 | Main melody (piano-type) | ST-02 | **Pizza2** | 0x17 | 0xD (−3) | none | 3–5 (unrestricted) |
| — | *backup for #1, not active* | ST-01 | RingPiano | 0x10 | 0x0 (0 or +1, TBD) | none | — |
| 2 | Haunting woodwind solo | ST-01 | **PanFlute** | 0x21 | 0xE (−2) | 0x1FE5 + 0x0051 | 3–4 (high) |
| 3 | Heartbeat kick | ST-01 | **BassDrum1** | 0x40 | — | none | C-4 only |
| 4 | Snare | ST-01 | **Snare2** | 0x22 | — | none | C-4 only |
| 5 | Hi-hat | ST-01 | **HiHat1** | 0x1C | — | none | C-4 only |
| 6 | Bass pulse | ST-01 | **MonoBass** | 0x20 | 0xB (−5) | 0x0AC2 + 0x0181 | 4–5 (low-to-medium) |
| 7 | Pad | ST-01 | **RichString** | 0x12 | 0xE (−2) | 0x09F6 + 0x10FC | 3–4 (medium-to-high) |
| 8 | Metallic chime | ST-02 | **Glockenspiel** | 0x28 | 0xD (−3) | none | 3–4 (high) |

**Decision history on instrument #1:** Originally "Steinway" (ST-01) was selected on the mistaken assumption it was a piano sample — user corrected this (despite the name, it is not a piano sample; reason unknown). Replaced with **ST-02/Pizza2** as primary, **ST-01/RingPiano** retained as an explicit backup in case Pizza2 is rejected later.

**Decision history on instrument #2:** ST-02/Blower was considered as an alternative to PanFlute; user confirmed a preference for **PanFlute**. Blower is no longer under consideration.

**Verification performed (this session):**
- All three loop points (PanFlute, MonoBass, RichString) checked arithmetically against real sample file lengths — all within bounds, no errors found.
- All finetune hex nibbles decoded against PT signed-nibble convention (0x0–0x7 = 0…+7, 0x8–0xF = −8…−1) and cross-checked against the user's own inline comments — all consistent, no discrepancies.

**Outstanding/unresolved:**
- RingPiano's finetune is marked TBD in `song.yml` (0x0, commented "0 or +1") — only relevant if Pizza2 is later rejected.
- Historical finetune values for these instruments were searched for and **do not exist as documented data** — the original Ultimate SoundTracker format (which ST-01/ST-02 shipped with) predates the finetune field entirely; finetune is a per-MOD authoring choice, not an inherent sample property. All finetune values in `song.yml` are therefore user-determined by ear, not sourced.

### Structural Arc (Step 3 — CONFIRMED)

Narrative seed: a clockwork mechanism waking, turning, and springing loose.

1. **Wind-up** — mechanism assembling itself, motif fragments entering one at a time
2. **Engagement** — full main theme running at speed, jaunty and confident
3. **Inner mechanism** — haunting solo section, as if we've been let inside the casing
4. **Re-engagement** — main theme returns, denser/more confident than first pass
5. **Release** — coda: the spring lets go — a flourish, not a fade-out

### Motif Map (Step 3 — CONFIRMED)

- **Motif A — "Ratchet Pulse":** BassDrum1 + MonoBass locked ostinato. Mechanical heartbeat/pulse underpinning most of the piece.
- **Motif B — "Drive Theme":** Pizza2 carrying the main jaunty melody. Circling, singable phrase, question/answer shape across 4-bar halves.
- **Motif C — "Sprocket Glint":** Glockenspiel accents on off-beats or phrase endings. Sparse, never sustained.
- **Motif D — "Inner Drift":** PanFlute solo over sustained RichString pad. Slow-moving, rubato-feeling within fixed tempo, minimal/no percussion underneath.

**Pattern roles as motif recombinations** (patterns layer motifs, not one-motif-per-pattern):
- Intro pattern: A entering alone, then B fragments layered in (wind-up)
- Main theme pattern(s): A + B + C together (full engagement)
- Chime-forward/bridge pattern: A + B (thinned) + C emphasized
- Drift pattern(s): D alone or D + sparse A (contrast section)
- Reprise pattern: A + B (denser/varied) + C (re-engagement)
- Coda pattern: fragments of A/B/C compressed and re-voiced into a final flourish (not a new motif)

Intent: low pattern count, heavy reuse; the *order list* — not new pattern content — creates the felt structure. Same pattern may serve double duty (e.g. intro pattern's tail reused as connective tissue before the coda).

---

## 3. Dependency Map

- **Tracker (testing only):** MilkyTracker, on PikaOS
- **Target runtime format:** ProTracker 2 (PT2) `.mod`, 4-channel
- **Pattern authoring:** custom external compiler (not MilkyTracker's own editor) — consumes MarkDown-table pattern data, see Pattern Format below
- **Sample archives:** ST-01, ST-02 (raw 8-bit signed PCM, headerless; user-supplied as tarballs, extracted and analyzed this session)
- No other tools/libraries in use.

---

## 4. Open Issues

- Exact final loop-point/volume/finetune values remain subject to the user's own by-ear adjustment per the Source-of-Truth Hierarchy — nothing in Section 2 above should be treated as beyond revision.
- RingPiano is an inactive backup; if activated, its finetune (currently a TBD placeholder) will need to be actually determined, not assumed.
- No pattern data has been written yet — order list currently empty in `song.yml` (placeholder `orderList: [0]`).
- Woodwind solo instrument is a substitution (PanFlute for an oboe); flagged and accepted by user, but worth remembering this is a compromise choice if future revision is considered.

---

## 5. "Golden" Code Blocks

### Instrument definitions (current authoritative source: user-provided `song.yml`, verified this session)

```yaml
title: Chrono Sprocket
speed: 6
bpm: 125
orderList:
  - 0
instruments:
  - id: 1
    source: st02
    name: ST-02/Pizza2
    volume: 0x17
    finetune: 0xd  # -3
    #source: st01
    #name: ST-01/RingPiano
    #volume: 0x10
    #finetune: 0x0  # 0 or +1
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
    volume: 0x20
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

### Pattern Format (compiler input spec — unchanged from original bootstrap)

Patterns are NOT entered into MilkyTracker directly; a custom compiler consumes them in this row format:

```
| RR | NNN II EEE | NNN II EEE | NNN II EEE | NNN II EEE |
```
- `RR` = row number
- `NNN` = note
- `II` = instrument slot
- `EEE` = effect

Compatible with MarkDown tables — each pattern gets a MarkDown table header with columns `Row`, `Ch1`, `Ch2`, `Ch3`, `Ch4`. No instrument = `--`. No effect = `---`. Omit entirely empty lines.

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
- Unless otherwise specified or required, output lone numbers in hex format (e.g. "3f").
- Explain effects the first time they're used.

---

## 6. Testing State

No pattern data exists yet, so there is nothing to test in MilkyTracker at this stage. All work so far (sample selection, volume/envelope measurement, loop-point and finetune verification) has been checked arithmetically against the actual extracted sample files, not assumed — see verification notes in Section 2.

---

## 7. Next Steps

- Begin writing the **intro pattern** (Motif A alone, then B fragments entering) in the compiler MarkDown table format.
- Write the **main theme pattern(s)** combining Motifs A + B + C.
- Write the **drift pattern(s)** for the PanFlute/RichString solo section (Motif D), respecting the confirmed note-range restrictions (PanFlute/RichString/Glockenspiel: octaves 3–4; MonoBass: octaves 4–5; Pizza2: unrestricted 3–5; percussion: C-4 only).
