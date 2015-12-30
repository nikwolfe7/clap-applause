# Applause Road Map #

_How do we proceed from here?_

## Desired Results ##

At the end of the semester, we would like to see (at least a prototype) of a Virtual World for interactive language learning, specifically low-resource and endangered languages. The end goal should have:

  1. A robust and accurate pronunciation scoring tool
  1. A web interface for users to submit pronunciation attempts for judges to score
  1. A web interface to allow judges to score pronunciation attempts by users so that we can continually improve the system
  1. A spoken interactive dialog system which can train users to improve their pronunciation in a given language over time
  1. An interface through which users can add language data for new / existing languages and have it seamlessly incorporated into the dialog tutoring system
  1. A mobile version of the aforementioned system to allow users in the field to contribute and interact with Applause
  1. A virtual world interface which can allow users to interact with virtual tutors to learn languages
  1. A [Speech Kitchen](http://speechkitchen.org/) virtual machine which can be distributed to anyone online


---

## How Do We Get There? ##

### 1. Pronunciation Scoring Tool ###

  * **Gathering Low-Resource Language Data:** We have already accumulated a lot of public domain data from the Peace Corps / Foreign Service, and various universities, in addition to the [CLAP](http://www.celebrate-language.com) corpus (not all of which is online).
    * ~~**TASK:** Finish gathering data, and choose a point to stop collecting~~
    * **TASK:** Get some statistics on the data to estimate how much we have in each language, and how much of it is transcribed

  * **Indexing and Organizing Language Data:** We need to come up with a definitive solution to organizing and indexing all data so that each and every phrase in every language can be easily found along with its transcription and translation (if available).
    * **TASK:** Chop up all remaining audio in CLAP corpus, and go back into the raw audio to retrieve second / third example attempts for each phrase
    * **TASK:** Organize CLAP corpus into nicely indexed database (MySQL?) and make sure there is a well-defined protocol for adding more data, e.g. we need a transcription, language name, module/lesson name, the audio, wav/mp3 formats, etc.
    * **TASK:** We need to organize the public domain language data we have for low-resource languages, convert it into the correct formats (mp3s are lossy but you can still make them into .wavs) and devise some way to chop them up and incorporate them into the same corpus as the CLAP system. If they are in different categories or do not match the CLAP corpus, the organizational structure should account for this.
    * **TASK:** We need to save the dialog / transcription structure of the FSI, Peace Corps, and other public domain data. If no dialog-based lesson structure is included, we can set those phrases aside for now (but still index them.)
      * Should we use English speech rec to transcribe the lessons? Will that work?
      * Are there transcriptions available? Can we transcribe them ourselves? Can we crowd source the work somehow?

  * **Testing / Fixing / Re-Evaluation of the Current Applause System:** We will almost certainly have to re-design some aspects of the Applause system.
    * **TASK:** Test the performance of the system using only MCD values for comparison. Can we be sure the articulatory features are helping?
    * **TASK:** Test the performance of the system using logmel features instead of MFCCs, and AFs, and so on (with current data.)
    * **TASK:** Fix the redundant computation of the pipeline. It currently recalculates all values for both the target and the src for every single test. It's many, many times the amount of computation that needs to be done. Once MFCCs and AFs have been extracted once for a particular utterance, there is no reason to extract them again.
    * **TASK:** Can we make the system more robust? Does it currently break easily? Are we losing information we don't need to lose? How do we handle it when we record a given phrase more than once by the same user? Delete the old file? Move it?
    * **TASK:** Is a CART better at predicting scores than a DNN? Can we use a DNN to learn the relationship between scores and pronunciations?
      * _Do we have enough data to train a DNN?_
      * _Automatic feature extraction?_
      * _What other kinds of machine learning can we try?_
    * **TASK:** Work on #2 to get the data to try new tests and see how it works...

  * **Evaluation of Improved Applause Pipeline:** If we manage to improve the results (after gathering more judging data and retraining / changing our ML), how does the system perform on the same benchmarks we've already done?
    * _Cross Validation_
    * _Sanity Checks: Same Speaker / Empty Audio_
    * _Phrase Matching w/ Same Speaker_
    * _Phrase Matching w/ Different Speaker_
    * _Performance Comparison w/ MCD, logmel model_


---

### 2. Web Interface for Users and Judges to Attempt / Score Pronunciation ###

  * **Web Interface for Users:** We need to build an application that can allow people to upload their pronunciation of a set of phrases
    * **TASK:** Determine how many languages we are going to use...
    * **TASK:** Make a web page that can use the user's microphone to record audio, play it back, trim, delete, and send
      * _Google Voice API?_
      * _Works on Mobile Devices?_
    * **TASK:** The web page must be able to cycle through a set of phrases and iteratively ask the user to record 1 or many of them. The uploaded audio must be incorporated into the existing data organization.
    * **TASK:** The web page must support user logins so that people can come back and continue their work -- people cannot identify themselves as native/non-native speakers of any language. They just login, take a phrase set in a given language, and talk.
    * **NOTE:** _This is not for the dialog app, this is training data for the machine learning..._

  * **Web Interface for Judges:** The complement to the above, we need a web application to allow judges to log in and score the performance of various users who attempt pronunciations of the target phrases.
    * **TASK:** The web page should display:
      1. Transcription
      1. Translation
      1. Play Target Audio
      1. Play Test User 1
      1. Play Test User 2
      1. Select superior ranking: User 1 / User 2
      1. Submit ranking to server
    * **TASK:** If we agree that ranking two at a time works, how to we internally represent the ranking?
      * _Groups of 5? 10?_
      * _Global ranking for all speakers?_
      * _What is the ranking algorithm? Do we randomly combine phrases and let them trickle to the top or do we base the matches on entropy?_
      * _How do we resolve conflicts between different judges?_
    * **TASK:** Promoting the judging site:
      * _What social platforms / sites can we use? (Whatsapp & Facebook are huge in Ghana.)_
      * _Can we make it a game? Can it be fun?_
      * _What are the criteria for making judges?_
      * _Do we pick the judges or allow anyone to register?_
      * _Offer a random audio --> English written translation task for new judges?_
    * **TASK:** Figure out how much data to collect...
      * _Do we continually add new judging data and retrain our model?_
      * _Wait until we have 'enough'?_
    * **TASK:** Allowing judges to make corrections...
      * _Can judges upload their own pronunciations?_

  * **Fixing/Setting Up the VM:** If we want this to be available for people to use as part of Speech Kitchen, we can't have the web-app layer being external to the VM.
    * **TASK:** We need a way (if we keep using a VM on islpc19.is.cs.cmu.edu) to use the application from the web -- Consider HTTP Forwarding from the host machine.
    * **TASK:** Modifying any code that requires the interaction of the web application with the VM over a network -- get rid of that SSH crap.
    * **TASK:** Incorporating the Virtual World into our VM

---

### 3. Interactive Dialog System ###
  * **Creating Dialog Logic:** We have to figure out how we are going to build the dialog system logic...
    * **TASK:** Convert / use the CLAP scripts?
    * **TASK:** Investigate adult language learning research. What is the best way to:
      * _Present the information_
      * _Introduce new topics (e.g. Travel, Lesson 1, Greeting dialogs...)_
      * _Repeat concepts (e.g. phrases they have already heard once)_
      * _Provide the user with feedback (e.g. "good job!" "work on your fricatives!")_
      * _Test the user_
      * _Quantify improvement over time_
      * _Decide when to move on, how much to move on, slower/faster, etc._
      * _Is the dialog system generic? How do we incorporate new lessons and content?_
      * _What is the overall learning algorithm?_

  * **Making the Tutor's Voice:** Whatever "teacher" there is to introduce new concepts needs to have a voice, because this is voice-based... right? Text based?
    * **TASK:** If voice-based, synthesize Nik's voice using the recorded and transcribed narrations from the CLAP audio
    * **TASK:** Evaluation of synthesized voice
    * **TASK:** Mixing canned phrases in with synthesized phrases to allow for less machine-like interactions...

  * **Evaluation of the Dialog System:** Do users actually learn language?
    * **TASK:** Get people to try the system for a period of time and see if they improve:
      * _Do users gain confidence?_
      * _Do users respond faster?_
      * _Do users' pronunciations actually 'improve' if their scores demonstrate improvement?_
      * _How well do users do with the things they learn?_
      * _What are the social impacts of being able to say a few things in a low-resource language?_
      * _Long term goals?_


---

### 4. Web Interface to Accumulate Low-Resource Language Data ###
  * **Create New Language Tool:** An interface to collect phrases / recordings in new languages
    * _Do users write narrations?_
    * _How do we evaluate new additions? On faith? A test?_
    * _Male / Female speakers?_
    * _Multiple Speakers?_
    * _User defined phrases or canned phrases in the system?_
    * _How easy can we make the process?_
    * _Do we need judging data? Particular to the language?_
    * _How much audio is enough?_
    * _Retrain the model?_
    * _Processing and feature extraction of the data_
    * _Do we release the data to the public immediately? Evaluate first?_

  * **Add New Language Tool:** An interface to collect recordings for existing languages
    * _Correct existing phrases?_
    * _Add additional pronunciations?_
    * _Average new pronunciations?_
    * _Make new lessons, annexes, special topics?_
    * _New narrations or existing narrations?_
    * _Incorporate and organize new data into existing system_
    * _Feature extraction / Retraining the model..._

  * **Evaluation:** Who are the target users?
    * _Native speakers?_
    * _Organizational/Government workers?_
    * _The military?_
    * _Peace Corps?_
    * _USAID?_
    * _Others?_


---

### 5. Mobile Applause ###
  * **Android Applause:**
    * _This project was actually started when I was in Ghana..._
    * _Contact [Alex Eveleth](mailto:eveleth.alex@gmail.com)_

  * **iPhone Applause:**
    * _Basically the same thing as the Android app... But for iPhone!_

  * **Webpage for Mobile Interface:**
    * _Using mobile web CSS/HTML5 design_
    * _Optimize for EDGE connections_
    * _Opera Mini_

  * **Old Crappy Nokia Phones:**
    * _What about the billions of phones out there that are not web-enabled?_
    * _Collecting audio?_
    * _Quality control?_

  * **Evaluation:**
    * _How do we test the various systems?_
    * _Do they work well in the field?_
    * _Use cases?_


---

### 6. Virtual World / Open Sim Interface ###

  * **Fixing Kaldi**
    * **TASK:** Switchboard corpus... Yajie says it's here: `/data/ASR4/babel/ymiao/swbd/exp/tri3b/Decode_Setup`

  * **Adding Parser**
    * **TASK:** etc...

  * **Creating Virtual Tutors**
  * **Incorporating Dialog System**
  * **Incorporating Speech Synthesis**
  * **Pronunciation Scorer / Kaldi Working Together**
  * **Building Virtual World**
