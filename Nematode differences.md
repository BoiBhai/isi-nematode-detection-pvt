# 6 types of nematodes

Y is the species of Meloidogyne:
1. Graminicola
2. Incognita
3. Javanica
4. Hapla
5. Enterolobii
6. Arenaria

X:
1. Collection region
2. Collection time

X hat derived from perineal imagery:
1. Vulva-anus distance



# Diferences between these types and detection mechanisms (Gemini)
### 1. Differentiating Perineal Pattern Features

Adult female root-knot nematodes (*Meloidogyne* spp.) are separated morphologically by cuticular ridges (striae), arch shape, and lateral markings around the vulva and anus.

---

| Species | Dorsal Arch | Striae & Cuticular Texture | Lateral Lines & Key Landmarks |
| --- | --- | --- | --- |
| ***M. graminicola*** | Low to rounded | Relatively fine, smooth to slightly wavy | Indistinct/weak lateral lines; prominent phasmids |
| ***M. incognita*** | High, squarish to rounded, often indented near tail | Wavy to coarse, closely spaced, often zig-zagging near dorsal arch | No distinct lateral incisures; dorsal striae bend sharply inward/downward near tail |
| ***M. javanica*** | Low to moderately rounded | Smooth to gently wavy | Clear, distinct lateral lines (incisures) separating dorsal and ventral striae |
| ***M. hapla*** | Low to rounded | Fine, smooth to slightly wavy | Often shows punctations (stippling) near tail tip; lateral lines weak/variable |
| ***M. enterolobii*** | High, rounded to oval | Smooth to wavy, generally finer/more uniform than *M. incognita* | Lacks prominent lateral incisures; high dorsal arch often overlaps *M. incognita* visually |
| ***M. arenaria*** | Low, rounded to flattened | Wavy striae with forking/short irregular striae near lateral lines | Lateral fields marked by forked or broken striae rather than a clean groove |

---

### 2. Signals to Leverage for Explainable ML

Perineal patterns alone have within-species variation and overlap (especially between *M. incognita*, *M. enterolobii*, and *M. javanica*), so pairing visual features with temporal metadata strengthens both accuracy and explanation.

* **Morphological & Texture Features (Images):**
* **Arch geometry:** Dorsal-to-ventral height ratio, arch curvature, and tail-tip indentation/stippling.
* **Ridge frequency & orientation:** Striae spacing, wave amplitude/roughness, and ridge angle near the lateral zones.
* **Lateral-zone discontinuities:** Presence of continuous lateral incisures (*M. javanica*) vs. forked/broken striae (*M. arenaria*) or phasmid/tail-tip cues (*M. graminicola*).


* **Collection Date & Time (Metadata):**
* **Seasonal & temperature proxies:** Cyclical encoding (`sin`/`cos` of day-of-year) captures crop cycles and soil temperature regimes—for example, *M. hapla* favors cooler/temperate conditions while *M. incognita*, *M. javanica*, and *M. graminicola* are prominent in warmer/tropical-subtropical windows.
* **Batch/session & time-of-day effects:** Collection timestamps often correlate with sampling site, host crop stage, or slide-prep/imaging batches. Treat timestamp features carefully as *contextual covariates* rather than direct species proof so the model does not over-rely on sampling bias.



### 3. Designing an Explainable Architecture

1. **Extract Interpretable + Deep Visual Features:** Combine domain-derived measurements (arch height-to-width ratio, stria spacing/orientation histograms, lateral-region edge energy) with a lightweight CNN backbone.
2. **Fuse Tabular Metadata Cleanly:** Feed cyclical date features and batch/time indicators into a tabular branch or GAM / shallow gradient-boosted layer fused with the image representation.
3. **Generate Faithful Explanations:**
* Use Grad-CAM or integrated gradients to verify the model focuses on the dorsal arch, lateral lines, or tail/phasmid zone rather than slide edges or artifacts.
* Use SHAP to show how much each visual trait versus seasonal timing pushed the prediction, and report per-species confidence/ambiguity flags when *M. incognita* and *M. enterolobii* look similar.