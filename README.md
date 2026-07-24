# PhysioSpace stress decoding of spaceflight tomato (VEG-05 / OSD-767)

**Manuscript:** *Light quality modulates spaceflight stress decoding with cell-type
asymmetry in tomato* — npj Microgravity submission package.

This repository holds the analysis, figures, supplementary data, and manuscript for
a **Light × Condition (2 × 2 factorial)** re-analysis of the NASA VEG-05 experiment,
in which dwarf tomato (*Solanum lycopersicum* cv. 'Red Robin') was grown aboard the
ISS under red- or blue-rich LED light versus ground controls. Beyond differential
expression and pathway enrichment, it adds **PhysioSpace stress-pattern decoding** —
projecting the spaceflight transcriptomes onto pre-built *Arabidopsis* stress-response
compendia to identify which established stress programs the response resembles — and a
**cell-type–resolved** analysis of radial asymmetry in the root.

- **Source dataset:** NASA OSDR [OSD-767](https://osdr.nasa.gov/bio/repo/data/studies/OSD-767) (GeneLab GLDS-709), VEG-05.
- **Reference genome:** *S. lycopersicum* SL3.0 / ITAG4.0.
- **Design:** 2 × 2 factorial (Light: Red/Blue × Condition: Ground/Flight); leaf (n=21) + adventitious root (n=15).
- **DE model:** DESeq2 `~ light + condition + light:condition` (interaction-first).
- **Stress decoding:** PhysioSpaceMethods + PlantPhysioSpace (3 *Arabidopsis* reference spaces).

> **Note on the name.** This work was previously stored under the working name
> `DeepLearning_VEG05`. The stress-decoding method used here is **PhysioSpace**
> (a linear projection onto reference stress signatures via the `PhysioSpaceMethods`
> R package), **not** a deep-learning / neural-network model. The repository has been
> renamed to reflect the actual method.

---

## Main-effects analysis (folded in as Supplementary Note 1)

The **additive main-effect** view of this dataset — DESeq2 `~ light + condition`
(light as covariate), estimating the light-averaged Flight-vs-Ground response
(2,132 leaf / 2,582 root DEGs, dominated by oxidative-stress and phenylpropanoid
metabolism) — is included here as **Supplementary Note 1**
(`supplementary/supplementary_note_1_main_effects.{md,html}`), with Supplementary
Figs. 20–21 and Supplementary Data 14. It provides the "core microgravity footprint"
against which this paper's Light × Condition interaction and PhysioSpace decoding are
interpreted; the interaction-model condition term (527 leaf / 704 root) and the
additive main effect are different estimands, not conflicting results.

The full analysis archive for that main-effects work (raw DESeq2 objects, all figures)
lives in the companion repository
[`VEGGIE_Tom_Red_Blue_Leaves_and_adv_roots`](https://github.com/dr-richard-barker/VEGGIE_Tom_Red_Blue_Leaves_and_adv_roots),
which shares the same upstream pipeline and scRNA markers (`scDATA/`).

---

## Repository structure

```
.
├── README.md
├── LICENSE                       ← CC0-1.0
├── CITATION.cff
│
├── manuscript/                   ← manuscript source (.md) + rendered PDFs (text-only + with-figures)
├── cover_letter/                 ← cover letter (.md + .pdf)
├── supplementary/                ← supplementary methods & materials (PDF/HTML)
├── supplementary_tables/         ← Supplementary Data 1–13 (CSV)
├── figures_main/                 ← 11 main figures (PNG 300 dpi, TIFF 600 dpi, PDF/SVG)
├── figures_supplementary/        ← 19 supplementary figures (PNG/TIFF/SVG/PDF)
├── scDATA/                       ← scRNA / TRAP-seq cell-type markers × DEG cross-reference
├── analysis/                     ← execution-trace notebook, analysis plan, and QC (qc/ MultiQC)
└── extra_results/                ← intermediate / exploratory outputs (see extra_results/readme.md)
    ├── DESeq2_roots_shoot/       ← per-tissue DESeq2 objects and plots
    ├── asymmetry_analysis_results/
    ├── cluster_annotation_results/
    ├── SBGN_pathways_results/
    └── Intermediate_Reports/
```

### Main figures (11)
1. Study design + differential-expression overview (with compensatory-model schematic)
2. Light × Condition interaction (leaf volcano; light-vs-interaction LFC scatter, r = −0.84)
3. Antenna proteins — compensatory rescue
4. Phenylpropanoid biosynthesis — blue-light-enhanced induction
5. Hormone / MAPK signaling — red-light-amplified stress
6. Organ-level interaction hotspots (cross-cell-type pathway LFC)
7. Circadian rhythm and root radial asymmetry
8. PhysioSpace stress-pattern heatmap (AT_Stress_Space)
9. Spaceflight stress-pattern activation by tissue × light
10. Flight × Light interaction on stress patterns (root Biotic.Hormone = −44.2)
11. Cell-type PhysioScore profiles

21 supplementary figures (19 in the main package + Figs. 20–21 for the folded-in
main-effects analysis) and 14 Supplementary Data tables are listed in the manuscript
(`manuscript/osd767_manuscript.md`, Figure/Table Legends) and provided in
`figures_supplementary/` and `supplementary_tables/`. Supplementary Note 1
(`supplementary/`) presents the additive main-effects analysis.

---

## Key results

- **Light dominates leaf, spaceflight dominates root:** leaf 2,314 light vs 527 condition DEGs; root 704 condition vs 256 light DEGs.
- **Compensatory dynamics:** leaf light-LFC vs interaction-LFC correlate at r = −0.84 — pathways pre-set by one light quality have less room to respond to spaceflight.
- **Radial root asymmetry:** outer cortex (Cortex_ACT2) is the top interaction hotspot (OR = 26.9); inner layers are balanced/down-skewed.
- **PhysioSpace decoding:** leaves show suppression of light-stress programs ("low-light syndrome"); roots show biotic/hormone defense activation, strongest under blue LED (Biotic.Hormone flight effect +58.4; interaction −44.2 — the largest modulatory signal at any scale).
- **Practical implication:** blue-rich ISS lighting maintains photosynthesis genes but hyperactivates root defense signaling — a light-design trade-off.

---

## Methods (summary)

DESeq2 interaction model (`~ light + condition + light:condition`, ashr shrinkage;
main-effect cutoffs padj < 0.05 & |LFC| ≥ 1, interaction padj < 0.1 & |LFC| ≥ 0.5) →
GO/KEGG enrichment (clusterProfiler, `organism = "sly"`) → cell-type deconvolution
against Yue et al. (leaf) and Kajala et al. (root TRAP-seq) markers (Fisher's exact) →
PhysioSpace mapping onto three *Arabidopsis* stress spaces (PhysioSpaceMethods +
PlantPhysioSpace) via Ensembl Plants Compara 1:1 orthologs. Full detail in
`supplementary/supplementary_methods.pdf` and `manuscript/` Methods.

---

## Data & code availability

- **Primary data:** NASA OSDR **OSD-767** / GeneLab **GLDS-709** (VEG-05).
- **Processed outputs:** Supplementary Data 1–13 in `supplementary_tables/`.
- **This analysis:** see `CITATION.cff`; a Zenodo deposit (DOI) is planned.

### Preparing the Zenodo deposit
Deposit as *Dataset*; set related identifiers "is derived from" OSD-767 (GLDS-709) and
"cites" the companion main-effects analysis; license CC0-1.0. Use the GitHub→Zenodo
release integration (tag a release) or upload the working tree (exclude `.git/`).

## License
**CC0 1.0 Universal** — see [`LICENSE`](LICENSE).
