# Effect of Weak Artefacts on Interpretability in Medical VLMs

**Notebook:** `effect-of-noise-on-intepretability-VLM.ipynb`

## Overview

This notebook provides a brief qualitative exploration of how weak image-level artefacts affect the interpretability of a medical vision-language model (VLM).

The investigation was motivated by [*Seeing the Trees for the Forest: Rethinking Weakly-Supervised Medical Visual Grounding*](https://doi.org/10.48550/arXiv.2505.15123), which introduces **Disease-Aware Prompting (DAP)** for weakly supervised medical visual grounding.

Recent work has demonstrated that medical VLMs can be vulnerable to noise and imaging artefacts. This raised the question of whether introducing artefacts directly at the image level, in pixel-space, could also affect the interpretability maps used by DAP.

## Motivation

DAP uses an interpretability approach, $\Phi$, to use as a basis for their disease aware prompting for visual grounding. The DAP paper already provides evidence that the method remains useful when the underlying interpretability method is imperfect. For example:

* Appendix E investigates the robustness of DAP to a flawed $\Phi$.
* Fig. 14 in Appendix A shows that DAP continues to outperform the baselines even when $\Phi$ performs poorly (Dice < 0.3).
* Chefer et al. [1] investigate the effect of perturbations on their interpretability approach, although these experiments operate at the **token level** rather than directly perturbing the input image.

This motivated a related question:

> **How does image-level corruption affect the interpretability map $\Phi$?**

Understanding this provides a potential link between the demonstrated robustness of DAP to imperfect grounding and the vulnerability of medical VLMs to image-level artefacts.

## Notebook Experiment

The notebook demonstrates a single qualitative example in which a chest X-ray is evaluated before and after the introduction of weak image-level artefacts.

For each image, the notebook:

1. Generates the interpretability map $\Phi$ for the original image.
2. Introduces a weak image-level artefact in pixel-space.
3. Generates $\Phi$ again for the corrupted image.
4. Compares the resulting interpretability maps.
5. Calculates Dice scores at several interpretability-map thresholds.

The purpose of the notebook is **not to establish the overall robustness of DAP from a single example**. Instead, it demonstrates how image-level artefacts can alter $\Phi$ and illustrates a potential mechanism through which image corruption could have downstream implications for DAP.

A systematic investigation could extend this experiment across multiple images, artefact types and magnitudes, interpretability thresholds, and potentially different training and inference settings.

## Potential Extension

A broader study could evaluate DAP under:

* Controlled pixel-space perturbations
* Realistic medical-image artefacts
* Different artefact magnitudes
* Multiple interpretability-map thresholds
* Zero-shot inference
* Training with corrupted or augmented images

This would complement existing analyses of imperfect visual grounding by investigating robustness to perturbations introduced **before the interpretability and grounding process, at the image level**.

## References

### [1] Chefer et al.

Chefer, Hila, Shir Gur, and Lior Wolf. “Generic Attention-Model Explainability for Interpreting Bi-Modal and Encoder-Decoder Transformers.” *arXiv:2103.15679*, 2021.
https://doi.org/10.48550/arXiv.2103.15679

### [2] Tiu et al.

Tiu, Ekin, Ellie Talius, Pujan Patel, Curtis P. Langlotz, Andrew Y. Ng, and Pranav Rajpurkar. “Expert-Level Detection of Pathologies from Unannotated Chest X-Ray Images via Self-Supervised Learning.” *Nature Biomedical Engineering* 6, no. 12 (2022): 1399–1406.
https://doi.org/10.1038/s41551-022-00936-9

### [3] Cheng et al.

Cheng, Zijie, Ariel Yuhan Ong, Siegfried K. Wagner, et al. “Understanding the Robustness of Vision-Language Models to Medical Image Artefacts.” *NPJ Digital Medicine* 8 (2025): 727.
https://doi.org/10.1038/s41746-025-02108-w

### [4] Huy et al.

Huy, Ta Duc, Duy Anh Huynh, Yutong Xie, et al. “Seeing the Trees for the Forest: Rethinking Weakly-Supervised Medical Visual Grounding.” *arXiv:2505.15123*, 2025.
https://doi.org/10.48550/arXiv.2505.15123
