# 01 — Patient Spine

The Spine is the patient-level data layer that lives above and around every episode. It is lifelong, never closes, and is composed of three visible elements: the Sticky Header, the Timeline sidebar, and the accordion of Spine sections (Profile, OB Performance, Surgical History, Reproductive).

## Default landing view

When the chart opens, the main screen is the **last visit of the active episode**. If no active episode exists, the most recent visit of any kind is shown.

The Timeline sidebar is visible by default on the left, with the active card highlighted and auto-scrolled into view. Sidebar can be minimized to a thin strip.

The Sticky Header sits above both, always visible.

## Sticky Header

Always-visible top bar carrying patient identity and quick actions.

**Fields:**
- Patient ID
- Name (EN + AR)
- Age (computed from date of birth)
- GPA (Gravida / Para / Abortion)
- Marital status
- Blood / Rh
- Allergies
- Current episode banner (e.g., "Pregnancy 20w 3d", "OI Cycle Day 7", "FET scheduled 18-Jan")
- Active flags rail (chronic illnesses, important surgical history, pinned findings)
- Action bar (see `08_STICKY_HEADER_ACTION_BAR.md`)

**Episode banner contents** vary by active episode type:
- Obstetrics: GA, EDD, twin flag if confirmed
- OI cycle: Protocol · Cycle Day · Next milestone (e.g., "OPU in 2 days")
- FET cycle: Protocol · Cycle Day · Next milestone (e.g., "FET 18-Jan")
- No active episode: blank or shows last episode closed

## Timeline sidebar

Chronological stack of episode cards, **oldest at top, newest at bottom**. Auto-generated from closed episodes; manually editable (add, remove, edit cards).

Mimics the user's paper-flipping mental model: at a glance, see what happened in order without diving into details.

**Card formats (one-liners):**
- Gynae visit → `Gynae · [type] · [date]` (e.g., "Gynae · IUD insertion · Mar 2022")
- Pregnancy → `Pregnancy G# · [outcome] · [year]` (e.g., "G2 · CS term · 2023")
- OI cycle → `OI/ICSI · [protocol] · [outcome]` (e.g., "ICSI · Progestin P · freeze-all, 2 emb")
- FET cycle → `FET · [protocol] · [outcome]` (e.g., "FET Letrozole · β+")
- Surgery → `Surgery · [procedure] · [year]`

Tap any card → opens full episode.

## Profile section

Demographic and identity data not in the header.

- Address
- Contact (phone, secondary phone, email)
- Occupation
- ID number
- Referral source
- Weight (latest, editable anywhere; logged per OB visit, see `03_OBSTETRICS.md`)
- Chronic illnesses
- Chronic medications
- Family history

**Not included:** BMI, height (used rarely; can add as a flagged finding if needed).

## OB Performance section

Brief summary of every prior pregnancy. One line per pregnancy:

- G# · year · GA at delivery · mode of delivery · outcome · baby gender · baby weight · complications flag

Tap-in opens the full closed Obstetrics episode for that pregnancy.

**Not tracked here:** breastfeeding history.

## Surgical History section

Free-form list of past surgeries. Collapses when long.

Each entry is free-text; no rigid schema. Date if known.

## Reproductive section

Infertility workup data + ART Summary nested inside.

**Fields:**
- Menstrual cycle history (length, regularity, dysmenorrhea, LMP) — captured for **all** patients, not just infertility cases.
- AMH — latest value prominent; tap to view prior values as a list. **No graph.**
- HSG — own assessment.
- Cavity assessment.
- AFC — latest value with date prominent; measured every visit in infertility patients; tap to view history list. **No graph.**
- Husband data + semen analysis.

### ART Summary (nested)

Live counters and history for assisted reproduction:

- Live frozen embryo count (single patient-level number, not per cycle)
- Cycles to date by purpose (TI / IUI / IVF-ICSI / FET counts)
- Outcomes summary (pregnancies / negatives / cancellations)
- Link to latest cycle

**Embryo bank rules:** patient-level counter. Increments on freeze, decrements on transfer. Tube-level detail and embryo photos remain in the originating cycle's record; the Spine shows only the headline number.

## Pin-to-header mechanism

Any finding from any episode can be promoted to the Sticky Header's flags rail.

**Gesture:** pin icon next to fields where layout permits; long-press fallback elsewhere.

**Pin metadata:** each pinned flag carries source (date + originating episode). Tapping a header flag jumps back to where it was first noted.

**Proactive AI suggestions** (e.g., auto-prompt when "bicornuate" is typed): **deferred**. Toggleable in Settings later.

## AMH dual-homing

AMH appears in two places:
- Reproductive section (latest + history list)
- Investigations panel (timestamped row alongside other labs)

Single source of truth, mirrored to both views. Editing in either place updates both.

## Settings hooks

- Auto-purge windows for media/attachments
- Abnormal-result cutoffs for auto-flagging (deferred for v1)
- Proactive pin suggestions toggle (deferred for v1)
- Bundle definitions

## Cross-references

- Sticky Header action bar → `08_STICKY_HEADER_ACTION_BAR.md`
- Pregnancy episode (writes to OB Performance) → `03_OBSTETRICS.md`
- IVF/FET cycles (writes to ART Summary, embryo bank) → `04_IVF_FET_CYCLES.md`
- Closure writeback → `10_EPISODE_CLOSURE.md`

## Changelog

- v1.0 — Initial spec.
