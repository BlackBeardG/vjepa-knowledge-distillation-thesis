# Self-Supervised Learning on Video Data for Resource-Constrained Environments

Diploma thesis, Aristotle University of Thessaloniki (AUTh), School of Electrical and Computer Engineering, Department of Electronics and Computers, 2026.

- **Author:** Georgios Ioannidis
- **Supervisor:** Prof. Anastasios Delopoulos
- **Co-supervisor:** Chrysa Episkopou, PhD candidate

📄 **[Read the thesis (PDF)](thesis.pdf)**

> The thesis is written in Greek (original title: *Αυτοεπιβλεπόμενη μάθηση με δεδομένα βίντεο για περιβάλλοντα με περιορισμένους υπολογιστικούς πόρους*). The English abstract is included in the PDF and reproduced below.

## Abstract

In recent years, the application of self-supervised learning (SSL) in computer vision has contributed significantly to advances in the field, enabling models to be pretrained on large volumes of unlabeled data and to learn generalizable visual representations. In this context, video foundation models have been developed that achieve strong performance across a wide range of applications. However, their large size and substantial memory, computational, and energy requirements limit their practical use.

The aim of this thesis is to investigate the feasibility of compressing a large video representation model pretrained through self-supervised learning. To this end, knowledge distillation is applied to transfer the knowledge of the original model to smaller and more computationally efficient architectures, suitable for resource-constrained environments.

More specifically, V-JEPA Large, a pretrained video foundation model, serves as the teacher, while the smaller V-JEPA Base, Small, and Tiny architectures serve as the students. The investigated strategies transfer knowledge either at the backbone level, by matching the representations produced by the teacher and the student, or at the level of the final predictions (logits) of the attentive classifier placed on top of the backbone, as well as through a combination of both approaches.

The effectiveness of these strategies is evaluated on human action recognition using the HMDB51 dataset. Depending on the strategy, the student models are trained either end-to-end or in two consecutive stages, comprising backbone distillation followed by the supervised training of the attentive classifier on its representations. This evaluation examines the extent to which the smaller architectures can approximate the performance of the teacher model and assesses the trade-off between classification accuracy and computational efficiency.

The experimental evaluation identifies backbone representation distillation, followed by separate training of the attentive classifier, as the most effective strategy. With the best configuration of this strategy, V-JEPA Base retains 94.2% of the teacher's accuracy with 70.3% fewer parameters. The smaller V-JEPA Small and Tiny offer an even greater reduction in parameters and memory requirements, with a corresponding trade-off in accuracy. Overall, the results indicate that the knowledge of a large self-supervised video model can be transferred to significantly smaller and less computationally demanding architectures, while retaining a substantial part of its performance.

**Keywords:** Self-Supervised Learning, Computer Vision, Video Foundation Model, Knowledge Distillation, V-JEPA

## Main results

HMDB51 split 1, test set. Students are distilled at the backbone level for 200 epochs on HMDB51 + UCF101, and then an attentive classifier is trained on HMDB51.

| Model | Test accuracy | % of teacher | Parameter reduction | Peak VRAM (MiB) | Throughput (videos/s) |
|-------|---------------|--------------|---------------------|-----------------|-----------------------|
| V-JEPA Large (teacher) | 81.31% | 100 | - | 2546 | 13.59 |
| V-JEPA Base (student) | 76.60% | 94.2 | 70.3% | 1400 | 38.39 |
| V-JEPA Small (student) | 72.75% | 89.5 | 92.4% | 693 | 55.28 |
| V-JEPA Tiny (student) | 61.31% | 75.4 | 98.0% | 402 | 57.71 |

Memory and throughput were measured on an NVIDIA A100 GPU, with batch size 16 and FP32. Throughput includes video decoding and preprocessing.

## Repository contents

```
thesis.pdf          Final thesis (Greek)
latex/DOCUMENT/     LaTeX source (main.tex, chapters, bibliography)
latex/PICS/         Figures used in the thesis
```

To build the PDF, run the following from `latex/DOCUMENT` (requires a TeX distribution with Greek support and the `kerkis` fonts):

```bash
pdflatex main && bibtex main && pdflatex main && pdflatex main
```

## Code

The experiment code will be released separately.

## Citation

```bibtex
@mastersthesis{ioannidis2026vjepakd,
  author = {Georgios Ioannidis},
  title  = {Self-Supervised Learning on Video Data for Resource-Constrained Environments},
  school = {Aristotle University of Thessaloniki},
  type   = {Diploma thesis},
  year   = {2026}
}
```

## License

© 2026 Georgios Ioannidis. All rights reserved. Figures reproduced from other works remain the property of their respective authors, and they are cited in the thesis.
