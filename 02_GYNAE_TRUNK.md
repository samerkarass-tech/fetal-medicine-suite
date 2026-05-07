# 02 — Gynae Trunk

The Gynae trunk is the lifelong root of every patient's chart. It is created automatically when a new patient record is opened, and never closes. It holds all non-pregnancy, non-cycle visits, and is the launching point for branching episodes (Pregnancies, OI cycles, FET cycles).

## Lifecycle

- **Auto-created** with every new patient record (see `11_NEW_PATIENT_INTAKE.md`).
- **Never closes.** Persists for the patient's lifetime.
- Coexists alongside any number of branching episodes.

## Structure

Visit list = chronological cards, **oldest at top**. Each card is a single Gynae visit.

## Visit card

Each Gynae visit has:

**Type selector** (single-select):
- Routine
- Premarital
- Contraception
- Postpartum
- Menopause
- Other
- Infertility

**Behavior:**
- Only "Infertility" unfolds extra fields (specific to fertility workup).
- Other types use the standard visit shell.

**Standard visit fields:**
- Date
- Complaint (the headline)
- Examination
- Investigations ordered / reviewed (links into the side rail; see `06_INVESTIGATIONS.md`)
- Plan
- Free-text notes

**Complaint is the headline** of the card — what shows in the chronological list at a glance.

## Branching to other episodes

Inside any Gynae visit row, two action buttons start sub-episodes:

- **Start Pregnancy** → opens an Obstetrics episode (see `03_OBSTETRICS.md`).
- **Start Stimulation Cycle** → opens an OI cycle template with a purpose selector (TI / IUI / IVF-ICSI). See `04_IVF_FET_CYCLES.md`.
- **Start FET** → opens an FET cycle template. See `04_IVF_FET_CYCLES.md`.

The originating Gynae visit becomes the parent context. Decisions made in that visit (planned protocol, drug list, planned start date) carry forward to the new episode (see `04_IVF_FET_CYCLES.md` carry-forward rules).

## Postpartum visits

A Postpartum visit is a special case:
- It is **one visit, two linked views**.
- Closes the parent Pregnancy episode (writeback to OB Performance).
- Appears as a card on the Gynae trunk like any other visit.
- Type selector pre-set to "Postpartum"; pre-fills with the closing Pregnancy episode's context.

## Cross-references

- Pregnancy episode → `03_OBSTETRICS.md`
- OI / FET cycles → `04_IVF_FET_CYCLES.md`
- Investigations → `06_INVESTIGATIONS.md`
- New patient intake (auto-creation trigger) → `11_NEW_PATIENT_INTAKE.md`

## Changelog

- v1.0 — Initial spec.
