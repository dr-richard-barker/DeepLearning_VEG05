# Supplementary Note 1. Additive main-effect analysis of the spaceflight response

## Rationale

The main text analyses the OSD-767 dataset with an **interaction** model
(`~ light + condition + light:condition`), in which the `condition` (Flight vs
Ground) coefficient estimates the spaceflight effect *at the reference light level*
rather than the effect averaged across light conditions. To complement this and to
quantify the total, light-averaged transcriptomic footprint of spaceflight, we also
fitted an **additive** model that treats light quality as a covariate. This note
reports that companion analysis; it corresponds to the "core microgravity footprint"
view of the data and is the subject of a separate archived analysis of the same
dataset.

## Methods

Gene-level RSEM counts for leaf (n = 21) and adventitious root (n = 15) were analysed
separately in DESeq2 with the design `~ light + condition`, contrasting Flight versus
Ground while adjusting for red/blue light spectrum. Low-count genes were pre-filtered;
log2 fold changes were shrunk (ashr). Differentially expressed genes (DEGs) were
defined at Benjamini–Hochberg FDR < 0.05 and |shrunk log2FC| ≥ 1. GO (BP/MF/CC) and
KEGG (`organism = "sly"`) over-representation used clusterProfiler with the same
parameters and Solyc→Entrez mapping as the main analysis.

## Results

**Extent of the response (Supplementary Fig. 20; Supplementary Data 14).** The
additive model recovered a far larger spaceflight footprint than the interaction
model's condition term (527 leaf / 704 root), because it estimates the light-averaged
effect rather than the effect at a single light level:

| Tissue | DEGs | Up in flight | Down in flight |
|--------|:----:|:------------:|:--------------:|
| Leaf | 2,132 | 1,032 | 1,100 |
| Adventitious root | 2,582 | 1,706 | 876 |

Adventitious roots showed the larger and more up-regulation-biased response
(≈2:1 up/down), with several loci induced from near-absent baselines (strongest
log2FC ≈ +25), consistent with the switch-like activation described in the main text.

**Functional enrichment (Supplementary Fig. 21).** Root up-regulated genes were
dominated by oxidative-stress management — GO "response to oxidative stress"
(32 genes, FDR ≈ 6.5 × 10⁻¹³), "hydrogen peroxide catabolic process" (28 genes),
"ethylene-activated signaling pathway" (FDR ≈ 1 × 10⁻⁶), and a strong heme-binding
molecular-function signature (67 genes, FDR ≈ 9 × 10⁻¹⁸) — together with KEGG
**phenylpropanoid biosynthesis** (45 genes, FDR ≈ 4 × 10⁻³⁰), flavonoid and stilbenoid
biosynthesis, and **glutathione metabolism**. Leaf up-regulated genes showed a related
but attenuated signature (heme/iron binding, monooxygenase activity, abscisic-acid
binding; KEGG phenylpropanoid and flavonoid biosynthesis, MAPK and plant-hormone
signalling). Down-regulated genes included the **plant circadian-rhythm** pathway in
both organs, with roots additionally suppressing Calvin-cycle carbon fixation and
starch/sucrose metabolism, and leaves suppressing transmembrane transport, galactose
and folate metabolism and glycolysis.

## Relationship to the interaction analysis

The additive main-effect DEGs (2,132 leaf / 2,582 root) and the interaction-model
condition DEGs (527 leaf / 704 root) are **different estimands**, not conflicting
results: the former is the spaceflight effect averaged over light, the latter the
effect at the reference light level. The systematic shrinkage of the interaction-model
condition coefficients toward zero for genes with large light effects (main text)
is the expected consequence of the compensatory light × condition dynamics. The
oxidative-stress and phenylpropanoid themes reported here at the light-averaged level
are the same programmes that the main analysis resolves into their light-dependent and
cell-type-specific components. This companion analysis therefore provides the broad
"core footprint" against which the interaction and PhysioSpace decoding are interpreted.
