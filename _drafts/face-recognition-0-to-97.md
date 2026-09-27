---
title: "Face recognition in a mining site: from 0% to 97%"
date: 2026-09-27
tags: [computer-vision, face-recognition, edge, jetson]
---

*Draft: bagian bertanda [[ISI]] harus diisi dulu dari catatanmu, jangan publish apa adanya. Angka yang sudah terverifikasi dari resume: 0% production -> 97% R&D; edge RAM 8GB -> 1.8GB; OCR plat 60% -> 94%.*

[[ISI: konteks produk. Dipakai untuk apa (attendance? safety monitoring?), siapa penggunanya, berapa kamera, kondisi lapangan (debu, cahaya, helm/APD menutupi wajah?), dan kenapa ini penting secara operasional.]]

## Titik awal: 0% di production

[[ISI: kenapa akurasinya 0% di production. Apa akar masalahnya: model generik tidak cocok domain? wajah terlalu kecil di frame? pencahayaan? angle kamera? orang pakai helm/masker? data registrasi tidak terkontrol? Kandidat model/pipeline awal apa yang dipakai?]]

## Yang saya ubah

[[ISI: pendekatannya. Contoh yang mungkin relevan: strategi pengumpulan data lapangan, pemilihan/retraining model (DeepFace/ArcFace-face recognition), threshold & face-size gating, perbaikan alignment, tuning kamera, atau perubahan arsitektur pipeline (deteksi -> alignment -> embedding). Tulis mekanisme konkret, bukan bahasa proses.]]

## Hasil

- R&D: **97%**
- Production: [[ISI: angka terakhir di production, dan metriknya apa (akurasi? TAR@FAR?)]]

## Pelajaran

- [[ISI: 2-3 pelajaran konkret]]
- Cerita sampingan yang layak jadi post sendiri: memory leak di NVIDIA Jetson (RAM 8GB -> 1.8GB dan 24GB -> 8GB) dan arsitektur upload evidence (data hilang ~40% -> 0%).
