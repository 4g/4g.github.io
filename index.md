### Indian Food Recognition & Automated Logging

![Food Recognition UI](<INSERT_IMAGE_URL_1>)  
![Sample Detections](<INSERT_IMAGE_URL_2>)

**Role & Timeline**  
Machine Learning Lead @ HealthifyMe — May 2018 to Jul 2019  
**Location:** Bengaluru, India

**Overview**  
Faced with high dropout rates due to manual food logging, I shipped India’s first AI-powered “snap‐and‐log” system in just **2 weeks**—proving feasibility to our CEO/CTO. Over 1 million Indian‐food images were collected to train a bespoke deep‐learning classifier, achieving > 83 % accuracy on diverse regional dishes. Thousands of users now log meals via a single tap.

**Key Contributions**  
- **Rapid Prototype (2 weeks):**  
  - Curated an initial dataset of 5 K+ home‐cooked dishes.  
  - Trained a lightweight CNN from scratch; deployed behind a simple Flask API and basic web UI.  
- **Scale & Accuracy:**  
  - Expanded to a **1 million–image Indian Food Dataset** covering 1 500+ dish classes.  
  - Optimized model for < 100 ms inference on CPU; integrated quantization and pruning.  
- **Production Deployment:**  
  - Built a production service for real‐time image upload, inference, and calorie estimation.  
  - Instrumented analytics to track usage and guide iterative improvements.

**Impact**  
- **User Engagement:** Snap‐and‐log feature increased meal‐logging retention by 60 %.  
- **Business Value:** Convinced leadership to spin out a dedicated Computer Vision team.

**Resources**  
- Press: [How HealthifyMe’s Ria 2.0 AI Assistant Improves Diet Tracking](https://indianexpress.com/article/technology/social/healthifyme-wants-to-improve-your-diet-with-its-ria2-0-ai-assistant-here-is-how-5544698/) :contentReference[oaicite:0]{index=0}  
### EyeMouse: Gaze-Based Cursor Control System

![Gaze Geometry Diagram](<INSERT_IMAGE_URL_1>)  
![EyeMouse Prototype Demo](<INSERT_IMAGE_URL_2>)

**Role & Timeline**  
Final-Year Project @ IIT Kanpur — 2011

**Overview**  
Built India’s first real-time gaze-driven cursor control system from scratch, without relying on neural nets or heavyweight CV libraries. The user simply looks at a point on screen, and the system maps head and eye landmarks via geometric models to move the cursor there with sub-100 ms latency on modest CPU hardware.

**Key Contributions**  
- **Custom Landmark Detection:** Implemented low-latency iris and head-pose estimation using handcrafted geometric algorithms.  
- **Lightweight Pipeline:** Optimized image capture, feature extraction, and mapping routines to run at ≥15 FPS on a single core, without GPU acceleration.  
- **End-to-End Integration:** Connected video input, gaze estimation, and OS‐level cursor APIs into a turnkey desktop application.

**Awards & Impact**  
- **IBM WebContest Innovation Award** for “Best Student Project” (2011)  
- Sparked my first hardware-software startup, partnering with an electronics engineer to build interactive assistive devices.

**Resources**  
- Paper: [IBM WebContest Winning Submission (PDF)](https://github.com/4g/4g.github.io/raw/master/IBM%20paper.pdf)  
## Indri: Ultralight Audio Model

![Indri Architecture Diagram](../../../Downloads/seq_diag.png)

**Overview**  
Indri is a novel, ultra-small transformer-based TTS/ASR model that treats audio as discrete tokens. It supports both Hindi and English, and delivers high-quality, style-consistent speech synthesis and recognition—all in a 124 M-parameter footprint.

**Key Features**  
- **Tiny & Fast:** Just 124 M parameters (GPT-2 small backbone) yet achieves realtime on CPU and up to 10× realtime on consumer GPUs (e.g. RTX6000 Ada: 400 tokens/s, <20 ms to first token).  
- **Streaming & Voice-Cloning:** Autoregressive audio-token decoding with streaming output; supports speaker style prompts (<5 s) for consistent voice cloning.  
- **Bilingual & Code-Mixing:** Natively handles English, Hindi, and mixed-language inputs.  
- **End-to-End Pipeline:**  
  1. Text → text-tokens  
  2. GPT-2 LM → audio-tokens  
  3. Mimi decoder → waveform

**Audio Samples**  
- **Sample 1:** मित्रों, हम आज एक नया छोटा और शक्तिशाली मॉडल…  
  <audio controls src="https://huggingface.co/11mlabs/indri-0.1-124m-tts/resolve/main/data/cebed668-62cb-4188-a2e1-3af8e017d3ba.wav"></audio>  
- **Sample 2:** भाइयों और बहनों, ये हमारा सौभाग्य है कि…  
  <audio controls src="https://huggingface.co/11mlabs/indri-0.1-124m-tts/resolve/main/data/6e0a4879-0379-4166-a52c-03220a3f2922.wav"></audio>  
- **Sample 3:** Hello दोस्तों, future of speech technology mein…  
  <audio controls src="https://huggingface.co/11mlabs/indri-0.1-124m-tts/resolve/main/data/5848b722-efe3-4e1f-a15e-5e7d431cd475.wav"></audio>  
- **Sample 4:** In this model zoo, a new model called Indri…  
  <audio controls src="https://huggingface.co/11mlabs/indri-0.1-124m-tts/resolve/main/data/7ac0df93-edbd-47b2-b850-fb88e329998c.wav"></audio>

**Links & Resources**  
- Blog post: [Building Indri TTS](https://www.indrivoice.ai/blog/2024-11-21-building-indri-tts)  
- Model & demos: [11mlabs/indri-0.1-124m-tts on Hugging Face](https://huggingface.co/11mlabs/indri-0.1-124m-tts)  
- Code & self-hosted service: [github.com/cmeraki/indri](https://github.com/cmeraki/indri)
### Fraud Detection & Liveness Verification

![Liveness Pipeline Overview](<INSERT_IMAGE_URL_1>)  
![Multi-Modal Signal Timeline](<INSERT_IMAGE_URL_2>)

**Role & Timeline**  
Freelance ML Engineer @ Fi — Jul 2022 to Jul 2023  
**Location:** Bengaluru, India

**Overview**  
Designed and built a real-time liveness verification system to block sophisticated fraudsters during Fi account onboarding. Users record an 8 s video speaking 4 random digits—our pipeline processes the first 8 s at 5 fps, extracting multi-modal time-series signals from both video and audio to detect spoofing attempts (replayed videos, displayed photos, hired actors).

**Key Components**  
- **Preprocessing:**  
  - Trim to first 8 s (≤40 frames) @ 5 fps; run ffmpeg/ffprobe with a 5 s timeout to handle corrupt or long videos.  
  - MediaPipe face & facemesh extraction via an object pool for concurrency safety.  
  - Audio loaded as a 1D NumPy waveform.  
- **Image Signals:**  
  1. **Spoof Score:** MobileNet classifier flags photo/video replays (moire patterns, device borders).  
  2. **Lip-Openness:** Distance between upper & lower lips to verify speech.  
  3. **Multi-Face Consistency:** Embedding-distance score to spot extra actors.  
  4. **Video Quality:** Frame brightness & variance metrics.  
  5. **Face Quality:** Face centroid & size stability.  
- **Audio Signals:**  
  1. **Human Speech Probability:** YAMNet @ 4 Hz to isolate speech segments.  
  2. **OTP Match Score:** Whisper-based ASR with n-gram matching (0.25/unigram, 0.5/bigram, …).  
- **Model:**  
  1D convolutional network across [40 time-steps × N signals], learning temporal and cross-signal anomalies (e.g. heard speech without lip movement).

**Deployment & Impact**  
- Packaged as a Dockerized FastAPI service (Gunicorn + 2 Uvicorn workers) on port 8085; also deployed on Kubernetes via Jarvis.  
- Reduced fraudulent onboarding by ~‍X % (internal metric).  

**Resources**  
- Repo: [epiFi/inhouse-liveness](https://github.com/epiFi/inhouse-liveness)  
- Sample Spoof Demo: [Watch Video](<INSERT_VIDEO_URL>)  ## Rank 1 @ Kaggle UltraMNIST 

![Synthetic Data Samples](<INSERT_IMAGE_URL_1>)  
![Detection & Classification Pipeline](<INSERT_IMAGE_URL_2>)

**Role & Timeline**  
Independent Project — Kaggle UltraMNIST Competition (Date)

**Overview**  
Secured **1st place** on the Kaggle UltraMNIST challenge with **99.109%** test accuracy. Combined a small-object detector (YOLOv5s) and a high-accuracy classifier (EfficientNetV2-B1) on a custom synthetic dataset to handle 2560×2560 images containing up to five tiny digits.

**Key Components**  
- **Synthetic Data Generation**  
  - Created checkerboards with boxes, circles, triangles.  
  - Applied perspective, rotation, zoom, and uniform digit placement (all 70 000 MNIST digits + empty images).  
- **Detection (YOLOv5s)**  
  - Input: 2560×2560; augmentation: light rotate/scale/translate/HSV/mosaic.  
  - Config: `conf_threshold=0.1`, `iou_threshold=0.1`, class-agnostic NMS, `max_det=5`.  
  - Recall > 95%.  
- **Classification (EfficientNetV2-B1)**  
  - Input: 128×128 crops (aspect-ratio normalized).  
  - Pretrained on ImageNet; light aug (shift/scale, perspective, invert, blur, HSV).  
  - Training: 200 epochs, LR schedule [3e-4 → 1e-5], TTA (invert images).  
  - Accuracy > 98%.  
- **Post-Processing**  
  - Removed nested detections and low-confidence (< 0.45) preds.  
  - Final ensemble accuracy: **99.109%**.

**Resources**  
- Code & Models: [github.com/4g/umnist](https://github.com/4g/umnist)  
- Competition: [UltraMNIST on Kaggle](https://www.kaggle.com/competitions/ultra-mnist)  
- Writeup : https://www.kaggle.com/competitions/ultra-mnist/discussion/319145## Pose Estimation on the Edge: Real-time Workout Feedback

![Embedded ML Architecture](<INSERT_IMAGE_URL_1>)  
![Model Variants Performance](<INSERT_IMAGE_URL_2>)

**Role & Timeline**  
Machine Learning Lead @ cult.fit — Jul 2020 to Dec 2021

**Overview**  
Built an on-device pose-estimation pipeline using TensorFlow Lite to power interactive workouts with real-time rep-counting, energy scoring, and form feedback without any server round-trips.

**Model & Deployment**  
- **Architecture:** CenterNet-inspired U-Net with MobileNet backbone, predicting 30 keypoint heatmaps (256×256 → 64×64).  
- **Variants:**  
  - **SMALL:** 1.27 M params, 58.6 FPS on laptop CPU  
  - **MEDIUM:** 2.45 M params, 29.8 FPS  
  - **LARGE:** 3.79 M params, 5.8 FPS 
  - **Edge Optimizations:** Mixed-precision training, data caching, and TFLite integration for sub-20 ms/frame inference on mobile CPUs.

**Robustness & Accuracy**  
- **Augmentations:** Random occlusion, brightness/contrast shifts, 90° rotations, horizontal flips.  
- **Inference Enhancements:**  
  - **Dynamic Cropping:** Uses last-frame keypoints to crop noisy inputs.  
  - **Low-Pass Filter:** Smooths high-frequency jitter for stable joint tracking. :contentReference[oaicite:4]{index=4}&#8203;:contentReference[oaicite:5]{index=5}

**Applications**  
- **Rep Counting:** Rule-based state machine on keypoints, deployed in the cult.fit app and gym-mirror prototype.  
- **Energy Meter:** Velocity-based scoring displayed live in UI to gamify workouts.

**Links & Resources** 
- Demo Images:  
  - [Architecture Diagram](https://drive.google.com/file/d/1bXlJB7xrEURkRF_aE9Sv25fHI5e0RkwY/view?usp=sharing)  
  - [Energy Meter UI](https://drive.google.com/file/d/18nPmwtC2yCFOxkDcAbVycDC2HkEqrS93/view?usp=sharing)
## Search and Ranking Systems - 2015
- Automated synonym generation, spell-correction, and query understanding.  
- Patents:  
  - [US20180060936A1: Search Ranking System](https://patents.google.com/patent/US20180060936A1)  
  - [US20160350395A1: Synonym Generation](https://patents.google.com/patent/US20160350395A1)
- Designed deep NNs to match user queries with document text & images.


### Synonym Generation System

![Synonym Generation Pipeline](<INSERT_IMAGE_URL_1>)  
![Similarity Scoring Diagram](<INSERT_IMAGE_URL_2>)

**Role & Timeline**  
Staff Engineer @ BloomReach — Oct 2013 to Mar 2018  
**Location:** Bengaluru, India

**Overview**  
Led the design and implementation of an **automated synonym generation** pipeline for BloomReach Discovery, processing **100 million+ product descriptions** and **30 million+ queries** weekly to extract high-quality synonym pairs for e-commerce search :contentReference[oaicite:0]{index=0}.

**Key Features**  
- **Data Mining & Representation:**  
  - Extract candidate phrase pairs from product catalog text, Web crawl, and search logs.  
  - Build contextual embeddings via co-occurrence contexts, click-through distributions, document-vector averages, and session proximity. :contentReference[oaicite:1]{index=1}  
- **Similarity Metrics & Filtering:**  
  - Combine symmetric (JS divergence) and asymmetric (hyponym/hypernym) measures, augmented by edit-distance heuristics.  
  - Apply phrase-specific thresholds (e.g. ensuring D(P, Q) < D(P, P′) where P′ is a known variant) to filter high-confidence pairs.  
  - Train a supervised classifier on multi-score feature vectors to rank and grade synonyms.  
- **Continuous Learning:** Weekly batch updates to capture evolving language, new trends, and seasonal shifts in user queries.

**Patents**  
- **US20180060936A1:** Search Ranking System—contextual term weighting and nonessential term filtering :contentReference[oaicite:3]{index=3}  
- **US20160350395A1:** Synonym Generation & Identification—vector-based candidate filtering & similarity modules :contentReference[oaicite:4]{index=4}  

**Resources**  
- Blog: [Discovery | Synonym Generation at Bloomreach](https://dev.to/bloomreach/discovery-synonym-generation-at-bloomreach-ob5)
