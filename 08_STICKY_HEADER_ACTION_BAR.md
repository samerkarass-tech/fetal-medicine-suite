# 08 — Sticky Header Action Bar

Six buttons on the Sticky Header, with defined behaviors.

## Briefing

**Flagship feature.** Generates a chronological summary of the patient on demand.

### v1: templated summary

- System pulls structured data (Spine sections, episode list, latest values, pinned flags, outstanding reminders, pending investigations) and formats deterministically.
- **No LLM call.** No hallucination risk. Fast, cheap.
- Data structure is well-defined (see `01_PATIENT_SPINE.md`), so the templated brief reads well.

### Upgrade path

- v2: LLM-generated paragraph for more natural narrative.
- v3: question-asking ("What was her response to letrozole last cycle?").

### Length

- **Adjustable** toggle: short / medium / long.
- Defaults to short.

### Content

- Headline: name, age, GPA, marital status.
- Active episode + key context (GA, cycle day, planned OPU/FET, etc.).
- Pinned flags from header (chronic conditions, important findings).
- Last visit summary — date and what happened.
- Outstanding patient-bound reminders.
- Pending investigation results.
- Recent significant events (last delivery, last cycle outcome).

### Generation behavior

- **Cached, regenerated silently after each chart save.** Instant when tapped.
- Does NOT override the default landing view (chart still opens to last visit, not to briefing).

### Audience

- For the doctor only in v1.
- "Generate referral letter" is a separate future feature, not part of Briefing.

## Schedule

Opens the shared clinic calendar.

### Calendar scope

- **One calendar with role-based filtered views** — single source of truth, doctor and secretary each see what's relevant by default with toggle to see everything.

### Two scheduling modes

- **Visit** (any type)
- **Surgery / OR**

### From the chart

- Pre-fills the patient when opened from inside that patient's chart.

### Surgery scheduling fields

- Date, time
- Procedure name
- OR room
- Anesthesia type
- Expected duration
- Notes

### No auto pre-op admin tasks

- Scheduling a surgery does NOT auto-create secretary tasks for consent, blood work, etc.

### Practical use

- Visits are typically delegated to the secretary via the task system (see `05_REMINDERS.md`).
- Doctor mostly uses Schedule for surgeries personally.

## Media

Opens the unified patient media gallery. Aggregates every file ever attached anywhere in the patient's chart (Investigations, cycle Media tab, Quick-capture, embryo photos).

See `09_MEDIA_HANDLING.md`.

## Reminders

Opens this patient's full reminder list — patient-bound reminders only. Add / edit / mark done.

See `05_REMINDERS.md`.

## Edit

Tap-to-edit anywhere is the **default**. Most fields are inline-editable wherever they appear.

### Protected identity fields

- **Name and Patient ID** are NOT inline-editable.
- Editable only via a dedicated **Edit Profile** screen reachable from this Edit button.
- Changes require an extra confirmation step.

### Audit log

- Not in v1. Deferred.

## Complete

Closes the current episode. Triggers the closure flow.

See `10_EPISODE_CLOSURE.md`.

## Quick-capture (related)

The **Quick-capture camera button** is on the Sticky Header but described separately in `06_INVESTIGATIONS.md` and `09_MEDIA_HANDLING.md`. It is not part of the action bar's six core buttons but lives in the same header zone.

## Cross-references

- Spine data sources for Briefing → `01_PATIENT_SPINE.md`
- Calendar scope ↔ task delegation → `05_REMINDERS.md`
- Media gallery → `09_MEDIA_HANDLING.md`
- Reminder list → `05_REMINDERS.md`
- Closure flow → `10_EPISODE_CLOSURE.md`

## Changelog

- v1.0 — Initial spec.
