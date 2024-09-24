# Study Freund
A LLM powered study app to make you study more smartly. 

## Details
The app uses LLMs, either local (Using Ollama) or with openAI key for using models like gpt4 etc. The start of the app will be with providing the course slides.The texts from the slides will be extracted and a segmantation mechanisms will be researched. The segmentation will be done according to the chapters. The detection of the chapters will be done automatically with some algorithms. 

Each of the segmented chapter will be fed into the LLM of choice will some predefined prompts. The LLM will then give out the features listed below. 

The information from the LLM will be used to form Flashcards, quizes etc. The questions from the quizes for example, can be used to test the student in a daily basis. 

# features 
* Summarization
* Automatic Topic segmentation
* Flask card generation
* Quiz generation
* 5 Year-Old explanation to hard concepts
* Creating Anagrams for memorizing bullet points

## Input
You just need to provide all the study materials (slides) to the app and it will do the rest.


### TODO
- [ ] Start a python notebook for testing
- [ ] Configure an LLM preferably from Groq cloud
- [ ] Write PDF extracting mechanisms
- [ ] Research about topic segmentation technologies.


## Segmentation technique
The most basic segmantion from the slides is the pages. We can say that each page in the slides in talking about different concepts while bigger concepts can snap across multiple slides as well. Thus we cannot always be sure that a new topic is starting in every page. 

What can be done is to get semantic embeddings from each sentences in the slide. The embeddings can then be matched to see if the topic is new or not. However, this requires more credits to be used by the paid users of chatGPT. For the free open-source LLM users, that is not a problem. 