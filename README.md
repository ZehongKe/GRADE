# GRADE: Guiding Realistic Autonomous Driving with Adaptive Trajectory Evolution

[![CVPR 2026](https://img.shields.io/badge/CVPR-2026-blue)](https://cvpr.thecvf.com/)
[![License](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)

This is the official implementation of **GRADE** (CVPR 2026), a unified framework for autonomous driving that performs planning through iterative trajectory evolution.

## 📖 Overview

Autonomous driving requires generating high-quality trajectories that balance multiple competing objectives (safety, comfort, efficiency) across complex scenarios. Existing methods typically rely on a single aggregated reward, struggling to explicitly model trade-offs between different planning objectives.

**GRADE** addresses this by introducing a unified planning framework with adaptive weight fluctuation that dynamically adjusts the importance of different factors during optimization.

---

## 🎯 Key Contributions

### 🔄 Unified Framework for Autonomous Driving

GRADE provides a **unified architecture** that works seamlessly across different settings:

- **Dual Compatibility**: Supports both **modular motion planning** (with vectorized inputs) and **end-to-end driving** (with raw sensor inputs)
- **Flexible Guidance**: Compatible with any custom trajectory scorer—whether **rule-based** or **learning-based**
- **Post-processing Module**: Can be deployed as a standalone planner or used to enhance existing models

### ⚙️ Adaptive Evolution Strategy

To explicitly regulate trade-offs between competing objectives, GRADE introduces an adaptive weight fluctuation mechanism that:

- Identifies performance bottlenecks in each iteration
- Dynamically upweights weak dimensions during optimization
- Achieves faster convergence with more balanced outcomes

### 🏆 SOTA Performance

GRADE achieves state-of-the-art performance on both major autonomous driving benchmarks:

- **nuPlan (Motion Planning)**: Best performance on Test14-hard (**80.06**) and Test14 (**91.65**)
- **NAVSIM (End-to-End)**: Achieves **92.1 PDMS** when combined with iPad—the new SOTA
- **Strong Generalization**: Consistent improvements across different scenarios and difficulty levels

---

## 🏗️ Framework

<p align="center">
  <img src="assets/pipeline.pdf" alt="GRADE Framework">
</p>

GRADE consists of three core components:

1. **Diffusion-based Trajectory Generator**: Lightweight unconditional diffusion model for diverse proposals
2. **Multi-dimensional Scorer**: Evaluates trajectories across safety, comfort, efficiency, etc.
3. **Adaptive Evolution Loop**: Identifies weak dimensions and adjusts weights iteratively

---

## 📊 Main Results

### nuPlan Benchmark (Motion Planning)

| Method | Val14 | Test14-hard | Test14 |
|--------|-------|-------------|--------|
| PDM-Closed | 92.12 | 75.19 | 91.63 |
| PDM-Hybrid | 92.11 | 76.07 | 91.28 |
| PLUTO | 76.88 | 76.88 | 90.29 |
| **GRADE (Ours)** | 90.36 | **80.06** | **91.65** |

GRADE achieves the best performance on Test14-hard and Test14, demonstrating superior robustness across challenging scenarios.

### NAVSIM Benchmark (End-to-End Driving)

| Method | NC | DAC | TTC | Comf. | EP | PDMS |
|--------|----|----|-----|-------|----|----|
| DiffusionDrive | 98.2 | 96.2 | 94.7 | 100 | 82.2 | 88.1 |
| iPad | 98.6 | 98.3 | 94.9 | 100 | 88.0 | 91.7 |
| **GRADE (Ours)** | 97.0 | 98.6 | 92.2 | 99.8 | 85.6 | 89.4 |
| GRADE + DiffDrive | 98.6 | 98.8 | 95.2 | 99.8 | 86.4 | 91.4 |
| **GRADE + iPad** | **98.8** | **99.0** | **95.3** | 100 | 87.6 | **92.1** |

When used as a post-processing module, GRADE significantly improves existing planners (e.g., +3.3 PDMS for DiffusionDrive).

### 🔄 Compatible with Different Planners

| Base Planner | w/o GRADE | w/ GRADE | Improvement |
|--------------|-----------|----------|-------------|
| Diffusion-ES | 60.69 | **86.83** | +43.1% |
| PLUTO | 88.79 | **91.49** | +3.0% |
| PDM-Closed | 86.87 | **89.32** | +2.8% |

GRADE consistently enhances planning performance across diverse planner types.

### 📈 Flexible Across Different Scorers

| Scorer | w/o GRADE | w/ GRADE | Improvement |
|--------|-----------|----------|-------------|
| PDM-Closed v1 | 84.99 | **91.26** | +7.38% |
| PDM-Closed v2 | 73.63 | **79.54** | +8.23% |
| S2O | 89.76 | **96.46** | +7.46% |

Validated across multiple evaluation systems with different weight configurations.

### ⚡ Efficiency Analysis

<p align="center">
  <img src="assets/efficiency_analysis.png" alt="Efficiency Analysis" width="600">
</p>

The adaptive weight fluctuation mechanism achieves faster convergence to superior results compared to fixed-weight strategies.

### 🚗 Real-vehicle Validation

<p align="center">
  <img src="assets/real-vehicle-scenes.png" alt="Real-vehicle Scenes" width="700">
</p>

<p align="center">
  <img src="assets/real-veh-exp-results.png" alt="Real-vehicle Results" width="700">
</p>

Validated on real autonomous vehicles across 6 scenarios in Suzhou, China, involving various interactions with human-driven vehicles.

---
## 📄 License

MIT License - see [LICENSE](LICENSE) for details.

---

## 📅 Release Roadmap

- [x] **README** - Project overview and documentation
- [ ] **Environment Setup** - Installation instructions and dependencies
- [ ] **Source Code** - Full implementation release
- [ ] **Training & Evaluation** - Scripts, configs, and pretrained checkpoints

⭐ **Star this repository to get notified about updates!**
