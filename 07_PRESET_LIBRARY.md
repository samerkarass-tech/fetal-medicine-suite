# 07 — Preset Library

Per-field smart autocomplete. Each text field has its own dropdown of saved phrases that grows over time as the doctor uses the app.

## Mental model

**Not** a templating system. Not variables, placeholders, or fuzzy logic. Just a per-field dictionary of saved phrases that auto-suggests as you type.

## Behavior

### Type-as-you-go matching

- As you type, items from this field's preset list filter to matching ones.
- Items disappear when input no longer matches.
- Pick one to insert.
- If your input doesn't match anything, it stays as free text.

### Save unmatched text as a new preset

- A small **"+" icon** next to the field appears when typed text doesn't match any preset.
- Tap → saves as a new preset for this specific field.
- Long-press / right-click on field text is the fallback if "+" icon would crowd the layout. The implementing developer makes the call based on actual layout.

### Almost-right preset

- Insert it, then edit. No edit-before-insert flow.

### Append mode (multi-pick)

- You can pick multiple presets in one field; they concatenate with a separator.
- **Separator is configurable per field type:**
  - Default for examination/plan-style fields: **period + space** ("Single living fetus. Placenta anterior. AFI normal.")
  - Default for short-list fields like complaint: **comma + space** ("headache, dizziness, nausea")
- Configurable in Settings.

### Order of items in dropdown

- Most-frequently-used first.
- Most-recently-used as tiebreaker.

## Editing the lists

### Inline (quick fixes)

- Long-press / right-click on a dropdown item → Edit / Delete.

### Settings (cleanup)

- Central Settings page lists every field and its preset list.
- Bulk edit, reorder, delete.

## Field scope

**Separable per context.** A field called "Examination" in OB visits has its own preset list, distinct from "Examination" in Gynae visits.

Reason: OB exam vocabulary ("single living fetus, placenta anterior") doesn't belong in a Gynae exam dropdown ("normal external genitalia, no adnexal mass").

Each (field × context) pair has its own list.

## What presets are NOT

- No variables (`[GA]`, `[fetal weight]`).
- No placeholders.
- No structured form replacement — the US examination field is a **single text field with dropdown**, not a structured form with separate cells for presentation/placenta/AFI.
- No proactive suggestions beyond plain prefix-match autocomplete.

## Self-curation

Lists grow as the doctor uses the app. Frequency/recency ordering means the most-used phrases bubble to the top automatically. Over time, each list curates itself around how the doctor actually practices.

## Cross-references

- US examination field on OB visits → `03_OBSTETRICS.md`
- Gynae visit fields → `02_GYNAE_TRUNK.md`
- Settings hooks → `00_INDEX.md`

## Changelog

- v1.0 — Initial spec.
