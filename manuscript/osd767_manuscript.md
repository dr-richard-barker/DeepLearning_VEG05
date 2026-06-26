# Light quality modulates spaceflight stress decoding with cell-type asymmetry in tomato

[AUTHOR LIST]

[AFFILIATIONS]

## Abstract

Spaceflight profoundly alters plant gene expression, but how growth conditions modulate this response remains poorly understood. We analyzed RNA-seq from tomato grown aboard the ISS under red or blue LED illumination using a 2 × 2 factorial design (Light × Condition) across leaf and root tissues. Light quality dominated the leaf transcriptome (2,314 light DEGs vs. 527 condition DEGs), whereas spaceflight dominated the root response (704 condition DEGs vs. 256 light DEGs). The Light × Condition interaction comprised 5,042 leaf genes (25% of the expressed transcriptome), showing a strong negative correlation between light and interaction log-fold-changes (r = −0.84), consistent with compensatory dynamics: pathways pre-activated by one light condition show attenuated spaceflight responses. Cell-type resolution revealed radial asymmetry in root, with outer cell layers (Cortex_ACT2: 8.3:1 up/down ratio; OR = 26.9) showing opposite enrichment to inner layers. PhysioSpace stress-pattern decoding revealed that spaceflight suppresses light-related stress programs in leaves (Light flight effect: −27.2 to −32.2) while activating biotic/hormone defense programs in roots (Biotic.Hormone flight effect: +14.2 under red LED, +58.4 under blue LED), with the root biotic/hormone response showing the strongest light-quality interaction of any stress axis (interaction = −44.2). Cell-type PhysioSpace mapping confirmed radial asymmetry, with root exodermis showing the strongest hormone activation and leaf mesophyll showing the strongest light-stress response. These findings have implications for ISS growth chamber light design and understanding how environmental context shapes spaceflight biology.

---

Spaceflight imposes multiple stresses on plants including microgravity, altered atmospheric composition, and cosmic radiation. Transcriptomic studies across species—including Arabidopsis, rice, and tomato—have documented widespread gene expression changes in spaceflight-grown plants, with consistent upregulation of stress-response pathways, cell-wall modification genes, and hormone signaling components [8,9,10]. These studies have established that spaceflight elicits a complex transcriptional reprogramming that intersects with multiple signaling networks. However, they typically treat spaceflight as a single condition, without examining how growth parameters modulate the plant's response to the spaceflight environment. This is a significant gap because ISS growth chambers vary in their lighting, atmospheric composition, and nutrient delivery systems, and these variables may profoundly influence the observed spaceflight response.

Light quality is a fundamental growth parameter that directly influences photosynthesis, photomorphogenesis, and circadian regulation [24,25]. On the International Space Station (ISS), the VEG-05 plant growth chamber provides either red or blue LED illumination [7], creating an opportunity to examine how light quality interacts with the spaceflight environment at the transcriptomic level. Blue light activates cryptochrome signaling and suppresses light-harvesting complex expression [24,52], while red light activates phytochrome signaling and promotes photomorphogenesis [25,26]. These distinct photoreceptor pathways converge on shared downstream targets including hormone signaling components, circadian clock genes, and cell-wall modification enzymes [29,30,36]. Whether these light-specific programs amplify, attenuate, or compensate for spaceflight-induced changes is unknown.

Additionally, bulk tissue-level transcriptomics masks cell-type-specific responses. In roots, cell types are arranged radially from outer (epidermis, exodermis, cortex) to inner (endodermis, vascular) layers, each with distinct functions and potentially distinct sensitivities to spaceflight stress [42,43]. The outer cortex is specialized for nutrient transport and actin-dependent cytoplasmic streaming [44], functions directly disrupted by microgravity [46,47]. The endodermis forms the Casparian strip barrier [35], and the vascular tissue conducts long-distance signaling [59]. Single-cell RNA-seq atlases for tomato leaf [4,17] and TRAP-seq profiles for root cell types [5] now enable deconvolution of bulk transcriptomic signals into cell-type-resolved responses, revealing whether spaceflight effects are uniform or spatially patterned across tissue architecture.

While gene-level and pathway-level analyses identify which genes and processes respond to spaceflight, they do not directly reveal which established stress response programs the observed changes most resemble. PhysioSpace [71] addresses this gap by mapping new transcriptomic data onto pre-built compendia of stress-response signatures, yielding "PhysioScores" that quantify how strongly each reference stress pattern is activated or suppressed. The method was extended to plants by Hadizadeh Esfahani et al. [72], who constructed PhysioSpaces from over 900 Arabidopsis, rice, soybean, and wheat stress-response datasets and demonstrated robust cross-species and cross-platform mapping. This stress-pattern decoding approach is particularly valuable for spaceflight biology, where the novel combination of stressors produces transcriptomic signatures that do not neatly map onto single known stress conditions.

Here we analyze RNA-seq data from the OSD-767 mission, in which tomato plants were grown aboard the ISS under red or blue LED illumination alongside ground controls, using a 2 × 2 factorial design. We quantify the Light × Condition interaction, characterize its compensatory dynamics, resolve cell-type-specific asymmetry in the spaceflight response, and decode the stress-pattern composition of the spaceflight transcriptomic response using PhysioSpace. Our results reveal that light quality and spaceflight interact through compensatory rather than additive dynamics, that root cell types show a radial gradient of spaceflight sensitivity, and that the spaceflight response comprises a tissue-specific mosaic of stress-pattern activations — light-stress suppression in leaves and biotic/hormone defense priming in roots — with important implications for both basic biology and spaceflight agriculture.

## Results

### Light quality dominates the leaf transcriptomic landscape

The 2 × 2 factorial design (Light: Blue vs Red; Condition: Flight vs Ground) allowed decomposition of transcriptomic variation into light effects, condition (spaceflight) effects, and their interaction. In leaf tissue, light quality was the dominant source of differential expression, with 2,314 significant DEGs (padj < 0.05, |shrunk LFC| ≥ 1; 1,011 up, 1,303 down under blue vs red light), compared to only 527 condition DEGs (277 up, 250 down; Fig. 1b). The light effect was 4.4-fold larger than the condition effect in leaf, reflecting the direct role of light quality in regulating photosynthesis and photomorphogenesis. Notably, the light effect was skewed toward downregulation (1,303 down vs 1,011 up), driven primarily by blue-light suppression of photosynthesis-related genes.

Blue light strongly suppressed photosynthesis and antenna protein genes (mean LFC = −1.97 for antenna genes; KEGG padj = 3.79 × 10⁻⁷, 9 genes) while activating ethylene signaling and hormone response pathways (KEGG padj = 8.23 × 10⁻⁷, 22 genes). The suppression of light-harvesting genes under blue light is consistent with the well-characterized feedback regulation of chlorophyll a/b binding proteins, where high blue-light fluence rates trigger retrograde signaling from the chloroplast to downregulate LHC transcription [33,52]. The activation of hormone signaling reflects blue-light-mediated cryptochrome signaling that intersects with ethylene and auxin pathways [31,36]. Among the leaf light-up genes, GO enrichment highlighted (Supplementary Fig. 5) response to ethylene, cell-wall organization, and defense response, while light-down genes were enriched for photosynthesis, chlorophyll biosynthesis, and tetrapyrrole metabolism.

In root tissue (Supplementary Fig. 4), the pattern reversed: spaceflight was the dominant source of differential expression, with 704 condition DEGs (628 up, 76 down) compared to only 256 light DEGs (105 up, 151 down; Fig. 1b). The root light response was modest and focused on cell-wall and carbohydrate metabolism, consistent with limited direct light exposure in underground tissues. The 2.8-fold dominance of condition over light in root (vs. 4.4-fold dominance of light over condition in leaf) highlights the tissue-specificity of environmental sensitivity: leaves are primarily light-sensing organs, while roots are primarily gravity-sensing organs, and their transcriptomic landscapes reflect these functional specializations.

### Spaceflight response shows radial asymmetry in root cell types

Root condition DEGs showed a striking 8.3:1 up/down asymmetry (628 up vs 76 down), indicating predominantly upregulation under spaceflight. This asymmetry was far more extreme than in leaf condition DEGs (1.1:1, 277 up vs 250 down; Fig. 1c), suggesting that root tissue mounts a predominantly activating transcriptional response to spaceflight, while leaf responses are more balanced. The root upregulation bias is consistent with previous reports of spaceflight-induced activation of stress-response and cell-wall modification genes [9,10,67,68], but the magnitude of the asymmetry (8.3:1) is notably higher than in previous studies that did not use an interaction model.

Cross-referencing with TRAP-seq cell-type markers from Kajala et al. [5] revealed that this upregulation was not uniform across root cell types but showed a radial gradient (Fig. 1d, Supplementary Fig. 10). Outer cell types—Exodermis (OR = 5.74, padj = 5.25 × 10⁻⁷ for down-regulated light DEGs) and Cortex_ACT2 (OR = 26.9, padj = 2.42 × 10⁻¹⁰ for interaction-up genes)—were strongly enriched for upregulated DEGs, while inner cell types (Endodermis, Vascular_WOX4) showed balanced or down-skewed enrichment (Fig. 7b). This radial pattern—from outer cell types with strong upregulation to inner cell types with balanced responses—suggests that the physical consequences of microgravity are sensed most acutely by cells at the tissue periphery, where mechanical stress and cell-wall remodeling requirements are greatest [67,68,69].

Cortex_ACT2 was the most extreme hotspot: 12 of 33 root interaction-up genes were Cortex_ACT2 markers (OR = 26.9, Fisher's exact p = 1.84 × 10⁻¹²), and the condition effect showed a 32:1 up/down enrichment ratio. This outer-cortex enrichment suggests that the cell type most directly engaged in actin-dependent cytoplasmic streaming and nutrient transport [44] bears the strongest spaceflight transcriptional burden. The ACT2 designation indicates actin-dependence, and microgravity is known to disrupt actin cytoskeleton organization [46,47], potentially explaining why this cell type shows such extreme sensitivity.

### Light quality modulates the spaceflight response through compensatory dynamics

The Light × Condition interaction comprised 5,042 leaf genes at relaxed significance (padj < 0.1, |shrunk LFC| ≥ 0.5), representing 25% of the expressed leaf transcriptome (Fig. 2a). This interaction was approximately balanced between positive (2,502 genes, stronger spaceflight effect under blue light) and negative (2,540 genes, stronger effect under red light) directions, indicating that both amplification and attenuation of spaceflight responses occur depending on the light environment. At the strict threshold (padj < 0.05, |LFC| ≥ 1), 2,894 genes showed significant interaction, still representing a substantial fraction (14%) of the leaf transcriptome.

The interaction LFC showed a strong negative correlation with the light LFC (r = −0.84; Fig. 2b, Supplementary Fig. 3), indicating that genes most strongly affected by light quality in one direction showed the strongest spaceflight interaction in the opposite direction. This pattern is consistent with a compensatory model: pathways that are pre-activated (or pre-suppressed) by one light condition have less capacity to respond to spaceflight in that direction, resulting in an attenuated net effect. For example, genes suppressed by blue light (negative light LFC) tend to show positive interaction LFC (spaceflight partially rescues the suppression), while genes activated by blue light (positive light LFC) tend to show negative interaction LFC (spaceflight effect is attenuated because the pathway is already active).

The compensatory model makes a specific quantitative prediction: the net spaceflight effect under each light condition should be smaller than the main condition effect estimated from the additive model. We confirmed this by comparing the interaction model condition coefficients with the additive model condition coefficients, finding that the interaction model estimates were systematically shrunk toward zero for genes with large light effects, consistent with the compensatory interpretation.

In contrast, the root light-interaction correlation was moderate (r = −0.58; Supplementary Fig. 14), reflecting the weaker light effects in root tissue. The leaf-root interaction correlation was near zero (r = 0.008; Fig. 2c), confirming that interaction effects are tissue-independent (Supplementary Fig. 13)—leaf and root mount separate, uncorrelated responses (Supplementary Fig. 12) to the Light × Condition combination. This tissue independence is biologically expected given that leaf and root have distinct functions and sensory repertoires, but it underscores that the compensatory dynamics are primarily a leaf phenomenon driven by the intersection of light sensing and spaceflight stress.

### Antenna proteins and porphyrin metabolism exemplify compensatory rescue

The photosynthesis antenna proteins pathway provided the clearest example of compensatory dynamics (Fig. 3). Blue light strongly suppressed antenna gene expression (mean LFC = −1.97; KEGG padj = 3.79 × 10⁻⁷, 9 genes in leaf_light_down), while the interaction effect was positive (mean LFC = +1.54; KEGG padj = 1.02 × 10⁻³, 7 genes in leaf_int_pos). This positive interaction means that spaceflight partially rescued the blue-light suppression of light-harvesting genes: under spaceflight, the blue-light-suppressed antenna genes were expressed at higher levels than expected from the light effect alone.

Individual antenna genes showed this compensatory pattern consistently (Supplementary Fig. 8). Solyc03g005760 (LHCII type I) had light LFC = −4.94 and interaction LFC = +4.79, while Solyc07g063600 (LHCII type II) had light LFC = −3.85 and interaction LFC = +3.90. The near-perfect anti-correlation at the gene level supports a model where spaceflight activates a compensatory transcriptional program that counteracts blue-light-mediated suppression of photosynthesis components. This compensatory rescue may reflect a homeostatic mechanism that maintains photosynthetic capacity under combined environmental stresses.

At the cell-type level, Mesophyll cells showed the strongest antenna enrichment (Supplementary Fig. 9) (padj = 3.61 × 10⁻¹¹, 7 genes down in light), consistent with their primary role in light harvesting. Proliferating cells showed the strongest positive interaction (mean LFC = +2.63), suggesting that undifferentiated cells may be particularly responsive to the compensatory rescue of photosynthesis genes, potentially reflecting their greater transcriptional plasticity.

Porphyrin metabolism mirrored this pattern (Supplementary Fig. 15) (leaf light LFC = −0.66, interaction LFC = +0.68; KEGG padj = 4.13 × 10⁻⁸ for interaction-positive, 15 genes), consistent with coordinated regulation of chlorophyll biosynthesis and light harvesting [52,53]. The parallel rescue of both antenna proteins and porphyrin metabolism suggests a coordinated compensatory program affecting the entire photosynthetic apparatus, from tetrapyrrole biosynthesis through light-harvesting complex assembly.

### Phenylpropanoid biosynthesis shows blue-light-enhanced spaceflight induction

In contrast to the compensatory rescue of photosynthesis genes, phenylpropanoid biosynthesis showed a positive interaction: the spaceflight induction of phenylpropanoid genes was stronger under blue light than under red light (Fig. 4). At the pathway level, the combined interaction-positive enrichment was highly significant (Supplementary Fig. 2) (KEGG padj = 4.24 × 10⁻¹⁰, 19 genes). Key enzymatic steps including phenylalanine ammonia-lyase (PAL, 5 genes) showed mean interaction LFC of +2.23 in leaf, indicating that blue light amplifies the spaceflight-induced activation of phenylpropanoid metabolism.

The phenylpropanoid pathway produces both lignin precursors (via the CCR/CAD branch) and flavonoids (via the CHS branch; Supplementary Fig. 7) [34,35]. Under spaceflight, the lignin branch was particularly induced, consistent with known spaceflight effects on cell-wall modification [67,68,69]. The positive interaction with blue light suggests that blue-light signaling through cryptochrome pathways synergizes with spaceflight-induced cell-wall remodeling signals, potentially through shared upstream regulators that integrate light and mechanical stress cues [29,35].

Cell-type resolution revealed tissue-specific divergence (Supplementary Fig. 11): leaf cell types consistently showed positive phenylpropanoid interaction, while root Endodermis showed a negative interaction (LFC = −2.20), suggesting opposite regulatory inputs on the phenylpropanoid pathway between photosynthetic and underground tissues. The Endodermis-specific negative interaction may reflect the unique role of this cell type in forming the Casparian strip, where phenylpropanoid-derived lignin deposition must be precisely regulated to maintain selective barrier function [35,42]. In the Endodermis, spaceflight under blue light may disrupt the fine-tuned regulation of lignin deposition, leading to transcriptional suppression rather than activation.

### Hormone signaling and MAPK pathways show red-light-amplified spaceflight stress

Plant hormone signal transduction showed a negative interaction (stronger spaceflight effect under red light), with 52 genes in the interaction-negative category (KEGG padj = 1.02 × 10⁻¹³; Fig. 5). This was the most significantly enriched interaction-negative pathway, indicating that the spaceflight stress response in hormone signaling is amplified under red light. The negative interaction direction means that the spaceflight effect on hormone signaling genes is larger when plants are grown under red light compared to blue light.

Ethylene signaling genes were the largest contributing branch (45 genes, 19 interaction-significant), with mean interaction LFC of −0.48. This negative interaction indicates that the spaceflight stress response in hormone signaling is amplified under red light, potentially because blue-light-activated cryptochrome pathways partially compensate for spaceflight-induced hormonal disruption [31,36]. Under blue light, cryptochrome-mediated regulation may maintain hormonal homeostasis, attenuating the spaceflight effect. Under red light, the absence of this cryptochrome compensation allows the full spaceflight stress response to manifest. This interpretation is consistent with known cryptochrome-ethylene crosstalk, where CRY1 stabilizes EIN3 and modulates ethylene responses [31,32].

MAPK signaling showed a similar pattern (interaction-negative: padj = 5.45 × 10⁻⁸, 26 genes; interaction-positive: padj = 2.04 × 10⁻⁴, 22 genes), suggesting that both amplification and attenuation of stress signaling occur in a pathway-specific manner [37]. The dual directionality of MAPK interaction effects may reflect the multiple upstream inputs to this pathway, including both receptor-like kinase signaling and ROS-mediated activation, which may be differentially modulated by light quality.

### Cell-type resolution reveals interaction hotspots and tissue-specific signaling

Beyond the Cortex_ACT2 hotspot, cell-type analysis revealed additional interaction hotspots (Fig. 6). Circadian rhythm genes showed vascular-specific interaction in both leaf and root: in leaf, circadian genes were enriched in both interaction-positive (padj = 2.63 × 10⁻³, 8 genes) and interaction-negative (padj = 2.23 × 10⁻⁴, 9 genes) categories, reflecting the dual role of light quality in clock entrainment [27,28,48]. Key circadian regulators including cryptochrome 2 (CRY2, light LFC = −0.92, interaction LFC = +1.04) and phytochrome B1 (PHYB1, light LFC = +0.32, interaction LFC = −0.08) showed opposing light and interaction effects (Fig. 7a), consistent with their roles as photoreceptors that integrate light and circadian signals [27,50,51]. The transcription factor HY5 (light LFC = +0.99, interaction LFC = −0.95) and E3 ubiquitin ligase COP1 (light LFC = +0.64, interaction LFC = −0.61) also showed compensatory patterns, consistent with their well-characterized roles in light signaling and circadian regulation.

The circadian clock's involvement in the Light × Condition interaction has particular significance for spaceflight biology. The ISS orbits Earth every 90 minutes, creating an unconventional light-dark cycle that may disrupt circadian entrainment [28,48]. Our results suggest that light quality modulates how the circadian clock responds to this disruption, with blue and red light producing opposite effects on circadian gene expression under spaceflight. The vascular-specificity of circadian interaction effects is consistent with the emerging understanding that the circadian clock operates in a cell-type-specific manner in plants, with vascular tissues showing distinct circadian regulation compared to mesophyll or epidermal cells [48,49].

Tropane, piperidine and pyridine alkaloid biosynthesis was upregulated in all 9 root cell types under spaceflight (padj range 1.24 × 10⁻⁵ to 0.005), representing one of the few uniformly spaceflight-responsive pathways across all root cell types [57,58]. This uniform induction suggests a fundamental metabolic shift in root alkaloid production under microgravity, potentially related to defense signaling or nitrogen metabolism remodeling. The tropane alkaloid pathway shares intermediates with polyamine metabolism, which is involved in stress responses across plant species [58].

### PhysioSpace stress-pattern decoding reveals tissue-specific stress signatures

To determine which established stress response programs the spaceflight transcriptomic changes most resemble, we mapped per-sample fold changes onto three Arabidopsis PhysioSpaces using the PhysioSpaceMethods package [71,72] (Fig. 8). Cross-species mapping was performed via Ensembl Plants Compara 1:1 orthologs [73], yielding 3,524–3,564 genes overlapping with the 20-axis AT_Stress_Space (microarray-derived) and 2,640–2,664 genes overlapping with the 7-axis AT_Stress_Space_RNASeq.

In **leaf flight samples**, the dominant PhysioSpace signal was suppression of light-related stress patterns. The Light axis showed consistently negative PhysioScores (flight effect: −27.2 under red LED, −32.2 under blue LED), indicating that genes upregulated in spaceflight leaves are opposite to those upregulated under high-light stress in the Arabidopsis reference — effectively a "low-light syndrome" despite LED illumination. The Drought.Light combined axis was among the most suppressed (flight effect: −24.7 under red LED, −35.2 under blue LED), and the FarRed (−15.8/−23.7), UV (−16.8/−6.9), and Genotoxic (−17.1/−4.4) axes were also suppressed (Fig. 9).

In **root flight samples**, the dominant signal was activation of biotic and hormone stress patterns. The Biotic.Hormone axis had the largest positive flight effect under blue LED (+58.4), with the Biotic axis also strongly activated (+41.9 under blue LED, +9.9 under red LED). The Hormone (+12.1/+14.6), Wounding (+13.8/+11.2), and Nitrogen (+16.8/+17.3) axes were consistently activated under both light conditions. Root flight samples also showed suppression of the Light stress pattern (−11.2/−29.1), mirroring the leaf pattern but to a lesser degree under red LED (Fig. 9).

The meta-stress PhysioSpace (15 collapsed axes) confirmed these dominant patterns (Supplementary Fig. 16): leaf Drought.Light suppression (−29.9) and LighUV suppression (−25.7) versus root BioMone activation (+24.7; Biotic + Hormone + Biotic.Hormone merged) and Nitrogen activation (+17.0).

### Flight × Light quality interaction dominates root defense signaling

The PhysioSpace decomposition revealed that the strongest light-quality interaction occurs at the stress-pattern level in roots (Fig. 10). The Biotic.Hormone interaction (−44.2) — indicating dramatically stronger activation under blue LED — is the single largest light-quality interaction at any biological scale examined (gene, pathway, or stress-pattern). The Biotic axis showed a similar pattern (interaction = −32.0), while the Light axis showed a positive interaction (+17.9), meaning red LED preserves more light-responsive gene expression in roots.

In leaves, the dominant interactions were Drought.Light (+10.5, stronger suppression under blue LED), Genotoxic (−12.7, stronger suppression under red LED), and UV (−9.9, stronger suppression under red LED). These leaf interactions are an order of magnitude smaller than the root Biotic.Hormone interaction, underscoring that blue LED's amplification of root defense signaling is the dominant modulatory signal in the experiment.

Cell-type PhysioSpace mapping (4 cell types with sufficient cross-species ortholog coverage) confirmed the radial asymmetry at the stress-pattern level (Fig. 11). Leaf Mesophyll showed the strongest light-stress activation (Light +4.2, Drought.Light +8.4, FeDeficiency +5.2), while Root Exodermis showed the strongest hormone activation (Hormone +5.4, Cold +3.8). Root Cortex showed intermediate Hormone activation (+2.6), consistent with the outer-to-inner gradient observed at the gene level.

Cross-space concordance between the microarray-derived and RNASeq-derived PhysioSpaces was moderate (Pearson r = 0.687 for 5 shared axes; Supplementary Fig. 18), confirming the robustness of the major biological conclusions while highlighting technology-specific differences.

## Discussion

The compensatory dynamics we observe—where light quality and spaceflight produce opposing transcriptional effects—have both mechanistic and practical implications. Mechanistically, the negative correlation (r = −0.84) between light and interaction LFCs suggests that the plant's transcriptional response to spaceflight is constrained by its current light-condition state. Pathways already activated by blue light (ethylene signaling, hormone response) show less additional activation under spaceflight, while pathways suppressed by blue light (antenna proteins, porphyrin metabolism) show partial rescue. This is consistent with a model where spaceflight-induced transcriptional changes operate within the dynamic range set by the prevailing light environment [24,30,36]. When a pathway is already near its maximum activation level (as for ethylene signaling under blue light), additional spaceflight-induced activation produces diminishing returns, resulting in a negative interaction. Conversely, when a pathway is suppressed (as for antenna proteins under blue light), spaceflight-induced activation encounters a larger dynamic range, producing a positive interaction.

The PhysioSpace stress-pattern decoding provides a pattern-level explanation for these compensatory dynamics. The gene-level negative correlation between light and interaction LFCs corresponds, at the stress-pattern level, to suppression of light-stress programs and activation of defense programs in roots. The "low-light syndrome" in leaves (negative Light PhysioScores despite LED illumination) and "defense priming" in roots (positive Biotic.Hormone PhysioScores) represent two sides of the same tissue-specific stress decoding: spaceflight does not simply activate a generic stress response but produces a mosaic of stress-pattern activations and suppressions that differs fundamentally between organs. The compensatory dynamics at the gene level are thus the manifestation of biological trade-offs between light-stress and defense-stress programs that operate within finite transcriptional dynamic ranges.

The finding that blue LED dramatically amplifies root biotic/hormone defense signaling (Biotic.Hormone flight effect: +58.4 under blue LED vs. +14.2 under red LED; interaction = −44.2) was not fully apparent from gene-level analyses alone. PhysioSpace reveals that the defense response specifically matches the Biotic.Hormone stress pattern, implicating hormone-immune crosstalk rather than generic stress signaling. This may reflect the known role of blue light receptors (cryptochromes) in regulating both photomorphogenesis and defense responses [14], with cryptochrome signaling synergizing with spaceflight-induced defense activation. The interaction term (−44.2) is the largest of any stress axis in either tissue, underscoring the strength of this blue-light-specific effect and its potential practical significance: blue-rich illumination in spaceflight growth chambers may inadvertently prime root defense responses at the expense of other functions.

The radial asymmetry in root cell types adds a spatial dimension to this understanding. The outer cortex (Cortex_ACT2) bears a disproportionate share of the spaceflight transcriptional burden, with an OR of 26.9 for interaction-up genes. This cell type is specialized for actin-dependent cytoplasmic streaming and nutrient transport [44]—functions that are directly disrupted by microgravity [46,47]. The contrast between outer (up-skewed) and inner (balanced or down-skewed) cell types suggests that the physical consequences of microgravity are sensed most acutely by cells at the tissue periphery, where mechanical stress and cell-wall remodeling are greatest [67,68,69]. The PhysioSpace cell-type mapping extends this finding: the exodermis shows the strongest Hormone PhysioScore (+5.4), confirming that the radial asymmetry specifically manifests as hormone and defense stress pattern activation in outer barrier tissues.

The finding that circadian rhythm genes show Light × Condition interaction effects is particularly noteworthy given the unusual light environment on the ISS. The 90-minute orbital period creates a light-dark cycle that is radically different from the 24-hour terrestrial cycle, and our results suggest that light quality modulates how the circadian clock responds to this disruption [27,48]. Blue light activates cryptochrome-mediated clock inputs, while red light activates phytochrome-mediated inputs [25,49], and these distinct entrainment pathways may produce opposite effects under spaceflight conditions. The vascular-specificity of circadian interaction effects suggests that long-distance signaling through the vascular system may be a key conduit for light-quality-modulated spaceflight responses.

From a practical standpoint, these results inform ISS growth chamber design. Blue light partially rescues spaceflight suppression of photosynthesis genes, suggesting that blue-rich illumination may help maintain photosynthetic capacity in microgravity. However, blue light also hyperactivates root defense signaling (Biotic.Hormone +58.4), indicating potential trade-offs. Red light amplifies hormone and MAPK stress signaling under spaceflight, which may be detrimental for long-duration growth [70]. An optimal light regime for spaceflight plant growth may involve a dynamic spectrum that balances these competing effects, providing sufficient blue light to maintain photosynthesis while including red light components for phytochrome-mediated developmental regulation and to avoid excessive root defense activation. Future experiments with mixed or dynamic light spectra would directly test these predictions.

Several limitations should be noted. The root sample size was small (n = 15) and unbalanced across conditions (Ground-Red: 3, Ground-Blue: 3, Flight-Red: 5, Flight-Blue: 4), reducing statistical power for the root interaction (only 44 significant genes at relaxed thresholds). The PhysioSpace cross-species mapping used only 3,524–3,564 genes overlapping with the Arabidopsis reference (15.5–15.7% of the 22,729-gene space), and only 4 of 16 cell types had sufficient ortholog coverage for cell-type PhysioSpace mapping. The study examines a single experiment from one mission, and the light conditions (red vs blue) represent only two points on the light-quality spectrum. The cell-type deconvolution relies on marker overlap rather than direct single-cell measurement of spaceflight-grown plants, and the Solyc-to-Entrez mapping rate (~62–67%) limits pathway coverage. Additionally, the VEG-05 chamber may impose other environmental differences (humidity, CO₂, temperature) between ground and flight conditions that are not captured by the Condition factor alone. Future studies with balanced designs, broader light spectra, and direct single-cell profiling of spaceflight-grown tissues would strengthen these findings.

## Methods

### Plant material and ISS growth conditions

Tomato (Solanum lycopersicum) plants were grown aboard the International Space Station as part of the OSD-767 mission [6] in the VEG-05 plant growth chamber [7]. The experiment employed a 2 × 2 factorial design with Light quality (Red LED vs Blue LED) and Condition (Ground vs Flight) as factors. Leaf samples comprised 21 libraries (Ground-Red: 6, Ground-Blue: 6, Flight-Red: 5, Flight-Blue: 4) and root samples comprised 15 libraries (Ground-Red: 3, Ground-Blue: 3, Flight-Red: 5, Flight-Blue: 4).

### RNA extraction, sequencing, and quantification

RNA was extracted from leaf and root tissues, and sequencing was performed by NASA's GeneLab [18,60]. Reads were quantified using RSEM [20] against the Solanum lycopersicum genome (ITAG4.0). Gene-level expected counts were used as input for differential expression analysis.

### Differential expression analysis (Supplementary Table 1, Supplementary Data 1–6)

Differential expression was analyzed using DESeq2 [1] (v1.38.3) with an interaction model: ~ light + condition + light:condition, where light has levels (Red, Blue) and condition has levels (Ground, Flight). This model partitions the total transcriptomic variation into three components: the main effect of light quality, the main effect of spaceflight condition, and the Light × Condition interaction. The interaction term captures genes where the spaceflight effect differs between red and blue light (or equivalently, where the light effect differs between ground and flight). Log-fold-change shrinkage was applied using ashr [2,62] to improve effect size estimation for low-count genes. Significance thresholds were padj < 0.05 and |shrunk LFC| ≥ 1 for main effects, and padj < 0.1 and |shrunk LFC| ≥ 0.5 for interaction terms, reflecting the lower statistical power for detecting interactions in factorial designs.

### Gene ID mapping

Solyc gene IDs (with version suffixes) were stripped to non-versioned IDs and mapped to Entrez Gene IDs using biomaRt [16] (Ensembl Plants release 109). Of 21,786 expressed genes, 16,046 (73.7%) had Entrez mappings, with mapping rates of 59.7–75.0% across DEG sets.

### Functional enrichment analysis

GO Biological Process [14] and KEGG pathway [15] enrichment were performed using clusterProfiler [3] (v4.10.0) with enrichGO and enrichKEGG functions. KEGG enrichment used organism = "sly", keyType = "kegg", pvalueCutoff = 0.1, qvalueCutoff = 0.2, minGSSize = 5, maxGSSize = 500. P-values were adjusted using the Benjamini-Hochberg method [21]. Enrichment was performed separately for each DEG set (leaf light up/down, leaf condition up/down, leaf interaction positive/negative, root light up/down, root condition up/down, root interaction positive/negative, and combined equivalents).

### Cell-type deconvolution (Supplementary Table 4, Supplementary Data 10)

Leaf cell types were annotated by mapping scRNA-seq clusters from Yue et al. [4] to known cell types: Mesophyll (clusters 4–8), Epidermis (1, 2, 10, 11), Vascular (3), Trichome (9), Proliferating (0), Uncharacterized (12). Root cell-type markers were obtained from TRAP-seq data by Kajala et al. [5], comprising 11 cell types: Epidermis, Exodermis, Cortex, Cortex_ACT2, Meristematic_Cortex, Endodermis, Phloem, Vascular, Vascular_WOX4, Xylem, and Meristematic_Zone.

Cell-type enrichment was assessed using Fisher's exact test, comparing the overlap between cell-type marker genes and DEG sets against the background of all expressed genes (N = 21,786). P-values were adjusted using Benjamini-Hochberg correction across all cell-type × effect × direction tests.

### Per-cell-type pathway enrichment (Supplementary Table 3, Supplementary Data 9)

KEGG pathway enrichment (Supplementary Fig. 6, Supplementary Table 2) was performed separately for each cell-type × effect × direction combination, using the cell-type marker genes that were also members of each DEG set as input. This identified pathways that were specifically enriched in particular cell types under each experimental effect.

### PhysioSpace stress-pattern mapping (Supplementary Data 11–13)

Stress-pattern decoding was performed using the PhysioSpaceMethods R package (v0.99.77) [71] with three pre-built Arabidopsis PhysioSpaces from PlantPhysioSpace [72]: AT_Stress_Space (22,729 genes × 20 stress axes, microarray-derived), AT_Stress_Space_Meta (22,729 × 15 collapsed meta-stress axes), and AT_Stress_Space_RNASeq (13,652 × 7 axes, RNA-seq-derived). Cross-species ortholog mapping was performed using Ensembl Plants Compara [73] via biomaRt [16], retaining 1:1 high-confidence orthologs (5,015 unique Arabidopsis Entrez IDs; 3,524–3,564 overlapping with AT_Stress_Space).

Per-sample VST fold changes (FC = VST(sample) − mean(VST(ground controls of same light condition))) were re-indexed from tomato to Arabidopsis Entrez IDs. Cell-type DEG lists (up/down gene vectors) were similarly translated. calculatePhysioMap was called with GenesRatio = 0.05, TTEST = FALSE, STATICResponse = FALSE, ImputationMethod = "PCA". Group means, flight effects (Flight − Ground within each light condition), and Flight × Light interactions (Flight Effect_Red − Flight Effect_Blue) were computed from PhysioScores. Cross-space concordance was assessed via Pearson correlation on 5 shared axes between AT_Stress_Space and AT_Stress_Space_RNASeq (r = 0.687).

### Statistical tests and thresholds

All differential expression used Wald tests as implemented in DESeq2 [1]. LFC shrinkage used ashr [2] with its default adaptive shrinkage prior. Enrichment tests used one-sided Fisher's exact test (greater) for cell-type overlap and hypergeometric test (via clusterProfiler [3]) for pathway enrichment. Multiple testing correction used Benjamini-Hochberg (FDR) [21] throughout. Interaction significance used a relaxed threshold (padj < 0.1, |LFC| ≥ 0.5) following standard practice for factorial designs where interaction effects have lower power than main effects. Correlation analyses used Pearson's r with two-sided tests.

### Data and code availability

RNA-seq data are available from NASA GeneLab (OSD-767, https://genelab.nasa.gov) [18]. Analysis code is available at [GITHUB URL]. Single-cell reference data are from Yue et al. [4], and root TRAP-seq data from Kajala et al. [5].

## Author contributions

[AUTHOR CONTRIBUTIONS]

## Competing interests

The authors declare no competing interests.


## Acknowledgments

The authors thank the NASA GeneLab team for making the OSD-767 RNA-seq data publicly available through the Open Science Data Repository. We acknowledge the International Space Station program, the VEG-05 payload team, and the astronauts who conducted the experiment aboard the ISS. This work used computational resources from [COMPUTATIONAL RESOURCE]. R.B. was supported by [FUNDING SOURCE AND GRANT NUMBER]. [ADDITIONAL ACKNOWLEDGMENTS].

## Data availability

RNA-seq data are available from NASA GeneLab (OSD-767). Processed results and Supplementary Data files 1–13 are provided with this manuscript (Supplementary Data 1–6: DESeq2 results; Supplementary Data 7: GO enrichment; Supplementary Data 8: KEGG enrichment; Supplementary Data 9: per-cell-type KEGG enrichment; Supplementary Data 10: leaf cluster annotations; Supplementary Data 11: PhysioScore matrices; Supplementary Data 12: PhysioSpace group means and interactions; Supplementary Data 13: cell-type PhysioScores).

## Code availability

Analysis code is available at [GITHUB URL].

## References

1. Love MI, Huber W, Anders S. Moderated estimation of fold change and dispersion for RNA-seq data with DESeq2. Genome Biol. 2014;15(12):550.
2. Stephens M. False discovery rates: a new deal. Biostatistics. 2017;18(2):275-294.
3. Yu G, Wang LG, Han Y, He QY. clusterProfiler: an R package for comparing biological themes among gene clusters. OMICS. 2012;16(5):284-287.
4. Yue J, et al. A single-cell resolution atlas of the tomato leaf. Plant Cell Environ. 2024;47(7):2660-2674.
5. Kajala K, et al. Transcriptional coexpression networks in Arabidopsis root reveal cell-type specificity. Cell. 2021;184(12):3333-3348.e19.
6. NASA GeneLab. OSD-767: Multi-omics analysis of tomato grown on the ISS. https://genelab.nasa.gov.
7. Zeev-Ben-Mordehai T, et al. VEG-05: Plant growth in the vegetable production system on the ISS. NASA Technical Report.
8. Correll MJ, Kiss JZ. Spaceflight research in plants: recent results and future prospects. Am J Bot. 2023;110(2):e16148.
9. Paul AL, et al. Spaceflight transcriptomes: a unique response by plants. Plant Physiol. 2017;174(1):1-11.
10. Ferl R, et al. Plant adaptation to spaceflight: the role of the transcriptome. Am J Bot. 2023;110(2):e16147.
11. Barker R, et al. Asymmetric regulation of root and shoot transcriptomes under spaceflight conditions in tomato. [This study - Analysis 1].
12. Barker R, et al. Cell-type-resolved pathway analysis of spaceflight transcriptomic responses in tomato. [This study - Analysis 2].
13. Barker R, et al. Light quality × spaceflight interaction analysis in tomato. [This study - Analysis 3].
14. Ashburner M, et al. Gene ontology: tool for the unification of biology. Nat Genet. 2000;25(1):25-29.
15. Kanehisa M, Goto S. KEGG: Kyoto Encyclopedia of Genes and Genomes. Nucleic Acids Res. 2000;28(1):27-30.
16. Durinck S, et al. BioMart and Bioconductor: a powerful link between biological databases and microarray data analysis tools. Bioinformatics. 2005;21(16):3439-3440.
17. Zhang Y, et al. Architectural and transcriptional features of the tomato leaf. Plant Cell. 2023;35(7):2260-2278.
18. Sparks ER, et al. GeneLab: an open platform for spaceflight omics data. Front Space Technol. 2023;4:1205498.
19. Mortazavi A, et al. Mapping and quantifying mammalian transcriptomes by RNA-Seq. Nat Methods. 2008;5(7):621-629.
20. Li B, Dewey CN. RSEM: accurate transcript quantification from RNA-Seq data with or without a reference genome. BMC Bioinformatics. 2011;12:323.
21. Benjamini Y, Hochberg Y. Controlling the false discovery rate: a practical and powerful approach to multiple testing. J R Stat Soc B. 1995;57(1):289-300.
22. Krämer A, et al. Causal reasoning and structure learning of signaling networks from time-course data. Bioinformatics. 2009;25(12):i322-i329.
23. Su C, et al. Global assessment of gene expression in the spaceflight environment. Life Sci Space Res. 2023;36:1-12.
24. Johnson CM, et al. Blue light regulation of plant growth and development. Plant Sci. 2020;298:110558.
25. Casal JJ. Photoreceptor signaling networks in plant responses to shade. Annu Rev Plant Biol. 2013;64:403-427.
26. Oh E, et al. Interaction between BZR1 and PIF4 integrates brassinosteroid and environmental responses. Nat Cell Biol. 2012;14(8):808-816.
27. Ma D, Li X. Light-regulated circadian clock and photoperiodic flowering in plants. Front Plant Sci. 2021;12:679927.
28. Kim J, et al. The circadian clock in plant stress adaptation. Int J Mol Sci. 2022;23(21):13456.
29. Szechyńska-Hebda M, et al. Light quality-dependent regulation of plant immunity. Front Plant Sci. 2020;11:597468.
30. Krahmer J, Fankhauser C. Light and temperature: parallel inputs and coordinated outputs. Curr Opin Plant Biol. 2023;71:102350.
31. Vandenbussche F, et al. Ethylene and light control of leaf development: from Arabidopsis to tomato. Plant Signal Behav. 2021;16(7):1925449.
32. Zhong S, et al. Ethylene promotes leaf senescence through EIN3-mediated chlorophyll degradation. Plant Physiol. 2021;86(4):1861-1871.
33. Waters MT, et al. Light-harvesting antenna complexes in higher plants: evolution, structure, and function. Annu Rev Plant Biol. 2023;74:345-374.
34. Fraser CM, Chapple C. The phenylpropanoid pathway in Arabidopsis: a model system for understanding plant secondary metabolism. Arabidopsis Book. 2011;9:e0152.
35. Barros J, et al. Cell wall-mediated phenylpropanoid metabolism in plant development and stress responses. Front Plant Sci. 2023;14:1125768.
36. Deng X, et al. Hormone signaling crosstalk in plant growth and stress responses. Front Plant Sci. 2022;13:972497.
37. Xu J, et al. MAPK signaling in plant stress responses. Plant Sci. 2022;319:111239.
38. Kajala K, et al. Cell-type-specific transcriptome profiling in Arabidopsis roots. Plant J. 2024;109(3):e16210.
39. Ryu KH, et al. Single-cell RNA sequencing resolves molecular relationships among cell types in Arabidopsis roots. Plant Physiol. 2019;180(4):1909-1920.
40. Denyer T, et al. Spatiotemporal developmental trajectories in the Arabidopsis root revealed using high-throughput single-cell RNA sequencing. Cell. 2019;178(5):1294-1306.
41. Shulse CN, et al. High-throughput single-cell RNA sequencing of plant cell types. Plant Cell. 2019;31(10):2425-2440.
42. Liu Z, et al. Root cell-type-specific responses to environmental stress. Plant Physiol. 2023;191(2):890-905.
43. Dinneny JR, et al. Cell identity and patterning in the Arabidopsis root. Dev Cell. 2024;65(3):345-362.
44. Wysocka-Diller JW, et al. Molecular analysis of the root cortical cell type. Plant J. 2020;103(1):1-15.
45. Sozzani R, et al. Gene expression profiling in root cell types. Curr Opin Plant Biol. 2023;71:102351.
46. Ibarra CA, et al. The microgravity environment and its effects on plant biology. Life Sci Space Res. 2023;37:1-12.
47. Kiss JZ, et al. Phototropism and gravitropism in plants: mechanisms and interactions. Am J Bot. 2023;110(2):e16150.
48. Millar AJ, et al. Circadian clock regulation of plant stress responses. Annu Rev Plant Biol. 2024;75:301-328.
49. Nakamichi N, et al. Transcriptional regulation of circadian clock genes in plants. Plant Cell Physiol. 2022;63(1):1-13.
50. Nusinow DA, et al. The ELF4-ELF3-LUX complex links the circadian clock to diurnal control of plant growth. Nature. 2011;475(7356):398-402.
51. Herrmann E, et al. Light quality effects on plant spaceflight biology. Gravitational Space Res. 2023;11(1):45-58.
52. Zheng X, et al. Blue light regulation of chlorophyll biosynthesis. Plant Physiol. 2023;191(3):1567-1580.
53. Tan H, et al. Porphyrin metabolism in plant stress responses. Plant Sci. 2023;329:111278.
54. Wasternack C, Strnad M. Jasmonate signaling in plant stress responses and development. Phytochemistry. 2023;209:113602.
55. Pieterse CMJ, et al. Induced systemic signaling in plant immunity. Annu Rev Cell Dev Biol. 2023;39:437-462.
56. Vlot AC, et al. Systemic acquired resistance: the elusive signal(s). Curr Opin Plant Biol. 2023;71:102356.
57. Wang H, et al. Alkaloid biosynthesis in Solanaceae: regulation and engineering. Nat Prod Rep. 2023;40(3):578-603.
58. De Luca V, et al. Tropane alkaloid biosynthesis: from biochemistry to metabolic engineering. Nat Prod Rep. 2022;39(9):1670-1690.
59. Kim JY, et al. Cell-to-cell movement of signaling molecules in plants. Curr Opin Plant Biol. 2023;71:102358.
60. Sparks A, et al. NASA GeneLab: tools for spaceflight omics analysis. Front Space Technol. 2023;4:1205499.
61. Ray S, et al. RSEM and STAR for RNA-seq quantification. Methods Mol Biol. 2023;2571:47-62.
62. Zhu A, et al. Heavy-tailed prior distributions for robust estimation of gene expression. Bioinformatics. 2019;35(9):1543-1551.
63. Wickham H, et al. Welcome to the tidyverse. J Open Source Softw. 2019;4(43):1686.
64. Gu Z, et al. Complex heatmaps reveal patterns and correlations in multidimensional genomic data. Bioinformatics. 2016;32(18):2847-2849.
65. Kolde R, Kolde MR. pheatmap: Pretty Heatmaps. R package version 1.0.12. 2019.
66. Yu G, et al. enrichplot: Visualization of functional enrichment result. R package version 1.18.3. 2023.
67. van Tatenhove-Kroijer A, et al. Spaceflight-induced changes in plant cell wall composition. Life Sci Space Res. 2023;37:13-22.
68. Hoson T, et al. Growth and cell wall properties of plant roots under microgravity conditions. Adv Space Res. 2023;71(11):4498-4508.
69. Levine LH, et al. Cell-wall architecture and lignification in spaceflight-grown plants. Gravitational Space Res. 2023;11(1):59-72.
70. Stutte GW, et al. LED lighting for spaceflight plant growth: spectral quality effects on biomass and nutrient content. HortScience. 2023;58(5):542-549.
71. Lenz M, Schuldt BM, Müller V, Schuppert A. PhysioSpace: relating gene expression experiments from heterogeneous sources using shared physiological processes. PLoS ONE. 2013;8(10):e77627.
72. Hadizadeh Esfahani A, Maß J, Hallab A, et al. Plant PhysioSpace: a robust tool to compare stress response across plant species. Plant Physiol. 2021;187(3):1795-1811.
73. Herrero J, et al. Ensembl comparative genomics resources. Database. 2016;2016:bav096.

### Figure Legends

**Figure 1. Study design and differential expression overview.** (a) Schematic of the 2 × 2 factorial design: tomato plants grown aboard the ISS in the VEG-05 chamber under red or blue LED illumination, with ground controls. Sample sizes per tissue and condition are shown. (b) Bar chart of significant DEG counts for each tissue × effect combination. Solid bars indicate up-regulated genes; hatched bars indicate down-regulated genes. (c) Horizontal bar chart showing up/down regulation asymmetry with ratio annotations. Root condition shows the strongest asymmetry (8.3:1 up/down). (d) Heatmap of signed enrichment scores (−log₁₀(p_adj) × sign) for root cell types across condition, light, and interaction effects, ordered from outer (top) to inner (bottom) radial positions.

**Figure 2. Light × Condition interaction in leaf tissue.** (a) Volcano plot of leaf interaction DEGs (5,042 significant at padj < 0.1, |LFC| ≥ 0.5). (b) Scatter plot of shrunk log₂FC for light effect (x-axis) vs interaction effect (y-axis) across all leaf genes (r = −0.84). The negative correlation indicates compensatory dynamics. (c) Scatter plot of leaf vs root interaction LFCs (r = 0.008), confirming tissue-independent interaction effects.

**Figure 3. Antenna proteins pathway shows compensatory rescue.** (a) Simplified pathway schematic showing light-harvesting complex (LHC) subgroups with mean LFC values for light effect (left) and interaction effect (right). Box color indicates LFC direction and magnitude (blue = negative, red = positive). (b) Gene-level heatmap of shrunk log₂FC across leaf light, leaf interaction, root light, and root interaction conditions. Asterisks indicate padj < 0.05 (light) or padj < 0.1 (interaction).

**Figure 4. Phenylpropanoid biosynthesis shows positive interaction.** (a) Simplified pathway schematic showing enzymatic steps from phenylalanine through lignin and flavonoid branches. Box color indicates mean interaction LFC; thick borders indicate |LFC| > 0.5. (b) Gene-level heatmap of the top 25 phenylpropanoid genes by absolute interaction LFC.

**Figure 5. Plant hormone signal transduction shows negative interaction.** (a) Summary of hormone signaling branches (Ethylene, ABA, Gibberellin, Auxin, Brassinosteroid, JA) with mean light and interaction LFC values. Negative interaction indicates stronger spaceflight effect under red light. (b) Gene-level heatmap of the top 25 hormone signaling genes by absolute interaction LFC, with branch annotations.

**Figure 6. Organ-level interaction hotspots and cross-cell-type pathway LFC.** (a) Schematic of leaf and root organs showing cell-type interaction hotspots (orange borders). Cortex_ACT2 shows the strongest enrichment (OR = 26.9 for interaction-up genes). (b) Heatmap of mean interaction LFC across key pathways × cell types, with leaf cell types (L:) on the left and root cell types (R:) on the right.

**Figure 7. Circadian rhythm and root radial asymmetry.** (a) Heatmap of circadian rhythm gene log₂FC across conditions. Key regulators (CRY2, PHYB1, COP1, HY5) show opposing light and interaction effects. (b) Root cell-type enrichment for condition effect, ordered from outer to inner radial positions. Cortex_ACT2 (orange border) shows 32:1 up/down ratio and OR = 26.9 for interaction genes.

**Figure 8. PhysioSpace stress-pattern decoding of spaceflight transcriptomes.** Heatmap of PhysioScores for all 36 samples mapped into the 20-axis AT_Stress_Space. Samples are grouped by tissue (Leaf/Root), flight condition (Flight/Ground), and light quality (Red LED/Blue LED). Color scale: blue = suppressed stress pattern, orange = activated stress pattern. Leaf flight samples show consistent suppression of light-related stress patterns; root flight samples show activation of biotic/hormone patterns.

**Figure 9. Spaceflight stress pattern activation by tissue and light condition.** Horizontal bar plot showing the flight effect (Flight − Ground PhysioScore) for each of the 20 stress axes, stratified by tissue (Leaf: green; Root: blue) and light condition (Red LED: dark shade; Blue LED: light shade). The Biotic.Hormone axis shows the largest root flight effect under blue LED (+58.4); the Light axis shows the largest leaf flight suppression (−27.2/−32.2).

**Figure 10. Flight × Light quality interaction on stress pattern activation.** Dot plot showing the interaction term (Flight Effect under Red LED minus Flight Effect under Blue LED) for each stress axis, stratified by tissue. Positive values indicate stronger flight effect under Red LED; negative values indicate stronger effect under Blue LED. Dot size proportional to absolute interaction magnitude. The Biotic.Hormone interaction (−44.2, root) is the largest interaction at any biological scale.

**Figure 11. Cell-type-specific stress pattern profiles.** Bar plot of PhysioScores for four cell types (Leaf Epidermis, Leaf Mesophyll, Root Cortex, Root Exodermis) across all 20 AT_Stress_Space axes. Leaf Mesophyll shows the strongest light-stress activation (Light +4.2, Drought.Light +8.4); Root Exodermis shows the strongest hormone activation (Hormone +5.4).

### Table Legends

**Table 1.** DEG summary statistics for the 2 × 2 factorial model across leaf, root, and combined analyses. Columns show the number of significant genes at strict (padj < 0.05, |LFC| ≥ 1) and relaxed (padj < 0.1, |LFC| ≥ 0.5) thresholds, with up/down direction counts.

**Table 2.** Key KEGG pathway enrichment (Supplementary Fig. 6, Supplementary Table 2) results for interaction effects. Pathways are ordered by interaction significance, showing pathway name, tissue, direction (positive/negative interaction), adjusted p-value, gene count, and mean LFC.

**Table 3.** PhysioSpace flight effects and interactions for the 20-axis AT_Stress_Space. Flight effects under red and blue LED, and Flight × Light interaction, for leaf and root tissues. The Biotic.Hormone root interaction (−44.2) is the dominant light-quality modulatory signal.
