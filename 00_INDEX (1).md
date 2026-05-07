# Fetal Medicine Suite — Specification

**Version:** 1.1
**Date locked:** May 2026
**Status:** Specification complete; awaiting code audit before implementation.

---

## Purpose

This folder is the single source of truth for the Fetal Medicine Suite. Every module spec was locked through structured Q&A. Decisions in these files take precedence over older designs in `index.html`, in prior chat history, or in implementation drafts. Where the existing code conflicts with the spec, the code is what changes.

## How to use these files

- **Reference document, not a rewrite mandate.** The spec describes what the finished product should be. Implementation will be sliced and incremental — see `12_IMPLEMENTATION_NOTES.md`.
- **One module per file.** Each module file is self-contained but cross-references others where needed.
- **"Locked" means decided.** "Deferred" means consciously postponed. "Open" means still to design.
- **Editable over time.** Specs evolve when implementation reveals constraints. Update the relevant file; bump the version above; note the change in a changelog at the bottom of the affected module.

## Module files

1. `01_PATIENT_SPINE.md` — Sticky header, Timeline sidebar, Profile, OB Performance, Surgical History, Reproductive (with ART Summary).
2. `02_GYNAE_TRUNK.md` — Lifelong root chart, visit cards, branching to other episodes.
3. `03_OBSTETRICS.md` — Pregnancy episodes, longitudinal visit table, ultrasound, postpartum.
4. `04_IVF_FET_CYCLES.md` — Stimulation cycles (TI/IUI/IVF-ICSI), FET cycles, embryo bank.
5. `05_REMINDERS.md` — Patient-bound reminders + personal/secretary task system.
6. `06_INVESTIGATIONS.md` — Investigations side rail, bundles, flagging, Assistant Inbox.
7. `07_PRESET_LIBRARY.md` — Per-field smart autocomplete.
8. `08_STICKY_HEADER_ACTION_BAR.md` — Briefing, Schedule, Media, Reminders, Edit, Complete buttons.
9. `09_MEDIA_HANDLING.md` — Capture, gallery, annotation, storage.
10. `10_EPISODE_CLOSURE.md` — Closure flow, outcome fields, writeback to Spine.
11. `11_NEW_PATIENT_INTAKE.md` — Chart creation, minimum viable record.
12. `12_IMPLEMENTATION_NOTES.md` — Sequencing, slicing, hosting orientation, cautions.

## Cross-cutting principles (apply everywhere)

- **Bilingual:** EN + AR throughout where patient-facing or shared with Arabic-reading staff.
- **Cloud-synced:** Same data, same state, every device. No manual sync.
- **Editable always:** Tap-to-edit anywhere, except identity fields (name, ID) which require an explicit Edit Profile flow.
- **Append-only history:** Closed episodes can be reopened; nothing is permanently sealed. Edits remain possible after closure.
- **Settings-driven:** Bundles, preset lists, auto-purge windows, abnormal-result cutoffs all configurable.
- **No surprises:** No proactive AI suggestions, no auto-flagging without explicit user action, in v1.

## Glossary

- **Spine** — the patient-level data layer (header + accordion + Timeline). Lifelong, never closes.
- **Episode** — a bounded clinical event with a beginning and end (Pregnancy, OI cycle, FET cycle, Surgery).
- **Trunk** — the Gynae chart; the lifelong root from which all episodes branch.
- **Branch** — an episode growing off the Gynae trunk.
- **Card** — a one-line summary of an event on the Timeline.
- **Bank** — the patient-level frozen embryo counter.
- **OI** — Ovarian (Induction) / Stimulation cycle. Covers TI, IUI, IVF-ICSI per a purpose selector.
- **OPU** — Oocyte Pickup.
- **ET** — Embryo Transfer.
- **FET** — Frozen Embryo Transfer.
- **AFC** — Antral Follicle Count.
- **GA** — Gestational Age.
- **GPA** — Gravida / Para / Abortion summary.
- **Bell** — the reminder/notification icon.
- **Assistant Inbox** — the stripped-down view used by the assistant to file results quickly.

## Changelog

- **v1.1 (May 2026)** — Four edits across the spec:
  1. `03_OBSTETRICS.md` — Replaced the structured trimester scan accordion (BPD/FL/AC/AFI/EFW with Hadlock auto-calc) with a lightweight three-card pinned strip: Done checkbox + short free-text note for 1st trimester / Anomaly / 3rd trimester.
  2. `09_MEDIA_HANDLING.md` — Clarified external sharing scope: no new surfaces in v1, but existing WhatsApp share buttons on MasterDiary appointments and Rx printing are retained.
  3. `12_IMPLEMENTATION_NOTES.md` — Added "Modules in-scope but out of spec" listing modules (MasterDiary, Billing, MasterControlTower, Layout Manager, Section Styles, Hidden Sections, Theme/font/bold settings, Cloud sync, Backup/Restore) that are preserved during slicing.
  4. `12_IMPLEMENTATION_NOTES.md` — Added a one-time data migration note: existing `hubCycles[]` arrays inside Infertility episodes lift out to free-standing OI/FET episodes on the Gynae trunk, retiring the Infertility hub umbrella.
- **v1.0 (May 2026)** — Initial spec lock.
