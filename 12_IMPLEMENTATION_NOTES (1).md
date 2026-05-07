# 12 — Implementation Notes

How to take this spec from document to working code without breaking what already exists.

## Principle

**Slice, don't rewrite.** The single biggest risk in this project is a big-bang rewrite that breaks the working version while reaching for the new one. Every step below is designed to keep something working at all times.

## Recommended sequence

### Step A: Lock the spec (done)

This folder is the locked spec. Treat it as the source of truth. Update the relevant module file when decisions change; bump versions; record changes in module changelogs.

### Step B: Code audit (next action)

Open a fresh chat (this one is long; the audit needs context window room). Upload:

- The current `index.html`
- The backup `index.html`
- This spec folder

Ask for a **gap analysis** — for each module in the spec:

- What already exists in the code?
- What partially exists?
- What is missing entirely?
- What conflicts with the spec?

No code changes during the audit. Just a map.

### Step C: Sliced implementation plan

From the gap analysis, produce an ordered, sliced plan. Each slice is a brief: what to build, acceptance criteria, what NOT to touch in other slices.

**Suggested slice order:**

1. **Slice 1 — Skeleton:** Patient Spine + Sticky Header + Timeline.
2. **Slice 2 — Trunk:** Gynae trunk + visit cards.
3. **Slice 3 — Obstetrics:** Pregnancy episode (longitudinal table, US field, reminders, investigations).
4. **Slice 4 — ART:** OI / FET cycles (most complex).
5. **Slice 5 — Cross-cutting:** Presets, Media gallery, Briefing, Investigations side rail completion, Reminders system completion, Schedule integration, Assistant Inbox.

Each slice should be shippable and testable on its own.

### Step D: Cursor execution, slice by slice

Hand Cursor **one slice's brief at a time** — never the full spec at once. Build, test, merge, then move to the next slice.

Between slices, return to a Claude chat to:

- Review what Cursor produced if anything looks off.
- Tighten the next slice's brief based on what changed.
- Adjust the spec file if implementation revealed a constraint.

### Step E: Backend / hosting

Separate track. After Slice 1 (or in parallel), decide:

- Hosting (Supabase or alternative)
- Authentication (doctor + secretary roles)
- Data sync model (realtime, last-write-wins, etc.)
- File storage (for media, with the 2-year auto-purge policy)
- Backup strategy

This spec doesn't lock the backend choice. Supabase is a strong default (Postgres + auth + storage + realtime in one product) but is not mandated.

## Cautions

### Don't hand Cursor the full spec at once

The spec is the destination. The slice brief is the next step. Confusing the two leads to a sprawling, partially-working rewrite. Keep Cursor focused on one slice with explicit acceptance criteria.

### Keep the backup untouched

The backup `index.html` is your insurance. Don't edit it. Don't let Cursor touch it. Don't let it drift from the version that works today. If a slice fails, you can always return to the backup.

### Build slices alongside the live version

Each slice should be testable in isolation without breaking the working app. If your setup is file-based, consider:

- Develop the new slice in a separate file or branch.
- Merge into `index.html` only after the slice is verified.
- Keep the previous version of `index.html` as a per-slice rollback point.

### Specs evolve

Some decisions in this spec will conflict with implementation realities. That's normal. When this happens:

1. Decide whether to adjust the spec or adjust the implementation.
2. Update the relevant module file.
3. Bump the version and note the change in the module's changelog.

The spec is a guide, not a contract.

### Progressive enhancement, not feature flag hell

Where possible, ship features in a usable state even if not fully spec'd. Examples:

- Briefing v1 (templated) ships before LLM v2 is touched.
- Investigations side rail ships with manual flagging before auto-cutoffs are added.
- Annotation ships with baked-in marks before any layered annotation work.

Don't build elaborate feature flags for capabilities not yet implemented; just ship what works and add the next layer when ready.

## Settings page — accumulating list

Items deferred to Settings across the spec:

- Investigation bundle definitions (per-trimester for OB, per-context for Gynae).
- Preset list management (per field, per context).
- Auto-purge windows for media/attachments (default 2 years).
- Abnormal-result cutoffs for auto-flagging (deferred from v1).
- Proactive pin-suggestion toggle (deferred from v1).
- Quick-capture default mode (file-now vs to-tray).
- Append-mode separator per field type.

Build the Settings page incrementally as each module's settings hook is implemented.

## Modules in-scope but out of spec

The following modules exist in the current app and remain in-scope for the v1 product, but are deliberately not respec'd in this folder. They are **preserved during slicing** — Cursor must not remove, refactor, or restyle them while implementing the spec'd modules unless a slice brief explicitly says so.

- MasterDiary
- Billing
- MasterControlTower
- Layout Manager
- Section Styles
- Hidden Sections
- Theme / font / bold settings
- Cloud sync
- Backup / Restore

If a slice requires touching one of these (e.g., adding a hook into MasterDiary), call it out in the slice brief. Default behavior is hands-off.

## Data migration: legacy `hubCycles[]` → free-standing OI/FET episodes

Existing patients have `hubCycles[]` arrays nested inside an Infertility hub episode. The spec retires the Infertility hub umbrella in favor of free-standing OI and FET cycle episodes that branch directly off the Gynae trunk (see `04_IVF_FET_CYCLES.md` and `02_GYNAE_TRUNK.md`).

A **one-time migration** is required:

- For each patient with an Infertility episode containing `hubCycles[]`, lift each cycle out as its own free-standing OI or FET episode on the Gynae trunk.
- Preserve original cycle dates, outcomes, embryo bank state, and any β+ → Pregnancy linkage.
- Retire the parent Infertility hub episode after migration (do not delete; mark as superseded so historic timeline references still resolve).

The migration runs once, before or alongside the ART slice. After migration, no new data is written to `hubCycles[]`; all new cycles are free-standing episodes per spec.

## What's deferred from v1

Explicit non-goals for v1, in order of likely future priority:

1. **LLM-powered Briefing.** v1 is templated; LLM is upgrade.
2. **Auto-flagging on abnormal results.** v1 is manual; cutoffs come later.
3. **Proactive pin suggestions.** v1 is manual; auto-suggest on terms like "bicornuate" comes later.
4. **Layered annotations.** v1 bakes in; layered editable annotations come later if needed.
5. **External sharing / referral letters.** Out of scope for v1.
6. **Audit log for edits.** Out of scope for v1.
7. **Bulk patient migration.** Manual entry for now.
8. **Trend / graph views.** v1 has none.
9. **Auto-routed WhatsApp inbound.** Manual matching by name in v1.
10. **Recurring reminders.** v1 is one-shot only.

## Cross-references

All other module files in this folder.

## Changelog

- v1.0 — Initial implementation guide.
- v1.1 — Added "Modules in-scope but out of spec" (MasterDiary, Billing, MasterControlTower, Layout Manager, Section Styles, Hidden Sections, Theme/font/bold settings, Cloud sync, Backup/Restore — preserved during slicing). Added "Data migration: legacy `hubCycles[]` → free-standing OI/FET episodes" describing the one-time migration required as the Infertility hub umbrella is retired.
