---
layout: default
title: Resume — Evan Hanif Widiatama
---

## About

AI Engineer focused on delivering production-ready AI systems with strong backend engineering and DevOps practices. Experienced in end-to-end machine learning, computer vision, LLM, and time series solutions for real-world problems. Proficient in Python for ML development and Node.js/Go for backend services, deploying scalable systems on Linux with Docker and CI/CD. Hands-on with vector databases, embeddings, and RAG pipelines, from edge hardware (NVIDIA Jetson) and real-time video pipelines to REST APIs and full-stack dashboards.

Detailed narratives with diagrams live in the [case studies](/projects/face-recognition-mining/). Printable version: hit Ctrl+P on this page.

## Profiles

🔗 [**LinkedIn**](https://www.linkedin.com/in/evanhanif/) | [**GitHub**](https://github.com/evanhfw) | [**DataCamp**](https://www.datacamp.com/portfolio/studiesevan) | [**Kaggle**](https://www.kaggle.com/vnn777) | [**Blog**](/blog/) | [**Certifications**](/certifications/) | [**Email**](mailto:evan.hanif.w@gmail.com)

📍 Semarang, Indonesia

## Experience

### **AI Engineer** | rubythalib.ai
📍 **May 2026 – Present** | Remote, deployed to Sinarmas Mining / PT Borneo Indobara

- Architected and productionized a **face recognition system**, raising accuracy from 0% in production to **97%** in R&D. [Case study](/projects/face-recognition-mining/)
- Raised **truck plate (OCR) accuracy** at a disposal site from **60% to 94%** by identifying root causes and bottlenecks, then developing a new model to fix them. [Case study](/projects/truck-plate-ocr/)
- Cut edge deployment (**NVIDIA Jetson**) RAM usage from **8GB to 1.8GB** and **24GB to 8GB** by identifying and fixing memory leaks.
- Eliminated missing evidence data at a hauling site from approximately **40% to 0%** by redesigning the upload architecture: Jetson devices sent images over the local network to a relay server, which handled uploads to Google Cloud Storage. [Case study](/projects/edge-relay-upload/)
- Deployed AI services to edge servers using NVIDIA Jetson for on-site real-time inference in mining safety operations.

**Tech:** Python, FastAPI, DeepFace, PostgreSQL, MySQL, Linux, Docker, NVIDIA Jetson, Google Cloud Storage

### **Computer Vision Engineer (Intern)** | DataIns (PT Global Data Inspirasi)
📍 **Dec 2024 – Apr 2025** | Yogyakarta

- Migrated object detection pipelines from **YOLOv10 to YOLOv11**, optimizing inference speed and accuracy.
- Retrained models on domain-specific datasets, achieving improvement in mAP/FPS/precision.
- Developed a computer vision system integrating object detection (YOLOv11) with **optical flow/tracking algorithms** to estimate vehicle speed from video streams.

**Tech:** Ultralytics YOLO, OpenCV, Roboflow Supervision

### **Machine Learning Engineer (Intern)** | rubythalib.ai
📍 **Jul – Dec 2025** | Remote

- Built computer vision systems for mining safety use cases at Sinarmas Mining: detection, tracking, and real-time video analytics, iterating on prototypes that later evolved into production-grade safety monitoring systems.
- Worked on engineering tickets across model development, video pipelines, backend integration, and deployment readiness.

**Tech:** Python, Ultralytics YOLO, CNN, OpenCV, TensorRT, NVIDIA DeepStream, FFmpeg, MediaMTX

### **Research Assistant** | Universitas Sebelas Maret
📍 **Dec 2024 – Jul 2026** | Surakarta

- Collaborated with a professor on a grant-funded research project to design high-accuracy **time series forecasting** and regression models using sliding window cross-validation. [Case study](/projects/electricity-forecasting/)
- Achieved a **30-day forecast MAPE of 1–2%** on real sequential data.
- Delivered an oral presentation of research methodology and results at **BiCopam 2024** (Brawijaya International Conference on Pure and Applied Mathematics).

**Tech:** XGBoost, Skforecast, Sktime, Shapley Values

## Projects

### **Hireonai.web.id** | Founder & Product Lead
*Jan 2026 – Present* · [github.com/hireonai](https://github.com/hireonai) · [Case study](/projects/hireonai/)

- Led end-to-end product lifecycle and built a cross-functional team of **5 engineers** from ideation to deployment.
- Built an **LLM-powered CV optimization agent** and AI cover letter generator.
- Built a **hybrid job recommendation engine** (**ChromaDB** + LLM embeddings retrieval with similarity scoring and ranking).
- Trained a transformer-based salary range predictor and a job category classifier.

**Tech:** Docker, GitHub Actions, Google Cloud Run, Google Vertex AI, ChromaDB, GCE, GCS

### **Dicodex** | Bootcamp Analytics Dashboard
*Personal project* · [github.com/evanhfw/dicodex](https://github.com/evanhfw/dicodex)

- Full-stack analytics dashboard (React/TypeScript + FastAPI) centralizing coding bootcamp cohort data; reached **1,000+ uses** by facilitators.
- Multi-user credential handling with no persistent credential storage; Dockerized full stack; CI/CD auto-deploys Docker images to a self-hosted VPS on every push to main.

**Tech:** React, TypeScript, FastAPI, Selenium, Docker Compose, GitHub Actions

### **VisionAI** | CCTV Traffic Analytics Platform
*Personal project, Feb 2026 – Present* · [github.com/evanhfw/visionai](https://github.com/evanhfw/visionai)

- Polyglot microservices platform for CCTV traffic analytics (Clean Architecture); vehicle detection layer in Python with OOP-based design, YOLO + OpenCV over GPU-accelerated RTSP/HLS streams (FFmpeg NVENC + MediaMTX).
- Planned: Go backend API layer, AI-powered SQL chatbot for natural-language querying of traffic data.

**Tech:** Python, YOLO, OpenCV, FFmpeg, MediaMTX, Go (planned), Docker

### **Homelab & Self-Hosted Infrastructure**
*Personal project, Feb 2025 – Present* · [Case study](/projects/homelab-cctv/)

- 4-node self-hosted infrastructure (workstation, mini-PC, STB controller, cloud VPS) connected over **Tailscale mesh**; all services containerized with Docker; monitoring with Uptime Kuma. This website runs on it. [Live stats](/lab/)
- Real-time CCTV analytics pipeline: **Frigate** person detection + **ArcFace** face recognition, detections logged to a database, real-time WhatsApp alerts.

**Tech:** Docker, Tailscale, Linux, Frigate, YOLO, ArcFace, PostgreSQL/MySQL, WhatsApp API, Uptime Kuma

## Education

🎓 **B.S. in Statistics** | Universitas Sebelas Maret, Surakarta | **Aug 2022 – Jul 2026**

- GPA: **3.57 / 4.00**
- Thesis: compared feature-engineering approaches for electricity load forecasting to identify the configuration with the lowest prediction error.
- Teaching Assistant: Big Data Timeseries (Jan 2026 – Jul 2026), Neural Networks and Introduction to Data Mining (Aug 2025 – Dec 2025)

## Skills

- **ML & Data:** Python · Machine Learning · Computer Vision · YOLO · DeepFace · XGBoost · Time Series Forecasting · Regression Modelling · LLM & RAG Systems · ChromaDB · Vector Databases
- **Backend & Infrastructure:** FastAPI · Go · Node.js · Docker · Linux · PostgreSQL · MySQL · CI/CD · Google Cloud Platform

## Achievements

🏆 **1st Winner** – Olimpiade Statistika SPSS | BINUS 2024 — XGBoost + SHAP for in-depth data analysis.

🏅 **Top 4** – LKTI Jambore Statistika XIV | Universitas Mulawarman 2025 — paper: "Narkoscan: Inovasi Deteksi Narkolepsi — Pengembangan Model Prediktif XGBoost berbasis Situs Web".

📄 **Festival Ilmiah Mahasiswa 2025** | Universitas Sebelas Maret — "DiabetTest: Sistem Deteksi Diabetes Berbasis AI dan ML untuk Optimasi Layanan Kesehatan di Daerah 3T".

🥇 **Ranked 1/196 (public)** – Hology 7.0 | Universitas Brawijaya 2024 — multilabel-multiclass CV classification (t-shirt vs hoodie, categories and colors).

🥇 **Ranked 4/222 (public), 3/222 (private)** – Dataslayer 2.0 ML Competition | Telkom University Purwokerto 2024 — computer vision classification.

🥇 **Ranked 9/84 (public), 7/84 (private)** – ANAVA Data Quest 2026 | Universitas Gadjah Mada — multiclass classification.

## Certifications

📜 Data analytics, data science, and machine learning certifications (Google, DataCamp, Dicoding, DeepLearning.AI). Full list [**here**](/certifications/).

## Languages

- **Indonesian**: Native
- **English**: B2 (British Council EnglishScore, 426)
