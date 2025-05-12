# Flicker of Hope (FoH): Examining the Impact of Animated Diffusion on Adversarial Patch Vulnerability

## 📘 Overview

"Flicker of Hope" (FoH) introduces a novel defense mechanism against adversarial patch attacks on object detection systems. Unlike traditional approaches, FoH leverages an Image-to-Video (I2V) diffusion model to dynamically alter input images, thereby degrading the adversarial patch’s effectiveness without modifying the underlying model.

---

## 🔍 Core Contributions

- ✅ Model-agnostic defense that does not require training on attacked data.
- 🎞️ Converts static adversarial images into video frames using Stable Video Diffusion (SVD).
- 📉 Demonstrated improved Mean Average Precision (MAP) scores compared to baseline and SAC defenses.
- 🧠 Proposes a new angle in adversarial defense research by animating static scenes.

---

📄 [Read the full report here](./Flicker%20of%20Hope%20-%20Final%20Report.pdf)

---

## 🛠️ Methodology

1. Input image xi is passed through the SVD model.
2. A short video (animation) is generated: Ai = SVD(xi).
3. A selected frame from Ai (e.g., frame 5) is passed to the object detector.
4. Predictions are made on the animated frame, not the static one.

### Architecture
```
[Static Image xi] → [SVD Image-to-Video] → [Selected Frame fAi] → [Object Detector] → [Object Predictions]
```

---

## ⚙️ Experimental Setup

- Dataset: MSCOCO (subset of 400 resized images, 576x1024)
- Adversarial Patch: DPatch (disappearance and illusion variants)
- Object Detector: Faster R-CNN
- Defense Baseline: Segment and Complete (SAC)
- Hardware: RTX 6000 Ada GPU

---

## 📈 Results Summary

| Method        | Clean | Disappearance (Adv.) | Illusion (Adv.) |
|---------------|--------|----------------------|-----------------|
| Baseline      | 0.391  | 0.140                | 0.131           |
| SAC           | 0.389  | 0.179                | 0.135           |
| FoH (Ours)    | 0.307  | 0.227                | 0.234           |

- FoH significantly outperforms SAC for Illusion attacks (p < 1e-19)
- Inference time overhead: SAC = +77 ms; FoH = +36 sec ⚠️

---

## 🔮 Future Work

- Swap SVD with faster and more efficient I2V models to reduce inference time.
- Integrate temporal attention mechanisms to further refine object preservation.
- Combine FoH with segmentation-based techniques for hybrid robustness.

---

## 📂 Repository Structure

```
.
├── Flicker of Hope - Final Report.pdf   # Project paper
├── README.md                            # This file
├── src/                                 # Source code
│   ├── fohtool.py                       # Main defense logic
│   └── utils.py                         # Utilities and metrics
└── data/
    └── coco_subset/                     # Evaluation dataset subset
```

---

## 👥 Authors

- Aviel Ben-Siman-Tov — avielben@post.bgu.ac.il
- Bar Dolev — dobar@post.bgu.ac.il
- Beni Ifland — ifliandb@post.bgu.ac.il
- Ido Paretsky — paretsky@post.bgu.ac.il
- Ken Yaggel — kenyag@post.bgu.ac.il
- Yarin Yerushalmi Levi — yarinye@post.bgu.ac.il
