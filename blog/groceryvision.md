## ICCV Retail workshop Competition
https://grocery-vision.github.io/

### Track 1

- 3 classes of events : Take, Return, Rummage
- Temporally and spatially locate the events. Temporal boundaries are frame precise. Spatial boundaries are bounding boxes around objects involved. 
- Camera is always placed at same location, inside the cart.  
- A single frame can be a part of multiple events

### Dataset
- 271 Videos
- 300k Frames
- 52k tagged frames with bboxes and event classes
- total 4k events ~1300 each class 

### One VLM to rule them all
- VLMs can emit rough bounding boxes
- VLMs can temporally locate event boundaries

**Context length problem** : In training set largest given video is 90 seconds@25fps = 2250 images
- Pixel shuffle brings tokens down to 81 per image
- 2250 * 81 = 182250 tokens is very very long
- So we need to iteratively detect precise boundaries, starting from 1fps = 90*81 = 7290 tokens ~8k tokens

**Classification accuracy** : Training set has about 4k events. 
- Training smolvlm to classify events on videos at 3fps gives about 88% accuracy after one epoch. So SmolVLM can detect these events, and they are detectable at 3fps.
- This is a small 2.2B vlm. Using Gemma might yeild better results. 


### Ideas to try

1. **Rolling Window (VLM)** : Keep a fixed number of frames at one time. Train to mark all of them. Use previous frames results in context ensuring continuity. 
    - 1st sequence : `<f1><f2><f3><f4><f5>| -> <r1><r2><r3><r4><r5>`
    - 2nd sequence : `<f2><f3><f4><f5><f6>|<r2><r3><r4><r5> -> <r6>`

    **Estimated Training Tokens (More quality tokens, more learning)**:
    - 1 image = 81 tokens
    - total images in dataset : ~300k
    - images with annotation : ~72k
    - one result = ~x,y,w,h,class ~10 tokens
    - 300k * 10 = ~3M tokens with loss (no loss will flow from image tokens as visual encoder is frozen)
    - 3M tokens are ok for finetuning
    - sequence of 25 images per sample
    - Number of samples => 300k (more samples can be made by augs like skipping frames, rotation/flipping of video)
    - Context length-> 25 * 81 + 25 * 10 = ~2250
    - Total tokens passing through = 300k * 2k = 600M tokens (1day on H100)
    - Total loss tokens = 300k * 250 = 75M tokens (actual 3M, 25x repeats due to windowing)
    - configurable -> 
        - seq len = 25, 
        - skip frames = 2
        - video rotation
        - video horizontal flip
        - vlm backbones -> smolvlm2, gemma3/3n, qwen2.5-3B 

2. **Video embedder (+regressor)** : VJEPA2, Video-Prism are both very high quality video embedders that emit sequence embeddings for videos. 
    - Known to work very well for event datasets like ssv2
    - Take video embeddings and train spatial-temporal regressors on top
    - https://huggingface.co/collections/facebook/v-jepa-2-6841bad8413014e185b497a6
    - VJEPA2 300M -> input 64 frames -> (8192, 1024) embedding
    - https://huggingface.co/facebook/vjepa2-vitl-fpc64-256/blob/main/notebook_finetuning.ipynb
    - much smaller and faster to train than a full vlm.

