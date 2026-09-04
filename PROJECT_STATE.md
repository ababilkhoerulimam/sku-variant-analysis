# Project State: SKU Variant Spin-Off Analysis

**Schema version:** 1.1
**Last updated:** 2026-09-04
**Status:** Completed
**Current phase:** Notebook documentation
**Project type:** RANKING
**Decision owner:** Hiring reviewer / brand operator (exact operational owner unknown)
**Primary notebook:** `stock-keeping-unit.documented-v2.ipynb`
**Last completed cell:** Cell 21
**Data snapshot:** `Dummy Brand _ PERFORMA PRODUK - JUNI sd AGUSTUS 2026.xlsx`, SHA-256 `EAC0DCD3274975CF97616741E5635144BEA9DC7A8BC15356DFE2500F24AB5623`
**Code version:** Git HEAD `4ae77a3579dc058b8b6edc666d02a9ed768061b4`; notebook SHA-256 `0C471F08F1DAD41BC041D1E8753DED32D5907D78A0E2E32ED9CBD4D7C247222D`

## Objective and Success Criteria

**Problem or decision:** Select at least three active variants under the dominant parent SKU `HMUG` that can be separated into standalone SKUs, with numerical justification that remains defensible despite duplicated aggregate figures.

**Unit of analysis:** One SKU variant observed through aggregate monthly sales and units for June, July, and August 2026.

**Outcome or target:** A descriptive, rule-based ranking and three recommended variants. There is no predictive target.

**Primary success metric:** Recommended variants must be active, have fully attributable sales under the conservative rule, sell in all three months, rank strongly on revenue, units, median monthly revenue, and weakest-month revenue, and remain defensible under sensitivity analysis.

**Constraints:** Three months of aggregate data only; no transaction IDs, profit, cost, stock, promotion, rating, or marketing-spend data; ambiguous repeated variant values cannot be assigned to a specific variant without an operational source.

## Data Inventory

| Source | Metadata / Grain | Time Coverage | Sensitivity | Exploration Status |
|---|---|---|---|---|
| `Dummy Brand _ PERFORMA PRODUK - JUNI sd AGUSTUS 2026.xlsx` | 5 sheets; store totals, 2,830 parent SKU rows, and 110 variant rows across three detailed parent SKUs | Jun–Aug 2026 | Internal / unknown | Loaded in Cell 2; audited in Cells 3–4 |
| `stock-keeping-unit.documented-v2.ipynb` | 21 documented Python code cells; descriptive ranking, robustness, and decision-visualization pipeline | Jun–Aug 2026 snapshot; August through day 28 | Internal / unknown | Validated sequentially through Cell 21; 21 Markdown annotations added by `document-notebook` |

## Progress

| Stage | Status | Evidence / Cell | Notes |
|---|---|---|---|
| Planning | Completed | Cells 1–2 | Descriptive ranking; machine learning explicitly excluded |
| Data quality and preparation | Completed | Cells 3–5; E-003 to E-005 and E-009 | One non-blocking parent/variant reconciliation issue isolated to HMUG; partial August period identified |
| EDA or statistical analysis | Completed | Cells 6–15 | Conservative scoring, sensitivity analysis, LOMO robustness, catalog impact, HHI, internal concentration, what-if, and ASP |
| Feature engineering | N/A | D-001 | No predictive model |
| Modeling and validation | N/A | D-001 | No machine learning |
| Explanation and error analysis | Completed | Cells 4, 7–9, and 13 | Duplicate aggregates, third-place sensitivity, LOMO, and residual internal concentration documented |
| Methodology design | N/A | D-002 | Transparent rules are sufficient; no custom model claimed |
| Delivery and export QA | Completed | Cells 11 and 21 | Base gate and 29-condition extended QA passed after all five visualization cells in sequential validation on 2026-09-04 |
| Operational monitoring | N/A | Not applicable | One-time case analysis |

## Assumptions Register

| ID | Assumption | Category | Confidence | Impact if Wrong | Validation Plan | Status |
|---|---|---|---|---|---|---|
| A-001 | Repeated positive monthly pairs of sales and units represent ambiguous attribution and must not be credited fully to every listed variant | DATA | MEDIUM | HIGH | Confirm mapping against transaction-level order IDs or the source system | OPEN |
| A-002 | Status `Normal` means the variant is currently eligible for a standalone listing | BUSINESS | MEDIUM | HIGH | Confirm production, inventory, and listing readiness with operations | OPEN |
| A-003 | Splitting a listing changes catalog concentration but does not by itself create new demand | BUSINESS | HIGH | HIGH | Treat any future uplift as a separate experiment rather than a result of this analysis | VALIDATED |

## Decisions Log

### D-001 — Use descriptive ranking without machine learning

- **Chosen:** Use auditable rules and sensitivity analysis.
- **Alternatives considered:** Predictive scoring or forecasting.
- **Why:** Only three monthly aggregate observations exist per variant and the decision is ranking, not prediction.
- **Evidence:** User instruction and Cells 1–2.
- **Revisit when:** Transaction-level history with a longer time span becomes available.

### D-002 — Exclude ambiguous revenue from the primary variant ranking

- **Chosen:** Credit a variant only with positive monthly sales-and-unit pairs that occur once within HMUG.
- **Alternatives considered:** Divide repeated revenue equally across all associated variants or across active variants only.
- **Why:** The source lacks transaction IDs or an ownership field; the conservative rule avoids inventing attribution.
- **Evidence:** Cells 4, 6–7; E-003, E-004, and E-007.
- **Revisit when:** The operational source identifies the true owner of repeated values.

### D-003 — Recommend three standalone variants

- **Chosen:** `VAR-A01,COL-01`, `VAR-C01,COL-03`, and `VAR-D02,COL-01`.
- **Alternatives considered:** `VAR-A02,COL-01`, `VAR-B03,COL-02`, and `VAR-C03,COL-03`.
- **Why:** The chosen variants are active, fully attributable under the conservative rule, sell in all three months, and occupy ranks 1–3 on revenue, units, median monthly revenue, and weakest-month revenue.
- **Evidence:** Cells 6, 8–9, and 11; E-006 and E-010.
- **Revisit when:** A-001 or A-002 is resolved with contradictory operational evidence.

### D-004 — Retain VAR-D02 as the third recommendation

- **Chosen:** Prefer `VAR-D02,COL-01` over `VAR-A02,COL-01`.
- **Alternatives considered:** Promote `VAR-A02,COL-01` based on the active-only allocation scenario.
- **Why:** D02 enters the top three in two of three sensitivity scenarios and has fully attributable revenue; A02 enters only under the scenario that reallocates ambiguous revenue away from deleted variants.
- **Evidence:** Cells 7–9; E-007 and E-010.
- **Revisit when:** Transaction-level attribution resolves A-001.

### D-005 — Supersede the deleted legacy project state

- **Chosen:** Preserve only claims supported by the current workbook and notebook.
- **Alternatives considered:** Restore legacy recommendations, uplift, HHI, margin, mockup, and PDF claims from Git history.
- **Why:** The legacy state conflicts with the current recommendation and references artifacts or simulations not present in the current working tree.
- **Evidence:** `git show HEAD:PROJECT_STATE.md`, current notebook Cells 1–11, and current Git status.
- **Revisit when:** A removed artifact is deliberately restored and independently revalidated.

## Evidence Ledger

| ID | Claim or Result | Value | Evidence Source | Evaluation Context | Status |
|---|---|---|---|---|---|
| E-001 | Total store sales | Rp816,449,942 | Workbook Sheet 1 and notebook Cell 2 | DESCRIPTIVE | VALIDATED |
| E-002 | HMUG parent sales and store share | Rp177,705,421; 21.8% | Workbook Sheet 2 and notebook Cell 8 | DESCRIPTIVE | VALIDATED |
| E-003 | Raw HMUG variant total exceeds its parent | Rp259,906,900; gap Rp82,201,479; ratio 146.3% | Notebook Cells 3–4 | DESCRIPTIVE | VALIDATED |
| E-004 | Deduplicating exact positive monthly sales-and-unit pairs reconciles HMUG | Difference Rp0 in June, July, and August | Notebook Cell 4 | DESCRIPTIVE DIAGNOSTIC | VALIDATED |
| E-005 | Data-quality gate | 0 blocking failures; 1 handled reconciliation warning | Notebook Cells 3, 11, and 18 | DESCRIPTIVE QA | VALIDATED |
| E-006 | Final recommended variants | A01 Rp94,297,119 / 629 units; C01 Rp12,827,862 / 71 units; D02 Rp8,446,915 / 44 units | Notebook Cells 6, 8, and 11 | DESCRIPTIVE RANKING | VALIDATED |
| E-007 | Sensitivity result | A01 and C01 top-three in 3/3 scenarios; D02 in 2/3; A02 in 1/3 | Notebook Cells 7–8 | SENSITIVITY ANALYSIS | VALIDATED |
| E-008 | Catalog split scenario | Selected total Rp115,571,896; residual HMUG Rp62,133,525; residual share 7.6%; largest post-split parent/listing HAMPERS at 19.1% | Notebook Cell 10 | DESCRIPTIVE SCENARIO, NOT FORECAST | VALIDATED |
| E-009 | Partial-period audit | August covers 28/31 days; daily run-rate +5.4% versus July; calendar-month run-rate Rp278,127,783 | Notebook Cell 5 | DESCRIPTIVE NORMALIZATION, NOT FORECAST | VALIDATED |
| E-010 | Leave-one-month-out robustness | A01 and C01 top-three in 3/3 folds; D02 in 2/3 | Notebook Cell 9 | ROBUSTNESS CHECK, NOT STATISTICAL VALIDATION | VALIDATED |
| E-011 | Store-level catalog HHI | 982.7 before; 703.8 or 700.9 after; reduction 28.4%–28.7% | Notebook Cell 12 | DESCRIPTIVE CONCENTRATION | VALIDATED |
| E-012 | Internal recommendation concentration | A01 share 81.6%; internal HHI 6,833.8; A01 share rises from 74.1% to 85.6% across recorded months | Notebook Cell 13 | DESCRIPTIVE CONCENTRATION | VALIDATED |
| E-013 | What-if range | Assumed selected-SKU change -10% to +20% implies store-total change -1.4% to +2.8% | Notebook Cell 14 | ASSUMPTION-BASED SCENARIO, NOT FORECAST | VALIDATED |
| E-014 | ASP and margin boundary | ASP: A01 Rp149,916; C01 Rp180,674; D02 Rp191,975; margin unavailable | Notebook Cell 15 | DESCRIPTIVE | VALIDATED |

## Methodology Design

**Method ID and version:** NOT APPLICABLE

**Maturity:** NOT APPLICABLE

**Method spec:** Not applicable

**Case signature and baseline gap:** Not applicable

**Exact next experiment:** Resolve A-001 using transaction-level identifiers, then rerun the same ranking rules.

## Model Drivers and Error Analysis

Not applicable. No model was trained. Ranking dimensions are revenue, units, median monthly revenue, weakest-month revenue, active status, attribution certainty, and three-month continuity.

## Artifacts

| Artifact | Purpose | Validation Status |
|---|---|---|
| `Dummy Brand _ PERFORMA PRODUK - JUNI sd AGUSTUS 2026.xlsx` | Read-only source data | HASHED AND AUDITED |
| `PROJECT_STATE.md` | Persistent evidence and decision trail | PASSED; validator returned 0 errors and 0 warnings |
| `stock-keeping-unit.documented-v2.ipynb` | Reproducible analysis, evidence-grounded documentation, and three decision visuals | PASSED; 21 code cells validated sequentially, Cell 21 passed all 29 checks, and 21 Markdown annotations are present; SHA-256 `DFAD231668740C91E82D0F1C70D9EBF2DE266300756ED64A98DA544138570ACD` |

## Operational Monitoring

**Status:** NOT APPLICABLE

**Owner and cadence:** Not applicable

**Signals and intervention thresholds:** Not applicable

**Fallback or rollback:** Not applicable

## Limitations and Risks

- Aggregate data cannot establish which variant owns duplicated sales-and-unit pairs; this directly affects A02 and the third-place comparison.
- Three months are insufficient to establish seasonality or forecast uplift; August is partial through day 28.
- No margin, cost, stock, promotion, return, rating, or marketing-spend data are available.
- The split scenario is an accounting/catalog reclassification, not evidence that demand or revenue will increase.
- Saved notebook output and execution counts are historical after cell reordering; Cells 18–21 have no saved output. The 21 code cells contained in the documented notebook were validated sequentially on 2026-09-04, while `document-notebook` itself remained static and did not execute code.

## Open Questions

- [ ] What source-system key links the repeated HMUG aggregates to their true variant owner?
- [ ] Does `Normal` guarantee inventory and operational readiness for a standalone SKU?
- [ ] Are profit margin, return rate, and stock availability available before launch approval?

## Exact Next Action

Open `stock-keeping-unit.documented-v2.ipynb`, review the 21 inserted Markdown annotations, then restart the kernel and run all cells to save the three new charts, Cell 21 QA output, and monotonic execution counts before submission.
