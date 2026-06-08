<div align="center">

# Navigating the Challenges of AI-Generated Image Detection in the Wild: What Truly Matters?

**[Despina Konstantinidou](https://orcid.org/0009-0005-3155-7228), [Dimitrios Karageorgiou](https://orcid.org/0009-0007-4259-8249), [Christos Koutlis](https://orcid.org/0000-0003-3682-408X), [Olga Papadopoulou](https://orcid.org/0000-0002-0498-7506), [Emmanouil Schinas](https://orcid.org/0009-0007-2132-3430), [Symeon Papadopoulos](https://orcid.org/0000-0002-5441-7341)**

Information Technologies Institute, CERTH

*The 5th ACM International Workshop on Multimedia AI against Disinformation (MAD '26), 2026*

[![Paper](https://img.shields.io/badge/Paper-arXiv-b31b1b?style=for-the-badge&logo=arxiv&logoColor=white)](https://arxiv.org/abs/2507.10236)
[![Project Page](https://img.shields.io/badge/Project-Page-2563eb?style=for-the-badge&logo=googlechrome&logoColor=white)](https://mever-team.github.io/itw-sm)
[![Hugging Face Dataset](https://img.shields.io/badge/Hugging_Face-Dataset-FFD21E?style=for-the-badge&logo=huggingface&logoColor=black)](https://huggingface.co/datasets/dkarageo/itw-sm)
[![DOI](https://img.shields.io/badge/DOI-10.1145%2F3810988.3812665-1f6feb?style=for-the-badge)](https://doi.org/10.1145/3810988.3812665)

</div>

---

## Overview

As generative AI advances, the realism of AI-generated imagery has reached a
threshold capable of deceiving even vigilant human observers. Yet, while current
**AI-generated Image Detection (AID)** approaches perform exceptionally well on
controlled benchmark datasets, they struggle significantly with real-world
cases.

To study this behavior we introduce **ITW-SM** (*In The Wild – Social Media*), a
curated dataset of **10,000** real and AI-generated images collected from four
major social media platforms (**Facebook, Instagram, LinkedIn, and X**). We use
it to analyze the key design choices behind a detector — its architecture,
pre-trained latent space, training data, and pre-processing — and show that
naively scaling pre-training or adding more training data does **not** always
improve detection in the wild. Instead, each design choice must be optimized so
the pipeline can propagate and analyze **both** low-level traces **and**
high-level image semantics.

Building on these findings, we obtain an **average improvement of 26.87% in AUC**
across multiple state-of-the-art detectors under real-world conditions —
providing a roadmap for building more resilient detectors.

<div align="center">
  <table>
    <tr>
      <td align="center"><img src="https://raw.githubusercontent.com/mever-team/itw-sm/website/static/images/real_car.jpg" width="180"/></td>
      <td align="center"><img src="https://raw.githubusercontent.com/mever-team/itw-sm/website/static/images/real_cat.jpg" width="180"/></td>
      <td align="center"><img src="https://raw.githubusercontent.com/mever-team/itw-sm/website/static/images/real_food.jpg" width="180"/></td>
      <td align="center"><img src="https://raw.githubusercontent.com/mever-team/itw-sm/website/static/images/real_monument.jpg" width="180"/></td>
    </tr>
    <tr>
      <td align="center"><b>Real</b></td>
      <td align="center"><b>Real</b></td>
      <td align="center"><b>Real</b></td>
      <td align="center"><b>Real</b></td>
    </tr>
    <tr>
      <td align="center"><img src="https://raw.githubusercontent.com/mever-team/itw-sm/website/static/images/fake_car.jpg" width="180"/></td>
      <td align="center"><img src="https://raw.githubusercontent.com/mever-team/itw-sm/website/static/images/fake_cat.jpg" width="180"/></td>
      <td align="center"><img src="https://raw.githubusercontent.com/mever-team/itw-sm/website/static/images/fake_food.jpg" width="180"/></td>
      <td align="center"><img src="https://raw.githubusercontent.com/mever-team/itw-sm/website/static/images/fake_monument.jpg" width="180"/></td>
    </tr>
    <tr>
      <td align="center"><b>AI-Generated</b></td>
      <td align="center"><b>AI-Generated</b></td>
      <td align="center"><b>AI-Generated</b></td>
      <td align="center"><b>AI-Generated</b></td>
    </tr>
  </table>
</div>

## Highlights

- 🔬 A systematic evaluation revealing the strengths and weaknesses of various AID approaches **in the wild**.
- 🗂️ **ITW-SM**, a new in-the-wild AID benchmark collected from four major social media platforms.
- 🧩 An impact analysis of **training data, pre-trained latent spaces, model architectures, pre-processing, and data augmentations**.
- 📈 An **average improvement of 26.87% in AUC** across four detector types under real-world conditions.
- 🧭 A set of **recommendations** for designing robust AID models that handle in-the-wild variations.

## The ITW-SM Dataset

ITW-SM contains **10,000 images**, evenly split between **5,000 real** and
**5,000 AI-generated**. Real images are collected from verified, trusted
accounts; AI-generated images are sourced from public accounts and communities
known to consistently share synthetic content. All images are kept at their
**original resolution**, preserving native compression artifacts. A multi-stage
filtering pipeline removed heavy text overlays, watermarks, non-photographic
content, and duplicates, and every sample was manually reviewed for label
correctness.

| Characteristic | **ITW-SM** | Chameleon | TWIGMA |
| --- | --- | --- | --- |
| AI-image source | Social media users | AI-painting communities | Twitter users |
| Real-image source | Verified social media accounts | Unsplash (photographers) | – |
| # Social media platforms | **4** | 0 | 1 |
| Resolution range | 0.1 – 45 MP | 0.1 – 31 MP | < 0.01 – 47 MP |
| Size | 10,000 | 26,033 | 800,000 |
| Intended focus | General in-the-wild robustness | Generalization to realistic AI | Analysis of AI art trends |

Compared with prior web-sampled datasets, ITW-SM directly represents the distribution present on
online social media platforms rather than some special purpose communities, e.g. online art communities.

### Download

The dataset is hosted on the 🤗 Hugging Face Hub:
**[`dkarageo/itw-sm`](https://huggingface.co/datasets/dkarageo/itw-sm)**.

```bash
pip install -U "huggingface_hub[cli]"

# Download the full dataset to ./ITW-SM
hf download dkarageo/itw-sm --repo-type dataset --local-dir ITW-SM
```

```python
from huggingface_hub import snapshot_download

path = snapshot_download(repo_id="dkarageo/itw-sm", repo_type="dataset")
print(path)  # local path containing 0_real/, 1_fake/ and metadata.csv
```

```python
# Or load it directly with the 🤗 datasets library (all images are in the "test" split)
from datasets import load_dataset

ds = load_dataset("dkarageo/itw-sm", split="test")
```

> **Access is gated** for research use: request access on the hugging-face dataset page.

### Structure

Images follow the standard AID label convention — `0_real` for real and
`1_fake` for AI-generated — with the originating platform encoded in each
filename:

```
ITW-SM/
├── 0_real/        # 5,000 real images        — e.g. Facebook_real_1042.jpg
├── 1_fake/        # 5,000 AI images          — e.g. instagram_1030.jpg
└── metadata.csv   # file_name, label, target, platform
```

| Platform  | Real  | AI-Generated |
| --------- | ----: | -----------: |
| Facebook  | 1,318 |        1,033 |
| Instagram | 1,206 |        2,179 |
| LinkedIn  | 1,269 |          931 |
| X         | 1,207 |          857 |
| **Total** | **5,000** |    **5,000** |

## Methodology

We define an experimental framework to systematically study four key components
typically considered when building an AID model.

<p align="center">
  <img src="https://raw.githubusercontent.com/mever-team/itw-sm/website/static/images/methodology.png" width="90%"/>
</p>

- **Training data composition** — how dataset diversity (e.g. combining benchmark LDM data with in-the-wild TWIGMA data) affects generalization.
- **Backbone architectures** — vision encoders (CLIP, BLIP2, DINO-V2, …) and their ability to capture low-level artifacts vs. high-level semantics.
- **Cropping strategies** — resizing, center cropping, 10-cropping, and texture-based cropping for preserving generation traces.
- **Data augmentations** — geometric and noise transformations that simulate real-world distortions.

We evaluate one representative model from each major AID family — **DMID**
(end-to-end supervised), **RINE** (VL-model-based), **NPR** (heuristic), **SPAI**
(reconstruction-based), and **Gemma 3 IT 27B** (zero-shot) — across three test
sets: **Synthbuster** (controlled), **Chameleon** (in-the-wild art), and
**ITW-SM** (in-the-wild social media).

## Core Results

Most methods achieve strong results on curated benchmarks but degrade
significantly on in-the-wild AI-generated images. By systematically updating
detectors with optimal design choices, we recover much of this gap — a
**26.87% average AUC improvement** under real-world conditions.

<p align="center">
  <img src="https://raw.githubusercontent.com/mever-team/itw-sm/website/static/images/comparison.png" width="90%"/>
</p>

**Key findings**

- **Backbones** — DINO-V2 outperforms CLIP-based encoders for AID, thanks to self-supervised training focused on visual understanding rather than image–text alignment.
- **Training data** — retraining on in-the-wild data consistently helps; end-to-end models benefit more from scale than methods relying on frozen pre-trained spaces.
- **Pre-processing** — TextureCrop preserves high-frequency synthetic artifacts in high-resolution images far better than center cropping or resizing.
- **Augmentations** — simulating compression and noise is vital to bridge the gap between training and real-world data.

See the [project page](https://mever-team.github.io/itw-sm) or the
[paper](https://arxiv.org/abs/2507.10236) for the full ablation tables.

## Citation

If you find ITW-SM or this study useful, please cite:

```bibtex
@inproceedings{konstantinidou2026navigating,
  title     = {Navigating the Challenges of AI-Generated Image Detection in the Wild: What Truly Matters?},
  author    = {Konstantinidou, Despina and Karageorgiou, Dimitrios and Koutlis, Christos and Papadopoulou, Olga and Schinas, Emmanouil and Papadopoulos, Symeon},
  booktitle = {The 5th ACM International Workshop on Multimedia AI against Disinformation (MAD '26)},
  year      = {2026},
  doi       = {10.1145/3810988.3812665},
  url       = {https://arxiv.org/abs/2507.10236}
}
```

## Acknowledgements

We thank Zacharias Chrysidis for his assistance with late-stage experimentation
on VL models. This work is funded by the Horizon Europe projects
**vera.ai** (GA No. 101070093), **AI-CODE** (GA No. 101135437), and **ELIAS**
(GA No. 101120237). Computational resources were provided by the National
Infrastructures for Research and Technology **GRNET** and funded by the EU
Recovery and Resilience Facility.

## License

The contents of this repository are released under the
[Apache-2.0 License](LICENSE).

The **ITW-SM dataset** is distributed for **research purposes only**. Please refer to the terms
on the [dataset page](https://huggingface.co/datasets/dkarageo/itw-sm) before use.
