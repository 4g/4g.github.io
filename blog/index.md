## Blog

experiments to understand LLMs/VLMs and how we may tame them. 

*I ask weird questions, and then answer them myself. Sometimes.*

### Oct 25
- [do visual cues help vlms](visual_cues.md): VLMs are very good at identifying events in videos. But it is hard to focus their attention on a specific action or object, specially if the object or action is a small part of the video. Humans use visual cues to attract attention towards a region or action, e.g. a stop sign on the road or a wiggly line drawn under wrongly spelled text. Once focused we can observe finegrained details from that region. This experiment is to determine if using visual cues like bboxes/trajectories will help VLMs focus better.


### June 25
- [using vlms to analyse retail stores](2025_retail.md): Brands care about demographics, product and category affinity of their customers. They would like to know how much time people spend on looking at their products, so they can design their campaigns effectively. Instrumentation for online commerce is well developed with precise pixels capturing every user interaction and analytics + ML systems detecting patterns. These help merchandisers make decisions about pricing, placement, tg etc. Can VLMs be used to build an offline equivalent for pixels? Most stores have cctv cameras that see all aisles and areas of a store. These cameras can see finegrained events like 'chips were picked but never kept in cart', which can form a detailed pixel like event heirarchy for bounce, add to cart, conversion. 

### May 25

- [models of small worlds](small_worlds.md) : LLMs are terrible at visual reasoning and cannot even reason around basic visual puzzles. 
There is a [million dollar prize](https://www.arcprize.org) to anyone who can make them 85% accurate on visual puzzles that are very simple for humans.
These puzzles use simple concepts such as copying, moving, colliding, large eats small etc. in a small world to create scenarios. 
To solve this, we need to find the precise program which will generate a scenario and apply it to a another instance of that world to solve a puzzle. 
This blog has my ideas, and attempts to solve this problem. 


### April 25
- [new internet](internet.md): how internet _might_ look in a few years. 


## Notes

- [MM duplex](mmduplex.md) : Can a Moshi like duplex model be made for videos ? And will it be better than usual vlms at parsing live events. This experiment was abandoned in favor of optical flow based video tokenizer. The code from mmduplex right now is a vlm that uses single token per image. It works well for describing videos.
- [Spatiotemporal tracking using vlms] (gvision.md) : Can vlms do precise spatio-temporal tracking of objects (No) ? Is that needed to solve real world problems, like detecting events (No) ? 

- [Time series prediction using transformers](timesfm.md) : Using timeseries for prediciting things like stock market. 
- [AI tutor](aitutor.md) : Is it even possible for an llm to actually teach without a shared mental space ? Teachers bring us to a shared space, by pointing to diagrams that they draw. Once I understand the diagram, the teacher and I are in the same shared visual space. Without this it is not possible to ensure the learner has understood. 