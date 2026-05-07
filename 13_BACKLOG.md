\# 13 — Backlog (parked items)



\*\*Purpose:\*\* Single source of truth for everything intentionally deferred or known-broken. Replaces ad-hoc "I'll remember it later." Update at end of each session.



\## Bugs



\- \*\*Drag-to-reorder in Waiting Queue doesn't persist\*\* — rows are draggable but snap back on drop. (Slice 1.5 known issue.)

\- \*\*Queue's "Open chart" navigation bypasses the leave-chart nudge\*\* — small design gap from Task 1.5-D.

\- \*\*Intake check-in creates duplicate appointments\*\* instead of mutating existing one. (Slice 1.6.)

\- \*\*Patients regenerate from seed every reload\*\* — they don't persist across page reloads. Affects testing of data-shape changes. (Slice 1.6.)

\- \*\*localStorage uses three keys, not two:\*\* `fetalMedicineSuite.v3` (appts/settings), `clinicPatients` (legacy/dead — has old shape `name`/`age`/`visits`, may be safe to delete), and live patients regenerate from seed (no stable key). Untangle during data-layer refactor.

\- \*\*Legacy `obstetricsHistory` key vs current `priorPregnancies` key\*\* — fallback exists, retire later.

\- \*\*Cycle-scoped labs leak into MIP via free-text regex\*\* — Slice 4 boundary.

\- \*\*AutoFlagSyncEngine vs spec's "no auto-flagging" principle\*\* — decide before Slice 5b.

\- \*\*Trimester scan grids still structured\*\* (v1.1 wants 3-card pinned strip) — Slice 3.

\- \*\*Print bug:\*\* `@media print` hides everything via `body \*` visibility:hidden, only un-hides `#rx-print-area` — fix in Slice 3.

\- \*\*`deleteEpisode` reads `patients` from closure scope\*\* (theoretical staleness with rapid concurrent deletes). Functionally fine; note for future.

\- \*\*IVF Stim / FET monitoring table cannot scroll horizontally\*\* — `InfertilityHubTemplate` (line 15620). Doctor can't see far-right columns. Slice 4.

\- \*\*IVF Stim header "Day —" stub\*\* — Cycle Day calculation not yet wired (intentional stub from Slice 1, resolves in Slice 4).



\## Deferred features



\- \*\*Collapsible visit cards across all visit-list templates\*\* (Gynae, Obstetrics, future templates) — implement as a reusable cross-cutting pattern in Slice 5 or dedicated UI polish pass. Don't add per-template.

\- \*\*Infertility-type visit unfolds extra fields\*\* (per spec `02\_GYNAE\_TRUNK.md`) — deferred from Task 2-C. Decide first whether to keep template-level fertility fields, move them per-visit-when-Infertility, or hybrid. Revisit after Slice 2 core is done.

\- \*\*Surgery-as-episode unification\*\* with the existing global `surgeries\[]` array. Currently two surgery models coexist. Don't unify in Slice 2; revisit when scoping the surgery branch flow.

\- \*\*Carry-forward from Gynae visit to spawned cycle\*\* (planned protocol, drug list, planned start date). `parentVisitId` is the link, but no carry-forward logic yet. Slice 4 (ART).

\- \*\*`hubCycles\[]` → free-standing OI/FET migration.\*\* One-time migration that retires the Infertility hub umbrella. Slice 4. Spec: `12\_IMPLEMENTATION\_NOTES.md` v1.1.

\- \*\*Visual indication of parent → branch relationship\*\* in Episodes sidebar / Timeline. `parentVisitId` is now stored on branched episodes (Task 2-D) but no UI consumes it yet. Task 2-F (Timeline trunk awareness) or Slice 5 polish.

\- \*\*`purpose` field on IVF Stim episodes\*\* — stored by Task 2-D, not yet read by `InfertilityHubTemplate`. Slice 4.

\- \*\*Header gets crowded during IVF/FET cycles\*\* — pinned flags + couple snapshot + cycle banner compete for space. Consider tiering or condensing pinned flags. Slice 5 polish or post-v1.

\- \*\*All v1 deferrals from `12\_IMPLEMENTATION\_NOTES.md`\*\* — LLM Briefing, auto-flagging, proactive pin suggestions, layered annotations, audit log, bulk migration, trend graphs, recurring reminders, auto-routed WhatsApp inbound. Tracked in that file; this entry is the cross-reference.

Clinical Forecast Calendar — month/year view of predicted clinical events (EDD ranges, OPU windows, FET dates, CS dates, anti-D windows) drawn from active episodes. Used for vacation/coverage planning. Renders events as ranges, not single dates, to reflect biological imprecision. Soft-warning layer over a vacation date selector. Slice 5 or dedicated slice after ART (Slice 4) is stable, because it reads from those data shapes.



\## Spec edits pending



\- \*\*Tighten bilingual scope in `00\_INDEX.md`\*\* — clarify doctor-only UI is EN-only; EN+AR is for patient-facing, secretary-facing, or printed/sent content. Bump to v1.2 next time the spec is edited.



\## Resolved (delete from this list when committed)



\_(empty)\_

