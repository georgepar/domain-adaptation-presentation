---
marp: true
theme: default
size: 16:9
class:
  - lead
  - invert
backgroundColor: "#222222"
style: |
  .columns2 {
    display: grid;
    grid-template-columns: repeat(2, minmax(0, 1fr));
    gap: 1rem;
  }
  .columns3 {
    display: grid;
    grid-template-columns: repeat(3, minmax(0, 1fr));
    gap: 1rem;
  }
  .grayout {
    opacity: 0.6; /* Real browsers */
    filter: alpha(opacity = 60); /* MSIE */
  }
  .invisible {
    opacity: 0.0; /* Real browsers */
    filter: alpha(opacity = 60); /* MSIE */
  }
  blockquote {
    border-top: 0.1em dashed #555;
    font-size: 60%;
    margin-top: auto;
  }
---

# Sample-Efficient Domain Adaptation

### Giorgos Paraskevopoulos

---


![bg](figs/ml_projects.svg)

---

<!-- Presenter notes. -->

# One solution: Fast Domain Adaptation
![height:15cm](figs/domain_adaptation.svg)


---


![bg cover invert:87%](figs/agi.png)

---


![bg contain invert:87%](figs/llm_growth.png)

---
<div class="columns2">

<div style="margin:auto">

![h:14cm](figs/sword.jpg)

</div>


<div style="margin:auto">


</div>

</div>

---

<div class="columns2">

<div style="margin:auto">

![h:14cm](figs/sword.jpg)

</div>


<div style="margin:auto">

![h:14cm](figs/knives.jpg)

</div>

</div>



---

# In this presentation

<div class="columns2">

<div style="margin:auto">

### Domain adaptation to improve:


* small-ish models (300M parameters)
* with few in-domain data
* for new application settings

</div>

<div class="invisible" style="margin:auto">

### Use-cases:

* Modular systems:

  * Automatic speech regognition (Language adaptation)

* End-to-end systems
 
   * Text classification (Sentiment analysis)
   * Automatic speech recognition (Acoustic adaptation)

</div>

</div>

---

# In this presentation

<div class="columns2">

<div class="grayout" style="margin:auto">

### Domain adaptation to improve:


* small-ish models (300M parameters)
* with few in-domain data
* for new application settings

</div>

<div style="margin:auto">

### Use-cases:

* Modular systems:

  * Automatic speech regognition (Language adaptation)

* End-to-end systems
 
   * Text classification (Sentiment analysis)
   * Automatic speech recognition (Acoustic adaptation)

</div>

</div>

---

# Language adaptation for ASR systems


---

# Modular ASR systems

![h:480 invert:87% contrast:100%](figs/hclg.png)

---

# Modular ASR systems

<div style="margin:auto">

![w:1280 h:480 invert:87% contrast:100%](figs/am_lm.png)

</div>

---

# 1. Collect in-domain text data
<div class="invisible"> 

# 2. Add new terminology to lexicon
# 3. Adapt $P(W)$

### Very cheap: Re-train new n-gram LM and swap the old one

### Automated recipe: Trivial to apply for new settings

</div>

---

<div class="grayout"> 

# 1. Collect in-domain text data

</div>

# 2. Add new terminology to lexicon

<div class="invisible"> 

# 3. Adapt $P(W)$ 

### Very cheap: Re-train new n-gram LM and swap the old one

### Automated recipe: Trivial to apply for new settings

</div>

---

<div class="grayout"> 

# 1. Collect in-domain text data
# 2. Add new terminology to lexicon
</div>

# 3. Adapt $P(W)$

<div class="invisible"> 

### Very cheap: Re-train new n-gram LM and swap the old one

### Automated recipe: Trivial to apply for new settings

</div>

---

<div class="grayout"> 


# 1. Collect in-domain text data
# 2. Add new terminology to lexicon

</div>

# 3. Adapt $P(W)$

### Very cheap: Train new n-gram LM and swap or interpolate the old one

### Automated recipe: Trivial to apply for new application domains

---

# Projects using this technique

<div class="columns3">

<div>


## Plan-V

Greek aphasic speech transcription and error detection


</div>


</div>

---


# NLP-Theater Results

<div class="columns2">

<div>

### Speech Recognition

| Model    | WER     |
| -------- | ------- |
| Google     | 32.4    |
| Ours unadapted | 39.2 |
| Ours adapted | **15.7** |

</div>

<div>

### Subtitle Synchronization



| Model | Error (mean) | Error (median) |
| ----- | ------------ | -------------- |
| Google |  10.30  | 3.78 |
| Ours adapted | **4.81** | 4.43 |


* Error measured in seconds
* Avoids extreme errors
</div>

</div>

> G. Bastas, et al. "Towards a DHH Accessible Theater: Real-Time Synchronization of Subtitles and Sign Language Videos with ASR and NLP Solutions." PETRA. 2022.


---

# Plan-V Results

<div class="columns2">


| Lev. Distance    | Percentage    (%) |
| -------- | ------- |
| 0     | 82.0    |
| 2     | 7.0 |
| 1 | 4.5 |
| > 3 | 6.5 | 


* Adapted model necessary
* Include mispronounced versions of words in lexicon
* Measure Levenshtein distance between transcribed word and ground truth
* Example: "καλοριθέρ" $\rightarrow$ "καλοριφέρ"


</div>

---


# Domain adaptation for end-to-end models

---


# Transfer learning <br/> Categorization

![bg contain](figs/tl-hierarchy.svg)

---


# Popular techniques for end to end models

<div class="columns3">

<div>

### Pseudolabeling

* Train model on labeled out-of-domain data
* Use model to annotate unlabeled in-domain data
* Reduce the task to supervised learning on generated labels

</div>


<div class="grayout">


### Adversarial Training

* Manipulate the latent space so that the extracted features are domain-invariant
* Use an adversarial cost so that the network can't predict the domain based on the latent features


</div>


<div class="grayout">

### Self-supervision

* Use pretext tasks to gradually adapt the model to the target domain data distribution
* Learn the task on the source domain 

</div>

</div>

---


# Popular techniques for end to end models

<div class="columns3">

<div class="grayout">

### Pseudolabeling

* Train model on labeled out-of-domain data
* Use model to annotate unlabeled in-domain data
* Reduce the task to supervised learning on generated labels

</div>


<div>


### Adversarial Training

* Manipulate the latent space so that the extracted features are domain-invariant
* Use an adversarial cost so that the network can't predict the domain based on the latent features


</div>


<div class="grayout">

### Self-supervision

* Use pretext tasks to gradually adapt the model to the target domain data distribution
* Learn the task on the source domain 

</div>

</div>

---


# Popular techniques for end to end models

<div class="columns3">

<div class="grayout">

### Pseudolabeling

* Train model on labeled out-of-domain data
* Use model to annotate unlabeled in-domain data
* Reduce the task to supervised learning on generated labels

</div>


<div class="grayout">


### Adversarial Training

* Manipulate the latent space so that the extracted features are domain-invariant
* Use an adversarial cost so that the network can't predict the domain based on the latent features


</div>


<div>

### Self-supervision

* Use pretext tasks to gradually adapt the model to the target domain data distribution
* Learn the task on the source domain 

</div>

</div>


---



# Popular techniques for end to end models

<div class="columns3">

<div>

### Pseudolabeling

* <span style="color:green"> **Pro**: </span>  Straightforward
* <span style="color:green"> **Pro**: </span>  Well explored in the literature
* <span style="color:red"> **Con**: </span> Error propagation


</div>


<div>


### Adversarial Training

* <span style="color:green"> **Pro**: </span>  Theoretical background
* <span style="color:green"> **Pro**: </span>  Truly e2e approach
* <span style="color:red"> **Con**: </span>  Convergence can be challenging


</div>


<div>

### Self-supervision

* <span style="color:green"> **Pro**: </span> Easy to apply
* <span style="color:green"> **Pro**: </span>  In-domain sample-efficiency
* <span style="color:red"> **Con**: </span>  Computationally more expensive

</div>

</div>

---

# Use case 1: Sentiment Analysis

###### C. Karouzos, <ins>G. Paraskevopoulos</ins>, A. Potamianos. "UDALM: Unsupervised Domain Adaptation through Language Modeling." NAACL 2021.

---



# Step 1

![invert:87%](figs/bert1.png)

> C. Karouzos, <ins>G. Paraskevopoulos</ins>, A. Potamianos. "UDALM: Unsupervised Domain Adaptation through Language Modeling." NAACL 2021.


---



# Step 2

![invert:87%](figs/bert2.png)

> C. Karouzos, <ins>G. Paraskevopoulos</ins>, A. Potamianos. "UDALM: Unsupervised Domain Adaptation through Language Modeling." NAACL 2021.

---

# Step 3

![invert:87%](figs/bert3.png)

> C. Karouzos, <ins>G. Paraskevopoulos</ins>, A. Potamianos. "UDALM: Unsupervised Domain Adaptation through Language Modeling." NAACL 2021.

---

# Overview

<div style="margin:auto">

![invert:87%](figs/bert4.png)

</div>

> C. Karouzos, <ins>G. Paraskevopoulos</ins>, A. Potamianos. "UDALM: Unsupervised Domain Adaptation through Language Modeling." NAACL 2021.

---

# Dataset: Amazon reviews

* Standard benchmark dataset for domain adaptation.
* Binary sentiment classification task.
* Domains: Books (**B**), DVDs (**D**), Electronics (**E**), Kitchen appliances (**K**)
* 12 adaptation scenarios of source-target domain pairs (e.g. **B** → **D**).
* 2,000 labeled reviews per domain.
* 19,809 **B**, 19,798 **D**, 19,937 **E** and 17,805 **K** unlabeled reviews.

> C. Karouzos, <ins>G. Paraskevopoulos</ins>, A. Potamianos. "UDALM: Unsupervised Domain Adaptation through Language Modeling." NAACL 2021.



---

# Results

<div style="margin:auto">


![invert:87% height:12cm](figs/results_udalm.png)

</div>

> C. Karouzos, <ins>G. Paraskevopoulos</ins>, A. Potamianos. "UDALM: Unsupervised Domain Adaptation through Language Modeling." NAACL 2021.

---

# Sample-Efficiency

<div style="margin:auto">

![invert:87% height:12cm](figs/sample_efficiency_udalm.png)

</div>

> C. Karouzos, <ins>G. Paraskevopoulos</ins>, A. Potamianos. "UDALM: Unsupervised Domain Adaptation through Language Modeling." NAACL 2021.

---

# Use case 2: Adaptation of XLSR-53 for ASR

###### <ins>G. Paraskevopoulos</ins> et al., Sample-Efficient Unsupervised Domain Adaptation of Speech Recognition Systems: A case study for Modern Greek, under revision IEEE/ACM TASL-P


---

# Key take-aways

* Apply ideas from UDALM for acoustic adaptation of XLSR-53 
  * Multi-domain instead of in-domain self-supervision 
* Combine with simple language adaptation techniques
* Apply for cross-corpus speech recognition in Greek
* Demonstrate sample-efficiency
* New corpus: Hellenic Parliament recordings (120 hours)

> <ins>G. Paraskevopoulos</ins>, T. Kouzelis, G. Rouvalis, A. Katsamanis, V. Katsouros, A. Potamianos, Sample-Efficient Unsupervised Domain Adaptation of Speech Recognition Systems: A case study for Modern Greek, under revision IEEE/ACM TASL-P
--- 

# M2DS2: Mixed Multi-domain Self-Supervision

<div class="columns2">

<div>

Method similar with UDALM
* No Continual Pretraining step
* Add source domain self-supervision in multitask loss
* Avoid mode-collapse of discrete code-vectors
  
</div>

<div>

![invert:87%](figs/m2ds2.png)
</div>


</div>

$L = L_{CTC}(\text{source samples}) + \alpha \cdot L_{SS}(\text{source samples}) + \beta \cdot L_{SS}(\text{target samples})$

> <ins>G. Paraskevopoulos</ins>, T. Kouzelis, G. Rouvalis, A. Katsamanis, V. Katsouros, A. Potamianos, Sample-Efficient Unsupervised Domain Adaptation of Speech Recognition Systems: A case study for Modern Greek, under revision IEEE/ACM TASL-P

---

# Corpora

<!-- <div style="margin:auto"> -->

![height:4cm invert:87%](figs/corpora_m2ds2.png)

* 6 adaptation scenarios between Logotypografia (LG), Common Voice (CV) and HParl (HP)

<!-- </div> -->

> <ins>G. Paraskevopoulos</ins>, T. Kouzelis, G. Rouvalis, A. Katsamanis, V. Katsouros, A. Potamianos, Sample-Efficient Unsupervised Domain Adaptation of Speech Recognition Systems: A case study for Modern Greek, under revision IEEE/ACM TASL-P

---

# Results 

![height:5cm invert:87%](figs/results_m2ds2.png)


* WER $\rightarrow$ Word Error Rate $\quad$ WRR $\rightarrow$ Relative adaptation improvement (%)
* G $\rightarrow$ Greedy decoding $\quad$ LM $\rightarrow$ Generic LM reweighting

> <ins>G. Paraskevopoulos</ins>, T. Kouzelis, G. Rouvalis, A. Katsamanis, V. Katsouros, A. Potamianos, Sample-Efficient Unsupervised Domain Adaptation of Speech Recognition Systems: A case study for Modern Greek, under revision IEEE/ACM TASL-P

--- 

# Sample Efficiency

<div style="margin:auto">

![invert:87%](figs/sample_efficiency_m2ds2.png)

</div>

> <ins>G. Paraskevopoulos</ins>, T. Kouzelis, G. Rouvalis, A. Katsamanis, V. Katsouros, A. Potamianos, Sample-Efficient Unsupervised Domain Adaptation of Speech Recognition Systems: A case study for Modern Greek, under revision IEEE/ACM TASL-P


---

# Combine with LM adaptation

<div class="columns2">
<div style="font-size:0.8em">

* Biased LM: 
  * Train N-gram LM on in-domain data
* Augmented LM:
  * Train N-gram LM on in-domain data
  * Use in-domain LM to filter lines with low perplexity from large corpus
  * Tran N-gram LM on augmented data

</div>

<div style="margin:auto">

![invert:87%](figs/lm_adapt_m2ds2.png)

</div>
  </div>

> <ins>G. Paraskevopoulos</ins>, T. Kouzelis, G. Rouvalis, A. Katsamanis, V. Katsouros, A. Potamianos, Sample-Efficient Unsupervised Domain Adaptation of Speech Recognition Systems: A case study for Modern Greek, under revision IEEE/ACM TASL-P


---

# What we gain overall?

<div style="margin:auto">

![height:12cm invert:87%](figs/overall_m2ds2.png)

</div>

> <ins>G. Paraskevopoulos</ins>, T. Kouzelis, G. Rouvalis, A. Katsamanis, V. Katsouros, A. Potamianos, Sample-Efficient Unsupervised Domain Adaptation of Speech Recognition Systems: A case study for Modern Greek, under revision IEEE/ACM TASL-P

--- 

# Conclusions

Under some closed world assumptions (known application domain) we can improve performance with

1. few in-domain data without annotations
2. in-domain self-supervision to avoid catastrophic forgetting

The techniques presented are:

1. simple to implement
2. evaluated in diverse settings
3. domain-invariant (no domain expertise needed)

<!-- 
 -->
