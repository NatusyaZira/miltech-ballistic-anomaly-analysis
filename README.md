# MilTech Ballistic Anomaly Analysis: $\Delta V_0$ Forecasting for D-30 Artillery Systems

## Overview

This repository contains a data analytics module designed to parse artillery firing logs and separate systematic errors (barrel wear) from high-amplitude variance (propellant/charge batch quality).

The mathematical and logical framework aligns with operational principles used in digital tactical systems like **"Kropyva" (Кропива)**, specifically focusing on isolating and predicting initial velocity deviations ($\Delta V_0$).

## Problem Statement

In field environments, tactical software requires precise input for velocity drops to calculate ballistic corrections. However, raw log data is highly corrupted by human entry errors, missing values ($NaN$), and extreme variance. For instance, while cumulative barrel wear accounts for a stable drop of roughly $-0.3\%$, ammunition charge batch variations can cause massive, unpredictable dispersion up to $-7\%$.

This project implements an automated pipeline to clean raw log data, isolate the impact of different ammunition batches, and visualize prediction reliability.

## Key Features & Tech Stack

- **Data Cleansing & Imputation:** Leveraging `NumPy` and `Pandas` to identify human errors, filter anomalies via statistical masking (`np.where`), and handle missing data ($NaN$) using logical interpolation based on target distance and system telemetry.
- **Statistical Separation:** Disentangling systematic degradation from stochastic charge variance using cumulative metrics (`np.cumsum`).
- **Data Visualization:** Built with `Seaborn` and `Matplotlib` to generate distribution plots (Violin/Box plots) for charge variance, allowing tactical commanders to instantly spot unstable ammunition batches.

## Dataset Structure

The analytical pipeline processes simulated 2,000-shot logs with the following features:

- `shot_id` / `barrel_id` — Chronological tracking of system wear.
- `ammunition_batch` — Categorical grouping of propellant data (e.g., `10A-25`).
- `sight_setting` — Tactical elevation metrics.
- `v0_barrel_delta` / `v0_charge_delta` — Disintegrated error parameters.
- `miss_distance_m` — Recorded fire deviation.

---

_Note: This is an independent analytical R&D project utilizing synthesized open-source ballistic logic and contains no restricted or classified military data._
