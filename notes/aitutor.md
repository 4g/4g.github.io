## Tools of a teacher

We explain things by trying to reach a shared state of ‘imagination’, where the other person is also ‘seeing’ what I am. This can be achieved by conversation where students try to visualize on their own, or by diagramming, where a visual is forced and both teacher and student work on \\same visual. 

differential : [https://www.youtube.com/watch?v=F40ZBDAG8-o](https://www.youtube.com/watch?v=F40ZBDAG8-o)  
photon emission from atom : [https://www.youtube.com/watch?v=sj52It93sWY](https://www.youtube.com/watch?v=sj52It93sWY)

1. Whiteboard with continuous editing marker  
2. Pointer to point at things on board  
3. Speaking to indicate information  
4. Knowledge of students state of mind

### Diagramming

*Real world Interactive diagramming*   
HCVerma explaining : [https://youtu.be/clgV9QtKtPE?t=660](https://youtu.be/clgV9QtKtPE?t=660)

*Attempts to diagram with current tools*

1. 24 kg nails to 9kg with a balancing pan

[https://claude.ai/chat/f91b3b4c-d0f8-4606-923a-7adad82fc72e](https://claude.ai/chat/f91b3b4c-d0f8-4606-923a-7adad82fc72e)

1. Chess board with 62 pieces  
   [https://claude.ai/chat/ebd63536-953e-473c-bcb4-a334fa0273da](https://claude.ai/chat/ebd63536-953e-473c-bcb4-a334fa0273da)  
     
2. Chatgpt teaching (non-interactive diagrams)  
   [https://youtu.be/\_nSmkyDNulk?t=58](https://youtu.be/_nSmkyDNulk?t=58)

*Problems*

1. Diagrams can be drawn with code, but are not very fine grained.   
2. people draw while speaking, and use pointers to point to the diagram  
3. Most explanations are visual, even in text heavy subjects such as mathematics, computer science, finance etc. 

### Students level of understanding

Expressing state can be hard with LLMs : [https://claude.ai/chat/b38140ac-841f-4b00-aa62-41fa6f2429bc](https://claude.ai/chat/b38140ac-841f-4b00-aa62-41fa6f2429bc)

1. If LLMs can eventually do everything a person does on a computer, can they become a good tutor ? : many proof points, physics wallah, coursera, mit ocw etc.   
   1. Need to validate if online learning sitting on a computer is a valid alternative to 

**Path to AI tutor**

1. Need data of tutors teaching students to make a good tutor  
2. Students in coaching classes prepare for exams, because there are very less good schools and colleges in india. Exam matters a lot and so does exam prep.   
3. Exam prep requires a lot of question solving and students solve many mock papers  
4. Although coaching centres help a lot with tutoring, they don’t help a lot with personal question solving

**POC** 

1. Solve a set of math, physics and chemistry questions on the app  
2. Add few concepts with details of their content  
3. Meter bridge question  
   1. Api wrapper for gpt  
   2. Content for meter bridge, fixed diagrams etc.   
   3. Audio recording and transcription  
   4. Hint after transcription \+ check api  
   5. Populate results in bottom drawer  
4. get question api, question sent as json, rendered on page as html  
5. display area for llm output  
6. send question \+ current answer and get hint and check api working  
7. write a doc  
   1. question bank and book scans \+ index  
   2. audio of user alongwith screen  
   3. simplest way for user to indicate what they need \[highlight information on page directly\]  
   4. audio \+ gestures  
8. store audio and send audio to get transcript. integrate one of live tts apis
