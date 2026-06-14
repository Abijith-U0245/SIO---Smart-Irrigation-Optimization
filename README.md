<div align="center">

# SIO — Smart Irrigation Optimization System

### *Precision AI for Precision Agriculture*

[![Platform](https://img.shields.io/badge/Platform-Altair%20RapidMiner%20AI%20Studio-orange?style=for-the-badge)](https://altair.com/altair-ai-studio/)
[![Model](https://img.shields.io/badge/Model-Random%20Forest-brightgreen?style=for-the-badge)](#ml-pipeline)
[![Accuracy](https://img.shields.io/badge/Accuracy-86%25-blue?style=for-the-badge)](#results)
[![Theme](https://img.shields.io/badge/Theme-Agriculture-yellowgreen?style=for-the-badge)](#)
[![License](https://img.shields.io/badge/License-MIT-lightgrey?style=for-the-badge)](LICENSE)

<br/>

> **Agriculture consumes 70% of the world's freshwater — yet up to 60% is wasted.**
> SIO uses Machine Learning to tell farmers exactly *when* to irrigate and *how much* — cutting waste without cutting yield.

<br/>

[Watch Demo](https://youtu.be/ju7gJz8-ReI?si=wFf5eIl_JyCExMuf) &nbsp;·&nbsp; [Dataset](#dataset) &nbsp;·&nbsp; [Workflow](#ml-pipeline) &nbsp;·&nbsp; [Results](#results)

</div>

---

## <img src="https://api.iconify.design/lucide/list.svg" width="20"/> Table of Contents

- [The Problem](#the-problem)
- [The Solution](#the-solution)
- [Dataset](#dataset)
- [ML Pipeline](#ml-pipeline)
- [Results](#results)
- [Repository Structure](#repository-structure)
- [How to Run](#how-to-run)
- [Real-World Impact](#real-world-impact)
- [SDG Alignment](#sdg-alignment)
- [Tech Stack](#tech-stack)
- [Authors](#authors)

---

## <img src="https://api.iconify.design/lucide/alert-triangle.svg" width="20"/> The Problem

| Statistic | Reality |
|---|---|
| Global freshwater used by agriculture | **70%** |
| Of that water, amount wasted | **up to 60%** |
| Farmers with access to data-driven irrigation tools | **very few** |

Traditional irrigation relies on intuition, fixed schedules, or guesswork. The result?

- **Over-irrigation** → waterlogging, root rot, runoff, salinity buildup
- **Under-irrigation** → stunted growth, crop failure, yield loss
- **No feedback loop** → farmers can't learn what worked

Small-scale farmers — who produce a significant share of the world's food — are hit hardest. They lack the tools, data, and expertise to optimise water use. **SIO changes that.**

---

## <img src="https://api.iconify.design/lucide/lightbulb.svg" width="20"/> The Solution

**SIO (Smart Irrigation Optimization)** is an AI-powered Decision Support System that puts precision irrigation in farmers' hands using nothing but low-cost sensor data.

```
Given: soil moisture, weather, crop type, growth stage
  ↓
SIO predicts:
  [+]  Should I irrigate today?   →  Yes / No  (86% accuracy)
  [+]  How much water is needed?  →  X mm
```

### Key Capabilities

| Capability | Detail |
|---|---|
| Irrigation Decision | Binary classification — Irrigate: **Yes / No** |
| Water Quantity | Regression — exact water requirement in **mm** |
| Multi-Crop Support | Wheat, Rice, Maize, Cotton, Sugarcane, Soybean, Tomato, Potato |
| IoT-Ready | Designed to work with low-cost ESP32 / DHT / soil sensor inputs |
| Interpretable | Includes Decision Tree for white-box explainability |

---

## <img src="https://api.iconify.design/lucide/database.svg" width="20"/> Dataset

| Property | Details |
|---|---|
| Records | **2,000** |
| Features | **11** |
| Targets | `Water_Requirement (mm)` + `Irrigate (Yes/No)` |
| Source | Custom synthetic irrigation dataset |

### Feature Overview

```
Input Features
├── Soil_Moisture        (%)          — primary irrigation signal
├── Temperature          (°C)         — evapotranspiration driver
├── Humidity             (%)          — atmospheric water demand
├── Rainfall_7day        (mm)         — recent precipitation
├── Soil_pH                           — crop-specific tolerance
├── Solar_Radiation      (MJ/m²/day)  — energy driving transpiration
├── Growth_Stage                      — vegetative / flowering / maturity
└── Crop_Type                         — one of 8 crops

Output Targets
├── Water_Requirement    (mm)         — regression target
└── Irrigate             (Yes/No)     — classification target
```

### Crop Types Supported

```
Wheat  |  Rice  |  Maize  |  Cotton
Sugarcane  |  Soybean  |  Tomato  |  Potato
```

---

## <img src="https://api.iconify.design/lucide/workflow.svg" width="20"/> ML Pipeline

Built entirely in **Altair RapidMiner AI Studio** (Free Academic License). The workflow is an 8-stage visual pipeline:

```
┌─────────────┐    ┌────────────┐    ┌──────────────────┐    ┌───────────┐
│  Read CSV   │───▶│  Set Role  │───▶│Select Attributes │───▶│ Normalize │
│ Import data │    │ Label + ID │    │Remove irrelevant  │    │  Z-Score  │
└─────────────┘    └────────────┘    └──────────────────┘    └─────┬─────┘
                                                                    │
┌─────────────┐    ┌────────────┐    ┌──────────────────┐    ┌─────▼─────┐
│ Performance │◀───│Apply Model │◀───│  Random Forest   │◀───│Split Data │
│  Evaluate   │    │  Test set  │    │ Train classifier  │    │  70 / 30  │
└─────────────┘    └────────────┘    └──────────────────┘    └───────────┘
```

### Stage-by-Stage Breakdown

| # | Stage | Purpose |
|---|---|---|
| 1 | **Read CSV** | Load `irrigation_dataset.csv` into RapidMiner |
| 2 | **Set Role** | Mark `Irrigate` as label; assign ID column |
| 3 | **Select Attributes** | Drop irrelevant or redundant features |
| 4 | **Normalize** | Z-transformation — zero mean, unit variance |
| 5 | **Split Data** | 70% training / 30% testing (stratified) |
| 6 | **Random Forest** | Train ensemble classifier (100 trees) |
| 7 | **Apply Model** | Run model on held-out test set |
| 8 | **Performance** | Compute accuracy, precision, recall, confusion matrix |

> **Also included:** A **Decision Tree** model for interpretability — allows farmers and agronomists to follow the exact rules the model uses.

---

## <img src="https://api.iconify.design/lucide/bar-chart-2.svg" width="20"/> Results

<div align="center">

| Metric | Value |
|---|---|
| Classification Accuracy | **86%** |
| Estimated Water Savings | **30%+ per season** |
| Crops Supported | **8** |
| Dataset Size | **2,000 records** |
| Primary Model | **Random Forest** |
| Secondary Model | **Decision Tree** (interpretability) |

</div>

### What 86% Accuracy Means in Practice

If 100 irrigation decisions are made daily, SIO gets **86 right using only what a cheap IoT kit provides**. Over a growing season, this translates to:

- Fewer unnecessary irrigation cycles
- Reduced waterlogging events
- Optimised water volume per irrigation event
- Better crop health outcomes

---

## <img src="https://api.iconify.design/lucide/folder-tree.svg" width="20"/> Repository Structure

```
SIO---Smart-Irrigation-Optimization/
│
├── irrigation_dataset.csv                # Primary dataset (2,000 records, 11 features)
├── Crop_recommendation.csv               # Supplementary crop reference data
├── Smart_Irrigation_Optimization.rmp     # RapidMiner process file — full ML workflow
├── Smart_Irrigation_Xpecto26.pptx        # Project presentation (Xpecto 2026)
└── README.md                             # This file
```

> **Key file:** `Smart_Irrigation_Optimization.rmp` — open this in Altair RapidMiner AI Studio to run the full pipeline end-to-end.

---

## <img src="https://api.iconify.design/lucide/terminal.svg" width="20"/> How to Run

### Prerequisites

- [Altair RapidMiner AI Studio](https://altair.com/altair-ai-studio/) — **Free Academic License** available for students

### Steps

```bash
# 1. Clone the repository
git clone https://github.com/Abijith-U0245/SIO---Smart-Irrigation-Optimization.git
cd SIO---Smart-Irrigation-Optimization
```

```
# 2. Open RapidMiner AI Studio

# 3. Import the process
   File → Open Process → Select Smart_Irrigation_Optimization.rmp

# 4. Verify dataset path
   The Read CSV operator should point to: irrigation_dataset.csv
   (Update the file path if needed via the operator's settings panel)

# 5. Run the workflow
   Click the Run button (or press F11)

# 6. View results
   Check the Performance operator output for accuracy metrics
   Check the Apply Model output for per-record predictions
```

### Expected Output

```
Accuracy: ~86%
Predicted columns:
  - prediction(Irrigate): Yes / No
  - confidence(Yes): 0.00 – 1.00
  - confidence(No):  0.00 – 1.00
```

---

## <img src="https://api.iconify.design/lucide/globe.svg" width="20"/> Real-World Impact

```
                    Water Saved
                         │
          ┌──────────────┼──────────────┐
          ▼              ▼              ▼
    Small Farmers   Large Farms    Arid Regions
    Precise alerts  Bulk savings   Critical need
          │              │              │
          └──────────────┼──────────────┘
                         ▼
              Healthier Crops
              Lower Input Costs
              Sustainable Agriculture
```

| Stakeholder | Benefit |
|---|---|
| Small-scale farmers | Actionable daily irrigation alerts, no expertise needed |
| Large farms | Systematic water budgeting across fields |
| Governments / NGOs | Tool for agricultural policy and water management programs |
| IoT integrators | ML backend ready for ESP32/Arduino sensor pipelines |

---

## <img src="https://api.iconify.design/lucide/target.svg" width="20"/> SDG Alignment

<div align="center">

| SDG | Goal | How SIO Contributes |
|---|---|---|
| **SDG 2** | Zero Hunger | Improved crop yields through precise irrigation reduces food insecurity |
| **SDG 6** | Clean Water & Sanitation | Reduces agricultural freshwater consumption by 30%+ |
| **SDG 13** | Climate Action | Lower water usage reduces energy costs of pumping, cutting carbon footprint |
| **SDG 17** | Partnerships | Open-source, deployable by NGOs and agri-tech startups |

</div>

---

## <img src="https://api.iconify.design/lucide/layers.svg" width="20"/> Tech Stack

| Component | Technology |
|---|---|
| ML Platform | Altair RapidMiner AI Studio (Academic) |
| Primary Model | Random Forest Classifier |
| Secondary Model | Decision Tree (interpretability) |
| Data | Custom synthetic CSV dataset |
| Evaluation | Accuracy, Precision, Recall, Confusion Matrix |
| IoT Compatibility | ESP32, DHT11/22, Capacitive Soil Moisture sensors |
| Presentation | PowerPoint (Xpecto 2026) |

---

## <img src="https://api.iconify.design/lucide/play-circle.svg" width="20"/> Demo

<div align="center">

[![SIO Demo Video](https://img.shields.io/badge/Watch%20Demo-YouTube-red?style=for-the-badge&logo=youtube)](https://youtu.be/ju7gJz8-ReI?si=wFf5eIl_JyCExMuf)

*Full walkthrough of the RapidMiner workflow, dataset, and results*

</div>

---

## <img src="https://api.iconify.design/lucide/user.svg" width="20"/> Authors

<div align="center">

**Abijith U**
Secretary, GDG On Campus · Chennai Institute of Technology

[![GitHub](https://img.shields.io/badge/GitHub-Abijith--U0245-181717?style=flat-square&logo=github)](https://github.com/Abijith-U0245)
[![LinkedIn](https://img.shields.io/badge/LinkedIn-abijithu45-0A66C2?style=flat-square&logo=linkedin)](https://linkedin.com/in/abijithu45)

</div>

---

## <img src="https://api.iconify.design/lucide/file-text.svg" width="20"/> License

This project is licensed under the **MIT License** — feel free to use, modify, and distribute with attribution.

---

<div align="center">

*Built for farmers, for the planet, and for the future of food.*

**If this project helped you, leave a star.**

</div>
