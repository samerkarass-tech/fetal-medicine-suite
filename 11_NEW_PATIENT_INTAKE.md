# 11 — New Patient Intake

Flow for creating a new patient record from first contact through first clinical visit.

## Who captures what

### Secretary (at first contact — booking or arrival)

- Full name (3 names minimum, 4 preferred)
- Date of birth (auto-computes age)
- Phone number
- Occupation
- Address
- Husband info

### Doctor (in the consultation room)

- Obstetrical history
- Menstrual cycle history
- Medical history
- Surgical history
- Whatever the visit type calls for (Routine / Premarital / Contraception / Postpartum / Menopause / Other / Infertility — see `02_GYNAE_TRUNK.md`)

## Minimum viable record

**Required to save a chart:**

- 3 names (minimum)
- Date of birth
- Phone number

**Bypassable** but with an explicit confirmation prompt:

> "Are you sure you want to skip phone number?"

Everything else (occupation, address, husband info, ID number, etc.) is optional and can be filled later.

## Chart creation point

- **Secretary creates the chart** at first contact, before the patient sees the doctor.
- The Gynae trunk auto-creates with the chart (see `02_GYNAE_TRUNK.md`).
- The Spine sections start empty for clinical data; the doctor populates them in the room.

## Referral vs walk-in

- **Same flow.** Referral source is just a Profile field; no separate intake path.

## Initial state when doctor opens the chart

- Sticky Header populated with what the secretary captured.
- Spine sections start empty for clinical data.
- **Default landing:** the first visit screen (no prior visit exists yet, so the standard "open to last visit" rule resolves to the new active visit).

## Existing patients on paper

- No bulk migration tool in v1. Enter as patients return.
- Manual entry into the standard Spine sections, as the doctor would normally take a history during a returning patient's visit.

## Cross-references

- Gynae trunk auto-creation → `02_GYNAE_TRUNK.md`
- Spine fields (Profile, Reproductive, Surgical History) → `01_PATIENT_SPINE.md`
- Sticky Header fields populated at intake → `01_PATIENT_SPINE.md`

## Changelog

- v1.0 — Initial spec.
