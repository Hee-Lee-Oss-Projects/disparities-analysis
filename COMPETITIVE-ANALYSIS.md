# Competitive + Improvement Analysis — `disparities-analysis`

> Subject: Hee-Lee Oss cancer good-deed project producing open, reproducible analyses of **cancer
> outcome disparities** from aggregate public data (race/ethnicity, geography, SES), with
> non-stigmatizing, structural (non-victim-blaming) framing. Risk: MEDIUM core / HIGH
> patient-facing. Analyst: Explore/research agent. Date: 2026-06-29.
> Plan reviewed: `PLAN.md` v0.1.0 (donated lane).

---

## 1. Correctness & completeness review of PLAN.md

The plan is unusually strong and self-aware. It already internalizes the hardest traps in this
domain. Findings below are organized as **confirmed strengths**, **gaps/risks**, and **concrete
fixes**.

### 1a. The framing/ethics guardrail — concrete and reviewed? (the dimension that matters most)

**Strength.** The plan treats non-stigmatizing framing as a *hard product requirement built
first*, not a disclaimer: a "non-stigmatizing health-equity editorial policy" is M0's first build
item, enforced as a release gate, with a dedicated **framing-review sign-off** (advocate/community
representative), a **reference-group policy** (no group silently coded "normal"), structural-
causation framing mandated, and a **no-ranking/no-scorecard** scope rule as the primary control
against "correct numbers, harmful use." It explicitly invokes "nothing about us without us"
(Improvement #20). This is materially more rigorous than every competitor surveyed in §2 — none of
which carry an *enforced, independently-reviewed framing gate*.

**Gap — the editorial policy is asserted but not yet specified.** The plan says the policy will
exist and be reviewed, but does not yet anchor it to an external, citable standard. There are
authoritative, vetted style guides it should adopt by reference so the policy is defensible and not
re-invented: **CDC's Health Equity Guiding Principles for Inclusive Communication / equity-centered
communication framework** (cdc.gov/pcd/issues/2023/23_0061.htm), the **CDC Health Equity Style
Guide** (built for the COVID-19 response), and the **AMA/AAMC Advancing Health Equity language
guide**. **Fix:** the M0 editorial-policy task should cite these as its normative base and record
deltas. This converts "we will be careful" into "we conform to a named, external standard,
reviewed."

**Gap — "structural framing" can itself overreach.** Mandating that every disparity be described as
the result of "modifiable structural/social conditions" is correct as the *default* frame, but if
applied mechanically it risks asserting a *causal structural claim* the specific dataset cannot
support — the mirror image of the biological-essentialism error. A purely ecological SEER cut does
not, by itself, demonstrate that *structural racism* caused a given gap; that attribution rests on
the broader literature. **Fix:** the editorial policy should require structural framing to be
**evidence-tiered** — distinguish "this analysis measures the gap" from "the established literature
attributes such gaps to structural factors X/Y (cite)" — so the framing is non-stigmatizing
*and* epistemically honest, not a reflexive causal claim. This is the single most important
correctness nuance the plan currently underspecifies.

### 1b. Avoiding biological-race essentialism

**Strength.** Explicitly requires treating race/ethnicity as **social/administrative constructs**
with documented misclassification, "never as biology" (Improvement #6; risk row). Excellent and
rare.

**Fix (small):** add an explicit prohibition on **interpreting genetic-ancestry/admixture as a
proxy for socially-assigned race** in any narrative, and require that area-based SES be described as
*exposure/environment*, not *individual behavior*. Add a positive instruction to name the
*mechanism* where known (insurance, screening access, environmental exposure) rather than leaving a
bare race coefficient to be misread as intrinsic.

### 1c. Small-population suppression / privacy

**Strength.** Strong and conservative: honors the **most-conservative applicable rule** (NCHS/CDC
WONDER < 10; SEER/USCS thresholds), adds **complementary suppression** (so suppressed cells can't be
back-calculated from margins), **RSE/stability flags**, an **adversarial re-identification review**,
and geographic coarsening — all blocking gates. Aggregate-only "by construction" and the explicit
exclusion of **SEER Research Plus case-level/DUA data** closes the most common "but it's
de-identified" loophole. This is best-in-class.

**Fix:** name the specific quantitative thresholds in the standard (e.g., NCHS: rates suppressed
when numerator < 10 or denominator < 20; mark rates with RSE > 30% unreliable; > 50% suppressed)
and the joinpoint minimum-points rule, so the suppression test is mechanically checkable rather than
"per source."

### 1d. Confounding + no causal overreach

**Strength.** Ecological-fallacy / "association is not causation" is mandated on **every** output,
a methods-review checklist item, and a top risk. Both **absolute and relative** disparity required
(prevents the classic small-base rate-ratio distortion). Strong.

**Gap:** the plan flags ecological inference but does not require an explicit statement of **what is
NOT adjusted for** (e.g., age-standardization controls age but not stage, comorbidity, access). A
reader can still over-interpret an age-adjusted gap as "pure." **Fix:** require each disparity
statement to carry a one-line "adjusted for / not adjusted for" note.

### 1e. Intersectionality

**Gap (notable).** The plan analyzes dimensions **one at a time** (race/ethnicity, sex, geography,
area-SES) and even treats multi-dimensional cuts mainly as a *re-identification risk* to suppress.
But the most policy-relevant disparities are often **intersectional** (e.g., rural + low-income +
Black; AIAN women). The tension is real: intersectional cells are exactly the thin cells suppression
removes. **Fix:** add an explicit, bounded intersectionality posture — report the few
intersectional cuts the data can support at acceptable suppression (and say so), and where it
cannot, *state the limitation* rather than silently omitting it (omission itself can erase the most
affected groups). This is both a completeness gap and an equity issue.

### 1f. Data limitations — race/ethnicity miscoding

**Strength.** Directly addressed: AIAN/NHPI/Hispanic-origin misclassification, bridged-vs-unbridged
denominators, and "avoid over-precise small-group claims" are a methods+framing requirement and a
dedicated risk. The competitive research confirms this is real and material — CDC's own USCS notes
incidence/mortality are **underestimated** for AIAN, API, and Hispanic people due to
misclassification, and recommends linkage (e.g., IHS linkage for AIAN). **Fix:** require, per
group, a recorded **direction-of-bias** note (which groups are under-counted and why) and adopt the
**OMB 1997 vs. 2024 revised race/ethnicity standards** question explicitly (the 2024 revision merges
race/ethnicity into one question and adds MENA — this will fracture trend comparability and belongs
in the methods standard now).

### 1g. Health-equity-expert review gate

**Strength.** Two MEDIUM gates (epi/biostat **and** health-equity/community framing), independence
+ recusal + version-scoped sign-off, plus a HIGH **oncologist + patient-advocate veto** for
patient-facing content with M4 *skipped entirely* if the pair isn't secured. The reviewer-acquisition
plan is dated with a build-vs-pivot rule. This governance is stronger than any surveyed competitor.

**Gap:** reviewer **sourcing and compensation** is an open question, and the whole MEDIUM surface is
blocked until two volunteer experts are secured by a date — a real single point of failure. **Fix:**
pre-line-up reviewer pipelines via **NCI-designated cancer-center COE offices**, schools of public
health, and the NCI/NIMHD networks (CRCHD PACHE, Community Networks); consider a named institutional
partner rather than two individuals.

### 1h. Actionability without blame

**Strength.** Site-selection criteria require the disparity be **actionable** (screening/access-
driven, e.g., colorectal/cervical), and outputs are framed as "conditions to fix." Good — this is
what turns a statistic into a program.

**Gap:** "actionable" is asserted but there's no artifact that *links a finding to an intervention*.
**Fix:** add an optional **"what works" pointer** that maps each finding to evidence-based
interventions — and note the natural source: **NIMHD HDPulse's Interventions Portal** and the
**Community Guide**. This both increases actionability and differentiates from pure-data competitors
(see §2/§4), without the project itself making clinical recommendations.

### 1i. Completeness / structural

All 17 PLAN_SPEC sections present and ordered; guardrails lead the Data and Quality sections; outcome
(not merge) is the definition of shipped; metrics are outcome-centric; the Python/R-for-stats
deviation from the TS default is honestly recorded for maintainer sign-off; `verifiedNeed:false` and
`TO BE SECURED` are used honestly throughout. **Minor:** the referenced `governance/proposals/
disparities-analysis.md` does not yet exist (self-flagged), and `TASKS.md` is referenced but not
reviewed here.

---

## 2. Competitive landscape

This is a **crowded, authoritative field** — the incumbents are federal agencies and the American
Cancer Society. The honest competitive truth: *the data and even the disparity math already exist and
are excellent.* The whitespace is **not new numbers**; it is **reproducibility + provenance +
reviewed non-stigmatizing narrative + last-mile fit for a specific community partner** (see §3–§4).

| Competitor | What it is | Strengths | Weaknesses (our opening) |
|---|---|---|---|
| **NCI SEER\*Explorer** ([seer.cancer.gov/statistics-network/explorer](https://seer.cancer.gov/statistics-network/explorer/application.html)) | Interactive aggregate incidence/mortality/survival by site, race, sex, age, stage | Authoritative source data; age-standardized; CIs; trend (APC) | A data-exploration UI, not a *reasoned, reviewed disparity analysis*; no narrative; no SES/area dimension; not a reproducible package |
| **NCI State Cancer Profiles** ([statecancerprofiles.cancer.gov](https://seer.cancer.gov/statistics/interactive.html)) | National/state/county maps + graphs, explicitly to "expose health disparities" | County granularity; standardized; disparity-oriented framing | Maps/numbers only; no structural narrative; no per-assertion provenance package; not partner-tailored |
| **NCI HD\*Calc** ([seer.cancer.gov/help/hdcalc](https://seer.cancer.gov/help/hdcalc/inference-methods/pre-calculated-statistics-1/measures-of-relative-disparity/index-of-disparity)) | Software computing **11 summary disparity measures** (incl. Index of Disparity, SII, RII) with CIs | Methodologically rigorous; the *de facto* standard for disparity indices; we should **use** it | A calculator, not an analysis or a narrative; expert-only; no framing/provenance/last-mile layer |
| **CDC U.S. Cancer Statistics Data Viz Tool** ([cdc.gov/united-states-cancer-statistics/dataviz](https://www.cdc.gov/united-states-cancer-statistics/dataviz/index.html)) | Full-population incidence/mortality by bridged race/ethnicity, stage, screening, risk factors | Most complete U.S. registry coverage (NPCR+SEER ~100%); careful race/ethnicity technical notes | Exploration tool; no reproducible analysis artifact; no structural narrative; subject to federal data-availability disruptions (note the *restoredcdc.org* mirrors) |
| **NIMHD HDPulse** ([hdpulse.nimhd.nih.gov](https://hdpulse.nimhd.nih.gov/)) | **Data Portal** (national/state/county disparity stats, maps, incl. cancer) **+ Interventions Portal** (evidence-based interventions) | *Closest competitor.* Disparity-focused, county-level, AND links to interventions — the actionability layer we lack | Tool/portal, not a per-site reviewed analysis with provenance-per-assertion; framing is generic; not a partner-co-developed deed |
| **American Cancer Society — Cancer Facts & Figures for [population]** + **Status of Cancer Disparities in the U.S., 2025** ([cancer.org](https://www.cancer.org/research/cancer-facts-statistics/cancer-facts-figures-for-african-americans.html); [PMC12707308](https://pmc.ncbi.nlm.nih.gov/articles/PMC12707308/)) | Authoritative narrative reports; explicitly trace disparities to **structural racism / social determinants** | Gold-standard *narrative + framing*; peer-reviewed (CA: Cancer J Clin); national reach | National, not local/partner-specific; PDF reports, **not reproducible/openly-pipelined**; annual cadence; not co-developed with a specific community |
| **County Health Rankings & Roadmaps** (RWJF + UW) ([countyhealthrankings.org](https://www.countyhealthrankings.org/sites/default/files/media/document/2024%20CHRR%20Technical%20Document_1.pdf)) | County-level health-outcome/factor model + rankings + "Roadmaps" action | County coverage; action-oriented; established | **Ranking model** — exactly the "naming/scorecard" stigma pattern our plan refuses; cancer is one indicator among many, not depth |
| **Our World in Data — Cancer** ([ourworldindata.org/cancer](https://ourworldindata.org/cancer)) | International cancer mortality/incidence from IHME GBD | Excellent reproducibility/open-data ethos; clear explainers; global | International/country-level; **not** U.S. within-country race/SES disparities; GBD modeled estimates, not registry |
| **AACR Cancer Disparities Progress Report** ([cancerprogressreport.aacr.org](https://cancerprogressreport.aacr.org/disparities/)) | Biennial science+policy narrative on disparities | Strong policy framing; authoritative | Narrative/policy, not a reproducible local analysis or tool |
| **Harvey L. Neiman HPI — Cancer Disparity Maps** ([neimanhpi.org/cancer-disparity-maps](https://www.neimanhpi.org/cancer-disparity-maps/)) | Imaging/screening-oriented cancer disparity maps | Specific, visual | Narrow (imaging lens); not a general reproducible package |

**Net read.** The market splits into (a) **federal data/exploration tools** (SEER\*Explorer, State
Cancer Profiles, USCS Data Viz, HDPulse) — rich data, weak reasoning/narrative/provenance-package;
(b) **authoritative narrative reports** (ACS, AACR) — strong framing, *not reproducible or local*;
and (c) **methods software** (HD\*Calc). **No incumbent delivers the combination of a reproducible,
provenance-per-assertion, independently methods-reviewed AND framing-reviewed, openly-licensed,
partner-co-developed analysis for a specific community.** That gap is the project's reason to exist.

---

## 3. Gaps we can fill

1. **Provenance-per-assertion + bit-for-bit reproducibility.** No incumbent ships an analysis where
   *every quantitative claim* carries a machine-checkable `Source` (dataset/version/query/retrieval
   date/license) and figures regenerate from source. ACS reports and federal tools are trustworthy
   but not *independently re-runnable artifacts*. This is our most defensible gap.
2. **Reviewed, non-stigmatizing narrative bound to the numbers.** ACS has framing; SEER/HDPulse have
   numbers. Nobody pairs a reproducible analysis with an *independently framing-reviewed*,
   community-voiced narrative as a release gate.
3. **Local / partner-specific depth.** Federal tools are national/state/county-generic; we
   co-develop *one exemplar site* analysis tuned to a specific COE catchment or coalition's need.
4. **Both absolute + relative disparity, always.** Most dashboards surface one measure; we mandate
   rate difference **and** rate ratio **and** an index of disparity (consuming HD\*Calc-grade
   methods), preventing small-base distortion.
5. **Honest limitations as first-class content** — misclassification direction-of-bias,
   suppression, ecological-inference, "not adjusted for," data vintage — attached automatically,
   not buried in technical notes.
6. **Actionability bridge** (per §1h): mapping a finding to evidence-based interventions (via
   HDPulse Interventions Portal / Community Guide) without the project itself giving clinical advice.
7. **Resilience to federal data disruption.** The *restoredcdc.org* mirrors in our search results
   show federal tools can go dark/change; an openly-licensed, checksum-pinned, reproducible package
   is a durable public good when portals are unstable.
8. **A reusable, parameterized engine** so a second cancer site is configuration, not a rewrite —
   incumbents are bespoke per report.

---

## 4. Differentiators to win

1. **"Reviewed reproducibility" as the product.** The unit isn't a chart; it's a sealed package:
   pinned inputs + documented queries + provenance-per-assertion + methods sign-off + framing
   sign-off + reproduction test. Nobody else ships this combination.
2. **Framing is a tested gate, not a disclaimer** — anchored to CDC/AMA equity style guides,
   community-reviewed ("nothing about us without us"), with a hard no-ranking/no-scorecard rule.
   This is the single strongest differentiator: it directly counters the field's chief failure mode
   (correct numbers used to stigmatize) and is the opposite of County Health Rankings' ranking model.
3. **Built *with* and *for* a specific beneficiary** (COE/coalition/health dept), shipped only on
   *adoption* — versus publish-and-walk-away national reports.
4. **Methodological maximalism using the field's own validated tools** (NCI Joinpoint, HD\*Calc-grade
   indices, lifelines/statsmodels) rather than bespoke reimplementation — credibility by *using* the
   tools reviewers already trust.
5. **Radical limitation-honesty** (direction-of-bias, intersectional-suppression disclosure,
   not-adjusted-for notes) builds the trust that wins adoption among careful equity researchers.

---

## 5. Claude API leverage — and the hard "Claude must NOT decide" line

**Where Claude adds real, safe value (drafting/checking *from* computed numbers, human-verified):**

1. **Draft non-stigmatizing explainers from computed statistics.** Given the analysis module's
   structured outputs (rates, CIs, rate difference, rate ratio, index of disparity, flags), Claude
   drafts the technical brief and the plain-language narrative in structural, person-first framing —
   *transforming verified numbers into prose*, never inventing numbers. (Strong fit for the explainer
   engine and a future MCP server, §7.)
2. **Automated structural-framing / stigma linter.** Claude reviews any draft against the editorial
   policy + CDC/AMA equity style guides and flags deficit framing, biologizing language, silent
   reference-group coding, relative-only statements, missing caveats, or absent "not medical advice"
   labels — a *first-pass* assist to the human framing reviewer, surfacing issues, not approving.
3. **Plain-language + reading-level + translation drafting** for community audiences; **caveat/
   limitation auto-attachment**; **provenance/citation-coverage triage** (flagging assertions that
   lack a `Source` before CI does, and suggesting the matching `DisparityMeasure`).
4. **Reviewer-burden reduction:** Claude pre-fills the methods/framing checklists and drafts the
   "adjusted-for / not-adjusted-for" and direction-of-bias notes for human verification.

**Where Claude must NOT decide (hard guardrails — enforce in the editorial/methods standard):**

- **No causal claims** and **no biological-race claims** — Claude may restate the established
  literature *with citations the human verifies*, but must never originate a causal/structural
  attribution from the data, nor a genetic/biological interpretation of race.
- **The numbers come from code, not the model.** Every statistic is computed by the validated
  Python/R pipeline; Claude never estimates, rounds, infers, or "fills in" a rate, CI, or count.
- **Framing is human-and-community-reviewed.** Claude's stigma-linter is advisory; the
  *health-equity/community* sign-off (preferably a representative of the affected community) and the
  *epi/biostat* sign-off are the deciders. For patient-facing content, the **oncologist + advocate
  veto is absolute** — Claude cannot clear it.
- **Accuracy + license + helpline facts are human-verified.** Claude never asserts a source's reuse
  terms, never decides suppression, and any helpline/resource info it drafts is independently
  verified and dated by a human.
- **No suppression / re-identification judgment** — that is a tested gate + adversarial human review.

The clean mental model: **Claude writes and checks the words; code computes the numbers; credentialed
humans and the affected community decide what is true, safe, and shippable.**

---

## 6. Ten concrete optimizations

1. **Anchor the editorial policy to named external standards** — CDC Health Equity Guiding
   Principles + CDC Health Equity Style Guide + AMA/AAMC equity language guide — and record deltas,
   so the framing gate is defensible, not re-invented (§1a).
2. **Make structural framing evidence-tiered** — separate "this analysis measures the gap" from
   "the literature attributes such gaps to structural factors (cite)," to be non-stigmatizing
   *without* over-claiming causation (the key correctness fix, §1a).
3. **Add a bounded intersectionality posture** — report the intersectional cuts the data supports
   and explicitly disclose where suppression forces omission, so the most-affected groups aren't
   silently erased (§1e).
4. **Build the stigma-linter (Claude) + checklist pre-fill** into CI as an advisory pre-gate ahead
   of human framing review (§5).
5. **Adopt HD\*Calc's measure set** (Index of Disparity, SII/RII, with CIs) as the disparity-index
   standard, and validate the pipeline's outputs against HD\*Calc on the exemplar site — instant
   methodological credibility (§2).
6. **Specify exact suppression/stability thresholds** (NCHS numerator<10, RSE>30% unreliable /
   >50% suppress, complementary suppression, joinpoint min-points) in the standard so the gate is
   mechanically testable (§1c).
7. **Add a "what works" actionability pointer** mapping each finding to evidence-based interventions
   via **HDPulse Interventions Portal / The Community Guide** — closes the gap to HDPulse while
   staying education-only (§1h, §3).
8. **Record per-group direction-of-bias** for race/ethnicity misclassification (which groups are
   under-counted, why, linkage caveats) and **pre-decide OMB 1997-vs-2024 standard handling** for
   trend comparability (§1f).
9. **Require an "adjusted-for / not-adjusted-for" line** on every disparity statement to block
   over-interpretation of age-adjusted-only gaps (§1d).
10. **Mirror/pin source pulls with checksums and archive raw extracts** so the package survives
    federal-portal disruption (the restoredcdc.org signal) and remains reproducible years later (§3).

---

## 7. Parallel & perpendicular spin-offs

**Parallel (same domain, reuse the engine):**
- **`incidence-explorers`** (named sibling in the Hee-Lee Oss roadmap): the same parameterized acquisition/
  provenance/age-standardization core powers incidence exploration; disparities-analysis is the
  reviewed-narrative layer on top.
- **`screening-coverage-trends`**: BRFSS/USCS screening-uptake disparities (colorectal, cervical,
  breast) — directly actionable, same pipeline, natural partner overlap with COE programs.
- **Second/third cancer sites** as configuration, not rewrite (M6), each cheaper to review.

**Perpendicular (different domain, same *machine*):**
- A **general "equity-framing-reviewed explainer engine"**: the combination of (validated-stats-in →
  Claude-drafted-structural-narrative → stigma-linter → human+community review → provenance-bound
  output) generalizes to **any** disparities domain — maternal health, diabetes, environmental
  justice, housing, education. The reviewed-framing pipeline is the reusable IP, not the cancer data.
- A **non-stigmatizing-framing linter** as a standalone library/service usable by journalists and
  advocacy orgs (the field's chief failure mode is bad framing of correct numbers).

**MCP server.** Expose the provenance store + computed `DisparityMeasure` records + the editorial
policy as an **MCP server** so any reviewer's agent (or a partner's) can query "give me the sourced,
suppression-safe, framing-compliant statement for colorectal mortality rate-ratio in [group] vs
reference, with caveats" — read-only, numbers-from-code, citations attached. This operationalizes
"Claude writes words, code owns numbers" and is a clean reusable surface across all the spin-offs.

---

## 8. Open questions

1. **Causation-framing calibration:** how strongly may a structural frame be stated from purely
   ecological data before it itself becomes an over-claim? (Needs the framing + methods reviewers to
   jointly define tiers — the §1a fix.)
2. **Intersectionality vs. suppression:** what is the principled rule for which intersectional cuts to
   report vs. disclose-as-suppressed, so omission doesn't erase the most-affected groups? (§1e)
3. **OMB 2024 race/ethnicity standard adoption:** when do new categories (combined question, MENA)
   enter, and how are pre/post trends bridged without misleading comparisons? (§1f)
4. **GLOBOCAN/IARC non-commercial terms vs. CC-BY-4.0** (already an open item) — method-and-pointer
   vs. per-artifact NC licensing; needs governance decision.
5. **Reviewer sourcing + compensation** — the MEDIUM surface is blocked on two volunteer experts;
   should the project secure an *institutional* COE/SPH partner instead, and how are community
   reviewers fairly credited/paid? (§1g)
6. **Area-based SES choice** (SVI vs. ADI vs. tract poverty) — which is most defensible and least
   stigmatizing for the exemplar site? (plan's own open question)
7. **Exemplar-site choice** — colorectal vs. cervical (both actionable/screening-driven); gates
   M1–M6, decided in M0.
8. **Actionability scope** — does adding a "what works" pointer (§7 intervention mapping) risk
   drifting toward advice, and where exactly is that line drawn relative to the HIGH patient-facing
   gate?

---

*Sources (key): SEER\*Explorer & State Cancer Profiles (seer.cancer.gov); NCI HD\*Calc index-of-
disparity docs (seer.cancer.gov/help/hdcalc); CDC U.S. Cancer Statistics Data Viz + race/ethnicity
technical notes (cdc.gov/united-states-cancer-statistics); NIMHD HDPulse data + interventions portals
(hdpulse.nimhd.nih.gov); NCI CRCHD (cancer.gov/about-nci/organization/crchd); ACS Cancer Facts &
Figures for African American/Black People 2025 + Status of Cancer Disparities 2025 (cancer.org;
PMC12707308); AACR Cancer Disparities Progress Report (cancerprogressreport.aacr.org); County Health
Rankings technical doc (countyhealthrankings.org); Our World in Data — Cancer (ourworldindata.org/
cancer); CDC Health Equity Guiding Principles / Style Guide + AMA/AAMC equity language guidance
(cdc.gov/pcd/issues/2023/23_0061.htm; cdc.gov/health-communication); Harvey L. Neiman HPI Cancer
Disparity Maps (neimanhpi.org).*
