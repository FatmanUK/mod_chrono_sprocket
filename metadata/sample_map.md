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
