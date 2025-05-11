# CartVision

### Month 1

**Test and finalize architecture**
There are no systems that work out of box for this problem. And there are multiple ways to design one. 
So first we will determine an architecture that works for this problem within given constraints (like compute budget and latency). First month will be spent in testing different architectures, their trainability, latency etc. 

Two example designs of this system can be : 
* Should we fine-tune YOLO and detect objects, then write a model to work on top of those detections?
* Or should we use a small VLM like Qwen-VL and fine-tune it to work for this problem?

We will write rough implementations of above and other systems and test their behaviour against sample data.  

We will also create a dummy cart in Bangalore to create realistic data.

**Deliverable** : Finalized architecture, its data and compute requirements. A Dummy cart in Bangalore that works similar to snappik.  

* **Engineer**: 1 CV engineer
* **Compute required**: Yes, Approx H100 × 240 hours
* **Snappik**: bandwidth required for requirements review

---

### Month 2

**Data collection & tagging**

Once a system architecture is finalized, we will start collecting data to finetune underlying models.

* For a YOLO-based approach: get bounding boxes around salient objects, and tag events in videos
* For a VLM approach: create time-aligned transcripts and event labels

This month will be spent collecting data, creating tools for it, and labeling the samples.

**Deliverable** : Data pipeline to collect data for system designed above. 

* **Engineer**: 1 CV engineer + 1 Snappik person (to ensure our data is correct)
* **Compute required**: Minimal (annotation server & storage)
* **Snappik**: bandwidth for data collection specs

---

### Month 3

**Train v0 model & evaluate**
Now that we have the data and architecture implemetation ready, we will start training the model. We will agree on a metric with Snappik so we can track the quality of system at all times. 

* Train baseline model (YOLO + downstream events classifier or fine-tuned VLM)

**Deliverable** : v0 of model and system.

- **Engineer**: 1 CV engineer
- **Compute required**: Yes, H100 x 480 hrs
- **Snappik**: None

---

### Month 4

**Integrate v0 & collect live data**

Deploy the v0 model onto a Snappik cart prototype for testing.

* Deploy the model into a server so that it supports parallel requests
* Run live sessions in stores and collect video/log data for error analysis
* Identify failure modes and edge-case scenarios

**Deliverable** : First working demo on the cart with reasonable accuracy. 

- **Engineer**: 1 CV engineer
- **Compute required**: yes. Inference only. L40 or A6000 for 600 hours. 
- **Snappik**: bandwidth for integration support and live-run coordination

---

### Month 5

**Iterate & refine model**

Use live-collected data to retrain and optimize model under real-world conditions. This will be a continuous process. 

* Retrain on new examples addressing v0 failures
* Optimize model size/architecture for latency and compute budget
* Achieve target accuracy (F1/recall/specificity) within production constraints

**Deliverable** : Improved accuracy. And a production ready model that is fast and accurate enough to be deployed in real life.  

- **Engineer**: 1 CV engineer
- **Compute required**: Yes, 240 x H100 GPU-hrs
- **Snappik**: bandwidth for feedback sessions and result validation

---

### Month 6

**Build production infra & deploy**

Finalize your production-grade inference infrastructure and roll out the refined model. Steps:

* Design and deploy a scalable inference service
* Quantize model so it can be deployed in production 
* Conduct final tuning and end-to-end acceptance testing

**Deliverable** : Model deployed in production within acceptable accuracy and latency. 

- **Engineer**: 1 CV engineer
- **Compute required**: Yes, Will depend on production scale
- **Snappik**: bandwidth for deployment coordination and handover documentation


## Resources : 

* Compute over 6 months : 1260 H100 hours [reserved cost : 4000$]
* 1 CV engineer : 10k pounds per month
