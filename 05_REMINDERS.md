# 05 — Reminders

Two distinct reminder kinds with two distinct lives. Schedule events (OPU, β-hCG, FET, deliveries) are **not** reminders — they belong to the scheduling system (see `08_STICKY_HEADER_ACTION_BAR.md`).

## The two kinds

### 1. Patient-bound reminders

About something to do *for this patient at her next visit* (e.g., "stop aspirin at 36w", "recheck Hb", "sedation before spinal"). These travel with the patient.

### 2. Personal / admin reminders + secretary tasks

About something *you* (or your secretary) need to do (e.g., "book OR for Mariam Tuesday 3pm", "call lab"). These live in a global notification center, separate from any chart. Bilingual EN ↔ AR.

These are **one entity type** with an "assigned to" field controlling who gets notified.

## Patient-bound reminders

### Surfacing

Two simultaneous places:

- **Strip at top of visit screen** — deletable. Marks done and dismisses.
- **Inline yellow-highlight echo** — appears in the relevant row of the visit table. Stays as a record after the strip is dismissed.

### Triggers

- By GA (e.g., "fire at 36w")
- By next visit (regardless of date)
- By specific date

### Defer

- "Show again next visit."

### Completion

- Mark as done. Strip dismisses; inline echo remains as record.

### Recurrence

None. One-shot only. To recur, create a new reminder.

## Personal / admin reminders + secretary tasks

### Inbox

Global notification center, accessible via the global header bell. **Shared inbox** — you and secretary both see, both can add, both can mark done.

### Item fields

- Text
- Linked patient (optional)
- Due date / time
- Status (open / done / snoozed)
- Created by (you / secretary)
- Assigned to (you / secretary / both)

### Bilingual mechanics

Single text field with optional **"Translate" button** that drafts an EN ↔ AR version. Translation is editable before sending. Avoids auto-translate risk on clinical phrasing.

### Notifications

When a task is assigned to the secretary (or to you):

- Bell badge on the header
- Toast popup on the recipient's screen
- Sound

### Defer

- Snooze to specific date / time.

### Completion

- Mark as done. Visible to both sides.

### Recurrence

None. One-shot only.

## Creation entry points

- **From any text field** → small bell icon → creates a patient-bound reminder pre-filled with the field's content + context.
- **From the global header bell** → creates a personal / secretary task.
- **From the Sticky Header's Reminders button** → opens this patient's full reminder list, can add/edit.

## What is NOT a reminder

- Schedule events (OPU, β-hCG day, FET day, scheduled deliveries, scheduled surgeries) — these belong to the calendar system. The line is sharp.
- Auto-fired alerts from abnormal investigation results — these are flagged manually by the doctor (see `06_INVESTIGATIONS.md`); flagging *creates* a patient-bound reminder.

## Cross-references

- Sticky Header Reminders button → `08_STICKY_HEADER_ACTION_BAR.md`
- Investigation flagging → `06_INVESTIGATIONS.md`
- Calendar / scheduling → `08_STICKY_HEADER_ACTION_BAR.md` (Schedule)
- Assistant Inbox notifications → `06_INVESTIGATIONS.md`

## Changelog

- v1.0 — Initial spec.
