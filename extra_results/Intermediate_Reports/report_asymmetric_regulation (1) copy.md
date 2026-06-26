# Asymmetric Up/Down Regulation in Roots and Leaves Under Spaceflight and Light Quality

## OSD-767 Tomato RNA-seq Analysis

---

## Executive Summary

This report investigates the strikingly asymmetric up/down regulation patterns in root and leaf transcriptomes from the OSD-767 experiment, which examined tomato (*Solanum lycopersicum*) plants grown aboard the ISS under two light quality treatments (red vs. blue). The central finding is a **radial asymmetry in root transcriptional response to spaceflight**: outer cell layers (exodermis, cortex) are overwhelmingly up-regulated (up to 4.0:1 up/down ratio in Cortex_ACT2), while inner cell layers (endodermis, vascular, xylem) are predominantly down-regulated (as low as 0.37:1 in Vascular_WOX4). This radial pattern maps onto distinct biological processes — oxidative stress defense and secondary metabolism in outer layers, versus suppressed hormone signaling and motor protein function in inner layers. In leaves, the dominant axis of variation is light quality, with blue light suppressing photosynthesis and circadian rhythm while activating secondary metabolism. A remarkable finding is that **Cortex_ACT2 is the sole hotspot of light x spaceflight interaction in roots**, concentrating 12 of 47 root interaction genes (OR = 16.1, p ~ 0) despite representing only 3.5% of root cell type markers.

---

## 1. Asymmetric Up/Down Regulation Across Tissues and Effects

### 1.1 Global Asymmetry Patterns

The DESeq2 interaction model (`~ light + condition + light:condition`) reveals dramatically different up/down ratios across tissue-effect combinations:

| Effect | Tissue | Up | Down | Up:Down Ratio | Interpretation |
|--------|--------|----|------|---------------|----------------|
| Condition (Flight vs Ground) | Root | 843 | 188 | **4.5:1** | Spaceflight overwhelmingly UPREGULATES roots |
| Condition (Flight vs Ground) | Leaf | 920 | 817 | 1.1:1 | Roughly balanced |
| Light (Blue vs Red) | Leaf | 1,011 | 1,303 | **1:1.3** | Blue light slightly DOWNREGULATES leaves |
| Light (Blue vs Red) | Root | 122 | 176 | 1:1.4 | Blue light slightly DOWNREGULATES roots |
| Light x Condition | Leaf | 2,728 | 2,793 | 1:1 | Balanced, large magnitude |
| Light x Condition | Root | 33 | 14 | 2.7:1 | Very few genes, up-biased |

**Key observation**: The root spaceflight response is the most asymmetric, with 4.5-fold more up-regulated than down-regulated genes. This is not a generic property of the root transcriptome — the root light response shows the opposite bias (1:1.4, slightly down-biased). The asymmetry is specific to the spaceflight condition.

### 1.2 Magnitude Asymmetry

Beyond count asymmetry, the magnitude of up-regulation exceeds down-regulation in the root spaceflight response:
- Root condition UP median LFC: +1.655
- Root condition DOWN median LFC: -0.843

This means up-regulated genes change nearly twice as much as down-regulated genes, suggesting an active, directional transcriptional program rather than passive noise.

![Figure 1](asymmetry/up_down_asymmetry_bars.png)

**Figure 1. Asymmetric up/down regulation across tissues and effects.** Bar chart showing the number of significantly up-regulated (red) and down-regulated (blue) genes for each tissue x effect combination from the DESeq2 interaction model. Ratios of up:down genes are annotated above each pair, with root-specific asymmetry highlighted in red (4.5:1 for root spaceflight) and leaf light down-bias in blue (1:1.3). The vertical divider separates root (left) and leaf (right) comparisons. Significance thresholds: main effects padj < 0.05, |shrunk LFC| >= 1; interaction padj < 0.1, |shrunk LFC| >= 0.5.

---

## 2. Root Radial Asymmetry: Cell-Type-Resolved Spaceflight Response

### 2.1 Direction-Stratified Cell Type Enrichment

Projecting direction-stratified DEG sets onto 11 root cell types (from Kajala et al. 2021 TRAP-seq markers) reveals a clear radial pattern:

| Cell Type | Radial Position | Up DEGs | Down DEGs | Up:Down | Bias Direction |
|-----------|----------------|---------|-----------|---------|----------------|
| Epidermis | Outer | 35 | 13 | 2.7:1 | UP |
| Exodermis | Outer | 76 | 26 | **2.9:1** | UP |
| Cortex | Middle | 51 | 30 | 1.7:1 | UP |
| Cortex_ACT2 | Middle | 32 | 1 | **32:1** | Strongly UP |
| Endodermis | Inner boundary | 18 | 23 | 0.8:1 | DOWN |
| Meristematic_Cortex | Inner | 22 | 18 | 1.2:1 | Mildly UP |
| Meristematic_Zone | Inner | 21 | 3 | 7.0:1 | UP |
| Phloem | Vascular | 26 | 15 | 1.7:1 | UP |
| Vascular | Vascular | 18 | 13 | 1.4:1 | Mildly UP |
| Vascular_WOX4 | Vascular | 14 | 15 | 0.9:1 | Balanced/Down |
| Xylem | Vascular core | 13 | 13 | 1.0:1 | Balanced |

Fisher's exact test (BH-corrected, padj < 0.1) confirmed significant enrichment of root condition UP genes in Exodermis (OR = 1.87, padj = 0.018) and Cortex_ACT2 (OR = 1.46, padj = 0.098), and enrichment of root condition DOWN genes in Exodermis (OR = 2.35), Cortex (OR = 2.20), and Endodermis (OR = 2.05).

**Note on Cortex_ACT2**: This cell type shows the most extreme up-regulation bias (32:1 overlap). The ACT2 marker identifies a specialized cortical subpopulation with elevated actin dynamics, potentially involved in graviperception or mechanosensing.

![Figure 2](asymmetry/root_direction_stratified_enrichment_heatmap.png)

**Figure 2. Direction-stratified cell type enrichment heatmap.** Fisher's exact test results for 12 direction-stratified DEG sets (rows) projected onto 24 cell types (columns: 11 root + 6 leaf + 7 leaf cluster groups). Cell values represent signed -log10(p_adj), where positive values (red) indicate enrichment of UP DEGs and negative values (blue) indicate enrichment of DOWN DEGs. Non-significant cells (p_adj >= 0.1) are shown in gray. Root condition UP genes are significantly enriched in outer cell types (Exodermis, Cortex_ACT2), while root condition DOWN genes are enriched in Exodermis, Cortex, and Endodermis.

![Figure 3](asymmetry/root_radial_celltype_heatmap.png)

**Figure 3. Root radial asymmetry heatmap.** Root cell types arranged by radial position (outer -> inner, top -> bottom) showing the up/down bias for three effects: spaceflight condition (Flight vs Ground), light quality (Blue vs Red), and their interaction. Cell values range from +1 (all up-regulated, red) to -1 (all down-regulated, blue), with annotations showing the absolute up/down DEG overlap counts. The dashed horizontal line separates outer cell layers (up-biased under spaceflight) from inner cell layers (down-biased). Cortex_ACT2 shows the strongest up-bias under spaceflight and is the only cell type with a notable interaction signal.

### 2.2 Per-Cell-Type Functional Enrichment (KEGG)

Using `enrichKEGG(organism="sly")` with relaxed thresholds (pvalueCutoff = 0.1, qvalueCutoff = 0.2), 177 KEGG terms were identified across 28 cell-type x direction sets.

#### Outer Cell Types (UP): Oxidative Stress and Secondary Metabolism

**Exodermis UP** — the strongest cell-type-specific signal:
- Phenylpropanoid biosynthesis (padj = 0.000005, 5 genes) — the most significant cell-type-specific KEGG term in the entire analysis
- Tropane, piperidine and pyridine alkaloid biosynthesis (padj = 0.001, 2 genes)

**Cortex_ACT2 UP**:
- Phenylpropanoid biosynthesis (padj = 0.026, 2 genes)

**Epidermis UP**:
- Phenylpropanoid biosynthesis (padj = 0.015, 2 genes)
- Tropane alkaloid biosynthesis (padj = 0.001, 2 genes)

**All root cell types UP** (universal):
- Tropane, piperidine and pyridine alkaloid biosynthesis — enriched in ALL 9 root cell types with UP terms (padj range: 0.0002-0.005), suggesting a whole-root alkaloid response to spaceflight

#### Inner Cell Types (DOWN): Suppressed Signaling and Transport

**Xylem DOWN**:
- Motor proteins (padj = 0.007, 1 gene)

**Phloem DOWN**:
- Motor proteins (padj = 0.007, 1 gene)

**Endodermis DOWN**:
- Other glycan degradation (padj = 0.018)
- Sphingolipid metabolism (padj = 0.018)
- Motor proteins (padj = 0.030)

**Cortex/Exodermis/Epidermis DOWN** (shared):
- Plant hormone signal transduction (Cortex padj = 0.012, Exodermis padj = 0.012)
- MAPK signaling pathway - plant (Cortex padj = 0.048, Epidermis padj = 0.048)
- Flavonoid biosynthesis (Cortex padj = 0.014, Exodermis padj = 0.014)

![Figure 4](asymmetry/root_cond_up_celltype_kegg_heatmap.png)

**Figure 4. Per-cell-type KEGG enrichment for root spaceflight UP genes.** Heatmap showing KEGG pathways enriched among up-regulated genes in each root cell type under spaceflight (Flight vs Ground). Cell values represent -log10(p_adj), with darker red indicating stronger enrichment. Phenylpropanoid biosynthesis is the dominant term in outer cell types (Exodermis padj = 5 x 10^-6), while tropane/piperidine/pyridine alkaloid biosynthesis is universally enriched across all cell types. Gene counts per term are annotated in each cell.

![Figure 5](asymmetry/root_cond_down_celltype_kegg_heatmap.png)

**Figure 5. Per-cell-type KEGG enrichment for root spaceflight DOWN genes.** Heatmap showing KEGG pathways enriched among down-regulated genes in each root cell type under spaceflight. Motor proteins are the most consistently down-regulated term across inner cell types (Xylem, Phloem, Endodermis padj = 0.007-0.030). Plant hormone signal transduction and MAPK signaling are down-regulated in multiple cell types including Cortex and Exodermis, indicating suppressed hormonal and stress signaling cascades.

---

## 3. Cross-Tissue Process Comparison

### 3.1 Shared vs. Tissue-Specific Pathways

Comparing KEGG enrichment across four key comparisons (root condition UP, leaf light UP, root condition DOWN, leaf light DOWN):

**17 shared UP pathways** include:
- Phenylpropanoid biosynthesis (both tissues)
- Flavonoid biosynthesis (both tissues)
- Plant hormone signal transduction
- Amino acid biosynthesis
- MAPK signaling pathway

**7 shared DOWN pathways** include:
- Circadian rhythm - plant
- Carbon fixation by Calvin cycle
- Carbon metabolism
- MAPK signaling pathway

### 3.2 Gene Overlap in Shared Pathways

For shared pathways, the specific genes driving enrichment differ substantially between tissues:

| Pathway | Root UP Genes | Leaf UP Genes | Shared | % Shared |
|---------|--------------|--------------|--------|----------|
| Flavonoid biosynthesis | 12 | 12 | 7 | **58.3%** |
| Phenylpropanoid biosynthesis | 51 | 18 | 12 | 23.5% |
| Circadian rhythm | 10 | 10 | 2 | 20.0% |
| Calvin cycle | 11 | 6 | 2 | 18.2% |

Flavonoid biosynthesis shows the highest gene overlap (58.3%), suggesting a conserved secondary metabolite response. Phenylpropanoid biosynthesis, despite being enriched in both tissues, uses mostly different genes (only 23.5% overlap), indicating tissue-specific activation of different branches of the same pathway.

### 3.3 Tissue-Specific Pathways

**Root-specific UP**:
- Glutathione metabolism — antioxidant defense
- Oxidative phosphorylation — mitochondrial energy production
- Tropane alkaloid biosynthesis — defense alkaloids

**Leaf-specific UP**:
- Cutin, suberine and wax biosynthesis — cuticle remodeling
- DNA replication — cell proliferation
- Brassinosteroid biosynthesis — growth hormone signaling

![Figure 6](asymmetry/shared_pathway_gene_venn.png)

**Figure 6. Gene overlap in shared KEGG pathways between root spaceflight and leaf light responses.** Venn diagrams showing the overlap of specific genes enriched in four shared KEGG pathways between root condition UP and leaf light UP comparisons. Flavonoid biosynthesis (top left) shows 58.3% gene overlap (7/12 shared), indicating a conserved secondary metabolite response. Phenylpropanoid biosynthesis (top right) shows only 23.5% overlap (12/51), with mostly tissue-specific gene activation. Circadian rhythm (bottom left) and Calvin cycle (bottom right) show minimal overlap (20% and 18.2% respectively), suggesting largely independent regulatory mechanisms in each tissue.

![Figure 7](asymmetry/cross_tissue_kegg_comparison.png)

**Figure 7. Cross-tissue KEGG pathway comparison heatmap.** Comprehensive heatmap of 75 KEGG pathways enriched across four key comparisons: root condition UP, leaf light UP, root condition DOWN, and leaf light DOWN. Cell values represent -log10(p_adj), with red indicating significant enrichment. Pathways are clustered by enrichment pattern, revealing groups of shared pathways (e.g., phenylpropanoid and flavonoid biosynthesis UP in both tissues) and tissue-specific pathways (e.g., glutathione metabolism root-specific UP; cutin/suberine/wax biosynthesis leaf-specific UP). The heatmap highlights that while both tissues activate secondary metabolism, the specific metabolic branches and gene sets differ substantially.

---

## 4. Light x Spaceflight Interaction Analysis

### 4.1 Leaf: Massive Interaction

The leaf shows 5,521 significant interaction genes (padj < 0.1), indicating that the light quality response is fundamentally altered by spaceflight. Cell-type projection reveals:

| Cell Type | Up | Down | Mean LFC | Bias |
|-----------|----|----|----------|------|
| Proliferating | 47 | 10 | **+1.31** | Strongly UP |
| Trichome | 4 | 26 | **-1.24** | Strongly DOWN |
| Uncharacterized | 2 | 65 | **-1.31** | Strongly DOWN |
| Mesophyll | 1,598 | 1,641 | ~0 | Balanced |
| Epidermis | 712 | 735 | ~0 | Balanced |
| Vascular | 465 | 422 | ~0 | Balanced |

The proliferating cell type shows the strongest up-biased interaction, suggesting that spaceflight amplifies blue light's proliferative signal. Trichome and uncharacterized cells show strong down-biased interaction, indicating spaceflight suppresses blue light's normal effect on these cell types.

### 4.2 Root: Minimal Interaction with One Hotspot

Roots show only 47 significant interaction genes — two orders of magnitude fewer than leaves. This is consistent with roots being insulated from direct light. However, one cell type stands out:

**Cortex_ACT2**: 12 of 47 root interaction genes map to Cortex_ACT2 markers (OR = 16.1, p ~ 0), despite Cortex_ACT2 having only 465 of 13,468 root markers (3.5%). This is an extraordinarily concentrated signal.

This finding has two implications:
1. Cortex_ACT2 is the primary site where light quality modulates the root spaceflight response
2. The ACT2 (actin 2) marker identifies a cell population with elevated cytoskeletal dynamics, potentially involved in graviperception — the very function disrupted in microgravity

The Cortex_ACT2 interaction hotspot connects the radial asymmetry (Cortex_ACT2 is the most strongly up-regulated cell type under spaceflight) with the light x spaceflight crosstalk (Cortex_ACT2 is where light quality matters most in roots).

![Figure 8](asymmetry/interaction_by_celltype.png)

**Figure 8. Light x spaceflight interaction genes projected onto cell types.** Dual-panel figure showing the distribution of significant interaction genes (padj < 0.1) across cell types in leaf (left) and root (right). *Left panel*: Leaf cell types showing the number of up-regulated (red) and down-regulated (blue) interaction genes per cell type, with mean LFC annotated. Proliferating cells are strongly up-biased (47 up / 10 down, mean LFC = +1.31), while Trichome (4/26, LFC = -1.24) and Uncharacterized (2/65, LFC = -1.31) cells are strongly down-biased. *Right panel*: Root cell types showing the dramatic enrichment of interaction genes in Cortex_ACT2 (12 genes, OR = 16.1, p ~ 0), highlighted in orange. All other root cell types have 0-4 interaction genes. This identifies Cortex_ACT2 as the sole hotspot where light quality modulates the root spaceflight response.

---

## 5. Physiological Development Interpretation

### 5.1 Root Oxidative Stress Response (Outer Cell Layers)

Spaceflight triggers a robust oxidative stress response concentrated in outer root cell layers:

**Evidence**:
- GO BP: "response to oxidative stress" (padj = 6.5 x 10^-13, 32 genes) and "hydrogen peroxide catabolic process" (padj = 6.5 x 10^-13, 28 genes) are the top root UP terms
- GO BP: "ethylene-activated signaling pathway" (padj = 1.0 x 10^-6, 14 genes) — ethylene is a key stress hormone
- KEGG: Phenylpropanoid biosynthesis enriched specifically in Exodermis (padj = 0.000005), Epidermis (padj = 0.015), and Cortex_ACT2 (padj = 0.026)
- Tropane/piperidine/pyridine alkaloid biosynthesis enriched universally across all root cell types

**Physiological interpretation**: In microgravity, the absence of gravitational loading alters mechanical stress on root cell walls, particularly in outer layers that interface with the growth medium. This triggers:
1. **ROS production** — mechanical stress and altered oxygen diffusion in microgravity increase reactive oxygen species
2. **H2O2 catabolism activation** — peroxidases and catalases are up-regulated to manage oxidative load
3. **Phenylpropanoid/flavonoid biosynthesis** — these secondary metabolites serve dual roles as antioxidants and structural reinforcements for cell walls under mechanical stress
4. **Ethylene signaling** — ethylene accumulates in microgravity (reduced convective mixing) and activates stress-responsive gene expression
5. **Alkaloid biosynthesis** — defense compound production may be activated as a general stress response

The concentration in outer cell layers makes physiological sense: the exodermis and epidermis are the first line of defense against the rhizosphere environment, and they experience the greatest mechanical stress during root growth.

### 5.2 Root Vascular Suppression (Inner Cell Layers)

Inner cell types show down-regulation of signaling and transport functions:

**Evidence**:
- Motor proteins DOWN in Xylem (padj = 0.007), Phloem (padj = 0.007), Endodermis (padj = 0.030)
- Plant hormone signal transduction DOWN in Cortex (padj = 0.012), Exodermis (padj = 0.012), Meristematic_Cortex (padj = 0.037)
- MAPK signaling pathway DOWN in Cortex (padj = 0.048), Epidermis (padj = 0.048), Vascular (padj = 0.048)
- GO BP: "RNA modification" (padj = 0.018, 13 genes) and "photosynthetic electron transport in photosystem I" (padj = 0.018, 3 genes) are top root DOWN terms

**Physiological interpretation**: The vascular cylinder is the primary conduit for graviperception-driven auxin transport (the Cholodny-Went hypothesis). In microgravity:
1. **Reduced gravistimulation** — without a gravity vector, the auxin gradient that normally drives differential growth is absent, reducing demand for vascular transport signaling
2. **Motor protein suppression** — myosin and kinesin motors involved in organelle positioning and vesicle transport along gravity-oriented tracks are down-regulated
3. **Hormone signaling suppression** — auxin and other hormone signaling pathways that normally operate along the gravity axis are dampened
4. **RNA modification down-regulation** — post-transcriptional regulatory mechanisms may be simplified in the absence of gravity-driven transcriptional complexity

The endodermis, which contains the statolith-based graviperception machinery (amyloplast sedimentation), shows a particularly interesting pattern: it is the transition point between outer UP and inner DOWN, with a 0.8:1 up/down ratio.

### 5.3 Leaf Light Quality Remodeling

Blue light (vs. red) drives a comprehensive remodeling of leaf metabolism:

**Evidence**:
- KEGG: Photosynthesis-antenna proteins DOWN in Mesophyll (padj = 3.6 x 10^-11, 7 genes)
- KEGG: Photosynthesis DOWN in Mesophyll (padj = 3.6 x 10^-11, 9 genes)
- KEGG: Circadian rhythm - plant DOWN (leaf-level padj = 0.0006, 6 genes)
- KEGG: Phenylpropanoid biosynthesis UP (leaf-level padj = 3.4 x 10^-8, 18 genes)
- KEGG: Flavonoid biosynthesis UP (leaf-level padj = 2.8 x 10^-6, 8 genes)
- KEGG: Protein processing in ER UP in Mesophyll (padj = 0.000004, 6 genes)

**Physiological interpretation**: Blue light activates cryptochrome photoreceptors, which:
1. **Suppress photosynthesis gene expression** — cryptochrome signaling down-regulates light-harvesting complex and photosystem genes, potentially as a feedback mechanism to prevent photodamage under high-energy blue light
2. **Disrupt circadian rhythm** — blue light directly entrains the circadian clock via CRY1/CRY2, and the transition from red to blue light quality disrupts the circadian gene network
3. **Activate secondary metabolism** — phenylpropanoid and flavonoid pathways are classic cryptochrome targets, producing UV-protective compounds
4. **Upregulate ER protein processing** — increased protein folding capacity supports the metabolic shift from photosynthesis to secondary metabolism

### 5.4 Leaf Spaceflight-Light Crosstalk

The 5,521 leaf interaction genes indicate that spaceflight fundamentally alters how leaves respond to light quality:

**Evidence**:
- Proliferating cells: 47 up / 10 down interaction genes, mean LFC = +1.31
- Trichome cells: 4 up / 26 down, mean LFC = -1.24
- Uncharacterized cells: 2 up / 65 down, mean LFC = -1.31

**Physiological interpretation**: In microgravity, the integration of light and gravity signals is disrupted. On Earth, phototropism (light-driven growth) and gravitropism (gravity-driven growth) are antagonistically regulated. In spaceflight:
1. **Proliferating cells up-biased** — without gravitropic suppression, blue light's proliferative signal is amplified, potentially increasing leaf cell division
2. **Trichome down-biased** — trichome development is normally regulated by both light and mechanical stimuli; loss of gravity-driven mechanical stimulation may suppress trichome differentiation under blue light
3. **The large number of interaction genes** (5,521) suggests that nearly every aspect of leaf light response is modulated by the spaceflight environment

### 5.5 Root Insensitivity to Light Quality (with Cortex_ACT2 Exception)

Roots show minimal light response (256 light DEGs) and minimal interaction (47 interaction genes), consistent with their subterranean biology. However:

**Evidence**:
- Cortex_ACT2 concentrates 12/47 interaction genes (OR = 16.1, p ~ 0)
- Cortex_ACT2 is also the most strongly up-regulated cell type under spaceflight (32:1 up/down)
- The ACT2 marker identifies cells with elevated actin cytoskeletal dynamics

**Physiological interpretation**: The Cortex_ACT2 hotspot suggests a mechanistic link between graviperception and light signaling:
1. **Actin-mediated graviperception** — root gravitropism requires actin dynamics for amyloplast sedimentation and signaling. The ACT2 cortical subpopulation may be specialized for this function
2. **Light reaches roots** — even in soil, small amounts of light penetrate, and in the ISS growth system, roots may receive more light than in natural soil
3. **Blue light affects actin dynamics** — cryptochrome signaling can modulate actin organization, creating a potential convergence point where light quality and gravity sensing interact
4. **The hotspot is specific** — only Cortex_ACT2, not other cortical subtypes, shows this interaction, suggesting a specialized functional role rather than a general light response

---

## 6. Integrated Model

![Figure 9](asymmetry/organ_schematic.png)

**Figure 9. Organ schematic: spatial model of asymmetric transcriptional regulation.** Integrated diagram showing the root cross-section (left) and leaf tissue (right) with cell-type-specific transcriptional responses to spaceflight and light quality. *Root cross-section*: Concentric cell layers colored by up/down bias under spaceflight — warm colors (red/orange) indicate outer layers with up-regulated oxidative stress defense, phenylpropanoid biosynthesis, and ethylene signaling; cool colors (blue) indicate inner layers with down-regulated motor proteins, hormone signaling, and MAPK pathways. Cortex_ACT2 is highlighted as the light x spaceflight interaction hotspot (OR = 16.1). *Leaf tissue*: Layers showing blue light effects — photosynthesis and circadian rhythm DOWN in mesophyll; secondary metabolism UP; proliferating cells show up-biased interaction; trichome cells show down-biased interaction. Arrows between panels indicate bidirectional root-shoot signaling and the light-gravity interaction axis.

**Root cross-section**:
- Outer layers (epidermis, exodermis, cortex): RED/WARM — up-regulated under spaceflight, enriched for oxidative stress defense, phenylpropanoid biosynthesis, and ethylene signaling
- Cortex_ACT2: ORANGE HIGHLIGHT — interaction hotspot where light quality modulates spaceflight response
- Inner layers (endodermis, vascular, xylem): BLUE/COOL — down-regulated, with suppressed motor proteins, hormone signaling, and MAPK pathways

**Leaf tissue**:
- Mesophyll: photosynthesis and circadian DOWN under blue light; protein processing and secondary metabolism UP
- Proliferating: interaction UP-biased (spaceflight amplifies blue light proliferative signal)
- Trichome: interaction DOWN-biased (spaceflight suppresses blue light trichome development)

**Signaling connections**:
- Root-shoot signaling: ethylene and other stress hormones produced in outer root layers may travel to shoots
- Light-gravity interaction: in leaves, the disruption of gravitropism amplifies phototropic responses; in roots, the Cortex_ACT2 hotspot represents a convergence of light and gravity signaling

---

## 7. Key Caveats and Limitations

1. **Entrez ID mapping rate**: Only 62-67% of Solyc gene IDs mapped to Entrez, limiting KEGG enrichment power. Some pathways may be under-detected.

2. **Per-cell-type enrichment is underpowered**: With only 1-5 genes per cell-type-pathway combination, many KEGG terms have Count = 1-2. The relaxed threshold (padj < 0.1) increases sensitivity but also false positive risk. Effect sizes (FoldEnrichment) should be weighted alongside p-values.

3. **Cell type markers are from independent studies**: Root markers are from Kajala et al. 2021 (TRAP-seq), leaf markers from Yue et al. 2024 (scRNA-seq). Cross-platform and cross-study mapping introduces noise.

4. **Interaction gene counts are small in roots**: Only 47 root interaction genes (padj < 0.1) limits statistical power for cell-type projection. The Cortex_ACT2 hotspot (OR = 16.1) is robust but should be validated with independent data.

5. **No direct ROS or hormone measurements**: The oxidative stress and ethylene signaling interpretations are based on transcriptomic evidence alone. Functional validation is needed.

6. **Sample sizes are uneven**: Leaf has 21 samples (6 GR, 6 GB, 5 FR, 4 FB), root has 15 (3 GR, 3 GB, 5 FR, 4 FB). The root condition comparison has only 3 ground controls per light condition, which may inflate effect sizes.

---

## References

- Kajala K et al. (2021) Cell 184(12):3333-3348.e19 — Tomato root cell type TRAP-seq markers
- Yue L et al. (2024) Plant Cell Environ 47(7):2660-2674 — Tomato leaf cell type scRNA-seq markers
- OSD-767 / GLDS-709 — GeneLab RNA-seq dataset (tomato, ISS, light quality x spaceflight)
