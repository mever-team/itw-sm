# ITW-SM — Project Page

This branch (`website`) hosts the **GitHub Pages project page** for the paper:

> **Navigating the Challenges of AI-Generated Image Detection in the Wild: What Truly Matters?**
> Despina Konstantinidou, Dimitrios Karageorgiou, Christos Koutlis, Olga Papadopoulou, Emmanouil Schinas, Symeon Papadopoulos
> *The 5th ACM International Workshop on Multimedia AI against Disinformation (MAD '26), 2026*

🌐 **Live page:** <https://mever-team.github.io/itw-sm>

[![Project Page](https://img.shields.io/badge/Project-Page-2563eb)](https://mever-team.github.io/itw-sm)
[![arXiv](https://img.shields.io/badge/arXiv-2507.10236-b31b1b)](https://arxiv.org/abs/2507.10236)
[![Main branch](https://img.shields.io/badge/branch-main-181717?logo=github)](https://github.com/mever-team/itw-sm/tree/main)

---

## About

This is a landing page site presenting our study of AI-generated image
detection (AID) **in the wild** and the accompanying **ITW-SM** dataset — 10,000
real and AI-generated images collected from four major social media platforms
(Facebook, Instagram, LinkedIn, and X). The page summarizes the paper's
key contributions.

For the paper's analysis code, dataset and models download, see the
[`main` branch README](https://github.com/mever-team/itw-sm/tree/main).

## Local preview

No build step is required — it is a plain static site.

```bash
git checkout website
python3 -m http.server 8000
# then open http://localhost:8000
```

## Credits

This page was built using the
[Academic Project Page Template](https://github.com/eliahuhorwitz/Academic-project-page-template), which was adapted from the
[Nerfies](https://nerfies.github.io) project page.

## Citation

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

## License

The project-page content is licensed under **CC BY-SA 4.0** . Other repository materials are licensed under
**Apache-2.0** (see [`LICENSE`](LICENSE)).
