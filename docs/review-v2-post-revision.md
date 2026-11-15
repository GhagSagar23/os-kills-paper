# Review v2: Post-Revision Assessment

**Paper:** "Measuring What Kills Your App: A Methodology for Detecting Background Execution Failures in Production Android Apps"
**Author:** Sagar Ghag, Kryonex Labs
**Review type:** Second pass, post-revision (self-commissioned critical review)
**Date:** 2026-11-15
**Target venue:** IEEE Software (rolling, 4000-6000 words, single-anonymous)

---

## Part 1: Revision Assessment

| Original Issue | Fix Applied | Verdict | Notes |
|---|---|---|---|
| **R1: Related work thin (13 refs)** | Expanded to 22 references. Added crash analytics (Fan 2018, Li 2020, Firebase Crashlytics), wake lock misuse (Liu 2016), background scheduling (González-Pérez 2022), OEM customisation (Wu 2015, Possemato 2021, Dong 2024). Related work restructured into six thematic sub-sections. | **Addressed** | The six sub-sections (crash reporting, background execution, permissions, reliability, OEM fragmentation, Flutter/cross-platform) cover the gaps the first review flagged. The new references are real, correctly cited, and properly positioned against the contribution. 22 refs is appropriate for IEEE Software at this length. |
| **R2: OEM aggression ratings subjective** | Three binary signals defined (S1: foreground service kill despite whitelist, S2: settings reset on OTA, S3: background-only kill). Rating formula: 5/5 = S1+S2, 4/5 = S1 only, 3/5 = S3 only, 2/5 = stock Android, 1/5 = AOSP. Signals declared testable via `Build` class and `PackageManager.resolveActivity()`. | **Addressed** | The signals are concrete and reproducible. A reviewer can disagree with the weighting but can replicate the measurement. The runtime-testability claim (via `Build` class) is a good addition: it ties the ratings to something an app can check programmatically, not just to field observations. |
| **R3: Four-org framing inflates sample** | Paper now reads "two primary fleets of 38 and 31 devices, two smaller with 6 and 1" throughout (abstract, Section 6 paragraph 1, OEM ratings paragraph). | **Partially addressed** | The framing is honest now. But the per-org counts introduce a new numerical inconsistency. See Part 3, Issue 1. |
| **R4: arXiv ID placeholder unfilled** | Still reads `arXiv:XXXX.XXXXX [cs.SE]` in `references.bib` line 124. | **Not addressed** | This is a hard blocker for submission. The self-citation `ghag2026testing` cannot go to a reviewer with a placeholder ID. Either submit that paper first and fill in the ID, or change the citation to a tech report with a URL. |
| **R5: Conclusion lacks explicit limitations** | Conclusion now has a full paragraph: "Two limitations bound these results. First, the methodology is validated against one app on one platform in one use case... Second, we have not implemented the specification and measured the before/after detection rate." Also adds iOS as a third limitation. | **Addressed** | Clean, direct, no hedging. The three limitations (N=1, no before/after, no iOS) are stated plainly and each points to the same next step. This reads well. |
| **Additional: Tracelet replaced with architecture description** | New Section 2.4 (Background Location Engine Architecture) describes the Rust FFI engine, headless isolate, `BOOT_COMPLETED` receiver, `stopOnTerminate: false` / `startOnBoot: true` config, and the three signals the architecture produces. No product name. | **Addressed** | Good call. The section is concise (one page), explains exactly what a reader needs to follow the validation, and the three-signal framing (odometer reset, headless waypoints, boot event) ties directly into the taxonomy. The old product name would have been a distraction. |

---

## Part 2: Gate Results

### Gate 3a: Is it a scientific paper?

**Verdict:** PASS

Abstract, introduction with four stated contributions, background (Section 2 with four sub-sections including the new architecture section), methodology core (Sections 3-5), validation with empirical data (Section 6), threats to validity (Section 7), related work (Section 8), discussion (Section 9), conclusion (Section 10). The structure is sound and unchanged from v1.

### Gate 3b: Is it software engineering?

**Verdict:** PASS

Runtime observability for mobile apps. Squarely SE. No change from v1.

### Gate 3c: arXiv quality gates

**(a) English:** PASS. Clear throughout.

**(b) Self-contained:** PASS. The new Section 2.4 actually strengthens this: a reader no longer needs to know what "Tracelet" is.

**(c) Scientifically honest:** PASS. Self-citation is transparent, researcher bias is addressed in threats to validity.

**(d) Scholarly writing quality:** PASS. Above average for the venue.

**(e) Bibliography:** PASS. 22 references, all cited in text, all present in `.bib`. Every `\cite{}` key resolves to a bib entry, and every bib entry is cited at least once.

**Overall Gate 3c:** PASS.

### Gate 4: Repository-Paper Correspondence

**Verdict:** CONDITIONAL PASS (same condition as v1)

Spot-checked the revised numbers against the analysis files:

| Claim | Data source | Match? |
|---|---|---|
| 159 tracking sessions | session-analysis.md | Yes |
| 14,094 waypoints | waypoint-gap-analysis.md | Yes |
| 509 gaps >5 min | waypoint-gap-analysis.md | Yes |
| 65 sessions ≤3 waypoints (40.9%) | session-analysis.md: 63 with 1-3 + 2 with 0 = 65 | Yes |
| 25 sessions ended by server timeout (15.7%) | session-analysis.md: end_reason=3, count=25 | Yes |
| GPS off/unknown at session end: 100/159 (62.9%) | session-analysis.md: None=51 + False=49 = 100 | Yes |
| Sessions ending ≤15% battery: 5 (3.1%) | session-analysis.md: 5 | Yes |
| Empty permission_event table | permission-events-analysis.md | Yes |
| Sequence resets (182→0, 174→0, 29→0) | waypoint-gap-analysis.md | Yes |
| Longest gap 110h 50m | waypoint-gap-analysis.md | Yes |
| 211 attendance sessions | session-analysis.md | Yes |
| **70 physical devices** | **device-fleet-profile.md says 86 physical records, dedup unclear** | **Plausible but not directly verifiable** |
| **38+31+6+1 = 76 per-org devices** | **Does not equal stated 70 total** | **Inconsistency (see Part 3)** |
| **50% Xiaomi** | **device-fleet-profile.md: 41.9% of records** | **Plausible after dedup but not verifiable** |

**Condition (unchanged from v1):** No public repository. Analysis data should be published alongside the paper, with appropriate anonymisation.

### Gate 5: osaudit.toml

**Verdict:** FAIL (expected, unchanged)

Still needed for arXiv cs.SE submission under the monperrus protocol.

---

## Part 3: New Issues

### Issue 1: Per-org device counts don't sum to the stated total [NUMERICAL]

The paper says "70 physical devices" and breaks this down as "two primary fleets of 38 and 31 devices, two smaller with 6 and 1." That's 38 + 31 + 6 + 1 = 76. Not 70.

The device fleet profile complicates things further: 94 total records, 86 physical (one row per app install, not per handset), 8 emulators. 86 - 8 = 78 records, but the note says "unique physical handsets are fewer than 86" due to duplicate rows across app version upgrades. So "70" is presumably the deduplicated count, and the per-org breakdown (38+31+6+1) may count records rather than unique handsets, or vice versa.

A reviewer who does the arithmetic will flag this. The fix is straightforward: either the per-org numbers need to sum to 70, or 70 needs to change to 76, or the paper needs one sentence explaining the discrepancy (e.g., "six devices appear in multiple organisations' registrations").

**Severity:** Medium. Numerical inconsistencies in a measurement paper undermine the data's credibility, even when the explanation is innocent.

### Issue 2: "50% Xiaomi" vs data [NUMERICAL]

The paper states "Xiaomi accounts for 50% of the physical fleet." The device fleet profile shows Xiaomi at 36/86 = 41.9% of physical device records. After deduplication to 70 devices, Xiaomi at 50% would mean 35 devices. This is plausible (the POCO X8 Pro Max has 30 records alone, many of which are duplicates), but the paper presents a round number with no derivation. Given the measurement-paper genre, stating the exact count and percentage would be stronger than a round "50%".

**Severity:** Low. The claim is directionally correct. But round numbers in a paper that elsewhere reports 40.9% and 15.7% to one decimal place look like they came from a different source or a different moment.

### Issue 3: "80% of the fleet runs on OEMs rated aggression 3/5 or higher" [NUMERICAL]

This appears in Section 2.2: "combined with OPPO, Vivo, and Realme, 80% of the fleet runs on OEMs rated aggression 3/5 or higher." From the device fleet profile, Xiaomi (36) + OPPO (7) + vivo (11) + realme (2) = 56 out of 86 physical records = 65.1%. After dedup to 70 devices, 80% = 56 devices on aggressive OEMs. Plausible but, again, not directly verifiable from the supporting data.

The same paragraph also says "two organisations account for 80% of the fleet." If the two primary orgs have 38 and 31 devices and the total is 70, that's 69/70 = 98.6%. If the total is 76, it's 69/76 = 90.8%. Neither is 80%.

Wait. I re-read more carefully. The "80%" about two organisations appears only in Section 6 paragraph 2: "Two organisations account for 80% of the fleet." The abstract says "two accounting for 80% of the fleet." But the per-org breakdown (38+31 out of 76 or 70) gives either 90.8% or 98.6%. Neither is 80%.

There may be two different "80%" claims conflated. One about OEM aggression (Xiaomi+OPPO+Vivo+Realme = aggressive OEMs), one about org concentration. If the org claim is about sessions rather than devices (106+45 = 151/159 = 95%), it's still not 80%. This needs reconciliation.

**Severity:** Medium. Two occurrences of "80%" that don't match the supporting data on any interpretation I can construct.

### Issue 4: R4 still open (arXiv placeholder)

`ghag2026testing` in `references.bib` still reads `arXiv:XXXX.XXXXX [cs.SE]`. This was R4 in the first review and is the only required revision that was not addressed. Cannot submit with a placeholder citation ID.

**Severity:** High. Blocker for both arXiv and IEEE Software submission.

### Issue 5: Section 2.4 integration is clean but creates a forward-reference concern

Section 2.4 (Background Location Engine Architecture) references `Section~\ref{sec:engine}`, which is its own label. That's fine. But the section introduces three signals (odometer reset, headless waypoints, boot event) that are used in the taxonomy (Section 3) and classification procedure (Section 5). A reader encountering Section 2.4 doesn't yet know the taxonomy. The section handles this correctly by describing the signals in architectural terms without taxonomy jargon. No fix needed; noting this as reviewed and clean.

**Severity:** None. Informational.

### Issue 6: "ten OEMs" vs device fleet data

Section 6 paragraph 2: "a long tail of 30+ distinct models from ten OEMs." The device fleet profile lists 10 OEMs for physical devices (Xiaomi including POCO/Redmi, Samsung, vivo, OPPO, Google, Infinix, realme, OnePlus, Motorola, LAVA). Consistent. But Samsung's 16 records are "all one model: SM-G990E (Galaxy S21 FE), a single device belonging to Org A used for development and testing. Not representative of Samsung's fleet diversity." The paper does not note that Samsung's fleet presence is a single dev device. This doesn't affect the methodology but it affects the OEM aggression rating for Samsung (4/5): the rating is assigned based on the fleet, but Samsung's only device in the fleet is a dev phone.

**Severity:** Low. The Samsung rating comes from known Samsung behaviour (Sleeping Apps), not solely from this fleet. But a careful reviewer might ask how a single dev device informed a 4/5 aggression rating.

### Issue 7: No new cross-section inconsistencies from multi-agent editing

I checked for the kind of inconsistency that arises when different agents edit different sections. The numbers in the abstract match the body. The contribution list in the introduction matches the section structure. The taxonomy categories in Table 2 match the classification procedure steps. The 12 gaps in Section 6.2 are numbered consistently. The related work references are all cited in the text and all resolve in `.bib`. No orphaned references, no phantom sections. Clean.

**Severity:** None. The revision was well-coordinated.

---

## Part 4: Final Verdict

**arXiv endorsement:** Not ready. R4 (arXiv ID placeholder) is still a blocker. Issues 1 and 3 (numerical inconsistencies) should also be resolved before submission but are not hard blockers for endorsement.

**IEEE Software submission:** One more pass. The paper improved materially from v1. The related work is now adequate. The OEM aggression ratings are grounded and reproducible. The org framing is honest. The new Section 2.4 strengthens reproducibility. The conclusion's limitations paragraph is direct and well-scoped.

Three things need fixing before submission:

1. **R4 (blocker):** Fill in the `ghag2026testing` arXiv ID or change the citation format.
2. **Numerical reconciliation (medium):** The per-org device counts (38+31+6+1=76) must sum to the stated total (70). The two uses of "80%" need to match verifiable data. "50% Xiaomi" should either show the exact percentage or explain the rounding.
3. **Gate 5 (arXiv only):** Add `osaudit.toml`.

Once those three are resolved, the paper is ready for IEEE Software submission. The core contribution (taxonomy + instrumentation spec + classification procedure, validated against production data) is sound and fills a genuine gap. The writing is clear. The limitations are stated honestly. [Likely to be accepted after one round of minor revision at the venue, conditional on the numerical fixes.]

The optional improvements from v1 (O1: implement one gap, O2: decision tree figure, O3: iOS comparison table) remain good ideas. O1 in particular would move the paper from "here is what you should measure" to "here is what happened when we did." But the paper is submittable without them.
