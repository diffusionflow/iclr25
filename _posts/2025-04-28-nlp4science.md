---
layout: distill
title: "NLP for Human-Centric Sciences"
description: "Can NLP predict heroin addiction outcomes, uncover suicide risks, or simulate and influence brain activity? Could LLMs one day earn a Nobel Prize for their role in simulating human behavior – and what part do NLP scientists play in crafting this reality? This post explores these questions and more, positioning NLP not just as a technological enabler but as a scientific power-multiplier for advancing human-centric sciences." 
date: 2025-04-28
future: true
htmlwidgets: true
hidden: false


# Anonymize when submitting
authors:
  - name: Anonymous

# must be the exact same name as your blogpost
bibliography: 2025-04-28-nlp4science.bib  

# Add a table of contents to your post.
#   - make sure that TOC names match the actual section names
#     for hyperlinks within the post to work correctly. 
#   - please use this format rather than manually creating a markdown table of contents.
toc:
  - name: Introduction
  - name: Science and NLP
  - name: Language as a Window Into the Mind
    subsections:
    - name: The Individual Level
    - name: The Collective Level
  - name: Applying NLP in Scientific Quests
    subsections:
    - name: Hypothesis Generation (Bottom-Up)
    - name: Theory Validation (Top-Down)
    - name: Simulating Human Behavior
    - name: Simulating the Human Brain
    - name: Extracting Applicable Insights from Corpora
  - name: Responsibility of the NLP Scientist
    subsections:
    - name: Interpretability-Aware Modeling
    - name: Meeting Scientific Standards
    - name: Interdisciplinary Collaboration
  - name: Summary

# Below is an example of injecting additional post-specific styles.
# This is used in the 'Layouts' section of this post.
# If you use this post as a template, delete this _styles block.
#_styles: >
#  .fake-img {
#    background: #bbb;
#    border: 1px solid rgba(0, 0, 0, 0.1);
#    box-shadow: 0 0px 4px rgba(0, 0, 0, 0.1);
#    margin-bottom: 12px;
#  }
#  .fake-img p {
#    font-family: monospace;
#    color: white;
#    text-align: left;
#    margin: 12px 0;
#    text-align: center;
#    font-size: 16px;
#  }
---

In this post, we delve into the evolving relationship between Natural Language Processing (NLP) and the broader realm of behavioral, cognitive, social and brain sciences, presenting NLP not only as a technological tool but as a transformative force multiplier across human-focused sciences. Language, after all, permeates every part of human life, offering insights far beyond data inputs for algorithms. Through examples spanning psychology to medicine, we showcase how NLP can serve as a window into the human mind, facilitating hypothesis generation, validation, human simulation, and more. We highlight its role in predicting rehabilitation outcomes, modeling physiological brain function, and uncovering new risk factors for suicide. Finally, we reflect on the responsibilities of NLP scientists, underlining the challenges of interdisciplinary collaboration and the commitment required to produce meaningful, interpretable scientific insights.

## Introduction

2024 marked a groundbreaking year for the relationship between AI and the natural sciences, with two Nobel Prizes awarded for contributions powered by, or deeply tied to, AI- specifically, deep learning. John J. Hopfield and Geoffrey E. Hinton received the Nobel Prize in Physics for foundational advancements in artificial neural networks, such as the Hopfield network, capable of storing and reconstructing patterns, and the Boltzmann machine, a generative model that classifies images and generates new examples based on training data. In Chemistry, Demis Hassabis, John Jumper, and David Baker were recognized for their work on AlphaFold, a deep learning system that accurately predicts protein structures, a long-standing challenge in molecular biology.
<div class="row mt-3">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/2025-04-28-nlp4science/noble-physics.jpg" class="img-fluid rounded z-depth-1" %}
    </div>
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/2025-04-28-nlp4science/noble-chem.jpg" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    2024 marked a groundbreaking year for deep learning, with two Nobel Prizes awarded. Could NLP be next?
</div>

AI, particularly deep learning, is indisputably transformative, impacting technology, society, and now, as these Nobel Prizes affirm, advancing research on natural sciences.

Yet two questions arise: First, has deep learning achieved similar breakthroughs in the human-centered sciences, such as psychology, psychiatry, sociology, or behavioral economics? Second, have any major scientific achievements- whether in exact or human sciences- stemmed from NLP? Put simply, if deep learning has succeeded in modeling physical phenomena, why does it struggle to capture human-centered scientific phenomena? And why hasn’t NLP, which relies on deep learning, demonstrated similar success?

We believe the reason is twofold: the subjective, hard-to-define nature of human-centric sciences, and the endless nuances inherent in language. Modeling scientific problems that lack clear-cut definitions, using a tool as flexible as language – changing across communities, generations, genders, and cognitive states – is an exceptionally complex endeavor. Additionally, for some human-centric problems, language alone may not suffice as input. Despite these challenges, as we will discuss, modeling science through language remains essential, as it provides a unique window into human cognition and behavior.

NLP is already applied across numerous intersections of language and natural or human-centered sciences, from analyzing clinical records<d-cite key="Dreisbach2019ASR"></d-cite> and suggesting medical diagnoses based on patient texts<d-cite key="Miotto2016DeepPA"></d-cite> to potentially diagnosing mental disorders<d-cite key="Leis2019DetectingSO"></d-cite> or predicting suicidal tendencies<d-cite key="Fernandes2018IdentifyingSI"></d-cite>. Yet, we argue that in order to reach the full potential of NLP as a scientific power-multiplier, it’s time to shift from a focus on application and prediction, to a focus on insight and discovery – to unveil and acquire knowledge. Science, after all, aims to understand the mechanisms governing the world, especially those involving human beings and society. Prediction, however accurate, may not be truly impactful if it fails to answer fundamental questions: What insights does this offer about the world, and how does it deepen our understanding of the reality around us?

## Science and NLP

Merriam-Webster defines [Science](https://www.merriam-webster.com/dictionary/science) as:  
<blockquote>
  A system of knowledge focused on general truths and laws, tested through empirical methods- identifying problems, gathering data through observation and experimentation, and testing hypotheses.
</blockquote>
Scientific disciplines are often divided into several major groups:
<br> **Formal sciences** (logic, mathematics, etc), **Natural sciences** (physics, chemistry, biology, etc), **Social sciences and Humanities** (sociology, psychology, etc), and **Applied sciences** (medicine, computer science, etc).

Where does NLP fit into this classification? The field of NLP emerged from the fusion of two different-yet-similar scientific fields: linguistics (which are a part of Social sciences and Humanities) and computer science, which belongs to applied sciences. Originally, NLP was driven by two key motivations:
<br>(1) **automating language understanding** and (2) **deciphering the structure of language**.
<br> Early efforts centered on parsing language for practical applications, such as translation and question-answering, relying on grammar-based, often rule-driven systems. The introduction of statistical methods, like Hidden Markov Models (HMMs) and probabilistic parsing, marked a shift toward data-driven models capable of learning from vast text corpora and handling larger contexts, enabling advanced tasks like sentiment analysis and text generation. Today, with abundant data and advanced computational resources, NLP is largely dominated by deep learning and large-scale models like Large Language Models (LLM), capable of tackling incredibly complex, context-sensitive tasks.

The remarkable capabilities of LLMs are one of the two main reasons we believe that now is the ideal moment to usher in a new era, in which NLP serves as a power multiplier for human-centric sciences. Although originally developed with the relatively straightforward goal of predicting the next word,  LLMs have, as a byproduct, evolved to present human-like behaviors, simulating interactions to a degree that sometimes even confounds us<d-cite key="Dou2021IsGT"></d-cite>. Their vast accessibility, along with their ability to analyze language-based phenomena across gigantic amounts of data, makes LLMs a super-tool for exploring scientific phenomena. They also open doors to opportunities that were previously unattainable or challenging, such as simulation, synthetic data generation, and annotation, adding invaluable capabilities to research in human-centered fields.

Apart from the rise of LLMs, we believe another factor may encourage researchers to view NLP as a power-multiplier in human-centric sciences: a fresh perspective on language itself. Traditionally, we see language as a sequence of words- a straightforward conduit of information or a simple data source for analysis. In this next section, we propose a different view: language as more than data for algorithms, but rather as a window into the human mind.

## Language as a Window Into the Mind

Language is the natural way in which humans express their complex collection of thoughts, knowledge, emotions, intentions, and experiences – i.e it is how humans process, perceive and interact with the world. The power of language (and NLP as a means of exploring it) for scientific exploration lies in its unique blend of structure (its "mathematical" nature) and depth of human nuances<d-cite key="Nefdt2023-NEFLSA"></d-cite>. Language holds a dual nature, serving as both the voice of the individual, and as the shared reality of larger groups – a bridge between personal expression and collective identity. By redefining language as a gateway to the human mind -on both individual and collective levels- we aim to inspire researchers to view NLP in a new light, driving innovation and impact in human-centered sciences.

### The Individual Level

Through language, we communicate our ideas, reveal beliefs, and express emotions, sharing our subjective reality. Word choice and linguistic nuances provide insights into cognitive and emotional states, making language a powerful tool for understanding human consciousness and behavior. Accordingly, studying language touches the core of what it means to be human, which is why it is central to fields like psychology, cognitive science, and neuroscience – disciplines dedicated to exploring the complexities of the individual’s mind.

In psychology, for example, language mirrors the intricacies of the human psyche, revealing mental and emotional states, and therapeutic conversations rely on verbal expression, where word choices and narrative structures can uncover underlying thoughts and behaviors. Persistent negative language may indicate depression<d-cite key="Eichstaedt2018FacebookLP"></d-cite>, while disorganized speech could signal cognitive disturbances like schizophrenia<d-cite key="Jeong2023ExploringTU"></d-cite>. Language analysis thus becomes invaluable for mental health assessment and intervention, as identifying valid, low-cost biomarkers that predict clinical outcomes is a holy grail in psychology and psychiatry<d-cite key="Corcoran2020LanguageAA"></d-cite>, holding the potential to assess treatment response and optimize interventions among individuals with various psychological issues.

One example of assessing treatment progression is presented in a pioneering study by <d-cite key="Agurto2023SpeakAY"></d-cite>, who applied NLP to predict clinical outcomes for 57 individuals with cocaine use disorder (iCUD) undergoing rehabilitation. Each participant provided five-minute recorded sessions discussing the positive consequences of abstinence and the negative effects of cocaine use. Using RoBERTa, the researchers analyzed these recordings and calculated similarity scores against standardized assessments. These NLP-derived insights were then applied in regression models to forecast long-term outcomes, particularly at 12 months, including withdrawal symptoms, craving levels, abstinence duration, and frequency of cocaine use. This study is just one of many that demonstrate NLP’s power in clinical research, showing how an individual’s language can serve as a gateway into their mind, uncovering patterns that enhance treatment response and deepen our understanding of addiction.
<div class="row mt-3">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/2025-04-28-nlp4science/icud.jpg" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
 Illustration of the approach applied by <d-cite key="Agurto2023SpeakAY"></d-cite> to predict cocaine-related outcomes in 57 individuals with cocaine use disorder, based on similarity scores between embeddings of participants' transcribed speech and assessment questionnaire items, then used these as inputs to a regression model. 
</div>

### The Collective Level

While the first view of language focuses on the individual mind – exploring personal cognition, emotion, and experience – this second perspective shifts to language as a model of communication within groups and societies. This approach allows us to analyze how language shapes and reflects social interactions and cultural norms, providing insights into collective behavior across fields like social science, political science, economics, and the humanities.

In social science, language patterns provide insights into social behaviors, group dynamics, and societal trends<d-cite key="Gonzales2010LanguageSM"></d-cite>. Political science applies language analysis to study rhetoric, persuasion, and public opinion<d-cite key="Wodak1989LanguagePA"></d-cite>. In literary studies, language is examined to interpret human experiences and emotions<d-cite key="Miall2011EmotionsAT"></d-cite>, while in economics, it helps gauge market sentiment and consumer behavior<d-cite key="Fatouros2023TransformingSA"></d-cite>. These analyses often involve vast textual datasets, sometimes spanning millions of documents. NLP is thus an essential tool for uncovering patterns, sentiments, and insights, deepening our understanding of collective human behavior.

Indeed, computational social science has emerged as one of the most established subfields of NLP. For example, in a study published in Nature<d-cite key="Avalle2024PersistentIP"></d-cite> the authors conducted a comprehensive analysis of approximately 500 million online social media comments from eight different platforms (e.g., Facebook, Reddit, Telegram, Twitter, and YouTube) spanning diverse topics, over three decades. Their goal was to understand whether online discussions are inherently toxic, as well as how toxic vs. non-toxic conversations differ. Clarifying these dynamics and how they have evolved over time is crucial for developing effective strategies and policies to mitigate online hostility. To handle this large-scale study, the authors employed NLP models to predict toxicity scores and other explanatory variables such as sentiment, conversation length, and more. NLP was essential in processing and analyzing such a vast amount of unstructured text data, enabling insights that would be unattainable through manual analysis. 

The authors found that, while longer conversations often exhibit higher levels of toxicity, inflammatory language doesn’t always deter participation, nor does hostility necessarily escalate as discussions progress. Their analysis suggests that debates and contrasting viewpoints among users significantly contribute to more intense and contentious interactions. This study exemplifies how analyzing the language of the collective can uncover nuanced dynamics in online interactions, revealing patterns that shape digital discourse.
<div class="row mt-3">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/2025-04-28-nlp4science/toxicity.png" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
  An example of <d-cite key="Avalle2024PersistentIP"></d-cite>’s analysis of 500 million social media comments across eight platforms, using NLP to determine toxicity scores. Findings show toxicity increases with conversation size, regardless of topic or platform.
</div>

## Applying NLP in Scientific Quests

In the previous section, we proposed a new way to frame language – as a window into the human mind, on an individual and collective level – and provided several examples that put this perspective into practice, driving remarkable innovation across various scientific fields. 

In this section, we turn our attention to practicality. For NLP practitioners seeking to utilize NLP as a tool for scientific inquiry, we present several practical approaches- along with examples- that showcase how NLP can creatively help drive scientific discovery and reveal new insights about our world. In particular, we will describe how NLP can:
* Generate scientific hypothesis.
* Validate existing theories.
* Empower simulations of human interaction, behavior, or the brain.
* Extract applicable insights from scientific corpora.

### Hypothesis Generation (Bottom-Up)

As previously mentioned, NLP methods are often applied to large text datasets, where they excel at learning prediction models to forecast specific phenomena. While this capability is undoubtedly impactful, we argue that **predictions alone** – based on patterns found in data – **do not always help us scientifically model and understand the reality around us**. A more effective approach might be to start with a hypothesis, following classic scientific principles. But what if we’re uncertain about where to begin? In this case, we propose **using NLP models to generate novel hypotheses** – a 'proposed explanation for a phenomenon.'

Typically, scientists generate hypotheses through a top-down approach, drawing from established theories or prior knowledge to guide their inquiries. While this approach leverages existing understanding, it may sometimes miss unexpected patterns within the data. By contrast, NLP models, especially those based on deep learning, function as powerful bottom-up tools – a strong predictive model can serve as a generator of insights. Through interpretable methods that clarify the basis of model predictions or reveal what the model encodes in its representations, we can transform predictive power into scientific discovery.

One example of this approach is presented in <d-cite key="Lissak2024BoredTD"></d-cite>, where researchers established a new risk factor for suicidal tendencies using NLP. The authors applied BERTopic<d-cite key="Grootendorst2022BERTopicNT"></d-cite> to cluster Facebook posts from individuals diagnosed with suicidal tendencies. Upon analyzing the clusters, they observed that boredom – an unrecognized and understated risk factor – emerged as one of the leading topics. To rigorously test this observation, they conducted a controlled experiment involving human participants who completed psychological assessments for suicide risk and boredom. Through statistical and causal analysis, the new hypothesis suggested by the NLP model – that boredom is indeed a significant risk factor for suicidal tendencies – was validated, providing researchers in psychology, for example, with new avenues for exploration.
<div class="row mt-3">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/2025-04-28-nlp4science/boredom.png" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
  Top: Four word clouds representing clusters of Facebook posts written by individuals diagnosed with suicidal ideation. The word clouds are arranged from left to right according to their predictive strength for suicide risk. This bottom-up NLP analysis highlights a potentially overlooked suicide risk factor: boredom.
  Bottom: The statistical analyses conducted in order to validate the new risk factor. Figures  sourced from <d-cite key="Lissak2024BoredTD"></d-cite>. 
</div>

### Theory Validation (Top-Down)

In cases where a scientific hypothesis already exists, NLP models can be leveraged to validate and strengthen it. In a separate study on suicide <d-cite key="Badian2023SocialMI"></d-cite>, researchers developed a multimodal model (incorporating both text and images) to predict suicidal tendencies based on pictures posted in users' Facebook profiles. Unlike the previous study’s bottom-up approach, this one followed a top-down strategy, aiming to validate and reinforce the psychological theory that loneliness is a risk factor of suicide.

Guided by domain experts, the researchers aimed to translate two psychiatric theories – the Interpersonal Theory <d-cite key="ribeiro2009interpersonal"></d-cite> and the Attachment Theory <d-cite key="Bowlby2012THEOO"></d-cite>) – into a set of language-vision features (e.g., "the photo is a selfie," "a photo of a family,"... see the examples in the Table below). Using the vision-language model CLIP <d-cite key="Radford2021LearningTV"></d-cite>, they queried images for the features derived from these theories, extracting predictors that could inform suicide risk. The extracted features are used to train a logistic regression model that predicts suicidal tendencies. By analyzing the coefficients of the model, the authors revealed, for example, that an increased frequency of selfies compared to group photos was a key predictive factor for suicide risk, likely reflecting heightened loneliness or a reduced social circle. This AI-driven insight computationally validates aspects of psychological theories, supporting the hypothesis that loneliness is a significant risk factor for suicide. Importantly, it demonstrates that multi-modality (i.e. the fact that features were derived based on both image and query) can help predict suicide risk more effectively than if one were to only use standard representations from state-of-the-art vision encoding models.
<div class="row mt-3">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/2025-04-28-nlp4science/suicide-clip.png" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
  The table, sourced from <d-cite key="Badian2023SocialMI"></d-cite>, presents three examples of CLIP scores between researcher-crafted queries and images. These scores were then used as inputs for a regression model to predict the suicide ideation of Facebook users. Remarkably, the resulting model could predict suicide risk based solely on images uploaded to social media. Moreover, by analyzing the importance of features, researchers could explain the findings in the context of established psychological theories. 
</div>

As this work demonstrates, incorporating NLP with other modalities - such as images - can significantly enhance the scientific insights "NLP for science" offers. But what if we took this potential further by embracing 'extreme multi-modality'? It’s entirely possible to envision models that incorporate not only text, images, and videos, but also brain scans, psychological biomarkers like blood tests, data from smartwatches, and more. Such a cohesive, NLP-centered multi-modal approach could truly transform scientific research. However, achieving this potential requires the NLP community to actively develop suitable architectures and models. "NLP for science" entails more than merely applying NLP to scientific problems; it calls for foundational models designed with a multi-modal, text-centric focus – a gap yet to be addressed.

### Simulating Human Behavior

Simulating and replicating human behavior with LLMs offers scientists a fast and affordable way to gain insights into social and economic scenarios. By generating human-like responses, LLMs can enable researchers to pilot studies, test experimental variations, examine different stimuli, and simulate demographics that are difficult to reach, thereby uncovering potential biases or clarity issues in study design. These models streamline the experimental process, allowing for the rapid testing of multiple approaches and helping identify the most effective methods, thus reducing the need for resource-intensive trials with human participants. 

NLP models, particularly LLMs, have recently shown potential as tools to track and emulate human behavior. This has been validated by multiple studies, including <d-cite key="Aher2022UsingLL"></d-cite> which introduced a series of behavioral tests they dubbed "Turing Experiment" (not to be confused with the Turing Test). These tests, drawn from psycholinguistics, behavioral economics, and social psychology, were crafted to examine whether language models could replicate human responses in various behavioral experiments. Another study by <d-cite key="Xie2024CanLL"></d-cite> explored whether language models could mirror human trust behaviors by using games from behavioral economics to observe interactions with other language models and, subsequently, with human participants. Their findings generally showed that language models exhibited trust behaviors highly aligned with human patterns, though some biases related to participant demographics were noted.

In another example focused on game theory, <d-cite key="Shapira2024GLEEAU"></d-cite> use LLM-based setups to simulate a two-player, sequential, language-based Persuasion Game<d-cite key="Kamenica2009BayesianP"></d-cite>. This game involves two roles: a message sender and receiver, or in their example, a travel agent and a traveller. The sender (e.g, travel agent), holding private knowledge about the hotel’s quality, communicates simplified text messages in each round. The receiver then decides whether to go to the hotel or stay at home, based on both the sender’s message and their own prior knowledge of hotel quality probabilities. The authors collected data from LLM vs. LLM as well as human vs. LLM games, using the results to draw comparisons and evaluate insights from their simulations. 

[//]: # (They also published this curated dataset as a benchmark, supporting further research into LLM-based simulations in economic game contexts. This benchmark aims to foster broader exploration of NLP’s role in understanding human, as well as agentic, decision-making processes.)

### Simulating the Human Brain

With language serving as a direct conduit into the biological mechanisms of the brain, NLP possesses the remarkable capability to model aspects of the human brain itself. Researchers approach this by measuring brain activity using techniques like functional Magnetic Resonance Imaging (fMRI) and Electroencephalography (EEG), then aligning the internal representations of NLP models, such as GPT-2 or large LLMs like GPT-4<d-cite key="Hasson2019DirectFT"></d-cite><d-cite key="Goldstein2022SharedCP"></d-cite>, with these measured brain signals. By correlating neural data with the computational processes of NLP models, they can uncover how language is encoded and processed in the brain, identifying shared principles and divergences that enrich our understanding of both artificial and natural intelligence.

This research holds promise for the future, enabling simulations with NLP models instead of humans and overcoming traditional neuroscience limitations, such as invasive procedures, high costs, and limited access to specialized equipment. Additionally, this line of research could lead to developing methods of decoding neural signals into speech<d-cite key="Chen2023ANS"></d-cite>, potentially giving a voice to individuals who are mute or in a vegetative state. By bridging the gap between NLP and neuroscience, we can pave the way for innovative therapies and technologies that enhance human communication and cognitive function.

One example for applying NLP for brain simulation is presented in <d-cite key="Tuckute2024DrivingAS"></d-cite>. The researchers focus on regions of the brain known as "the human language network" (a network of interconnected brain regions that collaborate to support all aspects of language, including speaking, listening, reading, and understanding language). They aim to test whether language models such as GPT2-XL can not only predict but also control neural activity in the human language network. 

The researchers recruited five participants who underwent functional MRI scans while reading 1,000 diverse sentences, measuring brain activity in their language network. In the first stage, they aligned and trained an encoding model using GPT2-XL, by extracting sentence embeddings. These embeddings were used in a ridge regression model to predict the average blood-oxygen-level-dependent (BOLD) response in the brain language network. The model demonstrated a prediction performance of r=0.38, indicating an undisputed correlation between the model's predictions and actual brain responses.

In the second stage, the researchers sought to determine if the model could identify whether new sentences would drive or suppress activity in the listener’s language network (i.e, would the new sentence make their brain activity increase or decrease). They approached this by searching through approximately 1.8 million sentences from large text corpora, using their model (GPT-XL + regression) to predict which sentences would elicit maximal or minimal brain responses. These model-selected sentences were then presented to new human participants in a held-out test, where brain responses were again measured using fMRI. The findings revealed that the sentences they predicted to drive neural activity- indeed elicited significantly higher responses, while those predicted to suppress activity led to lower responses in the language network. In other words, they could predict brain activity using NLP.
<div class="row mt-3">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/2025-04-28-nlp4science/brain1.png" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="row mt-3">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/2025-04-28-nlp4science/brain2.png" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
  Top: The two stages of the <d-cite key="Tuckute2024DrivingAS"></d-cite> study. First stage: measuring the activity of participants' brain language networks while they read sentences, then fitting a model that predicts these brain signals from the internal representations of the sentences in GPT2-XL. Second stage: the model estimated brain activity for 1.8 million sentences, identifying those predicted to maximize or minimize responses, which were then tested on new participants to measure actual brain activity.
  Bottom: Sentences identified by the NLP model as driving or suppressing brain activity indeed produced these effects in new human participants. At the bottom, examples of such sentences are provided.
</div>

The researchers found that sentences driving neural activity were often surprising, with moderate levels of grammaticality and plausibility, while activity-suppressing sentences were more predictable and easier to visualize. This indicates that less predictable sentences generally elicited stronger responses in the language network – a phenomenon interestingly captured by the language modeling task. Such findings have implications not only for understanding language processing in the brain but also for showcasing the potential of LLMs to non-invasively influence neural activity in higher-level cortical areas.

### Extracting Applicable Insights from Corpora

Finally, NLP can fulfill one of its original purposes – extracting insights from large corpora, in this case, scientific texts. While this strength of NLP can be applied across various scientific domains, here we focus on its extraction capabilities within human-centric sciences. For example, <d-cite key="Zhou2019AutomaticEA"></d-cite> used NLP to analyze hundreds of clinical notes to identify lifestyle factors influencing Alzheimer’s disease. By comparing notes from healthy individuals and Alzheimer’s patients, they extracted risk factors from a pre-defined, expert-curated list and examined their correlations with patients' diagnoses.

Their analysis confirmed the prevalence of well-known risk factors, such as tobacco use and malnutrition, in over 50% of Alzheimer’s cases. However, it also called certain popular medical hypotheses into question. Despite extensive research linking cardiovascular risk factors – such as high-fat and high-calorie diets – to Alzheimer’s disease (1), <d-cite key="Zhou2019AutomaticEA"></d-cite> found these factors mentioned in only about 1% of the clinical records analyzed. Instead, they observed significant associations with nutrient deficiencies, like potassium and calcium, documented in over 25% of cases. Curiously, despite these high correlations, actual laboratory results for these nutrient levels were rarely included. This observation raises an important question: if NLP tools like these were integrated into clinical practice, could they help enhance both medical research and patient care? 
<div class="row mt-3">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/2025-04-28-nlp4science/knowledge-extraction.png" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
  Ratios of top 10 lifestyle exposures identified in clinical notes, adjusted for age and other exposures. Figure sourced from <d-cite key="Zhou2019AutomaticEA"></d-cite>.
</div>

The work of <d-cite key="Zhou2019AutomaticEA"></d-cite> highlights NLP’s potential as a powerful tool in medicine for several reasons: (1) it enables large-scale analysis of expert-curated textual knowledge, (2) it both validates and challenges established medical hypotheses, and (3) it yields insights that can directly impact clinical decisions, such as blood work and patient care protocols.

Importantly, to ensure the robustness of their findings, <d-cite key="Zhou2019AutomaticEA"></d-cite> conducted comprehensive statistical analyses and drew conclusions only from risk factors that showed significant associations in the Alzheimer’s group. This brings us to our last topic: the requirements from the NLP scientist who applies these tools as a force multiplier across diverse scientific fields.

In the next section, we define the unique aspects of this role and examine the responsibilities and challenges it entails.

## Responsibility of the NLP Scientist

The role of NLP scientists goes far beyond choosing the most powerful model, writing code, and reporting results. To make a genuine contribution to scientific inquiry, they must thoroughly understand the problem, its objectives, and the limitations of the data- grasping the entire scope in order to make informed modeling choices. This may even require developing novel NLP methods tailored to the specific task or its evaluation. In short, an NLP scientist must keep three essential elements in mind: **how they model the problem** (especially with an emphasis on interpretability); **how to evaluate their results in a rigorous manner**; and **who they collaborate with** in order to strengthen and validate their research.

### Interpretability-Aware Modeling

The NLP scientist must understand that their primary goal is often – perhaps counterintuitively – not to achieve the highest model performance, but to gain interpretable scientific insights, even if this means sacrificing a few points in performance scores. They should critically examine the model's parameters and behaviors to understand why it predicts as it does, what patterns it captures from the data, and how these insights relate to the phenomena under study..

In this context, NLP interpretability serves a dual purpose. The first is common in NLP research: **improving model performance through interpretability** – debugging, identifying failure points, and refining the model. The second purpose, unique to "NLP for science", aims **to extract scientific insights**. By using interpretable methods to clarify model predictions and uncover what the model encodes, we can transform predictive power into meaningful scientific knowledge.
<div class="row mt-3">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/2025-04-28-nlp4science/papers-count.png" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
  Illustration of the surge in papers that employ interpretability methods, published within and outside of NLP literature. As we emphasize later, interpretability can be used to extract scientific insights from NLP models that have captured patterns in the data. Figure sourced from <d-cite key="Calderon2024OnBO"></d-cite>.
</div>

According to <d-cite key="Calderon2024OnBO"></d-cite>, an interpretability method is: "any approach that extracts insights into a mechanism of the NLP system," where "mechanism" can refer to the entire model or specific components. When the mechanism encompasses the full model (i.e., input-output mechanism), interpretability methods focus on explaining how input variations affect predictions. Alternatively, the method might target a specific part of the model, such as the first 22 layers of GPT-2 XL, to reveal what information these specific layers encode. In their work, <d-cite key="Calderon2024OnBO"></d-cite> define various interpretability paradigms designed to extract distinct insights; examples include "clustering" (e.g., predicting suicidal tendencies from Facebook posts) and "probing," which aligns with neuroscience studies that analyze internal model representations alongside brain signals to explore cognitive processing. The table below lists these paradigms, and the figure following it illustrates the distribution of NLP interpretability paradigms across research fields. A skilled NLP scientist should be well-versed in these paradigms, recognizing their strengths, limitations, and goals to select the most appropriate method for their research.
<div class="row mt-3">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/2025-04-28-nlp4science/paradigms.png" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
  Table: Interpretability paradigms in NLP, as introduced by <d-cite key="Calderon2024OnBO"></d-cite>, are based on key properties: 'Mechanism' – which part of the NLP system is being explained; 'Scope' – whether explanations are local (focused on a single instance) or global (spanning the entire data distribution); 'Time' – whether the interpretability method is embedded within the model itself; 'Access' – whether the method requires a specific model or can be applied broadly; and 'Presentation' – how insights are typically conveyed by the method.
  Figure: Distribution of NLP interpretability paradigms across various research fields, illustrating how NLP research is applied in practice across multiple disciplines. 
</div>

In addition to designing models with interpretability in mind, NLP scientists must focus on understanding the underlying reasons for specific predictions rather than merely identifying correlations. Prioritizing techniques that distinguish between correlation and causation is essential for reporting **sound conclusions**, i.e., ones that accurately reflect a model’s decision-making process, also known as “faithful explanations" <d-cite key="Jacovi2020TowardsFI"></d-cite>. In the context of "NLP for science" – where NLP is applied to model cognition, disease progression, decision-making, and more – unfaithful explanations, particularly those that appear plausible, can pose serious risks to human safety. Ensuring faithful explanations requires establishing causality in results <d-cite key="Gat2023FaithfulEO"></d-cite>, by incorporating techniques such as counterfactuals <d-cite key="Feder2020CausaLMCM"></d-cite>, interventions <d-cite key="Wu2023InterpretabilityAS"></d-cite>, adjustment <d-cite key="WoodDoughty2018ChallengesOU"></d-cite>, and matching <d-cite key="Zhang2023CausalMW"></d-cite>. We strongly encourage NLP scientists to integrate causality and interpretability mechanisms into their models to ensure their results are reliable, sound, and truly faithful.

### Meeting Scientific Standards

NLP scientists must recognize that they are in fact, conducting scientific research. Still, certain standards are often overlooked in AI literature. For instance, <d-cite key="PeledCohen2024ASR"></d-cite> found that among hundreds of studies on NLP for dementia, fewer than 35% report statistical significance or perform robustness tests, revealing a gap that can undermine the reliability of findings. In addition, <d-cite key="Calderon2024OnBO"></d-cite> found that less than 5% among thoudants of NLP interpretability papers employ causal-based methods. To elevate NLP as a credible scientific tool – particularly when aiming for publication beyond NLP-focused venues – scientists should prioritize rigorous methodology. This entails a structured approach to understanding phenomena: developing hypotheses, testing them through experiments and statistical analysis, and refining them based on the results. Statistical tests, whether general or tailored to NLP<d-cite key="Dror2018TheHG"></d-cite>, are essential to verify the significance of findings, lending credibility and supporting further exploration or application. Moreover, **validating results through controlled human experiments** is crucial to achieving impact and fostering adoption beyond the NLP community. 

Currently, in the NLP literature, if a model's reported performance cannot be replicated or lacks robustness in different domains, the repercussions are minimal – practitioners and researchers may simply choose not to use it. However, in scientific fields, unsound conclusions can have harsh consequences. Therefore, one of the crucial roles of NLP scientists is to develop methods that ensure the soundness of their findings. Indeed, there is an established line of work in NLP that focuses on developing causal methods <d-cite key="Feder2021CausalII"></d-cite> and robust statistical techniques for comparing models.<d-cite key="Dror2019DeepD"></d-cite>

The data used for NLP algorithms should also comply with scientific standards. In NLP research on linguistic risk factors for suicidal tendencies, for instance, data sources and annotation methods can vary significantly. Many NLP researchers might use Reddit posts labeled by the subreddit (e.g., posts from r/SuicideWatch vs posts from r/general) or crowd-sourced annotations (e.g., taking posts from those subreddits and manually annotating them as positive if the post indicates its author is in suicide risk). 
However, data with stronger scientific credibility might include posts from individuals who completed a standardized suicidal ideation questionnaire or, ideally, from those who have actually attempted suicide. Such choices profoundly impact the validity and applicability of the findings, particularly when trying to publish in non-CS journals.

Then, there’s the widely adopted approach of LLMs-based annotations. NLP scientists should remember that even the strongest of LLMs could introduce measurement errors – a mismatch between the true gold label and the LLM annotation – which can bias estimators and invalidate confidence intervals in downstream analyses. This can originate, for example, from inherent biases within the LLM (such as gender, racial, or social biases) and sensitivity to variations in prompts or setups. Accordingly, the role of NLP scientists is to propose robust statistical estimators for parameters of interest (such as political bias) using LLMs. 

For example, <d-cite key="Egami2023UsingIS"></d-cite> proposed a method called Design-based Supervised Learning (DSL), which combines synthetic and gold-standard labels to correct for measurement errors in statistical analyses. By selecting a small, randomly sampled subset of documents for expert annotation, the DSL estimator creates a bias-corrected pseudo-outcome that adjusts for the measurement error inherent in synthetic labels (i.e., the LLM predictions). 
<div class="row mt-3">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/2025-04-28-nlp4science/llm-annotations.png" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
  Computational social scientists may use LLMs to annotate documents, reducing the need for manual annotation across an entire corpus. However, LLMs can introduce biases. This figure illustrates a three-step approach to constructing unbiased estimators. Figure sourced from <d-cite key="Egami2023UsingIS"></d-cite>.
</div>

The core idea is as follows: Human annotators provide gold-standard labels ($$Y$$) to a small subset of documents. Then, LLMs are used to predict synthetic (surrogate) labels $$Q$$ for the entire dataset. The researchers assume that some explanatory variables ($$X$$) can be used to predict $$Y$$, for example when examining whether social media posts are annotated as containing hate speech,explanatory variables might include the poster's gender, education level, political affiliation etc. To construct an unbiased estimator, a machine learning model $$\hat{g}(Q,X)$$ is fitted to predict $$Y$$. In the second step, pseudo-labels are computed using a specific equation:

$$\tilde{Y} = \hat{g}(Q, X)+\frac{R}{\pi(Q, X)}(Y-\hat{g}(Q,X))$$

where $$R$$ is an indicator variable denoting whether an example has a gold-standard label ($$R=1$$) or not ($$R=0$$), and $$\pi(Q, X)$$ is the probability of an example having a gold-standard label (e.g, if the experts annotated the documents i.i.d., $$\pi$$ would be one divided by the total number of documents). The term on the right side of the equation, $$\frac{R}{\pi(Q, X)}(Y-\hat{g}(Q,X))$$, can be seen as a bias-correction term. By the end of this step, we have large-scale corrected labels ($$\tilde{Y}$$), automatically generated and free from the biases of the original LLMs. With this unbiased dataset, the NLP scientist can proceed to the third step: their intended downstream analysis, in a scientifically sound manner.

### Interdisciplinary Collaboration

Finally, for NLP to empower research, at least two experts are always required – one on the NLP side, and one on the scientific front. Without consulting with domain experts, the NLP Scientist can find themselves investing in efforts that – despite interesting – may not drive true impact. To portray this, let’s consider the task of NLP Dementia Detection (approached by dozens of researchers<d-cite key="Jarrold2014AidedDO,Edwards2020MultiscaleSF,BT2024PerformanceAO"></d-cite>, as an example) analyzing texts to differentiate between healthy individuals and ones with dementia. 

In consultation with a domain expert – namely, a highly respected professor who leads a research center on Alzheimer’s – we asked "how NLP might help advance research on dementia detection". Their response was straightforward:
<blockquote>
  "If the data used for training is collected from individuals already diagnosed with noticeable dementia, it wouldn’t be particularly helpful or impactful. When someone has already been diagnosed, the signs are usually quite detectable, so a predictive model wouldn’t add much value. The real challenge lies in identifying subtle, early signals that go unnoticed – in other words, detecting the onset of cognitive decline during the Mild Cognitive Impairment (MCI) phase. That’s where you should focus."
</blockquote>

No one could have provided this invaluable advice apart from a domain expert. This insight prompts reflection on the hundreds of existing studies on dementia detection<d-cite key="PeledCohen2024ASR"></d-cite>, who primarily rely on clinical datasets where the vast majority of participants are labeled as "Healthy" or "Dementia", with very few "MCI" individuals<d-cite key="Becker1994TheNH"></d-cite>. While these works demonstrate impressive detection accuracy of up to 90%, achieved through a range of algorithmic approaches, preprocessing techniques, and feature engineering, are these studies truly advancing scientific research on dementia? 

On the other side of the equation, we should consider what scientific domain experts can gain from collaborating closely with NLP scientists. As NLP (and LLMs in particular) become increasingly prevalent as research tools, NLP scientists have a vital responsibility to guide their counterparts on the strengths–and limitations–of their methods. An interesting example is provided by <d-cite key="Ophir2021TheHG"></d-cite>, who developed a guide for doctors on applying NLP in suicide risk treatment.

NLP scientists should always remember the unique expertise they bring to the table- they’re the specialists who understand the strengths of NLP, designing technical solutions, running experiments, and interpreting results. However, in "NLP for science", close collaboration with domain experts is essential for success. These scientific counterparts contribute invaluable insights – whether in shaping the initial problem definition, guiding data collection and annotation, or gauging the broader impact of results. By working together from the outset, NLP scientists and domain experts can ensure that the research is not only technically robust but also genuinely meaningful and impactful.

## Summary

With this blog post, we aim to inspire NLP experts to leverage their expertise and push the boundaries of human-centered sciences. We highlighted NLP’s unique capabilities across fields like neuroscience, psychology, behavioral economics, and beyond, illustrating how it can generate hypotheses, validate theories, perform simulations, and more. The time is ripe for NLP to drive scientific insights and transcend predictions alone, positioning language as a lens into human cognition and collective behavior. Moving forward, interdisciplinary collaboration, scientific rigor, and a commitment to meaningful research will be essential to make NLP a cornerstone of human-centered scientific discovery.
