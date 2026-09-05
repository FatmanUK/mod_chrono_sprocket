# Sample Set

## Selected Eight Samples

| Role | Sample | Source |
|---|---|---|
| Main melody (piano) | **Steinway** | ST-01 |
| Haunting woodwind solo | **PanFlute** | ST-01 |
| Heartbeat kick | **BassDrum1** | ST-01 |
| Snare | **Snare2** | ST-01 |
| Hi-hat | **HiHat1** | ST-01 |
| Bass pulse | **MonoBass** | ST-01 |
| Pad | **RichString** | ST-01 |
| Metallic chime | **Glockenspiel** | ST-02 |

No true "oboe" exists in either archive; **PanFlute** is the closest haunting-woodwind candidate by name/character. Flagging this substitution for your approval — if you'd rather audition an alternative (e.g. ST-02's **Blower**), say so before I lock the motif map to it.

## Note-Range Maps

Percussion (BassDrum1, Snare2, HiHat1) already fixed at **C-4** per your Arbitrary Guidelines.

For pitched samples, I don't have the original recorded base pitch (no metadata in the raw files), so I can't verify true low/high classification — only convention-based intent, pending your audition:

| Sample | Category | Octave range |
|---|---|---|
| MonoBass | Low-pitched | 4–5 |
| RichString | High-pitched (sits above bass) | 3–4 |
| PanFlute | High-pitched (solo register) | 3–4 |
| Glockenspiel | High-pitched | 3–4 |
| Steinway | Spans both — flagging deviation | 3–5 (full range, since it's the lead melodic voice; confirm during audition that no octave sounds aliased/broken) |

## Looping Recommendation
Forward-loop candidates (sustained/held roles): **PanFlute, MonoBass, RichString**.
No-loop, natural-decay candidates (transient/percussive/decaying roles): **Steinway, BassDrum1, Snare2, HiHat1, Glockenspiel**.
Final loop points are yours to set per the hierarchy.

## Volume/Envelope Analysis (measured directly from waveform data)

| Sample | Length (bytes) | Peak (0–127) | RMS | Envelope shape | Suggested default vol (dec/hex) |
|---|---|---|---|---|---|
| Steinway | 6900 | 127 | 32.6 | Sharp attack, smooth long decay — plucked/struck string behavior | 23 / 0x17 |
| PanFlute | 9900 | 116 | 45.9 | Uneven, breathy oscillation — vibrato-like RMS wobble | 33 / 0x21 |
| BassDrum1 | 1100 | 128 | 89.3 | Very fast, punchy transient, quick decay | 64 / 0x40 (reference) |
| Snare2 | 1900 | 128 | 46.9 | Sharp crack, moderate decay | 34 / 0x22 |
| HiHat1 | 1400 | 127 | 38.8 | Sustained noisy decay, slower than typical closed hat | 28 / 0x1C |
| MonoBass | 6600 | 127 | 45.2 | Even, sustained — good pulse candidate | 32 / 0x20 |
| RichString | 6900 | 79 | 25.6 | Slow swell, low peak — genuinely soft pad | 18 / 0x12 |
| Glockenspiel | 7600 | 94 | 21.1 | Bright transient, long bell-like decay | 15 / 0x0F |

Volumes are scaled relative to BassDrum1 as the loudest reference; treat these as a mix starting point, not final.

## Finetune — Missing Data, Per Document's Own Contingency

I searched for documented historical finetune values tied to these specific ST-01/ST-02 instrument names. **I found none.** Reason: the original Ultimate SoundTracker format (which these disks shipped with) predates the finetune field entirely — finetune was introduced later by NoiseTracker/ProTracker as a per-MOD authoring choice, not an inherent property of the sample. So "historical finetune value" doesn't exist as a fact to look up here — any value I supplied would be a guess, which your policy rules out.

Per the bootstrap's own fallback: **all eight samples are flagged for user-determined finetune, defaulting to 0 until you specify otherwise.**

## Instrument Set (Step 2 — CONFIRMED, sample audition passed)

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
