# 10 — Episode Closure Flow

Generic mechanics for closing any episode (Pregnancy, OI cycle, FET cycle, Surgery). The Gynae trunk does NOT close — it persists for the patient's lifetime.

## What is an episode

Anything with a beginning and an end that lives on the Gynae trunk:

- **Pregnancy** (Obstetrics) — opens at "Start Pregnancy"; closes at the postpartum visit.
- **OI / Stimulation cycle** — opens at "Start Stimulation Cycle"; closes per its closure menu.
- **FET cycle** — opens at "Start FET"; closes per its closure menu.
- **Surgery** — single event, closes when done.

Individual Gynae visits are cards on the trunk, not episodes — they don't close in this sense.

## Closing motion

1. Doctor taps **Complete** in the action bar of the active episode.
2. **Closure screen** appears with outcome fields specific to the episode type.
3. Fields are pre-filled from existing data where possible; doctor confirms or fills the rest.
4. Closure **never blocks** on missing data. Partial closure is allowed.
5. On confirm:
   - Outcome is recorded.
   - Spine writeback runs (see "Writeback" below).
   - A card is added to the Timeline.
   - Episode banner clears from the Sticky Header.

## Outcome fields by episode type

### Pregnancy

- Mode of delivery
- GA at delivery
- Baby gender
- Baby weight
- Complications flag
- Free-text notes

(Postpartum visit handled separately as a Gynae trunk visit linked to this closure — see `02_GYNAE_TRUNK.md`.)

### OI / Stimulation cycle

- Outcome: Cancelled / Fresh ET β+ → OB / Fresh ET β− / Freeze-all / Other (free text)
- Cancellation reason + carry-forward note (if cancelled)
- Embryo counts (oocytes, M2/M1/GV, D3/D5 fertilized) — typically already filled during the cycle
- Frozen embryo additions to bank
- β-hCG result if fresh transfer

### FET cycle

- Outcome: β+ → OB / β− / Cancelled / Other (free text)
- β-hCG result
- Embryos transferred (decrements bank)
- Cancellation reason + carry-forward note (if cancelled)

### Surgery

- Procedure done
- Complications
- Free-text notes

## Writeback to Spine

| Episode | Writes to |
|---|---|
| Pregnancy | OB Performance section (one new line per pregnancy) |
| OI cycle | ART Summary (cycle counts, outcome, embryo bank delta) |
| FET cycle | ART Summary (cycle counts, outcome, embryo bank delta) |
| Surgery | Surgical History |

In addition, **all closures** add a card to the Timeline (one-liner format per `01_PATIENT_SPINE.md`).

## β+ closures auto-create a new Pregnancy episode

When OI or FET closes positive:

- New Obstetrics episode auto-spawns.
- Conception date computed from ET date and embryo age (D5 → ET − 5; D3 → ET − 3). Editable.
- EDD computed from conception date (LMP-equivalent = conception − 14; EDD = LMP-equivalent + 280). Editable.
- Origin tag carried to OB sticky-header banner.
- Twin flag pre-armed (yellow, confirm at first scan) if 2 embryos transferred.

See `04_IVF_FET_CYCLES.md` for full handoff details.

## Reopen

Closed episodes can be reopened.

On reopen:
- Spine writeback is reverted.
- Timeline card is removed (or marked as active again).
- Episode returns to active state.
- Edits resume normally.

## Sealed vs editable

- Closed but **not sealed.** Content remains editable after closure (since reopen exists).
- The closure event itself is reversible.

## Cross-references

- Pregnancy specifics → `03_OBSTETRICS.md`
- OI / FET specifics, conception math, twin flag → `04_IVF_FET_CYCLES.md`
- Spine writeback targets → `01_PATIENT_SPINE.md`
- Postpartum dual-view → `02_GYNAE_TRUNK.md`
- Complete button on action bar → `08_STICKY_HEADER_ACTION_BAR.md`

## Changelog

- v1.0 — Initial spec.
