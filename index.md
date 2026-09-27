---
layout: default
title: AI Engineer
image: /assets/img/og-card.jpg?v=2
---

## **About Me**
AI Engineer focused on delivering production-ready AI systems with strong backend engineering and DevOps practices. Experienced in end-to-end machine learning, computer vision, LLM, and time series solutions for real-world problems. Proficient in Python for ML development and Node.js/Go for backend services, deploying scalable systems on Linux with Docker and CI/CD. Hands-on with vector databases, embeddings, and RAG pipelines, from edge hardware (NVIDIA Jetson) and real-time video pipelines to REST APIs and full-stack dashboards.

Currently an **AI Engineer at rubythalib.ai**, deployed to **Sinarmas Mining / PT Borneo Indobara**, building production AI systems for mining safety operations.

## **Profiles & Portfolio**
🔗 [**LinkedIn**](https://www.linkedin.com/in/evanhanif/) | [**GitHub**](https://github.com/evanhfw) | [**DataCamp**](https://www.datacamp.com/portfolio/studiesevan) | [**Kaggle**](https://www.kaggle.com/vnn777) | [**Blog**](/blog/) | [**Certifications**](/certifications/) | [**Email**](mailto:evan.hanif.w@gmail.com)

📍 Semarang, Indonesia

🧪 **Playground:** [Ask AI](/chat/) · [Lab](/lab/) · [Terminal](/terminal/) · [Uses](/uses/)

---

## **Experience**

### **AI Engineer** | rubythalib.ai
📍 **May 2026 – Present** | Remote, deployed to Sinarmas Mining / PT Borneo Indobara

- Architected and productionized a **face recognition system**, raising accuracy from 0% in production to **97%** in R&D.
- Raised **truck plate (OCR) accuracy** at a disposal site from **60% to 94%** by identifying root causes and bottlenecks, then developing a new model to fix them.
- Cut edge deployment (**NVIDIA Jetson**) RAM usage from **8GB to 1.8GB** and **24GB to 8GB** by identifying and fixing memory leaks.
- Eliminated missing evidence data at a hauling site from approximately **40% to 0%** by redesigning the upload architecture: Jetson devices sent images over the local network to a relay server, which handled uploads to Google Cloud Storage.
- Deployed AI services to edge servers using NVIDIA Jetson for on-site real-time inference in mining safety operations.
- Integrated AI services with **PostgreSQL/MySQL** and operational systems for automated safety monitoring and auditability.

**Tech:** Python, FastAPI, DeepFace, PostgreSQL, MySQL, Linux, Docker, NVIDIA Jetson, Google Cloud Storage

### **AI Engineer Intern** | rubythalib.ai
📍 **Oct 2025 – Apr 2026** | Remote (Ajinomoto and Sinarmas Mining projects)

- Developed **PPE compliance detection** models and built action recognition experiments for worker activity monitoring and safety-related behavior detection (Ajinomoto PoC).
- Fine-tuned **YOLOv11 and CNN-based models** for object detection, worker detection, and visual classification tasks.
- Built computer vision systems for mining safety use cases at Sinarmas Mining: detection, tracking, and real-time video analytics, iterating on prototypes that later evolved into production-grade safety monitoring systems.
- Worked on engineering tickets across model development, video pipelines, backend integration, and deployment readiness.

**Tech:** Python, Ultralytics YOLO, CNN, OpenCV, TensorRT, NVIDIA DeepStream, FFmpeg, MediaMTX

### **Research Assistant** | Universitas Sebelas Maret
📍 **Dec 2024 – Jul 2026** | Surakarta

- Collaborated with a professor on a grant-funded research project to design high-accuracy **time series forecasting** and regression models using sliding window cross-validation.
- Achieved a **30-day forecast MAPE of 1-2%** on real sequential data.
- Delivered an oral presentation of research methodology and results at **BiCopam 2024** (Brawijaya International Conference on Pure and Applied Mathematics).

**Tech:** XGBoost, Skforecast, Sktime, Shapley Values

### **Computer Vision Engineer Intern** | DataIns (PT Global Data Inspirasi)
📍 **Dec 2024 – Apr 2025** | Yogyakarta

- Migrated object detection pipelines from **YOLOv10 to YOLOv11**, optimizing inference speed and accuracy.
- Retrained models on domain-specific datasets, achieving improvement in mAP/FPS/precision.
- Developed a computer vision system integrating object detection (YOLOv11) with **optical flow/tracking algorithms** to estimate vehicle speed from video streams.

**Tech:** Ultralytics YOLO, Roboflow Supervision

---

## **Selected Projects**

### **Hireonai.web.id** | Founder & Product Lead
*Jan 2026 – Present* · [github.com/hireonai](https://github.com/hireonai)

Founded and led an AI-driven job portal startup focused on intelligent career-matching tools, CV optimization, and personalized job recommendations.

- Led end-to-end product lifecycle (product vision, MVP scope, alignment with market needs) and built a cross-functional team of **5 engineers** (3 Fullstack, 2 ML) from ideation to deployment.
- Built an **LLM-powered CV optimization agent**: semantic CV-JD compatibility scoring via LLM embeddings with EdX API course recommendations.
- Built an **AI cover letter generator** and a **hybrid job recommendation engine** (**ChromaDB** vector database + LLM embeddings retrieval with similarity scoring and ranking).
- Trained a transformer-based salary range predictor and a job category classifier (Tech/Finance/HR/Others).

**Tech:** Docker, GitHub Actions, Google Cloud Run, Google Vertex AI, ChromaDB, Google Compute Engine, Google Cloud Storage

### **Dicodex** | Bootcamp Analytics Dashboard
*Personal Project* · [github.com/evanhfw/dicodex](https://github.com/evanhfw/dicodex)

- Built a full-stack analytics dashboard (React/TypeScript + FastAPI) that centralized coding bootcamp cohort data, turning it into actionable student performance insights.
- Reached **1,000+ uses** by program facilitators, demonstrating sustained value in monitoring cohort performance.
- Designed multi-user credential handling with no persistent credential storage; containerized the full stack with Docker Compose.
- Set up CI/CD with GitHub Actions to build and auto-deploy Docker images to a self-hosted VPS on every push to main.

**Tech:** React, TypeScript, FastAPI, Selenium, Docker Compose, GitHub Actions

### **VisionAI** | CCTV Traffic Analytics Platform
*Personal Project, Feb 2026 – Present* · [github.com/evanhfw/visionai](https://github.com/evanhfw/visionai)

- Designing a polyglot microservices platform for CCTV traffic analytics, structured around Clean Architecture principles.
- Built the vehicle detection layer in Python with OOP-based design (interfaces/abstract classes for detector, video source, output handlers), using YOLO and OpenCV over GPU-accelerated RTSP/HLS streams (FFmpeg NVENC + MediaMTX).
- Planning a Go backend API layer and an AI-powered SQL chatbot for natural-language querying over traffic analytics data.

**Tech:** Python, YOLO, OpenCV, FFmpeg, MediaMTX, Go (planned), Docker

### **Personal Homelab & Self-Hosted Infrastructure**
*Personal Project, Feb 2025 – Present*

- Architected and maintained a 4-node self-hosted infrastructure: Ryzen 9 9900X workstation (GTX 1660 Super), i3-1215U mini-PC, Armbian-based STB as central controller, and a cloud VPS as public-facing reverse proxy, all connected over a **Tailscale mesh VPN**.
- Containerized and deployed all services with Docker; uptime monitoring and alerting with Uptime Kuma.
- Built a real-time CCTV analytics pipeline with **Frigate** (person detection + ArcFace face recognition), logging detections to a database and sending real-time WhatsApp alerts.

**Tech:** Docker, Tailscale, Linux, Frigate, YOLO, ArcFace, PostgreSQL/MySQL, WhatsApp API, Uptime Kuma

---

## **Education**
🎓 **B.S. in Statistics** | Universitas Sebelas Maret, Surakarta | **Aug 2022 – Jul 2026**

- GPA: **3.57 / 4.00**
- Thesis: compared feature-engineering approaches for electricity load forecasting to identify the configuration with the lowest prediction error.
- Teaching Assistant: Big Data Timeseries (Jan 2026 – Jul 2026), Neural Networks and Introduction to Data Mining (Aug 2025 – Dec 2025)

---

## **Skills**
- **ML & Data:** Python · Machine Learning · Computer Vision · YOLO · DeepFace · XGBoost · Time Series Forecasting · Regression Modelling · LLM & RAG Systems · ChromaDB · Vector Databases
- **Backend & Infrastructure:** FastAPI · Go · Node.js · Docker · Linux · PostgreSQL · MySQL · CI/CD · Google Cloud Platform

## **Achievements**
🏆 **1st Winner** – Olimpiade Statistika SPSS | BINUS 2024
- Implemented an XGBoost model with SHAP values for in-depth data analysis.

🏅 **Top 4** – LKTI Jambore Statistika XIV | Universitas Mulawarman 2025
- Paper: "Narkoscan: Inovasi Deteksi Narkolepsi - Pengembangan Model Prediktif XGBoost berbasis Situs Web".

📄 **Festival Ilmiah Mahasiswa 2025** | Universitas Sebelas Maret
- "DiabetTest: Sistem Deteksi Diabetes Berbasis AI dan ML untuk Optimasi Layanan Kesehatan di Daerah 3T".

🥇 **Ranked 1/196 (Public)** – Hology 7.0 | Universitas Brawijaya 2024
- Multilabel-multiclass computer vision classification (t-shirt vs hoodie categories and colors).

📊 **Ranked 4/222 (Public), 3/222 (Private)** – Dataslayer 2.0 ML Competition | Telkom University Purwokerto 2024
- Computer vision classification.

📈 **Ranked 9/84 (Public), 7/84 (Private)** – ANAVA Data Quest 2026 | Universitas Gadjah Mada
- Multiclass classification.

## **Certifications**
📜 Data analytics, data science, and machine learning certifications (Google, DataCamp, Dicoding, DeepLearning.AI). Full list [**here**](/certifications/).

## **Languages**
- **Indonesian**: Native
- **English**: B2 (British Council EnglishScore, 426)
