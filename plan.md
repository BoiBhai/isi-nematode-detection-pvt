# Approaches

1. Vanilla CNN on images
2. Convolution + Feature augmented NN
3. CNN -> 

## Reasons for including additional information with CV
1. Auxiliary confirmation/ deduction sometimes resolves visual ambiguities
2. Prunes improbable classes based on metadata


## Methods to augment CV with additional information
Data to incorporate:
1. structured metadata
2. tabular variables
3. text descriptions
4. spatiotemporal coordinates
5. sensor streams

The primary integration methods include:
* **Input-Level Stacking (Early Fusion):** Dense spatial metadata (e.g., depth maps, LiDAR projections, thermal bands, or rasterized coordinates) is concatenated directly as extra input channels to the first convolutional layer.
* **Feature Concatenation (Late Fusion):** The CNN extracts image embeddings while a separate encoder (e.g., [MLP](https://www.alphaxiv.org/abs/2607.07756), FT-Transformer) encodes metadata/tabular attributes. The resulting feature vectors are concatenated before final dense classification layers.
* **Feature-Wise Linear Modulation (FiLM / Conditioning):** Auxiliary inputs predict affine transformation parameters ($\gamma, \beta$) that scale and shift the intermediate convolutional feature maps:
$\text{FiLM}(x) = \gamma(z) \odot x + \beta(z)$. This lets metadata actively steer spatial feature extraction.
* **Hypernetworks:** A secondary network processes tabular/metadata inputs to directly generate or adapt the convolutional filter weights or adapter parameters ([HyperFusion](https://www.alphaxiv.org/abs/2403.13319), [PEFT Adapters](https://www.alphaxiv.org/abs/2606.11682)).
* **Cross-Attention & Gated Fusion:** Intermediate CNN activations and tabular/text embeddings interact dynamically via multi-head cross-attention or gating mechanisms ([MCFNet](https://www.alphaxiv.org/abs/2505.23365)), allowing the network to weight modalities according to sample-level confidence.
* **Multimodal Contrastive Pretraining:** Self-supervised alignment projects auxiliary data and images into a shared embedding space before fine-tuning, improving representation quality even when metadata is missing at inference ([TIP](https://www.alphaxiv.org/abs/2407.07582), [Cross-Contrastive Pre-Training](https://www.alphaxiv.org/abs/2504.20322)).

* **Bayesian / Logit-Level Post-Priors:** Independent classifiers run on images and metadata, combining outputs via product-of-experts or using metadata-derived class distributions as dynamic prior probabilities $P(y \mid z)$ over CNN softmax predictions.

# Pointers

2. Topological data analysis for partitionability analysis of datasets?
3. If variableSet-response relationship is noisy by structure, then
   1. Solution 1: try incorporating new variables
   2. Solution 2: try try creating new features
4. The CBM paper used NNs in both the concept identification layer as well as the prediction layer. If NN explainability is an issue, then taxonomists may as well as again:
   1. How are indecipherable image features being mapped to taxonomic features? Counter: decipheration has a limit; even the human mind deciphers through subconscious cues (someone's physique can be ideated based on how clothing drapes them).
   2. How are features interacting in indecipherable ways to provide a valid classification?


## Dataset specific tasks

### Processing, layer 1
1. **Eliminate lens dirt and artifacts**
   1. Analyse static artifacts remaining constant over all images (black specs of dirt, grease, etc.).
   2. Elimination method should be additive so as to "undo" but not "washout" the artefact. Image reconstruction is important.
2. **Eliinate maginification labels**
   1. If possible obtain text-unappended-over-images dataset with fixed maginification

### ML, layer 2
1. For all captured images, identify:
   1. The anatomical position whose image it is. Separate anatomy-wise ML models may be used for subanatomy detection and prediction
   2. The subanatomical features present and their measurements and distances within the anatomical part

## Processing, layer 3
1. Rotate images keeping vulva horizontal and centered 

protopnet
we can create broden type dataset for nematodes and publish a paper