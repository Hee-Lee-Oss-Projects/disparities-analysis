# Disparities-Analysis — PLAN.md

> Status: Draft · Version: 0.2.0 · Last updated: 2026-06-29 · Owner: TBD (maintainer) · Lane: donated

Open, reproducible analyses of **cancer outcome disparities** — differences in incidence, stage at
diagnosis, mortality, survival, and screening uptake across population groups — built **only** from
aggregate, open-access, de-identified public data, with careful, non-stigmatizing, health-equity
framing and provenance on every assertion. The output is a public good for health-equity
researchers, patient-advocacy organizations, community health workers, public-health departments,
and journalists — not medical advice, and not a tool that names, ranks, or stigmatizes any community.

---

## Executive summary

Cancer does not fall evenly. People in some racial and ethnic groups, some geographies, and some
socioeconomic conditions are diagnosed later, treated less, and die more — overwhelmingly because of
**modifiable structural and social conditions** (access to screening and care, insurance, exposure,
the downstream effects of structural racism and poverty), **not** because of anything inherent to a
group. Authoritative aggregate data describing these gaps exists and is open (NCI's SEER program and
SEER\*Explorer, the CDC/NCI U.S. Cancer Statistics, CDC WONDER mortality, IARC's Global Cancer
Observatory/GLOBOCAN), but it is scattered across portals, demands real epidemiological care to use
correctly (age-standardization, confidence intervals, small-cell suppression, trend modeling,
ecological-inference limits), and is easy to present in ways that **stigmatize** rather than
illuminate. Disparities-Analysis produces correct, reproducible, fully-sourced disparity analyses
and frames them as evidence of conditions to fix, handing communities and the people who serve them
something they can act on.

The single most important design fact is the **framing**. A disparity analysis done carelessly can
do harm — it can biologize race, imply a community is "to blame," launder ecological correlations
into causal claims, or re-identify a small group from a thin cell. So the **non-stigmatizing
health-equity editorial policy and the statistical-methods/provenance standard are the first build
items and hard product requirements** — reviewed and enforced, not a disclaimer, and **anchored to
named external standards** (CDC's Health Equity Guiding Principles for Inclusive Communication, the
CDC Health Equity Style Guide, and the AMA/AAMC Advancing Health Equity language guide) so the policy
conforms to a vetted base rather than being re-invented. Every analysis is mounted behind them:
aggregate-only data, verified source licenses, mandatory provenance per assertion, small-cell
suppression honored, both **absolute and relative** disparity reported, a deliberate reference-group
policy (never defaulting one group to "normal"), and an explicit ecological-fallacy/"association is
not causation" guardrail.

Two framing nuances sharpen this further and are first-class requirements in v0.2. First, structural
framing must be **evidence-tiered**: mandating that every gap be described as the result of
"modifiable structural/social conditions" is the correct *default* frame, but applied mechanically it
can itself **over-claim causation from ecological data** — the mirror image of biological
essentialism. A purely ecological SEER cut measures the gap; it does not, by itself, demonstrate that
*structural racism* caused that specific gap (that attribution rests on the broader literature). So
the policy separates **"this analysis measures the gap"** from **"the established literature
attributes such gaps to structural factors X/Y (cite)"** — non-stigmatizing *and* epistemically
honest. Second, the analysis must take a **bounded intersectionality posture**: because the
most policy-relevant disparities are often intersectional (e.g., rural + low-income + Black; AIAN
women) yet those are exactly the thin cells suppression removes, the project **reports the
intersectional cuts the data supports at acceptable suppression and explicitly discloses where
suppression forces omission** — silent omission would erase the most-affected groups, which is both a
completeness gap and an equity failure.

This is a **MEDIUM** risk-tier project on its core analytical surface (it needs domain accuracy:
epidemiology/biostatistics review + health-equity/community framing review), with a **HIGH** risk
tier on any **patient- or public-facing** content. Per `docs/good-deed-definition.md`, anything that
a patient could read as guidance about their own care (plain-language explainers, prevention or
screening information, helpline/resource packs) is treated as health/safety content: it is
**education only**, carries a persistent **"not medical advice — consult your care team"** label,
and **must not ship without blocking sign-off from a credentialed oncologist and a patient
advocate**; any crisis/helpline information must be independently verified against authoritative,
current sources and dated. Low-risk tooling/infra is `low`.

Honesty note: **no partner organization, advocacy group, or requestor is yet secured.** Every
delivery-dependent task is marked `TO BE SECURED` with `verifiedNeed: false` until a real
beneficiary (a health-equity research group, an NCI-designated cancer center's Community Outreach &
Engagement program, a patient-advocacy coalition, or a public-health department) agrees to use the
work. The project is **not "shipped" on merge**; it is shipped only when a real organization uses an
analysis to inform a program, report, grant, or community decision, with the methods and framing
independently verified.

**Partner-acquisition plan (dated) and build-vs-pivot decision rule.** Outreach is time-boxed
against the build, not left open-ended: by **2026-08-31** the exemplar cancer site and ≥ 3 candidate
partner organizations are selected and in active conversation, and a credentialed
epidemiology/biostatistics reviewer and a health-equity/community reviewer are secured (the MEDIUM
gate for analytical content); by **2026-10-31** an oncologist + patient-advocate reviewer pair is
secured **if** any HIGH-tier patient-facing content (M4) is to be attempted; by **2026-12-31** a
delivery partner/steward is secured (M5 gate). **Decision rule:** if no credentialed methods +
framing reviewer is secured by the M2 entry date, M2 analysis does not ship and the project holds at
M1 (pipeline + standards). If no oncologist + advocate pair is secured, **M4 patient-facing content
is not attempted at all** — the project ships only its researcher/advocate-facing analyses
(perfectly valuable on their own). If no delivery partner is secured by **~2027-03-31**, the project
does not "ship to no one": it either **pivots** the last-mile beneficiary (publish the
reproducibility package + exemplar analysis as a reference deed and offer it to a public-health
training program) or **mothballs** to maintenance-only — recorded in governance.

---

## Problem & beneficiaries

**Who is helped (directly):**

- **Health-equity researchers** who need correct, reproducible, fully-sourced aggregate disparity
  baselines without rebuilding the data pipeline and methods from scratch.
- **Patient-advocacy organizations and community coalitions** (especially those serving
  disproportionately affected communities) who need credible, plain numbers and careful framing to
  make the case for screening programs, navigation services, and funding.
- **Community health workers and navigators** who need accurate local/regional context (not advice
  to give patients, but situational awareness for their programs).
- **Public-health departments and NCI-designated cancer centers' Community Outreach & Engagement
  (COE) programs**, which are mandated to assess and address the cancer burden in their catchment
  areas and can use reproducible aggregate analyses directly.
- **Health/science journalists**, who frequently misreport disparities and need a sourced,
  non-stigmatizing reference.

**Who is helped (ultimately):** the **communities experiencing cancer disparities** — through
better-targeted screening, navigation, prevention, and policy driven by correct, non-stigmatizing
evidence. The benefit is mediated (we inform the people who run programs), which is exactly why a
secured delivery partner is the definition of shipped.

**The need.** Disparity statistics are simultaneously **available and hard to use well**. SEER and
USCS expose age-adjusted incidence/mortality and relative survival by race/ethnicity, sex, stage,
age, and (for some measures) county and area-based socioeconomic position; GLOBOCAN gives
international comparison; CDC WONDER gives mortality. But: rates must be **age-standardized** to
compare populations; small counts must be **suppressed** to protect privacy and flagged as
unstable; trends need **joinpoint** modeling, not eyeballing; comparisons need **both absolute and
relative** measures; race/ethnicity categories carry known **misclassification** (notably for
American Indian/Alaska Native, Native Hawaiian/Pacific Islander, and Hispanic-origin coding); and
aggregate data invites the **ecological fallacy**. Done badly, the result misleads or stigmatizes.
A reproducible, reviewed, openly-licensed pipeline that does it correctly is a genuine public good.

**Verified need / partner:** **TO BE SECURED.** No specific advocacy organization, cancer-center COE
program, public-health department, or research group has yet agreed to use or co-develop the work.
Target partner profiles to pursue: an NCI-designated cancer center COE office; a community cancer
coalition or condition-specific advocacy organization; a state/county public-health epidemiology
unit; an academic health-equity research group. Until one is secured, the project builds the
framing/methods standards, the provenance pipeline, and **one exemplar-site analysis** for review,
and marks all delivery/adoption work `TO BE SECURED` (`verifiedNeed: false`). Outreach is **dated**
(see the partner-acquisition plan above), and a **build-vs-pivot decision rule** governs slippage
rather than shipping to no real beneficiary.

---

## Competitive landscape & differentiation

This is a **crowded, authoritative field** — the incumbents are federal agencies and the American
Cancer Society — and the honest competitive truth is that **the data and even the disparity math
already exist and are excellent**. The whitespace is **not new numbers**; it is **reproducibility +
provenance-per-assertion + an independently-reviewed non-stigmatizing narrative + last-mile fit for a
specific community partner**. The market splits three ways:

- **Federal data / exploration tools** — rich data, weak reasoning/narrative/provenance-package:
  - **NCI SEER\*Explorer** — interactive aggregate incidence/mortality/survival by site, race, sex,
    age, stage (age-standardized, CIs, APC trends), but a data-exploration UI, not a reasoned,
    reviewed analysis; no SES/area dimension; not a reproducible package.
  - **NCI State Cancer Profiles** — national/state/county maps explicitly built to "expose health
    disparities"; county granularity, but maps/numbers only, no structural narrative, no
    per-assertion provenance, not partner-tailored.
  - **NCI HD\*Calc** — software computing **11 summary disparity measures** (Index of Disparity, SII,
    RII, with CIs); the *de facto* standard for disparity indices — we should **use** it, not compete
    with it; it is a calculator, not an analysis/narrative/last-mile layer.
  - **NCI SEER aggregate statistics** and **CDC U.S. Cancer Statistics Data Viz Tool** (NPCR+SEER
    ~100% coverage, careful race/ethnicity technical notes) — exploration tools, no reproducible
    artifact, subject to federal data-availability disruption (note the *restoredcdc.org* mirrors).
  - **NIMHD HDPulse** — the **closest competitor**: a Data Portal (national/state/county disparity
    stats incl. cancer) **plus an Interventions Portal** (evidence-based interventions — the
    actionability layer most others lack). Still a portal, not a per-site reviewed analysis with
    provenance-per-assertion; framing is generic; not partner-co-developed.
- **Authoritative narrative reports** — strong framing, *not reproducible or local*:
  - **ACS Cancer Facts & Figures for [specific populations]** + **Status of Cancer Disparities in the
    U.S., 2025** — gold-standard narrative that explicitly traces disparities to structural
    racism / social determinants, peer-reviewed (CA: Cancer J Clin); but national (not
    local/partner-specific), PDF reports rather than reproducible pipelines, annual cadence, not
    co-developed with a specific community.
  - **AACR Cancer Disparities Progress Report** — strong biennial science+policy framing, but
    narrative, not a reproducible local analysis or tool.
- **Ranking models / adjacent** — instructive as the pattern we **refuse**:
  - **County Health Rankings & Roadmaps** (RWJF + UW) — county ranking model; exactly the
    naming/scorecard stigma pattern our plan rejects, and cancer is one indicator among many.
  - **Our World in Data — Cancer** — excellent reproducibility ethos but international/country-level
    GBD modeled estimates, not U.S. within-country race/SES registry disparities.

**No incumbent delivers the combination** of a reproducible, provenance-per-assertion, independently
**methods-reviewed AND framing-reviewed**, openly-licensed, partner-co-developed analysis for a
specific community. That gap is the project's reason to exist.

**Differentiators to win.**

1. **"Reviewed reproducibility" as the product.** The unit is not a chart; it is a sealed package —
   pinned inputs + documented queries + provenance-per-assertion + methods sign-off + framing
   sign-off + a reproduction test. Nobody else ships this combination.
2. **Framing as a tested, independently-reviewed RELEASE GATE, not a disclaimer** — anchored to the
   **CDC/AMA equity style guides**, community-reviewed ("nothing about us without us"), with a **hard
   no-ranking / no-scorecard rule**. This directly counters the field's chief failure mode (correct
   numbers used to stigmatize) and is the opposite of County Health Rankings' ranking model — the
   single strongest differentiator.
3. **Built *with* and *for* a specific beneficiary** (COE / coalition / health department), shipped
   only on *adoption* — versus publish-and-walk-away national reports.
4. **Methodological maximalism using the field's own validated tools** (NCI Joinpoint, HD\*Calc-grade
   disparity indices, `lifelines`/`statsmodels`) rather than bespoke reimplementation — credibility
   by *using* the tools reviewers already trust, and validating our outputs against HD\*Calc on the
   exemplar site.
5. **Radical limitation-honesty** — misclassification direction-of-bias, intersectional-suppression
   disclosure, and "adjusted-for / not-adjusted-for" notes — building the trust that wins adoption
   among careful equity researchers.
6. **Resilience to federal data disruption** — an openly-licensed, checksum-pinned, reproducible
   package is a durable public good when federal portals go dark or change (the *restoredcdc.org*
   signal).

**Where we deliberately do NOT compete:** we do not re-derive the national numbers (we consume the
authoritative sources), we do not build another exploration dashboard, and we do not rank or
scorecard anyone.

---

## Goals and non-goals

**Goals**

- Produce **correct, reproducible, fully-sourced** analyses of cancer outcome disparities from
  aggregate, open-access, de-identified public data.
- Establish and enforce a **non-stigmatizing, health-equity editorial policy** and a rigorous
  **statistical-methods + provenance standard** as the foundation every analysis sits behind.
- Deliver, for at least one exemplar cancer site, a reviewed disparity analysis (age-standardized
  rates + CIs, trends, and **both absolute and relative** disparity measures across race/ethnicity,
  sex, geography, and area-based socioeconomic position) plus a reproducibility package.
- Frame every finding as evidence of **modifiable structural/social conditions**, with explicit
  limitations (ecological inference, misclassification, suppression, data vintage).
- Hand the work to a **real beneficiary** who uses it to inform a program, report, grant, or
  community decision — the definition of shipped.
- (Conditionally, and only if an oncologist + advocate reviewer pair is secured) publish a
  plain-language, **education-only** public explainer with verified resource information.

**Non-goals**

- **Not medical advice**, screening recommendations, prognosis, or anything a patient should act on
  about their own care. Patient-facing material is education only and expert-reviewed.
- **No individual-level or identifiable data.** Controlled-access datasets (dbGaP, EGA, individual
  biobanks) and case-level/record-level data requiring a Data Use Agreement — **including SEER
  Research Plus case-level extracts** — are **out of scope**; only aggregate, open, de-identified
  statistics are used.
- **No causal claims** that the data design cannot support; no biologizing of race; no implication
  that any community is "at fault" for its cancer burden.
- **Not** a ranking, scorecard, or "naming and shaming" of communities, providers, or institutions.
- **Not** a clinical decision tool, a patient registry, or a place that stores any personal data.
- **Not** a for-profit product; outputs are open (code MIT, data/content CC-BY-4.0 where source
  licenses permit — see *Data, licensing & compliance* for the GLOBOCAN/non-commercial caveat).

---

## Success metrics (outcomes)

Outcome-centric and beneficiary-first. Vanity metrics (page views, downloads alone) are explicitly
**not** success.

| Metric | Baseline | Target | How measured |
|---|---|---|---|
| Provenance coverage (assertions backed by a cited source) | none | **100%** of quantitative assertions carry a machine-checkable `Source` (dataset, release/version, query, retrieval date, license) | Citation-coverage CI check ("no assertion without source") + reviewer audit |
| Source-license verification before any data ships | none | **100%** of sources have recorded, verified reuse terms; 0 datasets published whose source license forbids it | License register review (blocking gate) |
| Small-cell suppression / re-identification safety | none | **0** published cells violating the source's suppression threshold; **0** re-identification findings in adversarial check | Suppression test against NCHS/SEER rules + re-identification review (blocking) |
| Reproducibility | none | **100%** of published figures/tables re-created bit-for-bit (or within documented tolerance) by an independent re-run from pinned inputs | Independent reproduction run in CI / by a second analyst |
| Statistical-methods review pass | n/a | **100%** of analytical outputs signed off by an epidemiology/biostatistics reviewer (age-standardization, CIs, trend method, disparity measures correct) | Methods-review checklist + governance log |
| Non-stigmatizing framing review pass | n/a | **100%** of outputs pass health-equity/community framing review (language, reference-group policy, causal caveats, no deficit framing) | Framing-review checklist + advocate sign-off |
| Expert sign-off on HIGH (patient-facing) content | n/a | **100%** of patient-facing content has recorded **oncologist + patient-advocate** sign-off before ship | Governance log (blocking gate) |
| Helpline/resource accuracy | n/a | **100%** of helpline/resource items verified against an authoritative current source with a recorded `lastVerified` date; **0** stale/incorrect entries at publish | Verification log + staleness check |
| Both absolute and relative disparity reported | n/a | **100%** of disparity statements report **both** a rate difference and a rate ratio (never relative-only) to avoid distortion | Output-format lint + reviewer check |
| **Adoption (the deed)** | 0 | **≥ 1** partner organization uses an analysis to inform a program/report/grant/community decision, recorded with the partner's confirmation | Steward's attested outcome log |
| Beneficiary-reported usefulness | 0 | **≥ 3** advocates/CHWs/COE staff report the analysis was usable and correctly framed | Structured feedback from partner |

The **defining success outcome** (Definition of Shipped): a real organization serving an affected
community adopts an analysis and uses it to inform a concrete program, report, grant, or decision —
with methods and non-stigmatizing framing independently verified, every assertion sourced, and (for
any patient-facing piece) oncologist + advocate sign-off recorded.

---

## Scope

**In scope**

- A **non-stigmatizing health-equity editorial policy** and a **statistical-methods + provenance +
  suppression standard**, enforced as gates on every output.
- A **reproducible data-acquisition + provenance pipeline** drawing from aggregate, open sources:
  **SEER\*Explorer / SEER aggregate statistics**, **U.S. Cancer Statistics (USCS, CDC+NCI)**, **CDC
  WONDER** (mortality / USCS), **IARC Global Cancer Observatory / GLOBOCAN** (international), and
  aggregate context layers (**Census/ACS** denominators and area-based socioeconomic measures, CDC/
  ATSDR **Social Vulnerability Index**, **BRFSS** screening prevalence) — each with verified license.
- For **one exemplar cancer site** (selected in M0 against explicit criteria — e.g., a site with
  large, well-documented, screening-actionable disparities such as colorectal or cervical cancer):
  age-standardized incidence/mortality rates with CIs, relative survival where available, stage at
  diagnosis, screening uptake context, **trend (joinpoint) analysis**, and **absolute + relative
  disparity** measures across race/ethnicity, sex, geography, and area-based socioeconomic position.
- A **technical disparity brief** (researcher/advocate audience, MEDIUM) and a **health-equity
  narrative report** (advocacy/policy audience, MEDIUM), each with explicit limitations.
- A **reproducibility package** (pinned inputs, documented queries, environment, re-runnable
  analysis) and an **annual data-refresh runbook**.
- *(Conditional, gated on secured oncologist + advocate)* a **plain-language public explainer**
  (HIGH, education-only) and a **verified resource/helpline pack** (HIGH).

**Out of scope (explicitly will NOT do)**

- **Any individual-level, record-level, or identifiable patient data**; any controlled-access
  dataset (dbGaP, EGA, biobanks) or DUA-gated case-level extract (**including SEER Research Plus
  case data**) — even when de-identified. Aggregate published statistics only.
- **Medical advice**, screening/prevention recommendations to individuals, prognosis, or treatment
  guidance.
- **Causal claims** beyond what the (largely ecological, observational) data supports; any
  biologizing of race/ethnicity; any framing that attributes a community's burden to the community.
- **Ranking/scorecarding** communities, providers, hospitals, or institutions; "worst places"
  listicles; or any output whose primary effect is stigma rather than action.
- Storing personal data of any kind; building a registry; clinical decision support.
- Publishing a derivative dataset whose **source license forbids redistribution** (see the GLOBOCAN/
  non-commercial caveat); when a source is non-commercial or no-derivatives, we publish the
  **method and a pointer**, not the restricted data.
- Sub-national geographies thin enough to risk re-identification or violate suppression rules.

When a contemplated analysis would require restricted data, would risk re-identification, or could
only be framed in a stigmatizing way, the project **does not produce it** and records why.

---

## Solution approach & architecture

This is primarily a **data + analysis + writing** project (deliverables: `dataset`, `document`),
with supporting tooling. Reproducibility, provenance, and review are the architecture.

**Stack and a deliberate convention note.** Hee-Lee Oss's default is TypeScript/ESM/pnpm, and all **glue,
validation, provenance-schema, CI, and lint tooling is TypeScript/ESM** accordingly. However, the
**statistical analysis itself uses the standard, citable open-source epidemiology toolchain**
(Python: `pandas`, `numpy`, `lifelines`/`statsmodels`; and/or R: `epitools`, plus NCI's
**Joinpoint Regression Program** for trend analysis), because these are the validated, peer-reviewed
tools epidemiologists actually use and review — using a bespoke TS reimplementation of
age-standardization or joinpoint would be *less* trustworthy, not more. This deviation from the
TS-only default is intentional and recorded here for the maintainer's sign-off; the agent-neutral
Hee-Lee Oss rules about no vendor lock-in and no secrets in logs still apply.

**Components / pipeline**

1. **Framing & methods gate (the "guardrail" of this project) — built first.** Two enforced
   standards, not documentation:
   - *Non-stigmatizing health-equity editorial policy* — **anchored by reference to named external
     standards** (CDC Health Equity Guiding Principles for Inclusive Communication, the CDC Health
     Equity Style Guide, and the AMA/AAMC Advancing Health Equity language guide), with any project
     deltas recorded — required language and framing rules: disparities described as outcomes of
     modifiable structural/social conditions; race/ethnicity treated as **social/administrative
     constructs** with documented misclassification, never as biology; an explicit prohibition on
     **interpreting genetic-ancestry/admixture as a proxy for socially-assigned race**, with
     area-based SES described as *exposure/environment*, not *individual behavior*, and a positive
     instruction to **name the mechanism** where known (insurance, screening access, environmental
     exposure) rather than leaving a bare race coefficient to be misread as intrinsic; **asset-based,
     person-first, community-centered language**; a **reference-group policy** that never silently
     codes one group as "normal" and that reports disparity **to a stated reference and** as an
     across-group index; mandatory caveats (data vintage, suppression, CIs, **"association is not
     causation"/ecological-fallacy** warning) on every output; and the "no medical advice" rule for
     any patient-facing surface.
     - **Evidence-tiered structural framing (key correctness rule).** Structural framing is the
       default frame but must not be applied mechanically: every claim is tiered to separate
       **"this analysis measures the gap"** (what the dataset supports) from **"the established
       literature attributes such gaps to structural factors X/Y (cite)"** (what the broader
       literature supports). This keeps the framing non-stigmatizing *without* over-claiming
       causation from ecological data — the mirror of the biological-essentialism error. The exact
       tier boundary (how strongly a structural frame may be stated from purely ecological data) is
       jointly calibrated by the framing **and** methods reviewers (see *Open questions*).
     - **Bounded intersectionality posture.** The analysis reports the intersectional cuts the data
       supports at acceptable suppression (e.g., rural + low-income + race; AIAN women) **and
       explicitly discloses where suppression forces omission**, rather than silently dropping thin
       intersectional cells — because silent omission erases the most-affected groups. The
       principled rule for "report vs. disclose-as-suppressed" is a methods+framing decision (see
       *Open questions*).
   - *Statistical-methods + provenance + suppression standard* — required methods:
     **age-standardization** (2000 U.S. standard population for U.S. data; WHO World Standard for
     international), **confidence intervals** (e.g., Tiwari-modified for SEER rates),
     relative-standard-error/stability flagging, **joinpoint** trend modeling with APC/AAPC,
     **both absolute (rate difference) and relative (rate ratio)** disparity plus an index of
     disparity, and **small-cell suppression** per the source's rule with a **re-identification
     safety check**. The standard names **exact, mechanically-checkable thresholds** rather than a
     vague "per source" rule: e.g., NCHS-style suppress rates with **numerator < 10** (and small
     denominators per source), flag rates with **RSE > 30% as unreliable** and **suppress at
     RSE > 50%**, apply **complementary suppression**, and set a **joinpoint minimum-points** rule;
     SEER/USCS thresholds are honored where more conservative. Each disparity statement also adopts
     **HD\*Calc's measure set** (Index of Disparity, SII/RII, with CIs), validated against HD\*Calc
     on the exemplar site, and carries a one-line **"adjusted for / not adjusted for"** note (e.g.,
     age-standardized controls age but *not* stage, comorbidity, or access) to block
     over-interpretation of an age-adjusted-only gap as "pure." Race/ethnicity handling records a
     per-group **direction-of-bias** note (which groups are under-counted and why — CDC/USCS note
     incidence/mortality are underestimated for AIAN, API, and Hispanic people; linkage such as IHS
     for AIAN is recommended) and **pre-decides OMB 1997-vs-2024 standard handling** (the 2024
     revision merges race/ethnicity into one question and adds MENA, which will fracture trend
     comparability) so pre/post trends are bridged, not silently mis-compared.

2. **Provenance layer (`provenance/`).** A machine-checkable `Source` record per dataset and per
   assertion: source name, dataset + **release/version year**, exact **query/parameters**,
   **retrieval date**, URL, **license / reuse terms**, suppression rules applied, and the standard
   population used. A CI check enforces **"no quantitative assertion without a `Source`."**

3. **Acquisition module (`acquire/`).** Documented, re-runnable acquisition of aggregate statistics
   from SEER\*Explorer/USCS/CDC WONDER/GCO (saved queries + parameters + raw pulls archived with
   checksums), plus context layers (ACS denominators, SVI, BRFSS). No scraping that violates a
   source's terms; honor rate limits and reuse conditions.

4. **Analysis module (`analysis/`).** Age-standardized rates + CIs, relative survival, stage
   distribution, trends (joinpoint), and disparity computation (absolute + relative + index of
   disparity) by race/ethnicity, sex, geography, and area-based socioeconomic position — all
   parameterized so a second cancer site is configuration, not a rewrite.

5. **Reporting (`reports/`).** The technical brief and the health-equity narrative report, generated
   from analysis outputs with citations and limitations auto-attached; figures regenerated from
   source so they cannot drift from the data. Each finding may carry an optional, education-only
   **"what works" pointer** that maps it to evidence-based interventions via **NIMHD HDPulse's
   Interventions Portal** and **The Community Guide** — increasing actionability and closing the gap
   to HDPulse **without** the project itself making any clinical recommendation (the line to the HIGH
   patient-facing gate is an *Open question*).

6. **Reproducibility harness (`scripts/reproduce.ts`).** Re-runs the pipeline from pinned inputs and
   asserts published figures/tables are reproduced (bit-for-bit or within a documented tolerance);
   wired into CI. Raw source pulls are **mirrored/pinned with checksums and archived** so the package
   survives federal-portal disruption (the *restoredcdc.org* signal) and remains reproducible years
   later.

**Claude API leverage (architecture-level — "Claude writes the words; code owns the numbers").** The
clean mental model governing every use of Claude here: **Claude writes and checks the words; code
computes the numbers; credentialed humans and the affected community decide what is true, safe, and
shippable.** Within that line, Claude is used to:

- **Draft non-stigmatizing structural explainers *from* code-computed statistics.** Given the
  analysis module's structured outputs (rates, CIs, rate difference, rate ratio, index of disparity,
  flags), Claude drafts the technical brief and the plain-language narrative in evidence-tiered,
  person-first, structural framing — *transforming verified numbers into prose, never inventing
  numbers* (strong fit for the explainer engine and a future MCP server, see *Adjacent
  opportunities*).
- **Run an automated structural-framing / stigma linter as an advisory pre-gate.** Claude reviews any
  draft against the editorial policy + CDC/AMA equity style guides and flags deficit framing,
  biologizing language, silent reference-group coding, relative-only statements, missing caveats,
  un-tiered causal claims, or absent "not medical advice" labels — wired into CI as an **advisory
  pre-gate ahead of human framing review**; it surfaces issues, it does not approve.
- **Draft plain-language / reading-level / translation** copy for community audiences, **auto-attach
  caveats and limitations** (including the "adjusted-for / not-adjusted-for" and direction-of-bias
  notes for human verification), and **triage provenance/citation-coverage** (flagging assertions
  that lack a `Source` before CI does, and suggesting the matching `DisparityMeasure`), reducing
  reviewer burden by pre-filling the methods/framing checklists.

**The hard "Claude must NOT decide" line (enforced in the editorial/methods standard):** the
**numbers come from code, not the model** (Claude never estimates, rounds, infers, or fills in a
rate, CI, or count); **no causal claims and no biological-race claims** originate from Claude (it may
restate the established literature only *with citations a human verifies*); **framing and
patient-facing safety are decided by credentialed humans + the affected community** (the
health-equity/community sign-off and epi/biostat sign-off are the deciders, and for patient-facing
content the **oncologist + advocate veto is absolute** — Claude's linter cannot clear it); and Claude
**never** decides a source's reuse terms, suppression, re-identification safety, or the accuracy of
any helpline/resource fact (all human-verified and dated).

**Data model (records)**

- **`Source`** — `{ name, dataset, releaseYear, query, retrievalDate, url, license, suppressionRule,
  standardPopulation, lastVerified, validUntil }`.
- **`DisparityMeasure`** — `{ cancerSite, measure(incidence|mortality|survival|stageAtDx|screening),
  dimension(raceEthnicity|sex|geography|areaSES|age), group, referenceGroup, rate, ciLow, ciHigh,
  standardPopulation, count|"suppressed", rateDifference, rateRatio, indexOfDisparity, stabilityFlag,
  sourceId }`.
- **`Assertion`** — every textual claim links to ≥ 1 `sourceId` and (if quantitative) a
  `DisparityMeasure`; unsourced quantitative assertions fail CI.

**Key decisions**

- Framing + methods + provenance + suppression are first-class, tested gates and release blockers —
  not prose.
- **Aggregate-only**, conservatively interpreted (case-level DUA data excluded) — privacy by
  construction: there is no individual data to leak because none is ever ingested.
- Depth-first on **one exemplar site** with full review before any breadth.
- **Both absolute and relative** disparity always reported (relative-only ratios distort when base
  rates are low).
- Validated, citable epi tooling over bespoke reimplementation.

---

## Data, licensing & compliance

**THIS SECTION LEADS WITH THE CANCER GUARDRAILS AND IS BINDING.**

**Aggregate / open / de-identified only.** The project uses **only aggregate, open-access,
de-identified published statistics**. Controlled-access and identifiable patient data are **out of
scope**: dbGaP, EGA, individual-level biobanks, and any record-level/case-level data requiring a
Data Use Agreement — **including SEER Research Plus case-level extracts** — are **not** used, even
when de-identified. Where a question can only be answered with restricted data, the project documents
the limitation rather than seeking access. Because no individual data is ever ingested, the dominant
privacy risk is **re-identification from thin aggregate cells**, which is controlled by suppression
(below).

**Sources and their licenses (each verified and recorded before use).**

| Source | What | Reuse terms (to verify per release) |
|---|---|---|
| **NCI SEER / SEER\*Explorer** (aggregate statistics) | Age-adjusted incidence/mortality, relative survival, stage, by race/ethnicity, sex, age, some geography | U.S. Government work; SEER\*Explorer **aggregate** statistics are public domain / freely usable with attribution. *(Case-level SEER Research data is DUA-gated → out of scope.)* |
| **U.S. Cancer Statistics (USCS)** — CDC + NCI (NPCR+SEER) | National/state aggregate incidence + mortality | U.S. Government work; public-use; **must honor suppression and no-re-identification terms** |
| **CDC WONDER** (mortality, USCS online) | Aggregate mortality/underlying-cause | Public; **data-use restriction: no attempt to re-identify; cells < 10 suppressed** |
| **IARC Global Cancer Observatory / GLOBOCAN** | International incidence/mortality estimates | **IARC terms — verify carefully:** generally free for non-commercial use **with attribution**; redistribution of derived data may be limited. **Potential CC-BY conflict (see below).** |
| **U.S. Census / ACS** | Population denominators; area-based socioeconomic measures | U.S. Government work; public domain |
| **CDC/ATSDR Social Vulnerability Index (SVI)** | Area-level social vulnerability context | U.S. Government work; public |
| **BRFSS** | Screening prevalence / risk-factor context | Public; honor suppression of small estimates |
| **WHO Mortality Database / IARC CI5** *(optional, intl.)* | International comparison | Verify WHO/IARC terms per dataset |

**Provenance model (mandatory).** Every quantitative assertion is backed by a `Source` record
(source, dataset, **release year**, exact query/parameters, **retrieval date**, URL, license,
suppression rule, standard population). A CI **citation-coverage** check enforces *no assertion
without a source*. Figures are regenerated from source so they cannot silently drift.

**Small-cell suppression & re-identification (blocking).** The project honors the **most
conservative applicable suppression rule** per source (e.g., NCHS/CDC WONDER suppress counts < 10;
SEER/USCS thresholds and complementary-suppression rules applied so a suppressed cell can't be
back-calculated from margins). Rates based on small numerators are flagged **unstable** (relative
standard error). An adversarial **re-identification review** checks that no published combination of
dimensions isolates a small, potentially identifiable group; sub-national geographies are coarsened
until safe. **No output ships that violates a suppression threshold or fails the re-identification
check.**

**Output licensing (with a real caveat).** Code: **MIT**. Derived data/content: **CC-BY-4.0** —
**but only where the source license permits redistribution under CC-BY.** SEER\*Explorer/USCS/WONDER/
Census/SVI derivatives (U.S. Government works) are fine under CC-BY-4.0 with attribution. **GLOBOCAN/
IARC and some WHO datasets may be non-commercial or restrict redistribution of derived data**, which
**conflicts with CC-BY-4.0** (CC-BY permits commercial reuse). Resolution: for any source whose terms
forbid CC-BY redistribution, the project publishes the **analysis method, the exact query, and a
pointer to the source** rather than the restricted derived data, or applies the source-mandated
attribution/NC terms to that specific artifact — recorded per artifact in the license register. This
is an open governance item (see *Open questions*).

**No medical advice / health-safety stance.** No output advises an individual about their care. Any
patient/public-facing surface (HIGH) carries a persistent **"This is general education, not medical
advice — consult your care team"** label and ships only with oncologist + advocate sign-off; any
helpline/crisis/resource information is **independently verified against an authoritative current
source and dated** (`lastVerified`), with a staleness check before publication.

**No secrets / no PII in artifacts** (Hee-Lee Oss rule). No API keys, tokens, or any personal data in
logs, receipts, notebooks, or committed files — trivially satisfied here because no personal data is
ingested, but enforced in CI regardless.

---

## Quality, review & risk gates

**Risk tier: MEDIUM** on the core analytical surface (per `docs/good-deed-definition.md`, work
requiring domain accuracy needs a reviewer with the relevant skill — here epidemiology/biostatistics
**and** health-equity/community framing). **HIGH** on any **patient- or public-facing** content
(health/safety domain): it **requires credentialed expert sign-off before merge**. Pure
tooling/infra is **LOW**.

**Required reviews before a deed is "done":**

- **Maintainer** review on all PRs (engineering quality, agent-neutral tooling, reproducibility,
  no secrets, CI green).
- **Epidemiology/biostatistics review** (MEDIUM+) — recorded sign-off that age-standardization, CIs,
  trend method, suppression, stability flags, and **absolute + relative** disparity measures are
  correct. No methods sign-off, no ship.
- **Health-equity / community framing review** (MEDIUM+) — recorded sign-off (patient advocate
  and/or community representative) that language is non-stigmatizing, the reference-group policy is
  honored, causal/ecological caveats are present, and no deficit/biologizing framing remains.
- **Oncologist + patient-advocate sign-off** (HIGH, **blocking, before merge**) — required for any
  patient-/public-facing content; verifies clinical accuracy, the "not medical advice" framing, and
  the safety/appropriateness of any resource/helpline information.
- **License verification** (blocking) — every source's reuse terms verified and recorded before its
  data is used or republished.
- **Suppression / re-identification check** (blocking) — automated suppression test + adversarial
  re-identification review.
- **Provenance/citation-coverage** (blocking) — CI fails if any quantitative assertion lacks a
  `Source`.
- **Reproducibility** (blocking) — independent re-run reproduces published figures/tables.

**Definition of Shipped (project):** a real organization serving an affected community adopts an
analysis and uses it to inform a concrete program, report, grant, or decision; methods + framing
independently verified; every assertion sourced and licenses cleared; suppression/re-identification
safe; and (for any patient-facing piece) oncologist + advocate sign-off recorded.

---

## Roadmap & milestones

Phased: standards + pipeline first; analysis only behind the standards; patient-facing content only
behind oncologist+advocate review and only if that pair is secured; delivery last and gated on a
secured partner.

- **M0 — Foundations, framing & methods standards (cold-start).**
  *Goal:* the framing/methods/provenance/suppression gates and a reproducible skeleton exist before
  any analysis; the exemplar cancer site is selected against explicit criteria.
  *Exit:* non-stigmatizing editorial policy **and** statistical-methods+provenance+suppression
  standard written and reviewer-approved; the editorial policy **cites the CDC/AMA equity style
  guides as its normative base and records deltas**, mandates **evidence-tiered structural framing**
  ("measures the gap" vs. "literature attributes such gaps to X, cite") and the **bounded
  intersectionality posture** (report what the data supports; disclose what suppression forces out);
  the methods standard names **exact suppression/stability thresholds** (numerator < 10; RSE > 30%
  unreliable / > 50% suppress; complementary suppression; joinpoint min-points), the **HD\*Calc
  measure set**, the **"adjusted-for / not-adjusted-for"** requirement, and the
  **direction-of-bias + OMB 1997-vs-2024** handling; source **license register** drafted with each
  candidate source's terms verified; repo skeleton + provenance schema + CI (citation-coverage,
  suppression, license-presence lint, **advisory stigma-linter pre-gate**) green; exemplar site
  selected with rationale.

- **M1 — Acquisition & provenance pipeline.**
  *Goal:* reproducible, provenance-complete acquisition of aggregate data for the exemplar site.
  *Exit:* acquisition module pulls SEER\*Explorer/USCS/WONDER (+ ACS/SVI context) with saved queries,
  retrieval dates, checksums, and **archived, checksum-pinned raw extracts** (durable against
  federal-portal disruption), and recorded licenses; provenance "no-assertion-without-source" check
  passing; a canonical **disparities data cube** for the exemplar site built, suppressed, and
  license-cleared. **Kill-gate:** if the open aggregate data cannot support a defensible disparity
  analysis for the chosen site at acceptable suppression, switch sites or narrow scope **before**
  investing in M2.

- **M2 — Core disparity analysis (exemplar site, MEDIUM).**
  *Goal:* the reviewed quantitative analysis.
  *Exit:* age-standardized rates + CIs, relative survival/stage where available, joinpoint trends,
  and **absolute + relative** disparity (+ index of disparity, **validated against HD\*Calc**) across
  race/ethnicity, sex, geography, area-SES — plus the **bounded intersectional cuts the data
  supports** (with suppressed cuts explicitly disclosed), each statement carrying its
  **"adjusted-for / not-adjusted-for"** and **direction-of-bias** notes and **evidence-tiered**
  structural framing — **methods-reviewed and framing-reviewed**, every figure sourced, suppression
  honored, reproducible. A **technical disparity brief** is produced.

- **M3 — Health-equity narrative report + reproducibility package (MEDIUM).**
  *Goal:* an advocacy/policy-audience report and a re-runnable package.
  *Exit:* narrative report (non-stigmatizing, limitations explicit, framing-reviewed, with optional
  education-only **"what works" intervention pointers** via HDPulse Interventions Portal / The
  Community Guide) published; reproducibility package re-runs and reproduces all figures in CI / by a
  second analyst.

- **M4 — Patient/public-facing explainer (HIGH — conditional, gated).**
  *Goal:* an education-only public explainer **only if** an oncologist + advocate pair is secured.
  *Exit:* plain-language explainer with persistent "not medical advice" framing and a
  **verified, dated** resource/helpline pack — **oncologist + patient-advocate sign-off recorded
  (blocking)**. If the pair is not secured, this milestone is **skipped** and the project ships
  M2–M3 outputs.

- **M5 — Partner delivery & handoff (the deed).**
  *Goal:* a real organization adopts and uses the work.
  *Exit (Definition of Shipped):* a secured partner uses an analysis to inform a program/report/
  grant/decision; methods + framing independently verified; outcome recorded with the partner's
  confirmation. *(Gated on a secured partner — TO BE SECURED.)*

- **M6 — Sustain & scale (post-delivery).**
  *Goal:* durable maintenance and careful expansion to additional sites.
  *Exit:* annual data-refresh + re-standardization runbook; maintenance rotation; a documented,
  reviewer-gated process for adding a second cancer site.

Dependencies flow M0 → M1 → M2 → M3 → (M4 optional) → M5; the **exemplar-site decision is made in M0
and gates M1–M6**; M2 analysis blocks on M0 standards + secured methods/framing reviewers; M4 blocks
on a secured oncologist + advocate pair; M5 blocks on a secured delivery partner.

---

## Work breakdown

The itemized, schema-mapped backlog lives in **`TASKS.md`**: ~18 tasks across milestones M0–M6 plus
a future backlog, each mapped to the Hee-Lee Oss Task JSON schema, with per-task acceptance criteria for
the most important items, milestone Definitions of Done, and a complete example Task JSON for the
first M0 task (the non-stigmatizing framing & editorial policy). The first build items are the
**framing/editorial policy** and the **statistical-methods + provenance + suppression standard**,
reflecting their status as hard product requirements; the **exemplar-site selection** (M0) and a
**data-feasibility kill-gate** (M1) are sequenced so analytical investment is gated on a viable
corpus, and HIGH-tier patient-facing work (M4) is sequenced last and conditional on a secured
oncologist + advocate pair.

---

## Governance, roles & stakeholders

- **Maintainer (Owner): TBD.** Owns the pipeline, reproducibility, provenance schema, CI, and merge
  quality; signs off the intentional Python/R-for-stats convention deviation.
- **Reviewers / rotation:**
  - **Epidemiology/biostatistics reviewer (MEDIUM+): TO BE SECURED** — verifies statistical
    correctness; sign-off recorded per output and **version-scoped** (re-sign-off required on
    material edits or data refresh).
  - **Health-equity / community framing reviewer (MEDIUM+): TO BE SECURED** — a patient advocate
    and/or community representative; verifies non-stigmatizing framing and the reference-group
    policy. Where possible, a representative **of an affected community** reviews framing
    ("nothing about us without us").
  - **Oncologist + patient-advocate pair (HIGH, blocking): TO BE SECURED** — required only for
    patient-facing content; clinical accuracy + "not medical advice" + resource safety.
  - **Guardrail/methods independence:** framing and methods reviewers are independent of the analyst
    who produced the output. Reviewers **recuse** from outputs touching an organization/community
    they have a material conflict with; sign-off is recorded with credentials and consent in a
    reviewers ledger, and a reviewer's name may be used only for the specific versions they
    approved (no implied endorsement of the whole project).
  - **Disagreement fallback:** on a HIGH-tier item, the oncologist/advocate hold a **veto on whether
    patient-facing content is safe to ship**; a maintainer cannot override a "do not ship" on
    substance. Unresolved disputes escalate to Hee-Lee Oss governance / a second credentialed reviewer.
- **Steward (last-mile owner): TO BE SECURED** — owns the partner relationship and the adoption that
  constitutes shipping; records the outcome.
- **Partner / requestor: TO BE SECURED** — the advocacy org, cancer-center COE program, public-health
  department, or research group that adopts the work.
- **Community / board:** the CC-BY-vs-source-NC license conflict, exemplar-site choice, and any
  edge-cases go through Hee-Lee Oss governance.

---

## Dependencies & integrations

- **External data sources:** SEER\*Explorer / SEER aggregate, USCS, CDC WONDER, IARC GCO/GLOBOCAN,
  Census/ACS, CDC/ATSDR SVI, BRFSS (and optionally WHO Mortality DB / IARC CI5) — each with verified
  reuse terms and recorded provenance.
- **Tooling:** NCI **Joinpoint Regression Program** (trend analysis); Python (`pandas`, `numpy`,
  `statsmodels`, `lifelines`) and/or R (`epitools`) for rates/CIs/survival; TypeScript/ESM for glue,
  provenance schema, CI, and lint.
- **Reference standards:** 2000 U.S. standard population (U.S. age-standardization); WHO World
  Standard (international); NCHS/SEER suppression rules; HD\*Calc disparity-measure set; **CDC Health
  Equity Guiding Principles for Inclusive Communication + CDC Health Equity Style Guide + AMA/AAMC
  Advancing Health Equity language guide** (editorial-policy normative base); OMB 1997 & 2024
  race/ethnicity standards.
- **Hee-Lee Oss pieces:** `packages/schema` (Task JSON), `CLAUDE.md` (work rules + cancer guardrails),
  `docs/good-deed-definition.md` (risk tiers), Hee-Lee Oss governance (license + edge-case decisions).
- **Human/decision dependencies (critical path):** the **exemplar-site decision (M0, gates M1–M6)**;
  a secured **epi/biostat reviewer + framing reviewer** (block M2); a secured **oncologist +
  advocate pair** (block M4); a secured **delivery partner/steward** (block M5).

---

## Risks & mitigations

| Risk | Likelihood | Impact | Mitigation | Owner |
|---|---|---|---|---|
| Analysis stigmatizes a community / biologizes race / implies fault | Medium | Critical | Non-stigmatizing editorial policy built first + framing review (advocate/community) as a blocking gate; mandatory structural-causation framing; reference-group policy; no ranking/scorecard outputs | Framing reviewer |
| Re-identification from a thin aggregate cell | Medium | Critical | Honor most-conservative suppression rule (NCHS/SEER); complementary suppression; adversarial re-identification review; coarsen sub-national geographies; aggregate-only by construction | Maintainer / Methods reviewer |
| Ecological fallacy / causal overclaim from aggregate data | High | High | Methods standard mandates "association not causation" + ecological-inference caveats on every output; methods review; no individual inference from group rates | Methods reviewer |
| **Structural framing applied mechanically over-claims causation** (the mirror of biological essentialism — asserting a structural-cause from a purely ecological cut) | Medium | High | **Evidence-tiered framing** ("measures the gap" vs. "literature attributes such gaps to X, cite"); framing+methods jointly calibrate the tier boundary; "adjusted-for / not-adjusted-for" note on every statement | Framing + Methods reviewers |
| **Silent omission of intersectional cells erases the most-affected groups** (suppression drops thin intersectional cuts) | Medium | High | **Bounded intersectionality posture**: report what the data supports at acceptable suppression, **explicitly disclose** what suppression forces out rather than dropping it silently; principled report-vs-disclose rule set in M0 | Framing + Methods reviewers |
| Uses out-of-scope restricted data (e.g., SEER case-level/DUA) | Low | Critical | Aggregate-only rule in scope + license register; SEER Research Plus explicitly excluded; license gate blocks any DUA-gated source | Maintainer |
| Patient reads output as medical advice | Medium | High | Patient-facing content is HIGH, education-only, "not medical advice — consult your care team," oncologist + advocate sign-off (blocking); M4 skipped if no expert pair | Oncologist/Advocate |
| Statistical error (no age-standardization, relative-only ratios, unstable rates) | Medium | High | Methods standard (age-standardization, CIs, stability flags, **absolute + relative** always); validated epi tooling (Joinpoint, lifelines); biostat review; reproducibility check | Methods reviewer |
| Source license forbids redistribution (esp. GLOBOCAN/IARC NC) | Medium | Medium | Per-source license register; CC-BY only where permitted; for NC/ND sources publish method + pointer, not restricted data; governance decision recorded | Maintainer |
| Stale data or out-of-date helpline/resource info | Medium | High | `lastVerified`/`validUntil` on sources + resources; staleness check; annual refresh runbook; helpline info re-verified before publish | Maintainer / Oncologist |
| No delivery partner secured → cannot reach Definition of Shipped | High | High | Honest `TO BE SECURED`/`verifiedNeed:false`; dated partner-acquisition plan; build-vs-pivot decision rule (~2027-03-31); reference deed remains valuable | Steward / Maintainer |
| No epi/framing reviewers secured → analysis blocked | Medium | High | Recruit via cancer-center COE programs, schools of public health, advocacy networks; do not ship MEDIUM content without sign-off (hard gate); hold at M1 | Maintainer |
| Misclassification of race/ethnicity distorts findings (esp. AIAN/NHPI/Hispanic) | High | Medium | Methods + framing standard require documenting known misclassification + bridged/linked-data caveats + a per-group **direction-of-bias** note (which groups are under-counted and why); pre-decided **OMB 1997-vs-2024** trend-bridging; report uncertainty; avoid over-precise small-group claims | Methods reviewer |

---

## Security & privacy

**Threat surface.** Unlike most software, the dominant risk here is **not** a system breach (no
personal data is ever ingested) but **(1) re-identification** of a small group from thin aggregate
cells, **(2) misuse of correct numbers for stigmatizing/discriminatory ends**, and **(3) integrity**
of the analysis (a subtle statistical or provenance error that misleads).

**Privacy / re-identification controls.** Aggregate-only by construction — there is no individual
record to expose. Suppression honored to the most conservative applicable threshold with
complementary suppression so suppressed cells can't be reconstructed from margins; adversarial
re-identification review before any sub-national or multi-dimensional cut ships; geographies coarsened
until safe. No personal data, secrets, or tokens in logs, notebooks, receipts, or committed files
(enforced in CI regardless).

**Misuse prevention.** The framing gate and the no-ranking/no-scorecard scope rule are the primary
controls against the "correct data, harmful use" failure mode: outputs are framed as **conditions to
fix**, not communities to blame; no "worst places" outputs; non-stigmatizing language enforced by
review. Outputs carry their limitations so they are harder to weaponize out of context.

**Integrity controls.** Provenance per assertion (no unsourced claim), figures regenerated from
source (no drift), validated epi tooling, independent methods review, and a reproducibility harness
that re-derives published results. Source `lastVerified`/`validUntil` drives a staleness fail-safe so
out-of-date numbers or helpline info are flagged or withheld rather than served as current.

**Patient-safety controls (HIGH content).** Education-only framing, "not medical advice" labeling,
oncologist + advocate blocking sign-off, and independent verification + dating of any helpline/crisis
information.

---

## Sustainability & maintenance

After delivery, a named **maintenance rotation** owns the pipeline and the **steward** owns the
partner relationship and outcome tracking. Public-health data is released on annual cycles
(SEER/USCS/GLOBOCAN), so an **annual data-refresh + re-standardization runbook** governs updates:
re-pull with new release years, re-run the reproducible pipeline, re-verify source licenses and
suppression, **re-run methods + framing review** for material changes, and re-verify any
helpline/resource info. Source `lastVerified`/`validUntil` makes staleness a visible, gated event
(auto-flag or withhold) rather than a silent error. Outcomes are tracked with the partner (programs
informed, reports/grants using the analysis, advocate-reported usefulness) — **not** download counts.
Expansion to additional cancer sites follows a documented, reviewer-gated process and reuses the
parameterized analysis module. Patient-facing content, if any, is on a re-review cadence tied to
clinical-guidance changes and re-requires oncologist + advocate sign-off.

---

## Adjacent opportunities

The reusable IP here is not the cancer data — it is the **reviewed-framing pipeline** (validated
stats in → Claude-drafted structural narrative → stigma-linter → human + community review →
provenance-bound output). Several adjacent deeds reuse that machine:

- **Parallel (same domain, shared engine).** The same parameterized acquisition / provenance /
  age-standardization core powers the roadmap sibling **`incidence-explorers`** (disparities-analysis
  becomes the reviewed-narrative layer on top) and a **`screening-coverage-trends`** project
  (BRFSS/USCS screening-uptake disparities for colorectal/cervical/breast — directly actionable, same
  pipeline, natural COE-partner overlap). Additional cancer sites remain *configuration, not a
  rewrite* (M6), each cheaper to review.
- **Perpendicular (different domain, same machine).** The combination above generalizes to a
  **general equity-framing-reviewed explainer engine** usable for *any* disparities domain — maternal
  health, diabetes, environmental justice, housing, education — and the **non-stigmatizing structural-
  framing / stigma linter** can stand alone as a library/service for journalists and advocacy orgs
  (the field's chief failure mode is bad framing of correct numbers).
- **MCP server.** Expose the provenance store + computed `DisparityMeasure` records + the editorial
  policy as a **read-only MCP server**, so any reviewer's (or partner's) agent can query "give me the
  sourced, suppression-safe, framing-compliant statement for colorectal mortality rate-ratio in
  [group] vs reference, with caveats" — numbers-from-code, citations attached. This operationalizes
  "Claude writes the words, code owns the numbers" as a clean reusable surface across all the
  spin-offs.

These are **opportunities, not commitments**: none is attempted before the exemplar deed ships, and
each would carry the same guardrails (aggregate-only, provenance, suppression, evidence-tiered
framing, community + methods review).

---

## Open questions

- **GLOBOCAN/IARC and other non-commercial source terms vs. CC-BY-4.0.** CC-BY permits commercial
  reuse, which some IARC/WHO terms forbid for derived data. Resolution path proposed (publish method
  + pointer, or apply source-mandated NC/attribution to that artifact), but the final license posture
  per source needs a Hee-Lee Oss governance decision and per-release verification.
- **Causation-framing calibration (evidence tiers).** How strongly may a structural frame be stated
  from purely ecological data before it itself becomes an over-claim? The "measures the gap" vs.
  "literature attributes such gaps to X (cite)" tier boundary needs the framing **and** methods
  reviewers to jointly define — the single most important framing-correctness decision.
- **Intersectionality vs. suppression rule.** What is the principled rule for which intersectional
  cuts to *report* vs. *disclose-as-suppressed*, so omission doesn't silently erase the most-affected
  groups while still honoring suppression? A methods+framing decision tied to the bounded
  intersectionality posture.
- **OMB 1997 vs. 2024 race/ethnicity standard adoption.** When do the new categories (combined
  race/ethnicity question, added MENA) enter, and how are pre/post trends bridged without misleading
  comparisons? Belongs in the methods standard now because it fractures trend comparability.
- **Actionability scope vs. the advice line.** Does adding a "what works" intervention pointer (via
  HDPulse Interventions Portal / The Community Guide) risk drifting toward advice, and where exactly
  is that line drawn relative to the HIGH patient-facing gate?
- **Which exemplar cancer site first? — decided in M0, not deferred,** because it gates M1–M6.
  Selection criteria, scored before M1: (1) large, well-documented disparities in **open aggregate**
  data at acceptable suppression; (2) the disparity is **actionable** (e.g., screening- or
  access-driven, like colorectal or cervical cancer) so the analysis can inform a real program;
  (3) availability of methods + framing reviewers with relevant expertise; (4) a candidate partner
  whose catchment/mission matches the site.
- **Will a HIGH-tier patient-facing explainer (M4) be attempted at all?** Only if an oncologist +
  advocate pair is secured; otherwise the project ships researcher/advocate-facing analyses only.
- **Race/ethnicity category and misclassification handling** — which standard categories, how to
  document AIAN/NHPI/Hispanic-origin misclassification and bridged-vs-unbridged population
  denominators, and how to report small-group uncertainty without over-precision.
- **Area-based socioeconomic measure** — SVI vs. Area Deprivation Index vs. census-tract poverty/
  income; which is most defensible and least stigmatizing for the chosen site.
- **Lane** — donated by default; is there a future funded lane (with a hard budget cap) for expert
  review hours without compromising reviewer independence?
- **Reviewer sourcing, compensation/credit, and single-point-of-failure.** The entire MEDIUM surface
  is blocked until two volunteer experts are secured by a date — a real single point of failure.
  Volunteer vs. funded; how to credit community reviewers fairly; and whether to secure a **named
  institutional partner** (an NCI-designated cancer-center COE office, a school of public health, or
  an NCI/NIMHD network such as CRCHD PACHE / Community Networks) **instead of two individuals** to
  de-risk reviewer acquisition.

---

## References

- Proposal: `governance/proposals/disparities-analysis.md` *(TO BE CREATED — not yet written)*
- Hee-Lee Oss work rules & cancer guardrails: `CLAUDE.md` (Track 8 domain guardrails)
- Good-deed definition & risk tiers: `docs/good-deed-definition.md`
- Task JSON schema: `packages/schema/src/schemas.ts`
- Portfolio context: `planning/ROADMAP.md` (Track 8b — `disparities-analysis`, `incidence-explorers`)
- Sibling Hee-Lee Oss plans for house style: `planning/projects/public-official-guide/{PLAN,TASKS}.md`,
  `planning/projects/open-data-datasheets/{PLAN,TASKS}.md`
- Data sources: NCI SEER & SEER\*Explorer; NCI State Cancer Profiles; U.S. Cancer Statistics
  (CDC+NCI) + USCS Data Viz Tool; CDC WONDER; IARC Global Cancer Observatory / GLOBOCAN; U.S.
  Census/ACS; CDC/ATSDR Social Vulnerability Index; BRFSS
- Disparity / intervention references: NCI **HD\*Calc** (Index of Disparity, SII/RII); **NIMHD
  HDPulse** Data + Interventions portals; **The Community Guide**; ACS Cancer Facts & Figures for
  specific populations + Status of Cancer Disparities in the U.S. 2025; AACR Cancer Disparities
  Progress Report
- Methods references: NCI Joinpoint Regression Program; 2000 U.S. standard population (age-
  standardization); NCHS/SEER small-cell suppression rules; OMB 1997 & 2024 race/ethnicity standards
- Editorial / framing standards: CDC Health Equity Guiding Principles for Inclusive Communication;
  CDC Health Equity Style Guide; AMA/AAMC Advancing Health Equity language guide

---

## Appendix A — Improvements applied

The following 25 specific improvements were identified during drafting and **have been applied**
to the plan above (and to `TASKS.md`). Each is concrete and verifiable against the documents.

1. **Aggregate-only made conservative and explicit.** Scope and *Data* sections explicitly exclude
   **SEER Research Plus case-level (DUA-gated) data**, not just dbGaP/EGA — closing the most likely
   "but it's de-identified" loophole an analyst might rationalize.
2. **Re-identification (not breach) named as the dominant privacy risk.** *Security & privacy*
   reframes the threat model around thin-cell re-identification and adds **complementary suppression**
   so suppressed cells can't be reconstructed from margins.
3. **Both absolute and relative disparity always required.** Added as a methods rule, a success
   metric, and an output-format lint — preventing the classic distortion where a large rate *ratio*
   on a tiny base rate is reported alone.
4. **Ecological-fallacy guardrail.** "Association is not causation" + ecological-inference caveats are
   mandated on every output and made a methods-review checklist item and a top risk.
5. **Reference-group policy.** Codified a rule that no group is silently coded as "normal";
   disparities are reported to a stated reference **and** as an across-group index of disparity.
6. **Race/ethnicity as social construct + misclassification.** Framing + methods standards require
   treating race/ethnicity as social/administrative categories and documenting AIAN/NHPI/Hispanic
   misclassification and bridged-population caveats; added as a dedicated risk.
7. **Tiered risk model (MEDIUM core / HIGH patient-facing / LOW infra).** Made explicit everywhere,
   matching the good-deed-definition tiers, instead of a single blanket tier.
8. **HIGH patient-facing content gated by a *blocking* oncologist + advocate sign-off** before merge,
   with M4 **skipped entirely** if the reviewer pair isn't secured — so the project still ships.
9. **GLOBOCAN/IARC license vs. CC-BY-4.0 conflict surfaced and resolved per-artifact.** *Data* and
   *Open questions* address that CC-BY (commercial-OK) can conflict with IARC NC terms; resolution is
   publish-method-and-pointer for restricted sources.
10. **Helpline/resource verification + dating.** Any crisis/helpline/resource info must be verified
    against an authoritative current source and carry `lastVerified`, with a staleness check
    (cancer-guardrail requirement) — added as a metric and a HIGH task.
11. **Provenance as a CI gate, not prose.** "No quantitative assertion without a `Source`" is an
    automated citation-coverage check; figures are regenerated from source to prevent drift.
12. **Suppression as a blocking automated test** against the most-conservative applicable rule
    (NCHS < 10, SEER/USCS thresholds), plus stability/RSE flags for small numerators.
13. **Intentional toolchain-convention deviation documented.** *Solution approach* records that stats
    use validated Python/R + NCI Joinpoint (not bespoke TS) and requires maintainer sign-off — honest
    about departing from the TS-only default and *why* it's the safer choice.
14. **Exemplar-site selection moved into M0 with explicit, scored criteria** (open-data feasibility,
    actionability, reviewer availability, partner fit) and made a dependency that gates M1–M6.
15. **M1 data-feasibility kill-gate.** If open aggregate data can't support a defensible analysis at
    acceptable suppression for the chosen site, switch/narrow *before* M2 investment.
16. **Dated partner-acquisition plan + build-vs-pivot decision rule** (mirrors the house pattern):
    concrete dates and an explicit pivot/mothball rule at ~2027-03-31 instead of an open `TBD`.
17. **Definition of Shipped is adoption, not merge.** Success metrics and M5 require a real
    organization to *use* an analysis for a program/report/grant/decision, recorded by the steward.
18. **Outcome-based metrics; vanity metrics explicitly rejected** (no "downloads = success");
    beneficiary-reported usefulness and documented programmatic use are the targets.
19. **Reviewer independence, recusal, version-scoped sign-off, and name-use limits** specified in
    *Governance*, with a HIGH-tier reviewer **veto** and an escalation fallback.
20. **"Nothing about us without us."** Framing review prefers a representative *of an affected
    community*, not just any advocate — embedding community voice in the review gate.
21. **No-ranking / no-scorecard scope rule** added to *Scope* and *Security* as the primary control
    against the "correct numbers, harmful use" misuse mode.
22. **Reproducibility harness as a blocking gate** (`scripts/reproduce.ts`) that re-derives published
    figures from pinned inputs — making reproducibility testable, not aspirational.
23. **Parameterized analysis module** so a second cancer site is configuration, not a rewrite —
    de-risking M6 expansion and lowering per-site review burden.
24. **Annual data-refresh + re-standardization runbook** tied to `lastVerified`/`validUntil`
    staleness fail-safe, since SEER/USCS/GLOBOCAN release annually.
25. **Schema-faithful TASKS.md** with a complete, validated example Task JSON (`verifiedNeed: false`,
    real `outputLicense`), risk tiers mapped per task, and `fundedBudgetUsd` documented as required
    only for any `funded` task (none planned at cold-start).

---

## Review sign-off

**Reviewer:** senior staff engineer + TPM (drafting author self-review pass).
**Date:** 2026-06-28. **Scope of review:** completeness against the 17-section PLAN_SPEC, correctness
against `CLAUDE.md` + `docs/good-deed-definition.md` cancer guardrails, schema-faithfulness of
`TASKS.md`, and internal consistency between the two documents.

**Completeness:** all 17 required H2 sections present and in order; *Data, licensing & compliance*
and *Quality, review & risk gates* lead with the cancer guardrails as required; HIGH-tier
patient-facing content is gated behind blocking expert (oncologist + advocate) review; `TASKS.md`
provides schema-mapped tasks, per-task acceptance criteria, milestone Definitions of Done, a backlog,
and a schema-valid example Task JSON. **Pass.**

**Correctness (guardrails):** aggregate/open/de-identified-only is stated and enforced, with
case-level DUA data (incl. SEER Research Plus) explicitly excluded; per-source license verification
is a blocking gate; provenance-per-assertion is a CI gate; suppression + re-identification are
blocking; no-medical-advice + "consult your care team" + oncologist/advocate review applies to all
patient-facing content; helpline info must be verified + dated. **Pass.**

**Corrections applied during review:**
- Reconciled the example Task JSON `outputLicense` (`CC-BY-4.0`) with the *Data* section's
  source-license caveat by scoping CC-BY to permitted (U.S. Government) sources and noting the
  GLOBOCAN exception in both files, so the two documents do not contradict.
- Ensured every milestone in `PLAN.md`'s roadmap has a matching `## Milestone` section in `TASKS.md`
  (M0–M6) and that task `Depends on` references resolve to real task IDs.
- Verified the example Task JSON includes all schema `required` fields and only schema-defined
  properties (no `fundedBudgetUsd` on the donated example), and that `verifiedNeed` is `false`
  consistent with no secured partner.
- Added the explicit note that **M4 is skipped** (not merely deferred) if no oncologist + advocate
  pair is secured, so "no expert → no patient-facing content" is unambiguous.

**Outstanding (needs a human decision):** (1) the CC-BY-vs-IARC/GLOBOCAN non-commercial license
posture; (2) the exemplar cancer-site choice; (3) whether the HIGH-tier patient-facing explainer is
attempted at all. These are flagged in *Open questions* and do not block M0–M1. **Sign-off: APPROVED
as a Draft v0.1.0 for partner outreach and M0 execution.**

---

## Changelog — v0.2 (analysis merged)

v0.2 merges the findings of `COMPETITIVE-ANALYSIS.md` (dated 2026-06-29) into the plan. The analysis
confirmed the v0.1 framing/methods/suppression guardrails as **best-in-class** and untouched here;
the changes below are **surgical and additive** and **strengthen, never weaken**, those guardrails.

**Concrete correctness fixes applied (from the analysis):**

- **Evidence-tiered structural framing (the key correctness fix).** Structural framing applied
  mechanically can itself **over-claim causation from ecological data** — the mirror of biological
  essentialism. The editorial policy now requires every claim to separate **"this analysis measures
  the gap"** from **"the literature attributes such gaps to structural factors X/Y (cite)."** Added
  to the Executive summary, the framing-gate component, M0/M2 exits, an *Open question*, and a new
  *Risks* row.
- **Anchored the editorial policy to named external standards** — CDC Health Equity Guiding
  Principles for Inclusive Communication, the CDC Health Equity Style Guide, and the AMA/AAMC
  Advancing Health Equity language guide (record deltas), so the policy conforms to a vetted base
  rather than being re-invented.
- **Bounded intersectionality posture.** The plan previously analyzed dimensions one at a time and
  treated multi-dimensional cuts mainly as a suppression risk; silent omission of thin intersectional
  cells erases the most-affected groups. Now: **report the intersectional cuts the data supports and
  explicitly disclose what suppression forces out.** Added to Executive summary, framing-gate
  component, M2 exit, an *Open question*, and a *Risks* row.
- **Sharpened anti-essentialism, thresholds, and limitation-honesty:** prohibition on
  genetic-ancestry-as-race-proxy and SES-as-environment-not-behavior + name-the-mechanism;
  **mechanically-checkable suppression/stability thresholds** (numerator < 10; RSE > 30% / > 50%;
  complementary suppression; joinpoint min-points); the **HD\*Calc** measure set validated against
  HD\*Calc; an **"adjusted-for / not-adjusted-for"** note per statement; per-group
  **direction-of-bias** and **OMB 1997-vs-2024** trend-bridging.

**Strategy integrated:**

- New **"Competitive landscape & differentiation"** section (SEER\*Explorer, State Cancer Profiles,
  USCS Data Viz, **NIMHD HDPulse** as closest competitor, **ACS Cancer Facts & Figures / Status of
  Cancer Disparities**, HD\*Calc, County Health Rankings as the refused ranking model). Differentiator
  = framing as a **tested, independently-reviewed release gate** (CDC/AMA-anchored, community-reviewed
  "nothing about us without us", hard no-ranking/no-scorecard rule) plus **reviewed reproducibility**.
- **Claude API leverage folded into the architecture** under "Claude writes the words; code owns the
  numbers": draft structural explainers from code-computed stats, an advisory **stigma-linter
  pre-gate**, plain-language/translation + auto-attached limitations — with the hard line that numbers
  come from code, causal/biological-race claims are forbidden, and framing + patient-facing safety are
  decided by credentialed humans + the affected community.
- **Optimizations folded into the Roadmap** (M0–M3 exits) and an optional education-only **"what
  works" intervention pointer** (HDPulse Interventions Portal / The Community Guide) plus
  **checksum-pinned raw archives** for federal-portal-disruption resilience.
- New **"Adjacent opportunities"** section (shared engine with `incidence-explorers` /
  `screening-coverage-trends`; a general equity-framing-reviewed explainer engine + standalone stigma
  linter; a read-only **MCP server**) — opportunities, not commitments, each under the same
  guardrails.
- **Open questions merged** (causation-framing tier calibration; intersectionality-vs-suppression
  rule; OMB 2024 adoption; actionability-vs-advice line; reviewer single-point-of-failure /
  institutional-partner option), and References/Dependencies updated with the new standards and
  sources.

**Preserved unchanged:** all 17 PLAN_SPEC sections and order; aggregate-public-data-only;
case-level/DUA exclusion (incl. SEER Research Plus); per-source license verification; provenance per
assertion; statistical rigor; non-stigmatizing framing + community/health-equity-expert review gates;
no-medical-advice + oncologist/advocate blocking sign-off; the honest `TO BE SECURED` /
`verifiedNeed:false` posture and the build-vs-pivot rule. No invented facts; no guardrail weakened.
