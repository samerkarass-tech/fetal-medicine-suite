# 03 — Obstetrics

A Pregnancy is an episode that branches off the Gynae trunk via "Start Pregnancy." It tracks the pregnancy from booking through delivery and closes with the postpartum visit.

## Lifecycle

- **Opens** when "Start Pregnancy" is clicked from a Gynae visit (or auto-created from a β+ closure of an OI/FET cycle — see `04_IVF_FET_CYCLES.md` and `10_EPISODE_CLOSURE.md`).
- **Closes** at the postpartum visit.
- Multiple pregnancies per patient over time; each is its own episode.

## Header flag

**Twin pregnancies** handled via a header flag on the episode banner. Auto-armed as a yellow "confirm at first scan" prompt when 2 embryos are transferred from an OI/FET cycle; sets firmly only after first scan confirmation.

## Trimester scan markers

A pinned strip at the top of the Pregnancy episode shows three scan cards: **1st trimester**, **Anomaly**, **3rd trimester**.

Each card is intentionally lightweight:
- A **Done** checkbox.
- A **short free-text note** (e.g., "unremarkable", "single live fetus, placenta anterior").

No structured measurement fields (no BPD/FL/AC/AFI/EFW, no Hadlock auto-calc). Detailed measurements live in the external US reporting system; the chart only needs a checkbox-plus-hint that the scan happened and what it showed.

Unchecked cards remain visible throughout the episode and act as a passive reminder to do the scan at the appropriate GA. Once checked, the note becomes the inline summary.

## Longitudinal visit table

Core view of the episode: a longitudinal table of every visit, **oldest → newest**, top → bottom.

**Columns:**
- Date
- GA (gestational age)
- BP (blood pressure)
- Wt (weight)
- Complaint
- Exam
- US (ultrasound)
- Inv (investigations)
- Rx (prescriptions)
- Plan

Each row = one visit. Editable inline.

## Ultrasound field

Hybrid:
- **Free-text** primary input.
- **Structured fields** available for key measurements (BPD, FL, AC, AFI, EFW, Doppler indices, etc.).
- **Presets** drive both via the per-field preset dropdown (see `07_PRESET_LIBRARY.md`).

The doctor does not author full US reports here (those live in another system). The US field captures the summary used in the chart context — typically a one-liner like "single living fetus, placenta anterior, AFI normal."

## Future reminders

Patient-bound reminders fire by GA, by next visit, or by specific date. See `05_REMINDERS.md`.

Examples:
- "Stop aspirin at 36w"
- "Recheck Hb next visit"
- "Sedation before spinal at delivery"

These appear as a deletable strip at the top of the visit screen and as inline yellow-highlight echoes in the relevant row.

## Per-trimester investigation bundles

The investigations side rail offers per-trimester bundles (1st / 2nd / 3rd trimester) that order a batch of routine investigations in one tap. Bundles are editable in Settings.

See `06_INVESTIGATIONS.md`.

## Episode closure (Postpartum)

The Postpartum visit closes the Pregnancy episode and writes back to OB Performance on the Spine. See `10_EPISODE_CLOSURE.md`.

**Closure outcome fields:**
- Mode of delivery
- GA at delivery
- Baby gender
- Baby weight
- Complications flag
- Free-text notes

Closure does not block on missing data.

## Tags carried from cycle origin

When a Pregnancy episode is auto-created from a β+ OI/FET cycle closure:
- **Conception date** auto-computed from ET date and embryo age (D5 → ET − 5; D3 → ET − 3). Editable.
- **EDD** computed from conception date (LMP-equivalent = conception − 14; EDD = LMP-equivalent + 280). Editable.
- **Origin tag** appears in the episode banner: "Conceived via ICSI", "FET, single embryo", "FET, 2 embryos", etc.
- **Twin flag** pre-armed if 2 embryos transferred (yellow, confirm at first scan).

## Cross-references

- Branching from Gynae → `02_GYNAE_TRUNK.md`
- Cycle β+ handoff → `04_IVF_FET_CYCLES.md`
- Reminders → `05_REMINDERS.md`
- Investigations side rail and bundles → `06_INVESTIGATIONS.md`
- Presets on US/exam fields → `07_PRESET_LIBRARY.md`
- Closure flow → `10_EPISODE_CLOSURE.md`

## Changelog

- v1.0 — Initial spec.
- v1.1 — Replaced the structured trimester scan accordion (BPD/FL/AC/AFI/EFW with Hadlock auto-calc) with a lightweight three-card pinned strip: Done checkbox + short free-text note for 1st trimester / Anomaly / 3rd trimester. Detailed measurements move out of scope.
