## Analytics of retail store events with VLMs [cctv]

### Pixels
Brands care about demographics, product and category affinity of their customers. They would like to know how much time people spend on looking at their products, so they can design their campaigns effectively. Instrumentation for online commerce is well developed with precise pixels capturing every user interaction and analytics + ML systems detecting patterns. These help merchandisers make decisions about pricing, placement, tg etc. We want to develop an offline equivalent for pixels.

This is a prelimnary design of such a system. You can find an implementation that uses Gemini here : [github repo](https://github.com/4g/cctv)

### Cameras
In India retailers are forced to install cameras as its a compliance requirement. These cameras are mostly IP cameras with attached DVR or NVR, and are accessible over network via RTSP. 

### VLMs
VLMs such as Gemini, Qwen-VL are excellent at understanding videos. Here is an example of Gemini's response given a video from ucf_crime dataset.

![image](https://raw.githubusercontent.com/4g/cctv/refs/heads/main/assets/shoplifting.gif)

```json
[
  {"timestamp": "00:00", "comment": "A man in a white shirt is standing at a display table with several devices. He has a grey cloth draped over his shoulder."},
  {"timestamp": "00:06", "comment": "He is looking down at the devices on the table."},
  {"timestamp": "00:14", "comment": "He starts to interact with one of the devices, possibly a tablet."},
  {"timestamp": "00:17", "comment": "He is focusing on the device, handling it with both hands."},
  {"timestamp": "00:20", "comment": "He lifts the device from its stand while still holding the cable connected to it."},
  {"timestamp": "00:23", "comment": "Alert: He quickly disconnects the device from the display cable and is now holding it freely."},
  {"timestamp": "00:30", "comment": "He has the device completely free from the stand and is holding it at his side."},
  {"timestamp": "00:33", "comment": "He looks around briefly before moving away from the table."},
  {"user": "A man in a white t-shirt and a grey cloth draped over his shoulder.", "actions": "Interacted with a device on a display table, disconnected it from the security cable, and moved away from the table with the device in hand."}
]
```

Gemini can capture and classify people activity, e.g. 'a 30 year old male picked chips from right shelf and kept it in his basket'. With some prompting, VLMs can be used to convert videos to events !!

### Some numbers

#### Cost
A large retail store stays open around 15+ hours in a day and has can have 100+ cameras. Small retailers have ~5 cameras. 

Gemini samples videos at 1fps, and tokenizes each image into 66 tokens at low resolution (and 200 tokens at high resolution). Thus an hour of video(without audio) has 240k tokens (800k at high res). At 0.15$/1M tokens input, each hour costs us 0.036$ at low res. This is about 3Rs./hour

Shops dont always have customers inside them. We can extract video chunks where atleast one person is shopping to reduce the size of video. Average chunk length would be the amount of time a person was in front of a camera (~15s)

So analyzing videos of a shop with 5 cameras, that opens for 12 hours in day, and has 20% occupancy will cost Rs. 36 per day in tokens. 

#### Latency
For 1000 input tokens Gemini produces 300 tokens/sec and time to first token is ~300ms. [link](https://artificialanalysis.ai/models/gemini-2-5-flash#time-to-first-answer-token). 

Thus end to end latency to process a 15 second chunk is < 1s. This is close to real time and effective in making on site decisions too. E.g. if a person is stealing goods from shop, an alert can be raised within 5 seconds. 

### System
We have to:
1. Connect to millions of IP cameras
2. stream all videos and detect chunks where people are present 
3. pass the chunks to Gemini, and ask for structured transcription of video
4. store gemini outputs in a queryable storage

#### Saving camera streams is bandwidth bound
Connecting to many cameras and saving their output every few minutes, doesnt require a lot of compute. Lets say a camera streams at 1280x720 @ 15fps = ~100KB/s after encoding. To stream and save output of 1000 cameras we need bandwidth of ~100MB/s. To store this we need 360GB / hr. 

#### Chunking to retain relevant bits is compute bound
Process the video with yolo and retain chunks where people are there. yolo works at 5fps on a single cpu thread. so we need 1 cpu core per video if we want to retain 5fps per video. A GPU like L4 can process 350fps.

Comparing costs to process 70 cameras across gpu and cpu machines:
1. Single L4 machine can process 350fps or 70 cameras = 1$/hr
2. a single cpu core does 5fps, we need 70 cpu cores = c5.18xlarge = 3$ / hr

For analytics we dont need real time data, and we can process videos in batches. We can use spot gpu instances for this. that cost 0.4$/hr. 

Most DVR devices expose old saved videos also via track apis and we can download these after 6 hours. This lets us use spot machines for download also. 

#### Pipeline
1. **Download and save**, bottleneck is network speed of dvr. Hence we may have long running tasks. Download camera videos in parallel and save them at 5fps to s3. Submit video urls to queue as downloads finish. Use spot machines, because source of truth is persistent. Scale the system down as downloads finish. 

2. **Chunk**: Queue the finished downloads. Use spot gpu machines to chunk videos. Submit chunks to another queue. 

3. **VLM** : Pull chunks from queue and upload them to gcp. GCP File API allows 20GB uploads per project per day. So we need to send videos along with the request instead. Trigger async requests within limit of gemini rpm and let writes happen in either a db or fs then db.

4. **Analytics Queries**: For analytical queries any standard db and query will do. data is small in size, few KBs per camera per day. Even after a year the amount of data will not exceed GBs.

5. **Search queries** : Now that we have transcribed what is happening in the video, we can also execute search across the text, to retrieve relevant chunks. Embed the text corresponding to chunks, and run a simple embedding match. Index embeddings if there is too many of them. 