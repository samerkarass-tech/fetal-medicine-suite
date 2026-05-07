# 06 — Investigations Side Rail

Investigations live in a per-episode panel, accessible but not in your face. Includes a stripped-down Assistant Inbox for secretary-side result entry.

## Structure

**Per-episode panels.** Each Gynae trunk, each Pregnancy, each OI cycle, each FET cycle has its own Investigations panel showing only that episode's investigations. Tap-to-expand opens a patient-level lifetime view.

**Resting state:** thin collapsed bar on the right edge of the screen. Hover to peek; click to open fully.

## Open panel layout

**Top: Bundle launcher**
- One-tap to order a bundle of routine investigations.
- Bundle definitions editable in Settings (per-trimester for OB, per-context for Gynae infertility, etc.).
- Pick individual items as alternative.

**Middle: result list**
- **Pending** section above (ordered, awaiting result).
- **Completed** section below (with values).
- Newest first within each section.
- Grouped by category (Lab / Imaging).

**Each row:**
- Date
- Test name
- Value
- Flag indicator (if flagged)
- Attachment indicator (if file attached)

Tap a row → detail view (full result, attachment, notes).

## Result entry

**Default: structured value only, no attachment.** Type the value. Zero storage cost.

**Optional: attach a file** (PDF or photo) per result, when the document is worth keeping.

**Auto-purge:** attachments deleted after 2 years (default; tunable in Settings). Structured values are kept forever.

## Flagging

Manual in v1; no auto-cutoffs (deferred to Settings later).

When you flag a result:
- A **patient-bound reminder** is auto-created (surfaces on next visit screen).
- The flag **pins to the Sticky Header flags rail** until acted on.

## No trend views

No graphs in v1. Hb included. Well-organized lists are sufficient.

## Cycle boundary

Cycle-specific lab values stay inside the cycle, not the Investigations panel:

- **β-hCG** → cycle outcome only.
- **E2 / P4 / LH / endometrium during stim** → cycle monitoring table only.

## Dual-homed values

- **AMH** lives in **both** the Investigations panel and the Reproductive section of the Spine. Single source of truth; auto-mirrored to both views. Editing in one updates the other.

## Quick-capture button

A camera button on the Sticky Header (works well on Surface Pro and phone):

- Tap → camera opens → snap.
- Auto-attaches to the current chart with a structured value field to type.
- No need to navigate phone → app → patient → tab. The file-now flow lives at the global header.

## Assistant Inbox

A separate, stripped-down view for the assistant. Designed for speed, not for clinical browsing.

### Single screen

- Big "Add Result" button.
- Patient search (fuzzy, EN + AR autocomplete; recently-viewed pinned).
- Optional file upload (drag-drop on desktop; tap-to-attach on phone).
- Test name + value text fields (or free-text "Hb 9.2, TSH 2.1").
- Save.

### What happens

- Result lands in that patient's Investigations panel.
- Status = Completed.
- A bell badge appears on the doctor's global header. Silent (no sound).
- Toast: "New results: Mariam Iskandar (3 items)."

### Permissions

The assistant retains full app access; the Inbox is the **fast path**, not a permission boundary. The doctor trusts the assistant with full read/write.

### Why the separate view

Reduces friction. Assistant doesn't need to learn the full chart; she just needs the fastest path from "patient sent results on WhatsApp" to "results filed in the system."

## Cross-references

- Spine AMH dual-homing → `01_PATIENT_SPINE.md`
- Cycle outcomes (β-hCG, monitoring values) → `04_IVF_FET_CYCLES.md`
- Reminder creation from flagging → `05_REMINDERS.md`
- Sticky Header flags rail → `01_PATIENT_SPINE.md`
- Quick-capture button location → `08_STICKY_HEADER_ACTION_BAR.md`
- Media gallery (where attached files surface) → `09_MEDIA_HANDLING.md`

## Changelog

- v1.0 — Initial spec.
