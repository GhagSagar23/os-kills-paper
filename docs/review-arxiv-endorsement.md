# Review: arXiv Endorsement Readiness & IEEE Software Submission Quality

**Paper:** "Measuring What Kills Your App: A Methodology for Detecting Background Execution Failures in Production Android Apps"
**Author:** Sagar Ghag, Kryonex Labs
**Reviewer:** Critical academic review (self-commissioned)
**Date:** 2026-11-15
**Target venue:** IEEE Software (rolling, 4000-6000 words, single-anonymous)

---

## arXiv Endorsement Gates (monperrus protocol)

### Gate 3a: Is it a scientific paper?

**Verdict:** PASS
**Confidence:** High

The paper has a structured abstract, introduction with stated contributions, a background section (Section 2), a methodology core (Sections 3-5: taxonomy, instrumentation spec, classification procedure), a validation section with empirical data (Section 6), threats to validity (Section 7), related work (Section 8), discussion (Section 9), and conclusion (Section 10). It follows the conventions of a methodology paper in software engineering. Not a blog post, not a manual. The structure is sound.

### Gate 3b: Is it software engineering?

**Verdict:** PASS
**Confidence:** High

The core subject is runtime observability for mobile apps: how to detect, classify, and measure background execution failures in production. This sits squarely in software maintenance, DevOps, and mobile software engineering. No AI/ML content. The contribution is a measurement methodology, not a tool or a library, which is appropriate for the venue.

### Gate 3c: arXiv quality gates

**(a) Written in English:** PASS. Clear, fluent English throughout. No machine-translation artefacts.

**(b) Self-contained:** PASS. Key claims are explained inline. The taxonomy is fully defined in Table 2. The instrumentation spec is complete in Section 4. External references (dontkillmyapp.com, Android documentation) are cited but not required to follow the argument.

**(c) Scientifically honest:** PASS. The paper identifies the authors as the developers of the audited app (Section 6, first paragraph) and addresses researcher bias explicitly in threats to validity. The self-citation (ghag2026testing) is transparent. No plagiarism signals.

**(d) Minimum scholarly writing quality:** PASS. The writing is above average for SE venues. Sentences are concrete, claims are specific (line counts, session counts, exact percentages). Not machine-generated filler. The discussion section (Section 9) contains genuine reflection, particularly the observation that the most consequential gap was a persistence failure rather than a missing event.

**(e) Bibliography/references section:** PASS. 13 references. Adequate for a methodology paper of this length, though thin (see IEEE Software assessment below).

**Overall Gate 3c verdict:** PASS. Confidence: High.

### Gate 4: Repository-Paper Correspondence

**Verdict:** CONDITIONAL PASS
**Confidence:** High

The paper's empirical claims were checked against the supporting analysis files in `data/analysis/`. Correspondence is strong:

| Paper claim | Data source | Match? |
|---|---|---|
| 159 tracking sessions | session-analysis.md: "Total: 159" | Yes |
| 14,094 waypoints | waypoint-gap-analysis.md: "Total waypoints: 14094" | Yes |
| 509 gaps >5 min | waypoint-gap-analysis.md: "Total gaps found: 509" | Yes |
| 65 sessions with ≤3 waypoints | session-analysis.md: 63 with 1-3 + 2 with 0 = 65 | Yes |
| 25 sessions ended by server timeout | session-analysis.md: end_reason=3 count=25 | Yes |
| 70 physical devices | permission-events-analysis.md: 76 total - 6 emulators = 70 | Yes |
| 81.7% foreground / 18.3% headless | waypoint-gap-analysis.md source distribution | Yes |
| Empty permission_event table | permission-events-analysis.md: "Empty. Zero rows." | Yes |
| Sequence resets (182→0, 174→0, 29→0) | waypoint-gap-analysis.md gap entries #8, #13, #10 | Yes |
| 39→246 gap (207 missing sequences) | waypoint-gap-analysis.md gap entry #45 | Yes |
| 4 deploying organisations | session-analysis.md: 5 customer_ids, but paper says 4 | Close (see note) |
| Longest gap 110h 50m | waypoint-gap-analysis.md gap #1 | Yes |

The paper references "four organisations." The session data shows 5 customer IDs, but one (628e6597) has a single session that appears to be a test ("Sample check-out tracking from Swagger"). The paper's count of four deploying organisations is defensible.

**Condition:** No public GitHub repository exists yet. The data files are local only. For full Gate 4 compliance, the analysis data (or anonymised derivatives) should be published alongside the paper. The raw database dump should not be published (it contains UUIDs, timestamps, and location data), but the aggregated analysis files could be released with minimal redaction.

### Gate 5: osaudit.toml

**Verdict:** FAIL (expected)
**Confidence:** High

No `osaudit.toml` exists in the repository. This is a TODO for arXiv submission. The file is a metadata requirement for the cs.SE category under the monperrus endorsement protocol. It should declare the paper type (methodology), the artefact type (analysis data), and the reproduction instructions.

---

## IEEE Software Readiness Assessment

### Summary

The paper proposes a measurement methodology for background execution failures on Android. The contribution has three parts: a five-category kill-cause taxonomy, a seven-event instrumentation specification, and a decision-tree classification procedure. Validation comes from auditing a production Flutter app (Zontra, 104,886 LOC, 70 devices, 4 organisations) against the specification, finding 6 existing signals and 12 gaps. A database analysis of 159 sessions and 14,094 waypoints quantifies what the gaps hide: 40.9% of sessions captured almost no data, 15.7% ran to server timeout, and the permission event table intended to be the canonical record was empty.

The paper is well-written and grounded in production experience. The question is whether it clears the bar from practitioner report to research contribution.

### Strengths

1. **The problem is real and underserved.** Background execution failure on Android is a documented practitioner pain point with no published measurement methodology. The gap between dontkillmyapp.com (workarounds per OEM) and what the paper proposes (detection methodology per app) is genuine. A reviewer looking for novelty will find it here: nobody has written this up as a structured methodology before. [Certain]

2. **The validation is concrete, not hypothetical.** The paper does not propose a methodology and wave at potential applications. It audits a real app with real data. The 12 gaps found are specific to code locations and detection failures. The database analysis produces numbers (509 gaps, 65 near-empty sessions, empty permission_event table) that a reader can verify against the described architecture. The incident examples (45 km route recorded as 0.0 km; 4-hour diagnosis time) give the contribution operational weight. [Certain]

3. **Honest about its limits.** The threats to validity section is unusually direct. The paper admits researcher bias, acknowledges the taxonomy is derived from one app, calls out the Doze/OEM disambiguation ceiling, and notes that the 40.9% figure is a symptom count rather than a diagnosis. The "Unknown" category in the taxonomy is a design choice that demonstrates epistemic discipline. The conclusion opens with "We have not solved the background kill problem. We have described how to see it." This kind of restraint is rare and a reviewer will notice it. [Certain]

4. **The persistence insight is a genuine contribution.** Section 9's observation that the most consequential gap was in-memory state lost on process death (not a missing event) is the kind of finding that only comes from production experience. The specific pattern (permission revocation state held in static Dart fields, lost on kill, causing a `foreground_resume` to be logged instead of `permission_revoked`) is something a practitioner can learn from directly. This is the paper's strongest single observation. [Likely]

5. **Appropriate scope for IEEE Software.** IEEE Software publishes methodology and practice papers, not just tool papers or empirical studies. The paper's format (taxonomy + spec + procedure + validation) fits the venue. The writing avoids jargon inflation and stays concrete throughout. [Certain]

### Weaknesses

1. **N=1 validation.** The methodology is validated against one app, one platform, one use case (field workforce tracking), one regional market (India, budget Android handsets). The paper claims framework-agnostic but validates only on Flutter/Android. The taxonomy may be complete for location tracking apps on aggressive OEMs, but health monitors, fitness apps, and IoT controllers face different kill profiles. A reviewer will ask: does this generalise? The paper's answer (threats to validity, Section 7) acknowledges the limitation but does not mitigate it. Even a second app (different category, different team) would strengthen the claim. Without it, the paper is a case study dressed as a methodology. [Likely]

2. **No before/after measurement.** The paper proposes an instrumentation specification but does not implement it. The validation finds gaps but does not close them. The conclusion acknowledges this ("What we have not done: implemented the full specification...and measured the before/after detection rate"). For a methodology paper, this is a significant omission. A reviewer will reasonably ask: how do you know the methodology works if you haven't run it? The gap analysis shows what existing telemetry misses; it does not show that the proposed telemetry catches it. The counterargument (the field deployment tests detection in production, not in a lab) is valid but does not fully compensate. [Certain]

3. **OEM aggression ratings are subjective.** Table 1 assigns aggression ratings (3/5 to 5/5) to six OEMs. The paper says these come from "field deployment with 70 physical devices" but provides no criteria for the rating scale, no inter-rater agreement, and acknowledges the fleet is "too small for confidence intervals per OEM." The classification procedure (Section 5) uses these ratings as decision-tree inputs ("classify as OEM Kill if the device OEM has aggression ≥4/5"). A subjective input to a classification procedure weakens the procedure's reproducibility. A reviewer will flag this. [Certain]

4. **Related work section is thin.** 13 references. The paper cites energy profiling (Li 2014, Pathak 2012), permissions (Felt 2011, Au 2012, Wijesekera 2015), performance bugs (Liu 2014, Nistor 2013), fragmentation (Wei 2016), Flutter (Ghag 2026, Biorn-Hansen 2020), and dontkillmyapp.com. Missing from the discussion:

   - **Mobile crash analytics literature.** Google's Vitals, Firebase Crashlytics, and the broader crash-reporting ecosystem. The paper's methodology complements crash reporting (it catches what crash reports miss), but the related work does not position against this body of work.
   - **Android lifecycle and process management.** There is academic work on Android process lifecycle management and its implications for app design. Yan et al. (2012, "DroidScope") and related Android analysis work should be surveyed.
   - **Observability and telemetry in mobile apps.** The broader mobile observability space (session replay, performance monitoring, APM) is not discussed. The paper's contribution is a specific kind of observability; positioning it in the broader landscape would strengthen the novelty claim.
   - **Background task scheduling.** WorkManager, JobScheduler, and their academic treatment. The paper mentions foreground services but does not discuss the literature on background task APIs and their failure modes.
   - **OEM customisation studies.** There may be empirical studies of OEM Android customisation beyond Wei 2016 that are relevant, particularly studies from the Chinese OEM ecosystem.
   
   For IEEE Software, 13 references is low. 20-25 would be more appropriate, and the missing areas above are genuine gaps in the positioning. [Likely]

5. **The "four organisations" framing inflates the sample.** Two organisations account for 80% of the fleet (38 and 31 devices). The third has 5-6 devices. The fourth has 1-2. Calling this "four organisations" is technically correct but gives a misleading impression of deployment breadth. A reviewer comparing this to other field studies will note the effective sample size. [Likely]

### Required Revisions

**R1. Strengthen the related work.** Add references to mobile crash analytics, Android lifecycle management, mobile observability/APM, and background task scheduling. Position the methodology against existing crash-reporting tools (Crashlytics, Bugsnag, Sentry) and explain what the methodology catches that they do not. Aim for 20+ references. (Section 8)

**R2. Operationalise the OEM aggression ratings.** Define criteria for each level (1/5 through 5/5). Even informal criteria ("kills foreground services within N minutes of screen-off despite battery optimisation whitelist" = 5/5) would make the ratings reproducible. Alternatively, remove the ratings from the classification procedure's decision logic and use them only as contextual metadata. (Table 1, Section 5 step 4)

**R3. Clarify the organisation count honestly.** Either describe the fleet as "two primary deploying organisations (38 and 31 devices) with two smaller deployments (5 and 2 devices)" or explain the four-org framing more carefully. The current presentation is not wrong, but it is the kind of thing a reviewer reads as optimistic framing. (Section 6, paragraph 2)

**R4. Address the self-citation.** Reference `ghag2026testing` currently has `arXiv:XXXX.XXXXX` as the identifier. This must be filled in before submission. If the cited paper has not been submitted to arXiv, it should be submitted first or the citation should be changed to a tech report with a URL. (references.bib, line 124)

**R5. Add a limitations paragraph to the conclusion.** The threats to validity section covers this, but IEEE Software reviewers expect the conclusion to briefly acknowledge the primary limitation (N=1 validation, no before/after measurement). The current conclusion alludes to the missing implementation but does not frame it as a limitation. (Section 10)

### Optional Improvements

**O1. Implement even one gap and report the result.** If the heartbeat event (gap 3) or the persisted permission state (gap 7) were implemented before submission and the before/after detection rate reported, it would transform the paper from "here is what you should measure" to "here is what you should measure, and here is what happened when we did." Even partial implementation on one gap would address Weakness 2. This is the single highest-ROI revision.

**O2. Add a figure for the classification decision tree.** Section 5's six-step procedure would benefit from a flowchart. IEEE Software readers expect visual aids for procedural content.

**O3. Include a brief iOS comparison.** Section 7 mentions iOS as out of scope. A half-page sidebar or table comparing which taxonomy categories exist on iOS and which signals differ would strengthen the framework-agnostic claim without requiring iOS validation data.

**O4. Word count check.** The paper currently reads at approximately 5000-5500 words (estimated from the LaTeX source), which is within the IEEE Software 4000-6000 range. Confirm with a compiled word count. The related work expansion (R1) will add 300-500 words; if this pushes past 6000, trim the background section (Section 2), which currently runs long for readers who already know about Doze and OEM kills.

**O5. Anonymise the app name.** The paper names "Zontra" and provides enough detail (104,886 LOC, Rust FFI, Tracelet, Flutter, Firebase) that the app is identifiable. IEEE Software is single-anonymous, so this is technically permissible. But naming the app while also being its developer creates a perception of self-promotion. Consider referring to it as "the audited app" or "App A" throughout, with a footnote disclosing the relationship.

---

## Verdict

**arXiv endorsement:** Ready after R4 (fix the self-citation placeholder) and Gate 5 (add `osaudit.toml`). The paper clears Gates 3a-3c cleanly and Gate 4 conditionally. It is a legitimate contribution to cs.SE.

**IEEE Software submission:** Ready after R1-R5. The paper is well above the reject threshold but currently sits in "major revision" territory, primarily because of the thin related work and the absence of any before/after validation. O1 (implement one gap) would move it to "minor revision" territory. The core contribution (taxonomy + spec + classification procedure grounded in production data) is sound and fills a genuine gap in the literature. [Likely to be accepted after one round of revision, conditional on R1 and R2.]

The paper's biggest asset is that it reads like it was written by someone who has actually debugged these failures in production. That is harder to fake than a larger sample size.
