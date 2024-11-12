---
layout: distill
title: Are LLMs 'just' next-token predictors?
description: LLMs are often labeled as 'just next-token predictors' devoid of cognitive capacities such as 'thought' or 'understanding'. We argue that these deflationary claims need further justification. Drawing on prominent theoretical and philosophical frameworks in cognitive science, we critically evaluate different forms of 'Justaism' that dismiss LLM cognition by labeling LLMs as 'just' simplistic entities without specifying or substantiating the critical capacities they supposedly lack.
date: 2025-04-28
future: true
htmlwidgets: true

# Anonymize when submitting
authors:
    - name: Anonymous

#authors:
#  - name: Albert Einstein
#    url: "https://en.wikipedia.org/wiki/Albert_Einstein"
#    affiliations:
#      name: IAS, Princeton
#  - name: Boris Podolsky
#    url: "https://en.wikipedia.org/wiki/Boris_Podolsky"
#    affiliations:
#      name: IAS, Princeton
#  - name: Nathan Rosen
#    url: "https://en.wikipedia.org/wiki/Nathan_Rosen"
#    affiliations:
#      name: IAS, Princeton

# must be the exact same name as your blogpost
bibliography: 2025-04-28-against-justaism.bib  

# Add a table of contents to your post.
#   - make sure that TOC names match the actual section names
#     for hyperlinks within the post to work correctly. 
#   - please use this format rather than manually creating a markdown table of contents.
toc:
  - name: Flavors of Justaism
    subsections:
    - name: Anti-simple-objectives
    - name: Anti-Anthropomorphism
    - name: Other criticisms of LLM cognition
  - name: Toward a more measured discussion

---

Over 70 years ago, Alan Turing posed a question that has since captivated computer scientists, cognitive scientists, and philosophers alike: "Can machines think?" <d-cite key="turing_icomputing_1950"></d-cite>. With the recent proliferation of impressively human-like artificial intelligence systems---namely, large language models (LLMs)---variants of this question have made their way far beyond the confines of academic departments. 

Some have asserted that LLMs cannot be said to "think" because they are "just...": "next-token predictors," "function approximators," or "stochastic parrots," and thus lack some essential capacity necessary for cognition. Unfortunately, in their most facile form, such deflationary claims fail to state what exactly this capacity is. These more facile claims have consequently been given the pejorative label "Justaism" (pronounced "just-a-ism") due to the confident self-evidence with which they are wielded <d-cite key="Aaronson2023ProblemHumanSpecialness"></d-cite>. To clarify, Justaism refers not to deflationary positions against LLM cognition *per se*, but specifically to *unsubstantiated* deflationary positions. 

In light of the high degree of representational and behavioral alignment observed between LLMs and humans (who ostensibly do "think"), we believe there is an onus on the objector to substantiate these deflationary claims. 
After all, opinions on the reality of LLM "thought," "reasoning," or "understanding" (henceforth, "cognition") have implications both for people's willingness to trust such systems <d-cite key="mitchell2023debate"></d-cite>, to use them as scientific tools, and, ultimately, for their socio-economic impact.  

In what follows, we present two flavors of Justaism, and provide a critical analysis of these positions based on prominent views in cognitive science. We refer to the flavors' prototypical forms but also provide specific examples found in the literature and public discussion on LLM cognition in a companion webpage ([anonymous](anonymous)).

## Flavors of Justaism

### Anti-simple-objectives

> *"It's just a next-token predictor."*

Perhaps the most common form of Justaism, which we dub *anti-simple-objectives Justaism*, takes issue with how LLMs are pre-trained. The assertion is that because the LLM pre-training objective is simply to predict the masked or next token, LLMs cannot be doing something as complex as cognition. 

Assuming proponents of this view believe that humans possess cognition, anti-simple-objectives Justaism can be refuted by making the following facetious analogy to humans and other creatures shaped by evolution: We humans are *just* "next-child producers," stumbling forward in pursuit of the all-encompassing base objective of inclusive fitness maximization---such a simple objective cannot possibly lead to cognition. To most, this analogy's conclusion is absurd, thus questioning the same reasoning when applied to LLM cognition. 

Of course, there are important differences between next-token prediction and next-child production. For instance, the ancestral environment from which we evolved was potentially richer than the online text corpora used to train LLMs. Combined with a sufficiently complex nervous system and other distinguishing factors (e.g., resource competition), biological evolution may lead to the development of *instrumental objectives* that are more conducive to cognition than next-token prediction. 

However, even if it were the case that these distinguishing factors are pivotal in the development of instrumental objectives *in humans*, it is nevertheless plausible that cognition-enabling representations and even instrumental objectives could be acquired via simple LLM pre-training objectives. Indeed, research suggests that LLMs are already employing such instrumental strategies in order to achieve high performance on the base objective <d-cite key="von2023uncovering"></d-cite>. Furthermore, these instrumental objectives may not need to be especially complex so as to be on par with those of human beings. After all, many foundational theories in cognitive science posit relatively simple (instrumental) objectives as fundamental components, with prominent examples including predictive brain theories <d-cite key="clark2013whatever"></d-cite>. If simple objectives are overall thought insufficient for the development of cognition, researchers need to clarify why humans are not in a similar position to LLMs in this regard. 

Ultimately, we would argue that it is by no means self-evident that an LLM seeking to predict the next token could not acquire representations and even instrumental objectives akin to humans. In light of the impressive behavioral and representational alignment between humans and LLMs, the onus is on the objector to substantiate why this is (likely) untrue.  

### Anti-Anthropomorphism

> *"It's just a machine."*

A second prominent form of Justaism, which we dub *Anti-anthropomorphic Justaism*, claims that attributing cognition to machines constitutes a fundamental error. In its strongest form, it argues that such thinking commits a category error because cognition is *by definition* a human capacity. On this view, the essential capacity that LLMs lack and humans possess is just that: humanness. 

Although logically valid, we would argue that this view is unproductively restrictive. Advances in scientific theory are often based on the realization that a concept is more general than previously believed. One instructive example comes from animal cognition research, where, in response to a growing body of empirical evidence, researchers began to see great utility in ascribing capacities previously thought to be uniquely human, including emotion, self-awareness, or consciousness, to non-human animals <d-cite key="de2016we"></d-cite>. We believe it should be *in principle* acceptable to consider such conceptual generalizations for information processing systems more broadly.  

There are, of course, more moderate forms of anti-anthropomorphic Justaism. For instance, one might take the view that although it is not a problem *in principle* to talk about LLM cognition, the burden of evidence for doing so should be set very high. One reason for this would be to guard against the Eliza effect <d-cite key="mitchell2023debate"></d-cite>, which refers to the human propensity to all-too-liberally ascribe "thought" to even the simplest of machines. 

Although we agree that it is important to reject naive anthropomorphism, we note that running counter to anthropomorphism is another, perhaps more infamous, human tendency: anthropocentrism. Regarding cognition, anthropocentrism is the tendency to view capacities such as "thought" as so unique that it would not make sense to ascribe them to "lesser" systems, such as non-human animals <d-cite key="de2016we"></d-cite>. In the context of artificial intelligence, it can be observed in the well-documented phenomenon of algorithmic aversion---the human tendency to rely more on human advisors over equally good or better-performing algorithms <d-cite key="jussupow2020we"></d-cite>. Anthropocentrism may ultimately have implications for the adoption of novel technologies that have the potential to contribute to human wealth and well-being.

In light of humans' countervailing tendency to view their own cognition as exceptional, we would advocate for specifying more precisely the forms of cognition in question and the evaluative criteria to be employed. We believe this will enable more substantive discussions of and comparisons between the capabilities of humans and other information-processing systems.

### Other criticisms of LLM cognition

Beyond *anti-simple-objectives* and *anti-anthropomorphic* forms of Justaism are more moderate forms of LLM deflationism. Perhaps most prominent in the literature are arguments that emphasize the importance of the distinction between *meaning* (semantics) and *form* (syntax) <d-cite key="bender2020climbing"></d-cite>, <d-cite key="searle1980minds"></d-cite>. One argument is that LLMs do not have access to *meaning* because of their lack of real-world grounding and, consequently, human-like understanding. These positions are considerably more substantial than their Justaic cousins mentioned above and thus do not deserve to be labeled as "Justaic." We are also more sympathetic to these views and believe that LLMs that are more physically and socially grounded are also likely to be cognitively more advanced. 

Nevertheless, we would caution against confidently concluding that LLMs lack cognition on these bases. Not only do the arguments draw on notoriously hard-to-define concepts (e.g., *meaning* or *grounding*), but they also rely heavily on thought experiments of a specific nature. These thought experiments make an appeal to our intuitions by showing that another system in an analogous but more intuitively transparent position to an LLM---such as the human in <d-cite key="searle1980minds"></d-cite>'s famous "Chinese Room"---appears cognitively lacking <d-cite key="bender2020climbing"></d-cite>, <d-cite key="searle1980minds"></d-cite>. However, the intuitions evoked by such thought experiments can be misleading, especially when applied to complex systems that have been trained on more data than a human could process in a lifetime. As a testament to the limits of intuition in this context, consider the to-many-astonishing effectiveness of "simply" scaling-up model and training set sizes for improving LLM performance <d-cite key="kaplan2020scaling"></d-cite>. Although we share the intuitions evoked by such thought experiments, we thus resist putting too much weight on them. 

## Toward a more measured discussion

In support of a more measured discussion of LLM cognition, we would like to advance three guiding principles: (i) modesty regarding human cognition (and our understanding of it), (ii) consistency for future work comparing humans and LLMs, and (iii) a focus on empirical benchmarks. 

Regarding modesty, we would reiterate that human history is littered with delusions of human exceptionalism <d-cite key="de2016we"></d-cite>. This is despite our limited understanding of the mechanisms underlying cognition. Thus, although we fully support cautioning against the dangers of (naive) anthropomorphism, we see the need for a backstop against the opposite tendency: viewing human cognition as too special to also be ascribed to LLMs.  

Regarding consistency, we would reiterate the need for consistent goalposts: Are we applying the same standards to LLMs as we would to humans? For instance, if we wish to reduce LLM cognition to its pre-training objective (i.e., next-token prediction), we must show why the same reductionism should not apply to humans as well. Similarly, when LLMs commit errors that appear so elementary to us as to discredit LLM cognition, it is important to recall the host of fallacies and illusions that humans are susceptible to and consequently may not so easily identify or view as significant. These considerations not only help guard against certain biases (e.g., algorithmic aversion), but they can also provide a new perspective on human cognition by helping identify aspects of cognition that are, in fact, uniquely human. 

Finally, we are sympathetic to <d-cite key="turing_icomputing_1950"></d-cite> and <d-cite key="niv2021primacy"></d-cite>'s view that discussions of cognition should focus on observables. As <d-cite key="trott2023large"></d-cite> note, axiomatic rejections of LLM cognition can lead to positions that have no empirically testable implications. Not only does this run contrary to good scientific practice, but it can also lead to investigations of LLM cognition that lack practical relevance. After all, it is predominantly the behavior of a system that impacts the world. Consequently, we believe in the need for clear and consistent empirical benchmarks that allow for direct evaluations of the cognitive capacities of humans and LLMs. 

Ultimately, the jury is still out on the existence and extent of LLM cognition. Empirical research has demonstrated interesting cognitive deficits in LLMs <d-cite key="berglund2023reversal"></d-cite>, but also impressive feats <d-cite key="bubeck2023sparks"></d-cite>. Given the limitations of Justaic reasoning, we believe the ball is in the skeptic's court to show why these feats do *not* constitute evidence of cognition.


