# Idea C — Measuring What Kills Your App: Detecting Background Execution Failures in Production Android Apps

**Type:** Methodology paper (measurement framework) · **Priority:** High · **Status:** Draft complete

## Working Title

Measuring What Kills Your App: A Methodology for Detecting Background Execution Failures in Production Android Apps

## Authors

- Sagar Ghag, Kryonex Labs (sagar.ghag1997@gmail.com)

## Contributions

1. Kill-cause taxonomy: five categories (Doze Kill, OEM Kill, User Force Stop, Reboot, Permission Revocation) with distinct observable signals
2. Instrumentation specification: seven core events, metadata contract, persistence requirements
3. Classification procedure: decision tree mapping observed signals to kill causes, with explicit disambiguation limits
4. Validation audit of Zontra (104,886 lines, 30 devices, 6 months): found 6 existing signals and 12 gaps

## Research Questions

- RQ1: What observable signals distinguish different categories of background execution failure on Android?
- RQ2: What is the minimum instrumentation required to detect and classify kill causes in a production app?
- RQ3: What fraction of background failures does typical ad-hoc telemetry miss?

## Target Venue

Primary: IEEE Software (rolling submissions, ~4000-6000 words, single-anonymous, IEEEtran format)
Backup: EASE 2027 / ESEM 2027

## Pivot from Original Idea

Originally scoped as a field study requiring hundreds of deployed devices for statistical significance. Pivoted to a methodology paper: the contribution is the measurement framework itself (taxonomy + instrumentation spec + classification procedure), validated against a production app's existing telemetry. The 30-device fleet validates the framework; scale comes from other adopters.

## Open Items

- [ ] Verify all OEM aggression numbers against current production data
- [ ] Fill arXiv ID for Idea D citation in references.bib
- [ ] Check IEEE Software word count (~4000-6000 target)
- [ ] Consider academic co-author (mobile SE or empirical SE)
- [ ] Compile LaTeX, verify table rendering (especially Table II, full-width)
- [ ] Internal review pass (re-read for sagar-writing voice compliance)
- [ ] Run the anti-generic pass from sagar-writing skill

## Log

- 2026-08-17 — Captured as field study idea. Parked due to fleet scale blocker.
- 2026-11-15 — Pivoted to methodology paper. Full draft written: all 10 sections complete (Intro, Kill Landscape, Taxonomy, Instrumentation, Classification, Validation, Threats, Related Work, Discussion, Conclusion). Bibliography created (13 references). Decision: methodology-only, no shipped package.
