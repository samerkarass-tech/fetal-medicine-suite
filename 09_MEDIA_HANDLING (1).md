# 09 — Media Handling

Unified model for capture, storage, viewing, annotation, and deletion of all media in the patient's chart.

## File types

- Photos (lab results, ultrasound stills, scans of paper documents)
- PDFs (lab reports, imaging reports)
- **No video.**

## Capture

### Quick-capture button (Sticky Header)

- Camera button on the global header.
- Tap → camera opens → snap.
- Two modes:
  - **File now** (default) → after snap, a quick overlay asks "for which patient and where?" with fuzzy patient search, last-viewed pre-filled, and a list of recent contexts (active OB episode, current OI cycle, etc.). Two taps to file. ~4–5 seconds total.
  - **To tray** → snap, snap, snap into an "unfiled" tray. Drag each one to the right patient/episode later.
- Default is "file now"; toggleable in Settings.
- Same workflow on Surface Pro and phone.

### Assistant Inbox

Assistant uploads via the stripped-down inbox view (see `06_INVESTIGATIONS.md`).

### From inside a chart

- Standard "attach file" affordances within Investigations panel rows, cycle Media tab, etc.

## Linking to clinical context

- **Automatic.** Media is tied to whatever screen / episode the user was on when uploaded.
- In phone "file now" mode, the user picks the context at capture time.

## Gallery (Media button on action bar)

Unified per patient. Every file ever attached in the patient's chart, in one place.

### Organization

**Tabbed:** chronological / by source / by episode.
**Default tab:** by episode (mirrors how the doctor thinks about the chart).

### No filtering or search

Just scroll. Lightweight.

### Tap behavior

- Tap image → fullscreen image viewer with annotation access.
- Tap PDF → multi-page scrollable PDF viewer.
- Both viewers include a **"go to source"** link that jumps to the chart location where the file was originally attached.

## Annotation

### Scope

- **Basic only.** Lines, circles, text labels.

### Storage

- **Annotations baked in.** Image saves with marks burned onto it; original is replaced by the annotated version.
- (No editable layered annotation in v1. If editability is later required, this is the upgrade point.)

## Delete

- **Two-step confirmation.** "Delete?" → "Really delete?"
- Applies to all media types.

## Storage / cost

- **2-year auto-purge default.** Tunable in Settings.
- Same policy as Investigation attachments (see `06_INVESTIGATIONS.md`).

## Sync

- **Cloud-synced** across phone, laptop, Surface Pro automatically.
- No manual sync. No "send to laptop" flow.
- Snap on phone → appears on laptop within seconds.

## Sharing / re-use

- **No new external sharing surfaces in v1.** Existing WhatsApp share buttons on MasterDiary appointments and Rx printing are retained.
- **No cross-episode re-use.** Media stays linked to its origin.

## Cross-references

- Quick-capture button placement → `08_STICKY_HEADER_ACTION_BAR.md`
- Assistant Inbox upload path → `06_INVESTIGATIONS.md`
- Media access from action bar → `08_STICKY_HEADER_ACTION_BAR.md`
- Settings (auto-purge tunable) → `00_INDEX.md`

## Changelog

- v1.0 — Initial spec.
- v1.1 — Clarified external sharing scope: no new surfaces in v1, but existing WhatsApp share buttons on MasterDiary appointments and Rx printing are retained.
