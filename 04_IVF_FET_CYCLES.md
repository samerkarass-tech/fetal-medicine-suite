# 04 — IVF / FET Cycles

Stimulation cycles (OI) and Frozen Embryo Transfer (FET) cycles are sub-episodes branching off the Gynae trunk. They cover the full assisted-reproduction workflow: stimulation, monitoring, OPU, lab results, embryo bank, and frozen embryo transfer.

## Branching from Gynae

Two buttons on the Gynae trunk visit row:

- **Start Stimulation Cycle** → opens an OI template with a **purpose selector** (TI / IUI / IVF-ICSI). OPU + lab + frozen embryo blocks render only when purpose = IVF-ICSI.
- **Start FET** → opens an FET template.

A "Plan FET" shortcut also appears on a freeze-all cycle's outcome screen — same destination as the Gynae trunk button.

## Carry-forward from Gynae

When you click "Start Stimulation Cycle," the new OI cycle pre-pulls from the most recent Gynae visit that committed the plan:

- Protocol name
- Drug list with doses
- Planned start date
- Purpose

All editable on arrival.

If the previous cycle was cancelled, its **cancellation reason + carry-forward note** surface as a dismissible banner at the top of the new cycle (informational, not auto-applied).

## OI cycle structure

### Header

- Protocol name (free-text or preset; editable mid-cycle)
- LMP
- Purpose selector (TI / IUI / IVF-ICSI)
- Modifier flags (e.g., "Freeze All", "ICSI 25k")

### Monitoring table

Columns are added per visit day, dynamically. Rows are vertical.

**Always-present rows:**
- Day
- Date
- E2 (estradiol)
- P4 (progesterone)
- LH
- Endometrium (thickness + pattern, e.g., "P3 5mm")
- Rt Ovary (follicle counts/sizes)
- Lt Ovary (follicle counts/sizes)

**AFC baseline column** before Day 1.

**Medication rows** added on demand:
- "+ Add medication" creates a new row.
- Daily dose cells per visit column.
- Edit dose mid-cycle by editing the relevant cell.
- Stop a med by writing "STOP" / "0" / equivalent.
- Cancel a row entirely if needed.

**Per-cell scan images** can be attached (one or more images per cell).

### Trigger event

Trigger shot is a **discrete milestone event**, not a med row.
- Timestamped.
- Auto-schedules OPU at +36 hours.
- Visible on the cycle banner as "OPU in 2 days" once set.

### OR results (post-OPU)

Timestamped event block, filled in same-day or next day:

- Total oocytes retrieved
- M2 count
- M1 count
- GV count

### Lab results (D3 / D5 post-OPU)

Timestamped event block, filled in when results return:

- D3 fertilized embryos (if used)
- D5 fertilized embryos (predominantly used in this practice)

### Frozen embryos

When embryos are frozen at the end of a cycle:
- Tube list with embryo count per tube (free-form numbered list).
- Embryo photos attached (live in the cycle's Media tab, labeled per embryo, e.g., "D5 #1, #2").
- **The patient-level embryo bank counter on the Spine increments** by the number frozen.

## FET cycle structure

### Header

- Protocol selector (Natural / Letrozole / HRT / Stimulated) — editable, custom protocols allowed.
- LMP
- Notes

### Monitoring table

Same structure as OI cycle (always-present rows, dynamic visit columns, dynamic med rows). In practice, FET monitoring uses fewer rows actively — typically Endometrium and P4 plus the meds — but the full row set is available.

### FET event

Discrete milestone:
- FET date
- Number of embryos transferred (typed value — **decrements the patient-level embryo bank** by this number)
- Single / double embryo flag for downstream tagging
- Notes (e.g., "smooth", "difficult catheter")

## Cycle banner (Sticky Header during active cycle)

- Protocol · Cycle Day · Next milestone (e.g., "OPU in 2 days", "FET 18-Jan")

Spine accordion handles age, AMH, fibroids, endometriosis, husband data — one click away.

## Closure menu

Editable / extensible (free-text "Other" always available):

- Cancelled (reason)
- Fresh ET β+ → auto-creates Obstetrics episode
- Fresh ET β−
- Freeze-all
- FET β+ → auto-creates Obstetrics episode
- FET β−
- Other (free text)

**Cancelled cycle:** logs reason; bank unchanged; carry-forward note (free-text) saved to surface at the next cycle's banner.

## β+ handoff to Obstetrics

When a cycle closes positive:

- New Obstetrics episode auto-created.
- **Conception date** = ET − 5 (D5 transfers) or ET − 3 (D3 transfers). Editable.
- **LMP-equivalent** = conception − 14.
- **EDD** = LMP-equivalent + 280. Editable.
- **Origin tag** carried to OB sticky-header banner: "Conceived via ICSI" / "FET, single embryo" / "FET, 2 embryos" / etc.
- **Twin flag** pre-armed (yellow, confirm at first scan) if 2 embryos transferred. Sets firmly on first-scan confirmation.

## Frozen embryo bank

- **Single patient-level counter** lives on the Spine (ART Summary, inside Reproductive section).
- Increments on freeze; decrements on transfer (typed-number model — user does not pick specific embryos).
- Tube-level detail and embryo photos remain in the originating cycle's record only.
- No hard FET ↔ IVF link required; FETs are free-standing on the Gynae trunk and just decrement the bank.

## OR / Lab results bubble-up

Aggregate counts (oocytes, M2/M1/GV, D3/D5 fertilized, frozen) bubble up to the Spine's ART Summary so the doctor can see lifetime ART numbers without diving into individual cycles.

## β-hCG result

Lives in the cycle outcome only (not in the Investigations panel).

## Cycle monitoring values (E2/P4/LH/endometrium during stim)

Live in the cycle's monitoring table only. Do not enter the Investigations panel.

## AMH

Lives in **both** the Investigations panel and the Reproductive section of the Spine. Single source of truth, mirrored to both views.

## Cross-references

- Gynae trunk branching → `02_GYNAE_TRUNK.md`
- Spine ART Summary, embryo bank → `01_PATIENT_SPINE.md`
- Obstetrics handoff → `03_OBSTETRICS.md`
- Investigations boundary → `06_INVESTIGATIONS.md`
- Closure mechanics → `10_EPISODE_CLOSURE.md`
- Schedule integration (OPU / FET booking) → `08_STICKY_HEADER_ACTION_BAR.md`

## Changelog

- v1.0 — Initial spec.
