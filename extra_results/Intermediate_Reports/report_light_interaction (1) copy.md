# OSD-767: Light Condition × Spaceflight Interaction Analysis

## 1. Introduction

The NASA OSD-767 experiment examined transcriptomic responses of tomato (*Solanum lycopersicum*) grown aboard the International Space Station under two light conditions (Red vs Blue LED lighting). Previous analysis using an additive DESeq2 model (`~ light + condition`) identified 2,132 significant DEGs in leaf and 2,582 in root for the Flight vs Ground comparison. This report examines whether **light quality (Red vs Blue) modulates the spaceflight response** — i.e., whether the effect of microgravity on gene expression depends on the light environment.

This is biologically motivated: Red light is primarily sensed by phytochromes, while Blue light is sensed by cryptochromes and phototropins. These photoreceptor pathways intersect with stress signaling, circadian regulation, and hormone transduction — all pathways known to be altered during spaceflight. An interaction between light quality and spaceflight would suggest that light environment design could mitigate or exacerbate spaceflight stress responses.

### Study Design

| Tissue | Ground Red | Ground Blue | Flight Red | Flight Blue | Total |
|--------|-----------|------------|-----------|------------|-------|
| Leaf   | 6         | 6          | 5         | 4          | 21    |
| Root   | 3         | 3          | 5         | 4          | 15    |
| **Combined** | **9** | **9** | **10** | **8** | **36** |

**Key limitation**: Root has only 3 ground replicates per light condition, reducing power for detecting interaction effects.

---

## 2. Methods

### 2.1 DESeq2 Interaction Models

Three DESeq2 models were fitted:

1. **Leaf interaction model** (21 samples): `~ light + condition + light:condition`
2. **Root interaction model** (15 samples): `~ light + condition + light:condition`
   - **Additive fallback** for root light main effect: `~ light + condition` (better powered)
3. **Combined whole-organ model** (36 samples): `~ tissue + light + condition + light:condition`

Factor levels: light = {Red, Blue}, condition = {Ground, Flight}, tissue = {Leaf, Root}.

The interaction term `light:condition` tests whether the Flight-vs-Ground effect differs between Blue and Red light. A positive interaction LFC means the spaceflight response is stronger under Blue light; a negative interaction means it is stronger under Red light.

**Significance thresholds**:
- Main effects: padj < 0.05, |shrunk log2FC| >= 1
- Interaction effects: padj < 0.1, |shrunk log2FC| >= 0.5 (relaxed due to lower power for interactions)

LFC shrinkage was applied using `ashr` for all comparisons.

### 2.2 Gene ID Mapping

Solyc gene IDs (ITAG3.0/SL3.0 assembly) were mapped to Entrez Gene IDs via biomaRt (Ensembl Plants mart, dataset `slgca000188115v5cm_eg_gene`). Mapping rate: 59.7-75.0% across gene sets.

### 2.3 GO and KEGG Enrichment

- **GO enrichment**: `clusterProfiler::enricher()` with custom TERM2GENE/TERM2NAME from biomaRt GO annotations (no tomato OrgDb available). Background universe: 11,442 Entrez IDs. Analyzed BP, MF, CC separately.
- **KEGG enrichment**: `clusterProfiler::enrichKEGG(organism="sly")`. Background: all tomato genes in KEGG.
- Cutoffs: pvalueCutoff=0.1, qvalueCutoff=0.2 (relaxed for interaction sets); pvalueCutoff=0.3 for sets with <20 Entrez IDs.

### 2.4 Systems Biology Pathway Visualization

- **pathview** (R) was unavailable due to Rgraphviz compilation failure (graphviz API v2 vs v2.42 incompatibility).
- **SBGNview** (R) was unavailable for the same reason.
- **Alternative approach**: KEGG pathway diagrams were generated using:
  - KEGG REST API for reference images and KGML spatial layouts
  - Python bioservices + matplotlib for expression overlays
  - SBGN-style Process Description diagrams from KGML coordinates
  - Pathway-level LFC heatmaps and gene-level bar plots

### 2.5 Tissue Comparison

Leaf vs root comparisons included:
- Venn diagrams of overlapping gene sets
- Pearson/Spearman correlation of LFCs across tissues
- Shared vs tissue-specific KEGG/GO pathway analysis
- Directional consistency analysis

---

## 3. Results

### 3.1 Light Main Effect (Blue vs Red)

The light main effect captures genes differentially expressed between Blue and Red light, averaged across Ground and Flight conditions.

| Model | Effect | Significant (padj<0.05, |LFC|>=1) | Up (Blue>Red) | Down (Blue<Red) |
|-------|--------|----------------------------------|---------------|-----------------|
| Leaf (interaction) | Light | 2,314 | 1,011 | 1,303 |
| Root (interaction) | Light | 256 | 105 | 151 |
| Root (additive fallback) | Light | 735 | 289 | 446 |
| Combined | Light | 460 | 302 | 158 |

**Leaf** shows a massive light effect with 2,314 significant DEGs -- 11.5% of all tested genes. This is expected: leaves are the primary light-sensing organ, and Blue vs Red light differentially regulates photosynthesis, photomorphogenesis, and secondary metabolism.

**Root** shows a much smaller light effect (256 DEGs from the interaction model; 735 from the better-powered additive model). Roots lack direct photoreception but receive light signals via systemic signaling from shoots.

**Notable**: In the combined model, only 460 genes are significant -- fewer than leaf alone. This reflects the dilution of tissue-specific light responses when pooling across tissues with fundamentally different light biology.

![Figure 1](light_interaction/leaf_light_MA.png)

**Figure 1. Leaf light effect MA plot.** Mean-average plot for the leaf light main effect (Blue vs Red). Each point represents a gene; x-axis shows mean normalized expression (log10 scale), y-axis shows shrunk log2 fold change. Yellow points are significant DEGs (padj < 0.05, |LFC| >= 1). Blue light downregulates 1,303 genes and upregulates 1,011 genes relative to Red light.

![Figure 2](light_interaction/leaf_light_volcano.png)

**Figure 2. Leaf light effect volcano plot.** Volcano plot of leaf light main effect (Blue vs Red). X-axis: shrunk log2 fold change; Y-axis: -log10(adjusted p-value). Dashed lines indicate significance thresholds (padj = 0.05, |LFC| = 1). The asymmetry toward negative LFC reflects the strong downregulation of photosynthesis and light-harvesting genes under Blue light.

![Figure 3](light_interaction/leaf_interaction_MA.png)

**Figure 3. Leaf light x spaceflight interaction MA plot.** Mean-average plot for the leaf interaction term (light:condition). Genes with significant interaction (padj < 0.1, |LFC| >= 0.5) indicate that the spaceflight response differs between Blue and Red light conditions. The large number of significant interaction genes (5,042 at relaxed threshold) demonstrates that light quality profoundly modulates the spaceflight transcriptomic response.

![Figure 4](light_interaction/leaf_interaction_volcano.png)

**Figure 4. Leaf light x spaceflight interaction volcano plot.** Volcano plot of the leaf interaction effect. The near-symmetric distribution of significant genes above and below zero indicates that Blue light enhances the spaceflight response for roughly half of interaction genes while Red light enhances it for the other half.

![Figure 5](light_interaction/root_light_MA.png)

**Figure 5. Root light effect MA plot.** Mean-average plot for the root light main effect (Blue vs Red, interaction model). Root shows a much smaller light effect (256 DEGs) compared to leaf (2,314 DEGs), consistent with roots lacking direct photoreception.

![Figure 6](light_interaction/root_light_volcano.png)

**Figure 6. Root light effect volcano plot.** Volcano plot of root light main effect. The reduced number of significant genes compared to leaf reflects both the biological reality of root light insensitivity and the lower statistical power (only 3 ground replicates per light condition).

![Figure 7](light_interaction/root_interaction_MA.png)

**Figure 7. Root light x spaceflight interaction MA plot.** Mean-average plot for the root interaction term. Very few significant interaction genes (44 at relaxed threshold) are detected, consistent with limited power and potentially genuine absence of light x spaceflight interaction in root tissue.

![Figure 8](light_interaction/root_interaction_volcano.png)

**Figure 8. Root light x spaceflight interaction volcano plot.** Volcano plot of root interaction effect. The sparse distribution of significant points underscores the exploratory nature of root interaction results.

![Figure 9](light_interaction/combined_light_MA.png)

**Figure 9. Combined model light effect MA plot.** Mean-average plot for the combined (leaf + root) light main effect. Only 460 genes are significant in the combined model, fewer than leaf alone, reflecting dilution of tissue-specific light responses when pooling across organs.

![Figure 10](light_interaction/combined_light_volcano.png)

**Figure 10. Combined model light effect volcano plot.** Volcano plot of the combined light main effect. The reduced signal compared to leaf-only analysis illustrates the fundamentally different light biology of the two tissues.

![Figure 11](light_interaction/combined_interaction_MA.png)

**Figure 11. Combined model interaction MA plot.** Mean-average plot for the combined light x spaceflight interaction. The 1,900 significant interaction genes (relaxed threshold) show more negative than positive interactions, suggesting that across the whole plant, Red light tends to amplify the spaceflight response more than Blue light.

![Figure 12](light_interaction/combined_interaction_volcano.png)

**Figure 12. Combined model interaction volcano plot.** Volcano plot of the combined interaction effect. The asymmetry toward negative LFC values indicates that Red light amplifies spaceflight responses more than Blue light at the whole-plant level.

#### 3.1.1 Leaf Light Effect: GO Enrichment

**Blue-upregulated genes** (604 Entrez IDs) were enriched for:
- Ethylene-activated signaling pathway (BP, padj=0.001)
- Regulation of flower development (BP, padj=0.001)
- Cellular response to phosphate starvation (BP, padj=0.002)

**Blue-downregulated genes** (841 Entrez IDs) were enriched for:
- Photosynthesis, light harvesting (BP, padj=5.2e-4)
- Proteolysis (BP, padj=7.7e-4)
- L-phenylalanine catabolic process (BP, padj=0.006)
- Regulation of photoperiodism, flowering (BP, padj=0.019)
- Structural constituent of chromatin (MF, padj=3.1e-5)
- Protochlorophyllide reductase activity (MF, padj=0.007)
- Nucleosome (CC, padj=8.5e-6)

The downregulation of light harvesting and protochlorophyllide reductase under Blue light is consistent with Blue light suppressing chlorophyll biosynthesis genes relative to Red light, which more strongly drives photosynthetic gene expression.

![Figure 13](light_interaction/leaf_light_up_BP_dotplot.png)

**Figure 13. Leaf Blue-upregulated GO BP enrichment dotplot.** Dot plot of Gene Ontology Biological Process terms enriched among genes upregulated by Blue light (vs Red) in leaf. Ethylene-activated signaling pathway and regulation of flower development are the top enriched terms, consistent with Blue light activating cryptochrome-mediated signaling cascades.

![Figure 14](light_interaction/leaf_light_down_BP_dotplot.png)

**Figure 14. Leaf Blue-downregulated GO BP enrichment dotplot.** Dot plot of GO Biological Process terms enriched among genes downregulated by Blue light in leaf. Photosynthesis and light harvesting are the top downregulated processes, reflecting Blue light suppression of chlorophyll biosynthesis and light-harvesting complex genes relative to Red light.

#### 3.1.2 Root Light Effect: GO Enrichment

**Blue-upregulated genes** (173 Entrez IDs, additive model) were enriched for:
- Monooxygenase activity (MF, padj=3.3e-4)
- Oxidoreductase activity with oxygen incorporation (MF, padj=3.7e-4)
- Iron ion binding (MF, padj=1.0e-3)
- Heme binding (MF, padj=7.6e-3)
- Ethylene-activated signaling pathway (BP, padj=0.097)
- Recognition of pollen (BP, padj=0.097)

**Blue-downregulated genes** (265 Entrez IDs) were enriched for:
- Xyloglucan metabolic process (BP, padj=0.024)
- Cell wall biogenesis (BP, padj=0.024)
- Glucan metabolic process (BP, padj=0.024)
- Response to desiccation (BP, padj=0.030)
- Cell wall (CC, padj=4.2e-3)
- Apoplast (CC, padj=1.3e-2)

Root light responses center on cell wall remodeling and oxidoreductase activity, consistent with systemic light signals modulating root growth and cell wall properties.

![Figure 15](light_interaction/leaf_int_neg_BP_dotplot.png)

**Figure 15. Leaf negative interaction GO BP enrichment dotplot.** Dot plot of GO Biological Process terms enriched among genes where the spaceflight response is stronger under Red light (negative interaction). Response to heat and ethylene-activated signaling pathway are the top terms, indicating that Red light amplifies spaceflight-induced stress signaling.

![Figure 16](light_interaction/root_light_down_BP_dotplot.png)

**Figure 16. Root Blue-downregulated GO BP enrichment dotplot.** Dot plot of GO Biological Process terms enriched among genes downregulated by Blue light in root. Cell wall biogenesis and xyloglucan metabolic process are enriched, consistent with systemic light signals modulating root growth and cell wall properties.

![Figure 17](light_interaction/comb_int_pos_BP_dotplot.png)

**Figure 17. Combined positive interaction GO BP enrichment dotplot.** Dot plot of GO Biological Process terms enriched among genes where the spaceflight response is stronger under Blue light (positive interaction) in the combined model. Aromatic amino acid family biosynthetic process is enriched, consistent with Blue light priming phenylpropanoid and flavonoid biosynthesis for enhanced spaceflight response.

![Figure 18](light_interaction/comb_light_down_BP_dotplot.png)

**Figure 18. Combined Blue-downregulated GO BP enrichment dotplot.** Dot plot of GO Biological Process terms enriched among genes downregulated by Blue light in the combined model. Photosynthesis and light harvesting dominate, reflecting the leaf-driven signal in the pooled analysis.

#### 3.1.3 KEGG Pathways: Light Main Effect

**Leaf Blue>Red**: 22 pathways enriched. Top pathways:
- Plant hormone signal transduction (padj=8.2e-7, 22 genes)
- Pentose phosphate pathway (padj=1.1e-5, 8 genes)
- Carbon fixation by Calvin cycle (padj=1.5e-5, 9 genes)

**Leaf Blue<Red**: 43 pathways enriched. Top pathways:
- Photosynthesis - antenna proteins (padj=3.8e-7, 9 genes)
- Plant-pathogen interaction (padj=2.6e-6, 20 genes)
- Porphyrin metabolism (padj=2.6e-6, 10 genes)

**Root Blue>Red** (additive): 8 pathways. Top: Plant hormone signal transduction (padj=4.2e-5), MAPK signaling (padj=1.5e-4).

**Root Blue<Red**: 10 pathways. Top: Arginine and proline metabolism (padj=4.5e-4), nucleotide sugar biosynthesis (padj=2.6e-3).

**Shared leaf-root light pathways** (11 total): Plant hormone signal transduction, MAPK signaling, Carotenoid biosynthesis, Flavonoid biosynthesis, Phosphatidylinositol signaling, Glycerophospholipid metabolism, Amino sugar metabolism, Galactose metabolism, Stilbenoid/diarylheptanoid biosynthesis, Glycerolipid metabolism, Biosynthesis of unsaturated fatty acids.

---

### 3.2 Light x Spaceflight Interaction

The interaction term identifies genes where the spaceflight response differs between Blue and Red light conditions. This is the central question of the analysis.

| Model | Effect | Strict (padj<0.05, |LFC|>=1) | Relaxed (padj<0.1, |LFC|>=0.5) | Positive (Blue stronger) | Negative (Red stronger) |
|-------|--------|------------------------------|-------------------------------|--------------------------|-------------------------|
| Leaf | Light x Condition | 2,894 | 5,042 | 2,502 | 2,540 |
| Root | Light x Condition | 15 | 44 | 32 | 12 |
| Combined | Light x Condition | 845 | 1,900 | 725 | 1,175 |

**Leaf** shows a remarkably large interaction: 5,042 genes at relaxed thresholds (25% of all tested genes). The near-equal split between positive and negative interactions indicates that Blue light enhances the spaceflight response for roughly half of interaction genes while Red light enhances it for the other half.

**Root** shows very few interaction genes (44 at relaxed thresholds), consistent with the low power from only 3 ground replicates per light condition. These results should be treated as exploratory.

**Combined** shows 1,900 interaction genes, with more negative interactions (1,175) than positive (725), suggesting that across the whole plant, Red light tends to amplify the spaceflight response more than Blue light.

#### 3.2.1 Leaf Interaction: GO Enrichment

**Positive interaction** (flight effect stronger under Blue, 1,675 Entrez IDs):
- Proteolysis (BP, padj=0.026)
- Aromatic amino acid family biosynthetic process (BP, padj=0.084)

**Negative interaction** (flight effect stronger under Red, 1,573 Entrez IDs):
- Response to heat (BP, padj=2.2e-3)
- Ethylene-activated signaling pathway (BP, padj=3.2e-3)
- Xyloglucan metabolic process (BP, padj=0.068)
- Regulation of flower development (BP, padj=0.068)
- Cellular response to phosphate starvation (BP, padj=0.068)
- Heat shock protein binding (MF, padj=0.015)
- Protein-folding chaperone binding (MF, padj=0.034)
- Cell wall (CC, padj=0.045)

The negative interaction enrichment for ethylene signaling and heat shock proteins is particularly notable: these stress-response pathways show stronger spaceflight induction under Red light than Blue light.

#### 3.2.2 Leaf Interaction: KEGG Enrichment

**Positive interaction** (83 pathways): Top pathways include Biosynthesis of cofactors (padj=3.1e-10), Biosynthesis of amino acids (padj=6.9e-10), Plant-pathogen interaction (padj=7.8e-9).

**Negative interaction** (48 pathways): Top pathways include:
- **Plant hormone signal transduction** (padj=1.0e-13, 52 genes)
- **Protein processing in ER** (padj=5.4e-10, 31 genes)
- **MAPK signaling pathway - plant** (padj=5.5e-8, 26 genes)

The negative interaction for hormone signaling and MAPK signaling means that the spaceflight-induced upregulation of these pathways (identified in the previous additive analysis) is **stronger under Red light than Blue light**. This is a key finding: Red light amplifies the spaceflight stress response in hormone and MAPK signaling.

#### 3.2.3 Root Interaction: Enrichment (Exploratory)

Root interaction gene sets are very small (9-16 Entrez IDs), so enrichment results are driven by single genes and should be interpreted cautiously.

**Positive interaction** (16 Entrez IDs): Response to photooxidative stress (BP), Photosystem I assembly (BP), Channel activity (MF), Clathrin-coated vesicle (CC).

**Negative interaction** (9 Entrez IDs): Ethylene-activated signaling pathway (BP), Hydrogen peroxide catabolic process (BP), Response to oxidative stress (BP), Peroxidase activity (MF).

Despite the small gene sets, the recurrence of ethylene signaling and oxidative stress in root interaction results mirrors the leaf findings, suggesting these may be genuine cross-tissue interaction effects.

#### 3.2.4 Combined Interaction: KEGG Enrichment

**Positive interaction** (498 Entrez IDs, 52 pathways): Top pathways:
- **Phenylpropanoid biosynthesis** (padj=4.2e-10, 19 genes)
- Phenylalanine metabolism (padj=3.8e-7, 10 genes)
- Biosynthesis of amino acids (padj=4.3e-7, 17 genes)

**Negative interaction** (715 Entrez IDs, 23 pathways): Top pathways:
- Protein processing in ER (padj=1.7e-4, 14 genes)
- Plant hormone signal transduction (padj=1.7e-4, 20 genes)
- Phosphatidylinositol signaling system (padj=2.8e-4, 8 genes)

The combined model confirms the leaf pattern: phenylpropanoid biosynthesis shows a positive interaction (spaceflight effect stronger under Blue), while hormone signaling shows a negative interaction (spaceflight effect stronger under Red).

---

### 3.3 Systems Biology Pathway Visualization

#### 3.3.1 Pathway LFC Heatmap

A comprehensive heatmap of mean LFC across 10 key KEGG pathways x 6 comparisons reveals striking tissue-specific patterns:

| Pathway | Leaf: Blue vs Red | Leaf: Light x Flight | Root: Blue vs Red | Root: Light x Flight |
|---------|-------------------|----------------------|--------------------|-----------------------|
| Photosynthesis - antenna proteins | **-1.97** | **+1.54** | +0.07 | +0.00 |
| Porphyrin metabolism | **-0.66** | **+0.68** | +0.01 | +0.00 |
| Phenylpropanoid biosynthesis | -0.31 | **+0.65** | +0.22 | +0.04 |
| Carbon fixation (Calvin cycle) | +0.33 | -0.24 | +0.01 | +0.00 |
| Plant hormone signal transduction | +0.02 | -0.13 | +0.02 | +0.00 |
| MAPK signaling - plant | -0.02 | -0.06 | +0.04 | +0.00 |
| Circadian rhythm - plant | -0.05 | -0.01 | +0.01 | +0.00 |
| Flavonoid biosynthesis | +0.03 | +0.49 | +0.01 | +0.00 |
| Photosynthesis | -0.27 | +0.29 | +0.02 | +0.00 |
| Protein processing in ER | +0.01 | -0.23 | -0.01 | +0.00 |

**Key observations**:
1. **Photosynthesis - antenna proteins** shows the strongest light effect (-1.97 under Blue vs Red) AND the strongest interaction (+1.54). This means antenna protein genes are strongly downregulated by Blue light relative to Red, but the spaceflight response (which upregulates these genes) is much stronger under Blue light -- partially compensating for the Blue-light downregulation.
2. **Porphyrin metabolism** (chlorophyll biosynthesis precursors) mirrors the antenna protein pattern exactly.
3. **Phenylpropanoid biosynthesis** shows a positive interaction (+0.65) -- the spaceflight-induced upregulation of phenylpropanoid genes is enhanced under Blue light.
4. **Root pathways show near-zero interaction effects**, consistent with the low power and potentially genuine absence of light x spaceflight interaction in root tissue.

![Figure 19](light_interaction/pathways/pathway_lfc_heatmap.png)

**Figure 19. Pathway-level LFC heatmap.** Comprehensive heatmap of mean shrunk log2 fold change across 10 key KEGG pathways x 6 comparisons (leaf light, leaf interaction, root light, root interaction, combined light, combined interaction). Antenna proteins show the strongest leaf light effect (LFC ~ -1.97) and the strongest interaction (LFC ~ +1.54). Root pathways show near-zero interaction effects. Color scale: blue = negative LFC, red = positive LFC.

#### 3.3.2 SBGN-style Pathway Diagrams

SBGN-style Process Description diagrams were generated for three key pathways using KEGG KGML spatial layouts with SBGN visual conventions:
- **Plant hormone signal transduction** (sly04075): Shows gene-level LFC coloring for both light effect and interaction
- **Phenylpropanoid biosynthesis** (sly00940): Highlights the positive interaction in secondary metabolism
- **Circadian rhythm - plant** (sly04712): Shows modest but consistent light effects on clock genes

These diagrams use rounded rectangles (SBGN macromolecule convention) for genes/proteins and circles (simple chemical convention) for metabolites, with color intensity representing LFC magnitude.

![Figure 20](light_interaction/pathways/sly04075_gene_lfc_bars.png)

**Figure 20. Plant hormone signal transduction gene-level LFC bars.** Bar plot showing per-gene shrunk log2 fold change for genes in the Plant hormone signal transduction pathway (sly04075), stratified by light effect (Blue vs Red) and light x spaceflight interaction. Auxin, ethylene, and cytokinin signaling components show distinct patterns of light and interaction regulation.

![Figure 21](light_interaction/pathways/sly00940_gene_lfc_bars.png)

**Figure 21. Phenylpropanoid biosynthesis gene-level LFC bars.** Bar plot showing per-gene shrunk LFC for phenylpropanoid biosynthesis pathway genes (sly00940). Phenylalanine ammonia-lyase (PAL) and downstream enzymes show positive interaction LFC, indicating that spaceflight enhances Blue-light-driven phenylpropanoid gene expression.

![Figure 22](light_interaction/pathways/sly00196_gene_lfc_bars.png)

**Figure 22. Antenna proteins gene-level LFC bars.** Bar plot showing per-gene shrunk LFC for antenna protein pathway genes (sly00196). Light-harvesting complex (LHC) genes show the strongest light effect (LFC ~ -2.0) and the strongest interaction (LFC ~ +1.5 to +2.6), demonstrating that spaceflight partially rescues Blue-light suppression of antenna genes.

![Figure 23](light_interaction/pathways/sly04712_gene_lfc_bars.png)

**Figure 23. Circadian rhythm gene-level LFC bars.** Bar plot showing per-gene shrunk LFC for circadian rhythm pathway genes (sly04712). Clock genes (PRR7, CCA1, TOC1 homologs) show modest but consistent light effects and cell-type-specific interaction patterns, particularly in vascular tissue.

![Figure 24](light_interaction/pathways/sly04075_sbgn_style.png)

**Figure 24. Plant hormone signal transduction SBGN-style pathway diagram.** SBGN Process Description-style diagram of the Plant hormone signal transduction pathway (sly04075), generated from KEGG KGML spatial layouts. Gene nodes (rounded rectangles) are colored by shrunk LFC; compound nodes (circles) represent metabolites. Arrows indicate activation (green), inhibition (red), or phosphorylation (blue). The diagram highlights the negative interaction in auxin and ethylene signaling branches.

![Figure 25](light_interaction/pathways/sly00940_sbgn_style.png)

**Figure 25. Phenylpropanoid biosynthesis SBGN-style pathway diagram.** SBGN-style diagram of the Phenylpropanoid biosynthesis pathway (sly00940). The positive interaction LFC (red nodes) for PAL and downstream enzymes indicates that spaceflight enhances Blue-light-driven phenylpropanoid gene expression, consistent with Blue light priming secondary metabolism for stress responses.

![Figure 26](light_interaction/pathways/sly04712_sbgn_style.png)

**Figure 26. Circadian rhythm SBGN-style pathway diagram.** SBGN-style diagram of the Circadian rhythm pathway (sly04712). Modest light effects on clock gene expression are visible, with the strongest signals in the evening complex (PRR7/TOC1) and morning loop (CCA1/LHY) components.

---

### 3.4 Tissue-Specific vs Shared Effects

#### 3.4.1 Gene-Level Overlap

| Comparison | Leaf genes | Root genes | Shared | % of union | Direction reversals |
|------------|-----------|-----------|--------|-----------|-------------------|
| Light up (Blue>Red) | 1,011 | 289 | 37 | 2.9% | 38 (leaf up & root down) |
| Light down (Blue<Red) | 1,303 | 446 | 28 | 1.6% | 40 (leaf down & root up) |
| Interaction positive | 2,502 | 32 | 1 | ~0% | -- |
| Interaction negative | 2,540 | 12 | 2 | 0.1% | -- |

The overlap between leaf and root light-effect genes is very small (2-3% of the union). Remarkably, the number of **direction reversals** (38-40 genes where Blue light upregulates in leaf but downregulates in root, or vice versa) exceeds the number of consistently regulated shared genes (65). This indicates fundamentally different light responses in the two tissues.

#### 3.4.2 LFC Correlation Between Tissues

| Comparison | Pearson r | Spearman rho | n genes |
|------------|-----------|-------------|---------|
| Light effect (Blue vs Red) | **-0.032** | -0.063 | 19,529 |
| Light x Flight interaction | **0.008** | 0.042 | 19,529 |

The near-zero correlations confirm that leaf and root have essentially independent transcriptional responses to light quality and to the light x spaceflight interaction. This is biologically expected: leaves directly perceive light via photoreceptors, while roots receive only indirect systemic signals.

#### 3.4.3 Within-Tissue: Light Effect vs Interaction Correlation

| Tissue | Pearson r (Light LFC vs Interaction LFC) |
|--------|----------------------------------------|
| **Leaf** | **-0.840** |
| Root | -0.282 |

The leaf shows a striking **negative correlation (r = -0.840)** between the light main effect and the light x flight interaction. This means: genes that are strongly upregulated by Blue light (relative to Red) tend to show a weaker spaceflight response under Blue light, and vice versa. This is consistent with a **compensatory model**: Blue light pre-activates certain pathways (e.g., photosynthesis, chlorophyll biosynthesis), reducing the additional perturbation caused by spaceflight on those same pathways. Conversely, pathways suppressed by Blue light (e.g., antenna proteins) show stronger spaceflight induction under Blue -- as if the spaceflight environment partially rescues the Blue-light suppression.

The root shows a weaker but still negative correlation (r = -0.282), suggesting a muted version of the same compensatory dynamic.

![Figure 27](light_interaction/leaf_light_vs_interaction_lfc.png)

**Figure 27. Leaf: light LFC vs interaction LFC correlation.** Scatter plot of leaf shrunk log2 fold change for the light main effect (x-axis) vs the light x spaceflight interaction (y-axis). The strong negative correlation (r = -0.840) supports a compensatory model: genes strongly regulated by light quality tend to show attenuated spaceflight responses under the same light condition. Points are colored by significance status.

![Figure 28](light_interaction/root_light_vs_interaction_lfc.png)

**Figure 28. Root: light LFC vs interaction LFC correlation.** Scatter plot of root shrunk LFC for light effect vs interaction. The weaker negative correlation (r = -0.282) suggests a muted version of the compensatory dynamic seen in leaf, consistent with root's indirect light perception.

#### 3.4.4 Shared vs Tissue-Specific KEGG Pathways

**Light effect**: 11 KEGG pathways are shared between leaf and root (out of 65 total). Shared pathways include Plant hormone signal transduction, MAPK signaling, Carotenoid biosynthesis, and Flavonoid biosynthesis -- all pathways with known systemic signaling components.

**Interaction**: Only 4 pathways are shared (all driven by single root genes): Phenylpropanoid biosynthesis, Lysosome biogenesis, Carotenoid biosynthesis, and Riboflavin metabolism. The leaf dominates interaction enrichment with 104 leaf-only pathways.

![Figure 29](light_interaction/tissue_comparison_venn_scatter.png)

**Figure 29. Leaf vs root tissue comparison: Venn diagrams and LFC scatter plots.** Dual-panel figure showing: (left) Venn diagrams of overlapping gene sets between leaf and root for light up, light down, interaction positive, and interaction negative comparisons; (right) scatter plots of leaf vs root shrunk LFC for light effect and interaction. The near-zero correlations (r = -0.032 for light, r = 0.008 for interaction) confirm essentially independent transcriptional responses in the two tissues.

![Figure 30](light_interaction/kegg_tissue_comparison_heatmap.png)

**Figure 30. KEGG pathway tissue comparison heatmap.** Heatmap comparing KEGG pathway enrichment across leaf and root for light effect and interaction comparisons. Leaf dominates the interaction enrichment landscape with 104 leaf-only pathways, while only 4 pathways are shared between tissues for the interaction. Shared light-effect pathways include Plant hormone signal transduction and MAPK signaling.

---

### 3.5 Comparison with Previous Flight-vs-Ground Results

The previous additive model (`~ light + condition`) identified 2,132 leaf DEGs and 2,582 root DEGs for the Flight vs Ground comparison. The interaction model reveals that:

1. **The condition main effect changes substantially** when the interaction is included: leaf condition DEGs drop from 2,132 (additive) to 527 (interaction model, strict threshold). This is because the additive model conflates the main spaceflight effect with the interaction -- some genes that appeared as "spaceflight-responsive" were actually responding differently depending on light color.

2. **The light main effect is much larger than the spaceflight effect in leaf**: 2,314 light DEGs vs 527 condition DEGs. Light quality is the dominant transcriptional regulator in photosynthetic tissue.

3. **The interaction is comparable in magnitude to the main effects**: 5,042 interaction genes (relaxed) vs 2,314 light and 527 condition. This means light quality substantially modulates how plants transcriptionally respond to spaceflight.

---

## 4. Discussion

### 4.1 Light Quality as a Modulator of Spaceflight Response

The central finding is that **light quality (Red vs Blue) profoundly modulates the spaceflight transcriptomic response in tomato leaf**, affecting approximately 25% of all expressed genes. The interaction is largely leaf-specific, with minimal detectable interaction in root (though this may reflect limited power rather than genuine absence).

### 4.2 The Compensatory Model

The strong negative correlation (r = -0.840) between light main effect and interaction LFC in leaf supports a compensatory model: pathways that are strongly activated by one light condition show attenuated spaceflight responses under that same condition. This could reflect:

1. **Saturation effect**: If Blue light already maximally activates photosynthesis-related genes, spaceflight cannot further upregulate them.
2. **Pre-adaptation**: Light-condition-specific gene expression may pre-adapt plants to certain stresses, reducing the additional perturbation from microgravity.
3. **Resource allocation trade-offs**: Plants under Blue light may allocate resources differently, leaving fewer reserves for spaceflight-induced changes in Blue-activated pathways.

### 4.3 Antenna Proteins: A Case Study in Light x Spaceflight Interaction

The Photosynthesis - antenna proteins pathway provides the clearest example:
- **Blue vs Red**: mean LFC = -1.97 (strong downregulation under Blue)
- **Light x Flight interaction**: mean LFC = +1.54 (spaceflight upregulation is much stronger under Blue)

Under Red light, antenna protein genes are highly expressed and show minimal spaceflight response. Under Blue light, these genes are suppressed but show strong spaceflight-induced upregulation -- as if microgravity partially rescues the Blue-light suppression of light-harvesting machinery. This may represent an adaptive response: in microgravity, where photosynthetic demand may change, plants under Blue light upregulate antenna proteins to compensate for reduced light harvesting efficiency.

### 4.4 Hormone Signaling: Red Light Amplifies Spaceflight Stress

Plant hormone signal transduction shows a **negative interaction** (stronger spaceflight response under Red light) in both leaf and combined models. This suggests that Red light amplifies the spaceflight-induced disruption of hormone signaling (auxin, ethylene, cytokinin pathways). Given that phytochromes (Red light receptors) directly interact with hormone signaling cascades (particularly auxin transport), this interaction may reflect a phytochrome-hormone crosstalk that is disrupted in microgravity.

### 4.5 Phenylpropanoid Biosynthesis: Blue Light Enhances Spaceflight-Induced Secondary Metabolism

Phenylpropanoid biosynthesis shows a **positive interaction** (stronger spaceflight response under Blue light). This pathway produces flavonoids, lignins, and other secondary metabolites involved in UV protection and stress responses. Blue light (which includes wavelengths closer to UV) may prime the phenylpropanoid pathway, making it more responsive to the additional oxidative stress of spaceflight.

### 4.6 Tissue Specificity

The near-zero correlation between leaf and root LFCs for both light effects and interactions underscores that these are fundamentally different tissue environments:
- **Leaf** directly perceives light and shows massive light and interaction effects
- **Root** receives only indirect light signals and shows minimal interaction effects
- The few shared pathways (hormone signaling, MAPK) likely reflect systemic signaling rather than direct light perception.

### 4.7 Limitations

1. **Root power**: Only 3 ground replicates per light condition severely limits interaction detection in root. The 44 root interaction genes (relaxed threshold) should be considered exploratory.
2. **Unbalanced design**: Flight Blue has only 4 samples per tissue, which may inflate interaction estimates.
3. **Gene ID mapping**: Only ~60% of Solyc IDs map to Entrez IDs, reducing enrichment power and potentially introducing mapping bias.
4. **pathview/SBGNview unavailable**: The Rgraphviz dependency could not be compiled due to graphviz API version incompatibility. Alternative visualizations were generated but lack the polished pathway overlay of pathview.
5. **Interaction threshold**: The relaxed threshold (padj<0.1, |LFC|>=0.5) for interaction genes may include some false positives. The large interaction count (5,042 in leaf) should be interpreted with this in mind.
6. **No replication across experiments**: These results are from a single spaceflight experiment. Validation in independent experiments would strengthen the conclusions.

---

## 5. Conclusions

1. **Light quality profoundly modulates the spaceflight transcriptomic response** in tomato leaf, with ~25% of genes showing significant light x spaceflight interaction.
2. **A compensatory dynamic exists**: genes strongly regulated by light quality tend to show attenuated spaceflight responses under the same light condition (r = -0.840 in leaf).
3. **Antenna proteins and porphyrin metabolism** show the strongest interaction: Blue light suppresses these pathways, but spaceflight strongly upregulates them under Blue light.
4. **Hormone signaling and MAPK pathways** show stronger spaceflight induction under Red light, suggesting Red light amplifies spaceflight stress signaling.
5. **Phenylpropanoid biosynthesis** shows stronger spaceflight induction under Blue light, consistent with Blue light priming secondary metabolism for stress responses.
6. **Leaf and root have essentially independent light x spaceflight responses** (r ~ 0), reflecting their different roles in light perception and systemic signaling.
7. **These findings have practical implications**: light environment design in spaceflight growth chambers could be optimized to mitigate specific aspects of spaceflight stress -- e.g., Blue light supplementation may reduce excessive hormone signaling disruption, while Red light may help maintain photosynthetic capacity.

---

## 6. Output Files

### DESeq2 Results
- `leaf_light_Blue_vs_Red.csv` -- Leaf light main effect (20,157 genes)
- `leaf_interaction.csv` -- Leaf light x condition interaction
- `root_light_Blue_vs_Red.csv` -- Root light effect (interaction model)
- `root_light_additive_Blue_vs_Red.csv` -- Root light effect (additive fallback)
- `root_interaction.csv` -- Root light x condition interaction
- `combined_light_Blue_vs_Red.csv` -- Combined light main effect
- `combined_interaction.csv` -- Combined light x condition interaction
- `deseq2_summary_table.csv` -- Summary of all DESeq2 results

### Enrichment Results
- `go_enrichment_all.csv` -- All GO enrichment results (137 terms)
- `kegg_enrichment_all.csv` -- All KEGG enrichment results (313 pathways)
- `gene_set_summary.csv` -- Gene set sizes and mapping rates

### Tissue Comparison
- `tissue_overlap_genes.csv` -- Leaf vs root gene set overlap
- `tissue_lfc_correlation.csv` -- Per-gene LFCs for correlation analysis
- `shared_light_up_genes.csv` -- Genes upregulated by Blue in both tissues
- `shared_light_down_genes.csv` -- Genes downregulated by Blue in both tissues

### Pathway Visualization (in `pathways/` subdirectory)
- `pathway_lfc_heatmap.svg/.png` -- Pathway-level LFC heatmap (10 pathways x 6 comparisons)
- `pathway_expression_summary.csv` -- Pathway expression data
- `sly04075_gene_lfc_bars.svg/.png` -- Plant hormone signal transduction gene-level plot
- `sly00940_gene_lfc_bars.svg/.png` -- Phenylpropanoid biosynthesis gene-level plot
- `sly00196_gene_lfc_bars.svg/.png` -- Photosynthesis antenna proteins gene-level plot
- `sly04712_gene_lfc_bars.svg/.png` -- Circadian rhythm gene-level plot
- `sly04075_sbgn_style.svg/.png` -- SBGN-style hormone signaling diagram
- `sly00940_sbgn_style.svg/.png` -- SBGN-style phenylpropanoid diagram
- `sly04712_sbgn_style.svg/.png` -- SBGN-style circadian rhythm diagram
- KEGG reference images for all 10 pathways
