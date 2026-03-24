# Real-Time Speech Translation System

Collab: https://colab.research.google.com/drive/1Q1AoobxYZVnUClrpEsrCTh3R7tB1JPat?usp=sharing#scrollTo=hEWAA-pX3Blk

Streaming speech recognition, translation, and voice synthesis pipeline with real-time playback in the browser.

---

## 🚀 Overview

This project implements a **real-time audio processing pipeline**:

microphone → speech recognition → translation → speech synthesis → playback

The system is designed as a **modular streaming architecture** with low-latency processing.

---

## 🧩 Architecture

Pipeline stages:

1. Audio capture (browser)
2. Streaming to backend (WebSocket)
3. Speech recognition (ASR)
4. Phrase stabilization
5. Machine translation
6. Text-to-speech (TTS)
7. Audio playback (browser)

Each stage runs independently and communicates via queues.

---

## ⚙️ Key Features

* Real-time audio streaming from browser (Web Audio API)
* Low-latency ASR using Faster-Whisper
* Phrase stabilization via hypothesis buffering
* Parallel translation and synthesis
* Voice cloning (XTTS v2)
* Queue-based pipeline for non-blocking processing
* Debug channel for observing system behavior

---

## 🧠 Interesting Engineering Solutions

### Hypothesis Stabilization

Streaming ASR produces unstable outputs.
To fix this:

* Maintained history of hypotheses
* Aligned outputs across time
* Extracted stable prefix using voting

Result:

* reduced text flickering
* more consistent output

---

### Sliding Window Processing

* Window size: 2s
* Step: 0.35s

Balanced:

* latency
* recognition stability

---

### Lightweight VAD

Used simple signal features:

* energy
* zero-crossing rate

Reduced unnecessary model calls and improved performance.

---

### Queue-Based Architecture

Separate queues for each stage:

* audio → ASR
* ASR → translation
* translation → TTS

Benefits:

* parallel processing
* no blocking
* easier scaling

---

## 🛠 Tech Stack

**Backend**

* Python
* FastAPI
* WebSockets

**ML**

* Faster-Whisper
* Hugging Face Transformers (translation)
* Coqui TTS (XTTS v2)

**Frontend**

* JavaScript
* Web Audio API
* AudioWorklet

---

## ⚠️ Limitations

* Prototype-level system
* Synthetic VAD
* Limited language support
* No production optimization

---

## 🚀 Future Improvements

* Advanced VAD
* Latency optimization
* More languages
* Better streaming strategies

---

## 📎 Notes

This project demonstrates how modern ML models can be combined into a real-time system rather than used in isolation.
