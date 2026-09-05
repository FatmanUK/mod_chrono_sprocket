# Pattern 00 Test

No true "oboe" exists in either archive; **PanFlute** is the closest haunting-woodwind candidate by name/character. Flagging this substitution for your approval — if you'd rather audition an alternative (e.g. ST-02's **Blower**), say so before I lock the motif map to it.

### Looping Recommendation
Forward-loop candidates (sustained/held roles): **PanFlute, MonoBass, RichString**.
No-loop, natural-decay candidates (transient/percussive/decaying roles): **Steinway, BassDrum1, Snare2, HiHat1, Glockenspiel**.
Final loop points are yours to set per the hierarchy.

### Volume/Envelope Analysis (measured directly from waveform data)

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

### Finetune — Missing Data, Per Document's Own Contingency

I searched for documented historical finetune values tied to these specific ST-01/ST-02 instrument names. **I found none.** Reason: the original Ultimate SoundTracker format (which these disks shipped with) predates the finetune field entirely — finetune was introduced later by NoiseTracker/ProTracker as a per-MOD authoring choice, not an inherent property of the sample. So "historical finetune value" doesn't exist as a fact to look up here — any value I supplied would be a guess, which your policy rules out.

Per the bootstrap's own fallback: **all eight samples are flagged for user-determined finetune, defaulting to 0 until you specify otherwise.**

### Note-Range Maps

Percussion (BassDrum1, Snare2, HiHat1) already fixed at **C-4** per your Arbitrary Guidelines.

For pitched samples, I don't have the original recorded base pitch (no metadata in the raw files), so I can't verify true low/high classification — only convention-based intent, pending your audition:

| Sample | Category | Octave range |
|---|---|---|
| MonoBass | Low-pitched | 4–5 |
| RichString | High-pitched (sits above bass) | 3–4 |
| PanFlute | High-pitched (solo register) | 3–4 |
| Glockenspiel | High-pitched | 3–4 |
| Steinway | Spans both — flagging deviation | 3–5 (full range, since it's the lead melodic voice; confirm during audition that no octave sounds aliased/broken) |

### Suggested Audition Criteria

1. **Steinway** — does it hold a believable "played by hand" tone across octaves 3–5, or does it thin out/alias at the extremes?
2. **PanFlute** — does its breathy wobble read as haunting/expressive when held, or just unstable?
3. **BassDrum1** — punchy enough to anchor Motif material at Speed 06 without needing volume compensation?
4. **Snare2 / HiHat1** — balance against BassDrum1 at the suggested volumes above.
5. **MonoBass** — smooth enough to loop without a clicking seam?
6. **RichString** — does its low peak (79) mean it needs a volume boost beyond 0x12, or does it work as a subtle bed?
7. **Glockenspiel** — decay length compatible with a 64-row pattern at this tempo, or does it ring past the next hit?

Please confirm/adjust the sample set, loop assignments, finetune values, and note-range calls above before I move to Step 3 (structural arc and motif map).

---

Despite the name, Steinway is not a piano sample. I don't know why it's named that way. Let's use ST-02/Pizza2 instead, and keep ST-01/RingPiano as a backup in case I decide against Pizza2.

I'll whip up a quick audition pattern. Please wait.

---

Understood — swapping the main melody instrument:

- **Primary: ST-02/Pizza2** (piano role)
- **Backup: ST-01/RingPiano**

I'll hold here and wait for your audition pattern before doing any further analysis or updating the volume/envelope/note-range data for the new candidate(s).

---

| Row | Ch1        | Ch2        | Ch3        | Ch4        |
|-----|------------|------------|------------|------------|
| 00  | C-4 01 E60 | C-4 04 C30 | C-5 06     | C-4 03     |
| 02  | ...        | C-4 04 C28 | ...        | C-4 03     |
| 04  | G-3 02     | C-4 05 C34 | C-4 07     | C-4 03     |
| 06  | ...        | C-4 05 C2C | ...        | C-4 03     |
| 08  | D-4 01     | ...        | ...        | C-4 03     |
| 10  | ...        | ...        | ...        | C-4 03     |
| 12  | B-3 02     | ...        | D-5 06     | C-4 03     |
| 14  | ...        | ...        | ...        | C-4 03     |
| 16  | E-4 01     | C-4 04 C30 | D-4 08     | C-4 03     |
| 18  | ...        | C-4 04 C28 | ...        | C-4 03     |
| 20  | D-4 02     | C-4 05 C34 | ...        | C-4 03     |
| 22  | ...        | C-4 05 C2C | ...        | C-4 03     |
| 24  | F-4 01     | ...        | E-5 06     | C-4 03     |
| 26  | ...        | ...        | ...        | C-4 03     |
| 28  | F-4 02     | ...        | E-4 07     | C-4 03     |
| 30  | ...        | ...        | ...        | C-4 03     |
| 31  | ... .. E63 | ...        | ...        | ...        |
| 32  | G-4 01 E60 | C-4 04 C30 | C-5 06     | C-4 03     |
| 34  | ...        | C-4 04 C28 | ...        | C-4 03     |
| 36  | F-4 02     | C-4 05 C34 | C-4 08     | C-4 03     |
| 38  | ...        | C-4 05 C2C | ...        | C-4 03     |
| 40  | A-4 01     | ...        | ...        | C-4 03     |
| 42  | ...        | ...        | ...        | C-4 03     |
| 44  | G-4 02     | ...        | D-5 06     | C-4 03     |
| 46  | ...        | ...        | ...        | C-4 03     |
| 48  | B-4 01     | C-4 04 C30 | D-4 07     | C-4 03     |
| 50  | ...        | C-4 04 C28 | ...        | C-4 03     |
| 52  | A-4 02     | C-4 05 C34 | ...        | C-4 03     |
| 54  | ...        | C-4 05 C2C | ...        | C-4 03     |
| 56  | C-5 01     | ...        | E-5 06     | C-4 03     |
| 58  | ...        | ...        | ...        | C-4 03     |
| 60  | B-4 02     | ...        | E-4 08     | C-4 03     |
| 62  | ...        | ...        | ...        | C-4 03     |
| 63  | ... .. E63 | ...        | ...        | ...        |
