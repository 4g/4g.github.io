### Fraud Detection & Liveness Verification

![Liveness Pipeline Overview](<INSERT_IMAGE_URL_1>)  
![Multi-Modal Signal Timeline](<INSERT_IMAGE_URL_2>)

**Machine Learning Lead** @ Fi.money — Jul 2022 to Jul 2023

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
- Resulted in removal of 100k+ accounts and stopped similar number from onboarding. 
