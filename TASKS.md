# Disparities-Analysis — TASKS.md

> Status: Draft · Version: 0.2.0 · Last updated: 2026-06-29 · Owner: TBD (maintainer) · Lane: donated

Backlog for **Disparities-Analysis** (slug: `disparities-analysis`), open, reproducible analyses of
cancer outcome disparities built **only** from aggregate, open-access, de-identified public data,
with careful, non-stigmatizing, health-equity framing and provenance on every assertion. See
`PLAN.md` for full context.

The **non-stigmatizing framing/editorial policy** and the **statistical-methods + provenance +
suppression standard** are the **first build items** and hard product requirements (the project's
equivalent of a guardrail layer). This project is **MEDIUM** risk on its analytical surface
(epidemiology/biostatistics + health-equity framing review required) and **HIGH** risk on any
**patient-/public-facing** content (education only, "not medical advice — consult your care team",
**blocking oncologist + patient-advocate sign-off** before merge; helpline/resource info verified +
dated). No partner organization or reviewer is yet secured, so delivery-dependent tasks carry
`requestor: TO BE SECURED` and `verifiedNeed: false`.

## How these tasks map to Hee-Lee Oss

Each task below becomes a Hee-Lee Oss **Task JSON** validated against `packages/schema/src/schemas.ts`.
Field mapping:

- **id** — stable slug `disparities-analysis-<area>-NNN` (e.g. `disparities-analysis-framing-001`).
- **title** — the task title in the milestone table.
- **project** — `disparities-analysis`.
- **type** — one of `code | research | writing | data | design-spec | maintenance`.
- **lane** — `donated` (default; no funded tasks planned. Any `funded` task **must** add
  `fundedBudgetUsd` with a hard cap — schema-enforced).
- **priority** — `high | medium | low`.
- **domain** — array, e.g. `["health","cancer","epidemiology","health-equity","data"]`.
- **riskTier** — `low | medium | high`. **HIGH** = any patient-/public-facing content (health/safety
  domain → credentialed expert sign-off before merge); **MEDIUM** = analytical content needing
  domain accuracy (epi/biostat + framing review); **LOW** = pure tooling/infra.
- **urgent** — boolean (no urgent tasks at cold-start).
- **deliverable** — `pr | dataset | document | translation`.
- **tokenEstimate** — `small | medium | large` (maps to the Size column).
- **status** — `open | in-progress | review | delivered | done` (all start `open`).
- **context / objective / acceptanceCriteria[] / resources[] / output** — per task.
- **requestor** — partner/steward/reviewer; `TO BE SECURED` where unknown.
- **verifiedNeed** — `true` only once a specific partner/need is confirmed; otherwise `false`
  (currently `false` everywhere — no partner secured).
- **outputLicense** — code: **MIT**; derived data/content: **CC-BY-4.0** *where the source license
  permits* (U.S. Government sources: SEER/USCS/WONDER/Census/SVI). For non-commercial/no-deriv
  sources (e.g. **IARC GLOBOCAN**), publish method + pointer or apply the source-mandated terms to
  that artifact — see `PLAN.md` *Data, licensing & compliance*.

Size legend: small ≈ tokenEstimate `small`, med ≈ `medium`, large ≈ `large`.
Reviewer abbreviations: **Maintainer**; **Methods** = epidemiology/biostatistics reviewer (TO BE
SECURED); **Framing** = health-equity / community framing reviewer (TO BE SECURED); **Onc+Adv** =
oncologist + patient-advocate pair (HIGH, blocking, TO BE SECURED).

---

## Milestone M0 — Foundations, framing & methods standards (cold-start)

| ID | Title | Type | Size | Risk | Deliverable | Depends on | Reviewer |
|---|---|---|---|---|---|---|---|
| disparities-analysis-framing-001 | Non-stigmatizing health-equity editorial & framing policy spec | design-spec | medium | medium | document | — | Framing + Maintainer |
| disparities-analysis-methods-002 | Statistical-methods + provenance + suppression standard | design-spec | medium | medium | document | — | Methods + Maintainer |
| disparities-analysis-licensing-003 | Source license & access register (aggregate-only; verify reuse terms per source) | research | medium | medium | document | — | Maintainer + Methods |
| disparities-analysis-site-004 | Exemplar cancer-site selection (scored against explicit criteria) — gates M1–M6 | research | small | medium | document | 003 | Maintainer + Methods + Framing |
| disparities-analysis-repo-005 | Repo skeleton + provenance schema + CI (citation-coverage, suppression, license-presence lint, advisory stigma-linter pre-gate) | code | medium | low | pr | — | Maintainer |

**Acceptance criteria — key tasks**

- **disparities-analysis-framing-001** (framing/editorial policy)
  - **Anchors the policy to named external standards** — CDC Health Equity Guiding Principles for
    Inclusive Communication, the CDC Health Equity Style Guide, and the AMA/AAMC Advancing Health
    Equity language guide — citing them as the normative base and recording any project deltas.
  - Defines required framing: disparities described as outcomes of **modifiable structural/social
    conditions**, never as inherent group attributes; **no causal claims** beyond what the design
    supports.
  - **Requires evidence-tiered structural framing:** every claim separates **"this analysis measures
    the gap"** (what the dataset supports) from **"the established literature attributes such gaps to
    structural factors X/Y (cite)"** — so structural framing is non-stigmatizing *without*
    over-claiming causation from ecological data (the mirror of biological essentialism).
  - **Adopts a bounded intersectionality posture:** report the intersectional cuts the data supports
    at acceptable suppression **and explicitly disclose where suppression forces omission**, rather
    than silently dropping thin intersectional cells (silent omission erases the most-affected
    groups).
  - Treats race/ethnicity as **social/administrative constructs** with documented misclassification
    (esp. AIAN/NHPI/Hispanic-origin); forbids biologizing race; **prohibits interpreting
    genetic-ancestry/admixture as a proxy for socially-assigned race**, requires area-based SES to be
    described as *exposure/environment* not *individual behavior*, and instructs naming the
    **mechanism** where known (insurance, screening access, environmental exposure).
  - Mandates **asset-based, person-first, community-centered** language and a **reference-group
    policy** (no group silently coded "normal"; report to a stated reference **and** an across-group
    index of disparity).
  - Requires mandatory caveats on every output (data vintage, suppression, CIs, **"association is not
    causation"/ecological-fallacy**) and the **no-medical-advice** rule + "consult your care team"
    label for any patient-facing surface.
  - Establishes the **no-ranking/no-scorecard** rule (no "worst places"/"naming and shaming").
  - Reviewed and signed off by a health-equity/community framing reviewer (recorded in the reviewers
    ledger); prefers a representative of an affected community.

- **disparities-analysis-methods-002** (methods/provenance/suppression standard)
  - Mandates **age-standardization** (2000 U.S. standard population for U.S. data; WHO World Standard
    international), **confidence intervals** (e.g. Tiwari-modified for SEER rates), and
    relative-standard-error/stability flagging for small numerators.
  - Mandates **joinpoint** trend modeling (APC/AAPC) and **both absolute (rate difference) and
    relative (rate ratio)** disparity measures + an index of disparity; **adopts the HD\*Calc measure
    set** (Index of Disparity, SII/RII with CIs) and **validates pipeline outputs against HD\*Calc**
    on the exemplar site.
  - Requires a one-line **"adjusted for / not adjusted for"** note on every disparity statement (e.g.
    age-standardized controls age but not stage, comorbidity, or access) to block over-interpretation
    of an age-adjusted-only gap.
  - Defines the `Source`/`DisparityMeasure`/`Assertion` records and the **"no quantitative assertion
    without a `Source`"** rule.
  - Defines **small-cell suppression** with **exact, mechanically-checkable thresholds** (NCHS-style:
    numerator < 10; flag RSE > 30% unreliable, suppress at RSE > 50%; SEER/USCS thresholds honored
    where more conservative; a joinpoint minimum-points rule) **plus complementary suppression**
    (suppressed cells not reconstructable from margins) and the re-identification check.
  - Records a per-group **direction-of-bias** note for race/ethnicity misclassification (which groups
    are under-counted and why — CDC/USCS note under-estimation for AIAN/API/Hispanic people; linkage
    such as IHS for AIAN) and **pre-decides OMB 1997-vs-2024 standard handling** (combined question +
    MENA) so pre/post trends are bridged, not silently mis-compared.
  - Signed off by the epidemiology/biostatistics reviewer.

- **disparities-analysis-licensing-003** (license & access register)
  - Records, per candidate source (SEER\*Explorer, USCS, CDC WONDER, GLOBOCAN/IARC, Census/ACS, SVI,
    BRFSS), the **verified reuse terms**, whether redistribution under CC-BY-4.0 is permitted, and
    any non-commercial/no-derivatives constraint.
  - **Explicitly excludes** controlled-access / DUA-gated case-level data (dbGaP, EGA, **SEER
    Research Plus** case extracts) as out of scope.
  - Flags the **GLOBOCAN/IARC vs. CC-BY** conflict and records the per-artifact resolution (method +
    pointer, or source-mandated terms).
  - This register is a **blocking gate**: no source's data is used or republished until its row is
    verified.

- **disparities-analysis-site-004** (exemplar-site selection)
  - Scores candidate sites against: (1) large, well-documented disparities in **open aggregate** data
    at acceptable suppression; (2) **actionability** (screening/access-driven, e.g. colorectal or
    cervical); (3) reviewer availability; (4) candidate-partner fit.
  - Records the decision (or shortlist + decision deadline of 2026-08-31) with rationale; the chosen
    site gates M1–M6.

**M0 Definition of Done:** framing/editorial policy (CDC/AMA-anchored, evidence-tiered structural
framing, bounded intersectionality posture) + methods/provenance/suppression standard (exact
thresholds, HD\*Calc set, adjusted-for note, direction-of-bias + OMB handling) written and
reviewer-approved; source license register drafted with each candidate source's terms verified and
out-of-scope restricted data excluded; repo skeleton + provenance schema + CI (citation-coverage,
suppression, license-presence lint, **advisory stigma-linter pre-gate**) green; exemplar cancer site
selected (or shortlisted with a fixed decision) so M1+ builds against a viable corpus.

---

## Milestone M1 — Acquisition & provenance pipeline

| ID | Title | Type | Size | Risk | Deliverable | Depends on | Reviewer |
|---|---|---|---|---|---|---|---|
| disparities-analysis-provenance-006 | Provenance + assertion-citation schema implementation + "no assertion without source" CI check | code | medium | low | pr | 002, 005 | Maintainer |
| disparities-analysis-acquire-007 | Reproducible acquisition module (SEER\*Explorer/USCS/WONDER + ACS/SVI context) with saved queries, retrieval dates, checksums | code | large | medium | pr | 003, 006 | Maintainer + Methods |
| disparities-analysis-cube-008 | Canonical disparities data cube for exemplar site (aggregate, suppressed, license-cleared) + feasibility kill-gate | data | medium | medium | dataset | 004, 007 | Methods + Maintainer |

**Acceptance criteria — key tasks**

- **disparities-analysis-acquire-007** (acquisition module)
  - Re-runnable acquisition of **aggregate** statistics with **saved queries/parameters**,
    **retrieval dates**, archived raw pulls, and **checksums**; honors each source's terms and rate
    limits; ingests **no** individual-level data.
  - Each pulled dataset writes a complete `Source` record (incl. release year + verified license).
  - No secrets/tokens/PII in code, logs, or committed files (CI-enforced).

- **disparities-analysis-cube-008** (data cube + kill-gate)
  - Builds a canonical, **suppressed**, license-cleared aggregate cube for the exemplar site across
    race/ethnicity, sex, geography, area-SES, and year.
  - Suppression test passes (no cell below threshold; complementary suppression applied); stability
    flags attached.
  - **Feasibility kill-gate:** if open aggregate data cannot support a defensible disparity analysis
    at acceptable suppression for the chosen site, the task records this and **M2 pauses** for a
    site-switch/scope-narrow decision rather than proceeding.

**M1 Definition of Done:** provenance schema + "no-assertion-without-source" CI check live;
reproducible acquisition module pulling aggregate data with full provenance and verified licenses;
canonical suppressed data cube for the exemplar site built and license-cleared; the data-feasibility
kill-gate passed (or a site/scope decision recorded) before M2 investment.

---

## Milestone M2 — Core disparity analysis (exemplar site, MEDIUM)

| ID | Title | Type | Size | Risk | Deliverable | Depends on | Reviewer |
|---|---|---|---|---|---|---|---|
| disparities-analysis-rates-009 | Age-standardized rates + CIs + relative survival/stage + joinpoint trends (exemplar site) | code | large | medium | pr | 008 | Methods |
| disparities-analysis-disparity-010 | Absolute + relative disparity + index of disparity across dimensions (reference-group policy) | code | medium | medium | pr | 009 | Methods + Framing |
| disparities-analysis-brief-011 | Technical disparity brief (methods, findings, limitations; non-stigmatizing) | writing | medium | medium | document | 010 | Methods + Framing |

**Acceptance criteria — key tasks**

- **disparities-analysis-rates-009** (rates + trends)
  - Computes **age-standardized** incidence/mortality rates with **confidence intervals** and
    stability flags; relative survival and stage-at-diagnosis where available; **joinpoint** trends
    with APC/AAPC.
  - Uses validated tooling (NCI Joinpoint; `lifelines`/`statsmodels`/`epitools`); every output figure
    carries a `Source`; figures regenerated from source (no drift).
  - Methods reviewer sign-off recorded (version-scoped).

- **disparities-analysis-disparity-010** (disparity measures)
  - Reports **both** a rate difference **and** a rate ratio for every disparity statement (never
    relative-only) plus an **index of disparity** (and SII/RII) across all groups, using the
    **HD\*Calc measure set validated against HD\*Calc**.
  - Applies the **bounded intersectionality posture**: computes the intersectional cuts the data
    supports at acceptable suppression and **explicitly discloses the cuts suppression forces out**
    (no silent omission).
  - Attaches a one-line **"adjusted for / not adjusted for"** note to each statement.
  - Honors the **reference-group policy** (no group silently coded "normal"; reference explicitly
    stated); documents race/ethnicity misclassification caveats with a per-group
    **direction-of-bias** note.
  - Methods + framing sign-off recorded.

- **disparities-analysis-brief-011** (technical brief)
  - States findings with mandatory caveats (data vintage, suppression, CIs, **ecological-fallacy /
    association-not-causation**, "adjusted-for / not-adjusted-for"); frames disparities as
    **modifiable structural/social conditions** using **evidence-tiered** framing (measures-the-gap
    vs. literature-attributes-with-citation), and discloses intersectional cuts suppression forced
    out.
  - Every quantitative assertion is sourced (citation-coverage check passes); no ranking/scorecard
    framing; passes framing review.

**M2 Definition of Done:** age-standardized rates + CIs + trends and absolute+relative disparity (+
index of disparity) computed for the exemplar site, **methods-reviewed and framing-reviewed**, every
figure sourced, suppression honored, reproducible; the technical disparity brief drafted, sourced,
and framing-approved.

---

## Milestone M3 — Health-equity narrative report + reproducibility package (MEDIUM)

| ID | Title | Type | Size | Risk | Deliverable | Depends on | Reviewer |
|---|---|---|---|---|---|---|---|
| disparities-analysis-report-012 | Health-equity narrative report (advocacy/policy audience; non-stigmatizing) | writing | medium | medium | document | 011 | Framing + Methods |
| disparities-analysis-reproduce-013 | Reproducibility package + `scripts/reproduce.ts` re-derivation harness (CI gate) | code | medium | low | pr | 009, 010 | Maintainer |

**Acceptance criteria — key tasks**

- **disparities-analysis-report-012** (narrative report)
  - Translates the analysis for an advocacy/policy audience with **evidence-tiered structural framing**
    ("measures the gap" vs. "literature attributes such gaps to X, cite"), explicit limitations
    (including intersectional cuts suppression forced out), and actionable (non-prescriptive) context;
    **no medical advice**, no ranking/scorecard.
  - May include optional **education-only "what works" intervention pointers** mapping findings to
    evidence-based interventions via the **NIMHD HDPulse Interventions Portal / The Community Guide**,
    without the project itself making any clinical recommendation.
  - All quantitative claims sourced; framing review sign-off recorded.

- **disparities-analysis-reproduce-013** (reproducibility harness)
  - Re-runs the pipeline from **pinned inputs** and asserts published figures/tables are reproduced
    bit-for-bit (or within documented tolerance); wired into CI as a **blocking gate**.
  - Documents environment, pinned dataset release years, and exact queries so a second analyst can
    re-derive results.

**M3 Definition of Done:** non-stigmatizing health-equity narrative report published and
framing-reviewed; reproducibility package re-runs and reproduces all figures in CI / by a second
analyst.

---

## Milestone M4 — Patient/public-facing explainer (HIGH — conditional, gated)

> **Gated:** attempted **only if** an oncologist + patient-advocate reviewer pair is secured.
> If not, this milestone is **skipped** and the project ships M2–M3 outputs. All tasks here are
> **HIGH** risk: education only, persistent "not medical advice — consult your care team", **blocking
> Onc+Adv sign-off before merge**, and **verified + dated** helpline/resource info.

| ID | Title | Type | Size | Risk | Deliverable | Depends on | Reviewer |
|---|---|---|---|---|---|---|---|
| disparities-analysis-explainer-014 | Plain-language public explainer (education-only; "not medical advice") | writing | medium | high | document | 012 | Onc+Adv (blocking) + Framing |
| disparities-analysis-resources-015 | Verified resource/helpline information pack (dated, authoritative-sourced) | data | small | high | document | 014 | Onc+Adv (blocking) |

**Acceptance criteria — key tasks**

- **disparities-analysis-explainer-014** (public explainer)
  - Plain-language, **education-only**; carries a persistent **"This is general education, not medical
    advice — consult your care team"** label; gives **no** screening/prevention/treatment
    recommendation to individuals.
  - All facts sourced and framing-reviewed; non-stigmatizing; **oncologist + patient-advocate
    sign-off recorded before merge** (blocking).

- **disparities-analysis-resources-015** (resource/helpline pack)
  - Every helpline/resource item **verified against an authoritative current source** (e.g. NCI
    1-800-4-CANCER, 988) with a recorded **`lastVerified`** date; staleness check passes; **0**
    incorrect/stale entries at publish.
  - Oncologist + advocate sign-off recorded (blocking).

**M4 Definition of Done (conditional):** if the Onc+Adv pair is secured, the education-only explainer
and a verified+dated resource pack ship with **recorded blocking sign-off** and "not medical advice"
framing throughout; otherwise the milestone is formally **skipped** and recorded in governance.

---

## Milestone M5 — Partner delivery & handoff (the deed)

| ID | Title | Type | Size | Risk | Deliverable | Depends on | Reviewer |
|---|---|---|---|---|---|---|---|
| disparities-analysis-partner-016 | Secure delivery partner/steward + independent methods/framing audit of shipped outputs | research | medium | medium | document | 011, 012, 013 | Steward + Methods + Framing |
| disparities-analysis-handoff-017 | Partner uses an analysis to inform a program/report/grant/decision; outcome recorded (the deed) | maintenance | medium | medium | document | 016 | Steward + Methods + Framing |

**Acceptance criteria — key tasks**

- **disparities-analysis-partner-016** (secure partner + audit)
  - A real organization (advocacy coalition, cancer-center COE, public-health department, or research
    group) is secured; steward assigned; `verifiedNeed` flips to `true`.
  - Independent methods + framing audit of the shipped outputs recorded; licenses + suppression +
    provenance re-confirmed.
  - Driven by the **dated partner-acquisition plan** (site + ≥3 candidates + reviewers by 2026-08-31;
    partner/steward by 2026-12-31). If no partner by **~2027-03-31**, apply the **build-vs-pivot
    decision rule** (PLAN exec summary): pivot the last-mile beneficiary (publish as a reference deed
    / offer to a public-health training program) or mothball to maintenance-only — recorded in
    governance.

- **disparities-analysis-handoff-017** (closed loop — the deed)
  - The partner demonstrably uses an analysis to inform a concrete program, report, grant, or
    community decision; the outcome is recorded with the partner's confirmation.
  - Framing + methods independently verified; "not medical advice" upheld on any patient-facing piece.

**M5 Definition of Done:** project-level **Definition of Shipped** met — a real organization adopts an
analysis and uses it to inform a program/report/grant/decision; methods + framing independently
verified; every assertion sourced and licenses cleared; outcome recorded. *(Gated on a secured
partner — TO BE SECURED.)*

---

## Milestone M6 — Sustain & scale (post-delivery)

| ID | Title | Type | Size | Risk | Deliverable | Depends on | Reviewer |
|---|---|---|---|---|---|---|---|
| disparities-analysis-refresh-018 | Annual data-refresh + re-standardization runbook + maintenance rotation + second-site process | maintenance | medium | medium | document | 017 | Maintainer + Methods |

**Acceptance criteria — disparities-analysis-refresh-018**
- Runbook covers re-pull with new release years, re-run of the reproducible pipeline, re-verification
  of source licenses + suppression, **re-run of methods + framing review** for material changes, and
  re-verification of any helpline/resource info; `lastVerified`/`validUntil` staleness fail-safe in
  force.
- Named maintenance rotation; outcomes tracked with the partner (programs informed, reports/grants
  using the analysis) — **not** download counts.
- Documented, reviewer-gated process for adding a second cancer site using the parameterized analysis
  module.

**M6 Definition of Done:** project sustainably maintained with outcomes tracked, a rotation owning it,
an annual refresh + staleness cadence, and a gated multi-site expansion process.

---

## Backlog / future

| ID | Title | Type | Size | Risk | Deliverable | Notes |
|---|---|---|---|---|---|---|
| disparities-analysis-site2-019 | Second cancer-site analysis pack | data | large | medium | dataset | Only after M6; full methods + framing review; reuses parameterized module |
| disparities-analysis-intl-020 | International GLOBOCAN/CI5 comparison (WHO World Standard) | data | medium | medium | dataset | Honor IARC reuse terms; CC-BY conflict resolved per-artifact |
| disparities-analysis-ses-021 | Area-deprivation deep-dive (SVI vs. ADI vs. tract poverty) | research | medium | medium | document | Choose least-stigmatizing, most-defensible measure |
| disparities-analysis-notebook-022 | Reproducible explanatory notebook / methods walkthrough | writing | medium | low | document | Teaching artifact for "reading disparity stats correctly" |
| disparities-analysis-i18n-023 | Translate the public explainer (HIGH) into priority languages | writing | medium | high | translation | Only after M4 ships; per-language framing + Onc+Adv review |
| disparities-analysis-dashboard-024 | Static, no-PII aggregate visualization of the data cube | code | medium | medium | pr | Aggregate-only; suppression honored; no ranking/scorecard |

---

## Generated task index

> Auto-generated by Hee-Lee Oss task-decomposition on 2026-06-29. All 24 tasks validated against
> `packages/schema/src/schemas.ts` (draft-07, additionalProperties:false). Seed file preserved as-is.

| File | ID | Title | Type | Risk | Deliverable | Status |
|---|---|---|---|---|---|---|
| tasks/disparities-analysis-framing-001.json | disparities-analysis-framing-001 | Non-stigmatizing health-equity editorial & framing policy spec | design-spec | medium | document | open |
| tasks/disparities-analysis-methods-002.json | disparities-analysis-methods-002 | Statistical-methods + provenance + suppression standard | design-spec | medium | document | open |
| tasks/disparities-analysis-licensing-003.json | disparities-analysis-licensing-003 | Source license & access register (aggregate-only; verify reuse terms per source) | research | medium | document | open |
| tasks/disparities-analysis-site-004.json | disparities-analysis-site-004 | Exemplar cancer-site selection (scored against explicit criteria) — gates M1-M6 | research | medium | document | open |
| tasks/disparities-analysis-repo-005.json | disparities-analysis-repo-005 | Repo skeleton + provenance schema + CI (citation-coverage, suppression, license-presence lint, advisory stigma-linter pre-gate) | code | low | pr | open |
| tasks/disparities-analysis-provenance-006.json | disparities-analysis-provenance-006 | Provenance + assertion-citation schema implementation + "no assertion without source" CI check | code | low | pr | open |
| tasks/disparities-analysis-acquire-007.json | disparities-analysis-acquire-007 | Reproducible acquisition module (SEER*Explorer/USCS/WONDER + ACS/SVI context) with saved queries, retrieval dates, checksums | code | medium | pr | open |
| tasks/disparities-analysis-cube-008.json | disparities-analysis-cube-008 | Canonical disparities data cube for exemplar site (aggregate, suppressed, license-cleared) + feasibility kill-gate | data | medium | dataset | open |
| tasks/disparities-analysis-rates-009.json | disparities-analysis-rates-009 | Age-standardized rates + CIs + relative survival/stage + joinpoint trends (exemplar site) | code | medium | pr | open |
| tasks/disparities-analysis-disparity-010.json | disparities-analysis-disparity-010 | Absolute + relative disparity + index of disparity across dimensions (reference-group policy) | code | medium | pr | open |
| tasks/disparities-analysis-brief-011.json | disparities-analysis-brief-011 | Technical disparity brief (methods, findings, limitations; non-stigmatizing) | writing | medium | document | open |
| tasks/disparities-analysis-report-012.json | disparities-analysis-report-012 | Health-equity narrative report (advocacy/policy audience; non-stigmatizing) | writing | medium | document | open |
| tasks/disparities-analysis-reproduce-013.json | disparities-analysis-reproduce-013 | Reproducibility package + scripts/reproduce.ts re-derivation harness (CI gate) | code | low | pr | open |
| tasks/disparities-analysis-explainer-014.json | disparities-analysis-explainer-014 | Plain-language public explainer (education-only; "not medical advice") | writing | high | document | open |
| tasks/disparities-analysis-resources-015.json | disparities-analysis-resources-015 | Verified resource/helpline information pack (dated, authoritative-sourced) | data | high | document | open |
| tasks/disparities-analysis-partner-016.json | disparities-analysis-partner-016 | Secure delivery partner/steward + independent methods/framing audit of shipped outputs | research | medium | document | open |
| tasks/disparities-analysis-handoff-017.json | disparities-analysis-handoff-017 | Partner uses an analysis to inform a program/report/grant/decision; outcome recorded (the deed) | maintenance | medium | document | open |
| tasks/disparities-analysis-refresh-018.json | disparities-analysis-refresh-018 | Annual data-refresh + re-standardization runbook + maintenance rotation + second-site process | maintenance | medium | document | open |
| tasks/disparities-analysis-site2-019.json | disparities-analysis-site2-019 | Second cancer-site analysis pack | data | medium | dataset | open |
| tasks/disparities-analysis-intl-020.json | disparities-analysis-intl-020 | International GLOBOCAN/CI5 comparison (WHO World Standard) | data | medium | dataset | open |
| tasks/disparities-analysis-ses-021.json | disparities-analysis-ses-021 | Area-deprivation deep-dive (SVI vs. ADI vs. tract poverty) | research | medium | document | open |
| tasks/disparities-analysis-notebook-022.json | disparities-analysis-notebook-022 | Reproducible explanatory notebook / methods walkthrough | writing | low | document | open |
| tasks/disparities-analysis-i18n-023.json | disparities-analysis-i18n-023 | Translate the public explainer (HIGH) into priority languages | writing | high | translation | open |
| tasks/disparities-analysis-dashboard-024.json | disparities-analysis-dashboard-024 | Static, no-PII aggregate visualization of the data cube | code | medium | pr | open |

**Totals:** 24 task files (1 seed preserved + 23 generated). Validation: ALL VALID (node validate-tasks.mjs tasks/).

---

## Example task JSON

Complete, schema-valid Task JSON for the first M0 task (`disparities-analysis-framing-001`):

```json
{
  "id": "disparities-analysis-framing-001",
  "title": "Non-stigmatizing health-equity editorial & framing policy spec",
  "project": "disparities-analysis",
  "type": "design-spec",
  "lane": "donated",
  "priority": "high",
  "domain": ["health", "cancer", "health-equity", "epidemiology", "editorial"],
  "riskTier": "medium",
  "urgent": false,
  "deliverable": "document",
  "tokenEstimate": "medium",
  "status": "open",
  "context": "Disparities-Analysis produces open, reproducible analyses of cancer outcome disparities (incidence, stage at diagnosis, mortality, survival, screening uptake) using ONLY aggregate, open-access, de-identified public data (SEER*Explorer, USCS, CDC WONDER, GLOBOCAN). A disparity analysis done carelessly can do real harm: it can biologize race, imply a community is to blame, launder ecological correlations into causal claims, or stigmatize. So the non-stigmatizing health-equity editorial/framing policy is a hard product requirement built FIRST, alongside the statistical-methods+provenance+suppression standard. This cold-start task writes that policy; every later analysis is mounted behind it. No partner organization or framing reviewer is yet secured.",
  "objective": "Write the authoritative non-stigmatizing health-equity editorial and framing policy that all later analyses and write-ups must follow and be reviewed against, anchored to named external standards (CDC Health Equity Guiding Principles for Inclusive Communication, CDC Health Equity Style Guide, AMA/AAMC Advancing Health Equity language guide): evidence-tiered structural framing (separating 'this analysis measures the gap' from 'the literature attributes such gaps to structural factors X/Y, cite'), a bounded intersectionality posture (report what the data supports; disclose what suppression forces out), treatment of race/ethnicity as a social/administrative construct with documented misclassification (no genetic-ancestry-as-race proxy; SES as exposure not behavior; name the mechanism), asset-based and community-centered language, the reference-group policy, the mandatory caveats (data vintage, suppression, confidence intervals, ecological-fallacy/'association is not causation', adjusted-for/not-adjusted-for), the no-ranking/no-scorecard rule, and the no-medical-advice + 'consult your care team' rule for any patient-facing surface.",
  "acceptanceCriteria": [
    "Cites the CDC Health Equity Guiding Principles for Inclusive Communication, the CDC Health Equity Style Guide, and the AMA/AAMC Advancing Health Equity language guide as the policy's normative base and records any project deltas",
    "Mandates that disparities are described as outcomes of modifiable structural/social conditions (access, insurance, exposure, structural racism, poverty), never as inherent group attributes, and forbids causal claims beyond what the data design supports",
    "Requires evidence-tiered structural framing: every claim separates 'this analysis measures the gap' from 'the established literature attributes such gaps to structural factors X/Y (cite)', so structural framing does not itself over-claim causation from ecological data",
    "Adopts a bounded intersectionality posture: report the intersectional cuts the data supports at acceptable suppression AND explicitly disclose where suppression forces omission, instead of silently dropping thin intersectional cells",
    "Treats race/ethnicity as social/administrative constructs, requires documenting known misclassification (especially AIAN, NHPI, and Hispanic-origin coding) and bridged-population caveats, forbids biologizing race, prohibits interpreting genetic-ancestry/admixture as a proxy for socially-assigned race, requires SES to be framed as exposure/environment not individual behavior, and instructs naming the mechanism where known",
    "Requires asset-based, person-first, community-centered language and a reference-group policy: no group is silently coded as 'normal'; disparities are reported to an explicitly stated reference AND as an across-group index of disparity",
    "Requires both absolute (rate difference) and relative (rate ratio) measures to accompany every disparity statement (never relative-only)",
    "Mandates standard caveats on every output: data vintage, small-cell suppression, confidence intervals, and an 'association is not causation'/ecological-fallacy warning",
    "Establishes the no-ranking/no-scorecard rule (no 'worst places', no naming-and-shaming of communities, providers, or institutions)",
    "Requires the persistent 'general education, not medical advice - consult your care team' labeling and the blocking oncologist + patient-advocate sign-off gate for any patient-/public-facing content",
    "Reviewed and signed off by a health-equity/community framing reviewer (recorded in the reviewers ledger), preferring a representative of an affected community"
  ],
  "resources": [
    "planning/projects/disparities-analysis/PLAN.md",
    "CLAUDE.md",
    "docs/good-deed-definition.md",
    "packages/schema/src/schemas.ts",
    "planning/ROADMAP.md"
  ],
  "output": "A reviewed policy-specification document (the non-stigmatizing health-equity editorial/framing charter) defining structural-causation framing, race/ethnicity-as-construct + misclassification handling, language rules, the reference-group policy, mandatory caveats, the no-ranking/no-scorecard rule, and the no-medical-advice + expert-sign-off gates - the contract that disparities-analysis-brief-011, disparities-analysis-report-012, and disparities-analysis-explainer-014 are reviewed against.",
  "requestor": "TO BE SECURED",
  "verifiedNeed": false,
  "outputLicense": "CC-BY-4.0"
}
```
