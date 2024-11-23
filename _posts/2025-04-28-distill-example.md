---
layout: distill
title: "Diffusion Models and Gaussian Flow Matching: Two Sides of the Same Coin"
description: "Flow matching and diffusion models are two popular frameworks in generative modeling. Despite seeming similar, there is some confusion in the community about their exact connection. In this post we aim to clear up this confusion and show that <i>diffusion models and Gaussian flow matching are the same</i>, although  different model specifications can lead to different noise schedules and loss weighting terms. This means you can use the two frameworks interchangeably, as we will show."
date: 2025-11-12
future: true
htmlwidgets: true
hidden: false

# Anonymize when submitting
authors:
  - name: Anonymous

# authors:
#   - name: Albert Einstein
#     url: "https://en.wikipedia.org/wiki/Albert_Einstein"
#     affiliations:
#       name: IAS, Princeton
#   - name: Boris Podolsky
#     url: "https://en.wikipedia.org/wiki/Boris_Podolsky"
#     affiliations:
#       name: IAS, Princeton
#   - name: Nathan Rosen
#     url: "https://en.wikipedia.org/wiki/Nathan_Rosen"
#     affiliations:
#       name: IAS, Princeton

# must be the exact same name as your blogpost
bibliography: 2025-04-28-distill-example.bib  

# Add a table of contents to your post.
#   - make sure that TOC names match the actual section names
#     for hyperlinks within the post to work correctly. 
#   - please use this format rather than manually creating a markdown table of contents.
toc:
  - name: Overview
  - name: Sampling
  - name: Training
  - name: Diving deeper into samplers
  - name: From Diffusion Models to Flow Matching and Back

# Below is an example of injecting additional post-specific styles.
# This is used in the 'Layouts' section of this post.
# If you use this post as a template, delete this _styles block.
_styles: >
  .fake-img {
    background: #bbb;
    border: 1px solid rgba(0, 0, 0, 0.1);
    box-shadow: 0 0px 4px rgba(0, 0, 0, 0.1);
    margin-bottom: 12px;
  }
  .fake-img p {
    font-family: monospace;
    color: white;
    text-align: left;
    margin: 12px 0;
    text-align: center;
    font-size: 16px;
  }
---

{% include figure.html path="assets/img/2025-04-28-distill-example/twotrees.jpg" class="img-fluid" %}


Flow matching is gaining popularity recently, due to the simplicity of its formulation and the  “straightness” of its induced sampling trajectories. This raises the commonly asked question:

<p align="center"><i>"Which is better, diffusion or flow matching?"</i></p>

The purpose of this blog post is to explain that the two methods are equivalent (for the common special case that the source distribution used with flow matching corresponds to a Gaussian). We will show how to convert one formalism to another. This allows you to mix and match techniques. For example, after training a flow matching model, you can use either a stochastic or deterministic sampling method (in contrast to the common misunderstanding that flow matching is always deterministic). We will focus on  the most commonly used flow matching formalism  <d-cite key="lipman2022flow"></d-cite>, which is closely related to <d-cite key="liu2022flow,albergo2023stochastic"></d-cite>. Our purpose is not to recommend one approach over another. Instead our goal is to explain similarities and differences between the methods, and to explain the degrees of freedom one has when tuning each algorithm.



## Overview

We start with a quick overview of the two frameworks.



### Diffusion models

A diffusion process gradually destroys an observed datapoint $${\bf x}$$ (such as an image) over multiple time steps, indexed by $$t$$, by mixing the data with Gaussian noise. More precisely, the noisy version of the input at time $$t$$ is given by:

$$
\begin{equation}
{\bf z}_t = \alpha_t {\bf x} + \sigma_t {\boldsymbol \epsilon}, \;\mathrm{where} \; {\boldsymbol \epsilon} \sim \mathcal{N}(0, {\bf I}).
\label{eq:forward}
\end{equation}
$$

Here $$\alpha_t$$ and $$\sigma_t$$ define the **noise schedule** ,such as the variance-preserving schedule ($$\alpha_t^2 + \sigma_t^2 = 1$$). An important quantity we will need later is the log signal-to-noise ratio, given by $$\lambda_t = \log(\alpha_t^2 / \sigma_t^2)$$, which decreases as $$t$$ increases from $$0$$ (clean data) to $$1$$ (Gaussian noise).

### Comparison

We can already see that the two frameworks are very similar, but there seem to be some differences, too.
To summarize what we have seen so far:


<div style="padding: 10px 10px 10px 10px; border-left: 6px solid #FFD700; margin-bottom: 20px;">
  <p>1. <strong>Same forward process</strong>: If we assume that one end of flow matching is a Gaussian distribtuion, and if we define the noise schedule of diffusion models in a particular form, then we have shown that the two approaches define an identical forward process. </p>
  <p  style="margin: 0;">2. <strong>"Similar" sampling processes</strong>: we have shown that both methods follow an iterative update that involves a guess of the clean data at the current time step and then an update. Below we will show that the sampling process turns out to be identical. </p>
</div>


## Sampling 

A common thought is that the two frameworks are different in sampling: Flow matching is deterministic and with "straight" paths, while diffusion model sampling is stochastic and with curved paths. Let's discuss it first. 

We will focus on deterministic sampling first which is simpler. Imagine you want to use your trained denoiser model to transform random noise into a datapoint. Recall that the DDIM update is given by $${\bf z}_{s} = \alpha_{s} \hat{\bf x} + \sigma_{s} \hat{\boldsymbol \epsilon}$$. Interestingly, rearranging terms it can be expressed in the following formulation, with respect to several network outputs and reparametrizations:

$$
\begin{equation}
\tilde{\bf z}_{s} = \tilde{\bf z}_{t} + \mathrm{Network \; output} \cdot (\eta_s - \eta_t) \\
\end{equation}
$$

| Network Output  | Reparametrization   |
| :------------- |-------------:|
| $$\hat{\bf x}$$-prediction      |    $$\tilde{\bf z}_t = {\bf z}_t / \sigma_t$$ and $$\eta_t = {\alpha_t}/{\sigma_t}$$ |
| $$\hat{\boldsymbol \epsilon}$$-prediction      |    $$\tilde{\bf z}_t = {\bf z}_t / \alpha_t$$ and $$\eta_t = {\sigma_t}/{\alpha_t}$$ |
| $$\hat{\bf u}$$-flow matching vector field      |    $$\tilde{\bf z}_t = {\bf z}_t/(\alpha_t + \sigma_t)$$ and $$\eta_t = {\alpha_t}/(\alpha_t + \sigma_t)$$ | 

Recall the flow matching update in Equation (4), look similar? With $$\hat{\bf u}$$ prediction and $$\alpha_t = t$$, $$\sigma_t = 1- t$$, we have $$\tilde{\bf z}_t = {\bf z}_t$$ and $$\eta_t = t$$, so that it recovers the flow matching update! More formally, the flow matching update can be considered the Euler integration of the underlying sampling ODE <d-footnote> That is, $\mathrm{d}\tilde{\bf z}_t = \mathrm{[Network \; output]}\cdot\mathrm{d}\eta_t$</d-footnote>, and

<div style="padding: 10px 10px 10px 10px; border-left: 6px solid #FFD700; margin-bottom: 20px;">
  <!-- <p>For weighting functions,</p> -->
  <p align="center" style="margin: 0;"><em>Diffusion with DDIM sampling == Flow matching sampling (Euler).</em></p>
</div>

Other traits about the DDIM sampler:


1. DDIM sampler *analyically* integrates the underlying sampling ODE if the network output is a *constant* over time. Of course the network prediction is not constant, but it means the inaccuracy of DDIM sampler only comes from approximating the intractable integral of the network output <d-footnote>not from additional linear term of ${\bf z}_t$ as in the Euler sampler of probability flow ODE <d-cite key="song2020score"></d-cite></d-footnote>. This holds for all three network outputs.

2. DDIM update and final samples are invariant to a linear scaling applied to the noise schedule, as a scaling does not affect $\tilde{\bf z}_t$ and $\eta_t$. 

<!-- In both frameworks deterministic sampling comes down to integrating an ODE. One of the choice we have, is the numerical method to compute the ODE. A famous inegrator is the DDIM sampler, which analyically integrates the sampling ODE for a *constant* prediction from your network. Of course the network prediction is not constant, but if the stepsize is small enough one hopes it suffices. We have seen this sampler in the introduction section before and it is: -->


<!-- Recall that rescalings of $\alpha_t$ $\sigma_t$ should not matter, instead the important thing is their ratio $\alpha_t / \sigma_t$. 
What's special about DDIM is that it is insensitive to rescalings of $\alpha_t$ and $\sigma_t$. No matter whether your schedule is variance preserving, variance exploding or flow matching, it gives the same answer!<d-footnote>You may have to rescale your inputs and outputs of your neural net for this, but it is pretty straightforward. Other choices in literature are standard Euler method or higher-order methods, but these give different results with different results depending on the choice of $\alpha$ and $\sigma$.</d-footnote> -->


<!-- An interesting special case is the standard flow matching interpolation ($\alpha_t = 1. - t$, $\sigma_t = t$). In this case Euler integration (used by flow matching) is exactly the same as DDIM. -->


Skeptical about 2? Check it out for yourself below: We consider several settings between the flow matching (FM) schedule and a variance-preserving (VP)  schedule by changing a linear scaling. DDIM always gives the same final samples regardless of the scaling of the schedule, which is also the same as the flow matching sampler. The paths bend in different ways as $${\bf z}_t$$ (not $$\tilde{\bf z}_t$$) is scale-dependent along the path. For the Euler sampler of diffusion probabilty flow ODE introduced in <d-cite key="song2020score"></d-cite>, the scaling makes a true difference: Both the paths and the final samples change.


<!-- Beware to that generating the same samples does not mean following the same path. The ODE and DDIM paths do bend as you change the slider but note how start and end-points never change. -->
<!-- When adjusting the slider to the right we adjust $\alpha$ and $\sigma$ towards the Variance Preserving (VP) schedule. -->

<!-- The ground truth line is the true ODE path while the DDIM and ODE lines show an approximation with just a few sampling steps. -->

<div class="l-page">
  <iframe src="{{ 'assets/html/2025-04-28-distill-example/interactive_alpha_sigma.html' | relative_url }}" frameborder='0' scrolling='no' height="600px" width="100%"></iframe>
</div>

<p align="center"><i>"Flow matching paths are straight, whereas diffusion paths are curved."</i></p>

Wait? The flow matching schedule is said to result in straighter paths, but in the above figure its sampling trajectories look *curved* and the VP paths look *straight*.

So why is the flow matching parameterization said to result in straighter sampling paths?
If the model would be perfectly confident about the data point it is moving to, the path from noise to data will be a straight line with the flow matching schedule.
Straight line ODEs would be great because it means that there is no integration error whatsoever.
Unfortunately, the predictions are not for a single point. Instead they average over a larger distribution.
<!-- In this case, there is no guarantee that the flow matching formulation or DDIM integration leads to less error. -->

<div style="padding: 10px 10px 10px 10px; border-left: 6px solid #FFD700; margin-bottom: 20px;">
  <!-- <p>For weighting functions,</p> -->
  <p align="center" style="margin: 0;"><em>Straight to a point != Straight to a distribution.</em></p>
</div>


In fact, in the interactive graph below you can change the variance of a simple Guassian data distribution.
Note how the variance preserving schedule is the best for wide distributions while the flow matching schedule works well for narrow distributions.

<div class="l-page">
  <iframe src="{{ 'assets/html/2025-04-28-distill-example/interactive_vp_vs_flow.html' | relative_url }}" frameborder='0' scrolling='no' height="600px" width="100%"></iframe>
</div>


Finding such straight paths for real-life datasets like images is of course much less straightforward. But the conclusion remains the same: The optimal integration method depends on the data and the models prediction.

Two important takeaways from determinstic sampling:

<div style="padding: 10px 10px 10px 10px; border-left: 6px solid #FFD700; margin-bottom: 20px;">
  <p>1. DDIM is equivalent to the flow matching sampling, and is invariant to a linear scaling to the noise schedule. </p>
  <p  style="margin: 0;">2. Flow matching schedule is only straight for a model predicting a single point. For realistic distributions other interpolations can give straighter paths.</p>
</div>

<!-- 1. For DDIM the interpolation between data and noise is irrelevant and always equivalant to flow matching <d-footnote>The variance exploding formulation ($\alpha_t = 1$, $\sigma_t = t$) is also equivalant to DDIM and flow matching. -->

## Training 

<!-- For training, a neural network is estimated to predict $$\hat{\boldsymbol \epsilon} = \hat{\boldsymbol \epsilon}({\bf z}_t; t)$$ that effectively estimates $${\mathbb E} [{\boldsymbol \epsilon} \vert {\bf z}_t]$$, the expected noise added to the data given the noisy sample. Other **model outputs** have been proposed in the literature which are linear combinations of $$\hat{\boldsymbol \epsilon}$$ and $${\bf z}_t$$, and $$\hat{\boldsymbol \epsilon}$$ can be derived from the model output given $${\bf z}_t$$.  -->

Diffusion models <d-cite key="kingma2024understanding"></d-cite> are trained by estimating $$\hat{\bf x} = \hat{\bf x}({\bf z}_t; t)$$ with a neural net. In practice, one chooses a linear combination of $$\hat{\bf x}$$ and $${\bf z}_t$$ for stability reasons.
<!-- <d-footnote>It take a little bit of effort to show that indeed you only need linear combinations to define model outputs such as $$\hat{\boldsymbol{\epsilon}}$$, $$\hat{\bf v}$$ and $$\hat{\bf u}$$ (from flow matching)</d-footnote>. -->
Learning the model is done by minimizing a weighted mean squared error (MSE) loss:
$$
\begin{equation}
\mathcal{L}(\mathbf{x}) = \mathbb{E}_{t \sim \mathcal{U}(0,1), \boldsymbol{\epsilon} \sim \mathcal{N}(0, \mathbf{I})} \left[ \textcolor{green}{w(\lambda_t)} \cdot \frac{\mathrm{d}\lambda}{\mathrm{d}t} \cdot \lVert\hat{\bf x} - {\bf x}\rVert_2^2 \right],
\end{equation}
$$
where $$\lambda_t$$ is the log signal-to-noise ratio, and $$\textcolor{green}{w(\lambda_t)}$$ is the **weighting function**, balancing the importance of the loss at different noise levels. The term $$\mathrm{d}\lambda / {\mathrm{d}t}$$ in the training objective seems unnatural and in the literature is often merged with the weighting function. However, their separation helps *disentangle* the factors of noise schedule and weighting function clearly, and helps emphasize the more important weighting components.  

Flow matching also fits in the training objective, recall the conditional flow matching objective used by <d-cite key="lipman2022flow, liu2022flow"></d-cite> is

$$
\begin{equation}
\mathcal{L}_{\mathrm{CFM}}(\mathbf{x}) = \mathbb{E}_{t \sim \mathcal{U}(0,1), \boldsymbol{\epsilon} \sim \mathcal{N}(0, \mathbf{I})} \left[ \lVert \hat{\bf u} - {\bf u} \rVert_2^2 \right]
\end{equation}
$$

Since $$\hat{\bf u}$$ is also a linear combination of $$\hat{\bf x}$$ and $${\bf z}_t$$, the CFM training objective can be rewritten as mean squared error on $${\bf x}$$ with a specific weighting. 


### How do we choose the weighting term?
The weighting is the most important part of the loss, it balances the importance of high frequency and low frequency components.  **(TODO, making a figure to illustrate weighting function versus frequency components.)** 
This is important when modeling images, videos and audios, as certain high frequency components in those signals are not visible to human perception, and thus better not to waste model capacity on them. Viewing losses via their weighting, one can derive that:

<div style="padding: 10px 10px 10px 10px; border-left: 6px solid #FFD700; margin-bottom: 20px;">
  <!-- <p>For weighting functions,</p> -->
  <p align="center" style="margin: 0;"><em>Flow matching weighting == diffusion weighting of ${\bf v}$-MSE loss + cosine noise schedule.</em></p>
</div>

That is, the flow matching training objective is the same as a commonly used setting in diffusion models! See Appendix D.2-3 in <d-cite key="kingma2024understanding"></d-cite> for a detailed derivation. Figure **TODO** plots several commonly used weighting functions in the literature. 

### How do we choose what the network should output?
Below we summarize several network outputs proposed in the literature, including a few of diffusion models and the one of flow matching. One may see the training objective defined with different network outputs in different papers. From the perspective of training objective, they all correspond to having some additional weighting in front of the $${\bf x}$$-MSE that can be absorbed in the weighting function. 

| Network Output  | Formulation   | MSE on Network Output  |
| :------------- |:-------------:|-----:|
| $${\bf x}$$-prediction      | $$\hat{\bf x} $$      | $$ \lVert\hat{\bf x} - {\bf x}\rVert_2^2 $$ |
| $${\boldsymbol \epsilon}$$-prediction      |$$\hat{\boldsymbol \epsilon} = ({\bf z}_t - \alpha_t \hat{\bf x}) / \sigma_t$$ | $$\lVert\hat{\boldsymbol{\epsilon}} - \boldsymbol{\epsilon}\rVert_2^2 = e^{\lambda} \lVert\hat{\bf x} - {\bf x}\rVert_2^2 $$|
| $${\bf v}$$-prediction | $$\hat{\bf v} = \alpha_t \hat{\boldsymbol{\epsilon}} - \sigma_t \hat{\bf x} $$      |    $$ \lVert\hat{\bf v} - {\bf v}\rVert_2^2 = \sigma_t^2(e^{-\lambda} + 1)^2 \lVert\hat{\bf x} - {\bf x}\rVert_2^2 $$ |
| $${\bf u}$$-flow matching vector field | $$\hat{\bf u} = \hat{\bf x} - \hat{\boldsymbol{\epsilon}} $$      |    $$ \lVert\hat{\bf u} - {\bf u}\rVert_2^2 = (1 + e^{\lambda / 2})^2 \lVert\hat{\bf x} - {\bf x}\rVert_2^2 $$ |

In practice, however, the model output might make a difference. For example,
* $${\bf x}$$-prediction can be problematic at low noise levels, because small changes create a large loss under typical weightings. You can also see in the sampler that any error in $$\hat{\bf x}$$ will get amplified in $$\hat{\boldsymbol \epsilon} = ({\bf z}_t - \alpha_t \hat{\bf x}) / \sigma_t$$, as $$\sigma_t$$ is close to 0.
* Following the similar reason, $${\boldsymbol \epsilon}$$-prediction is problematic at high noise levels, because $$\hat{\boldsymbol \epsilon}$$ is not informative, and the error gets amplified in $$\hat{\bf x}$$.

Therefore, a heuristic is to choose a network output that is a combination of $${\bf x}$$- and $${\boldsymbol \epsilon}$$-prediction, which applies to the $${\bf v}$$-prediction and the flow matching vector field $${\bf u} = {\bf x} - {\bf \epsilon}$$.


### How do we choose the noise schedule?
A few remarks about training noise schedule:
1. All noise schedules can be normalized as a variance-preserving schedule, with a linear scaling of $${\bf z}_t$$ and an unscaling at the network input. The key defining property of a noise schedule is the log signal-to-noise ratio $$\lambda_t$$.
2. The training loss is *invariant* to the training noise schedule, since the loss fuction can be rewritten as $$\mathcal{L}(\mathbf{x}) = \int_{\lambda_{\min}}^{\lambda_{\max}} w(\lambda) \mathbb{E}_{\boldsymbol{\epsilon} \sim \mathcal{N}(0, \mathbf{I})} \left[ \|\hat{\boldsymbol{\epsilon}} - \boldsymbol{\epsilon}\|_2^2 \right] \, d\lambda$$, which is only related to the endpoints but not the schedule of $$\lambda_t$$. However, $$\lambda_t$$ might still affect the variance of the Monte Carlo estimator of the training loss. A few heuristics have been proposed in the literature to automatically adjust the noise schedules over the training course. [Sander's blog post](https://sander.ai/2024/06/14/noise-schedules.html#adaptive) has a nice summary.
3. one can choose completely different noise schedules for training and sampling, based on distinct heuristics: For training, it is desirable to have a noise schedule that minimizes the variance of the Monte Calor estimator, whereas for sampling the noise schedule is more related to the discretization error of the ODE / SDE sampling trajectories and the model curvature.

### Summary

In summary, we have the following conclusions for diffusion models / flow matching training:

<div style="padding: 10px 10px 10px 10px; border-left: 6px solid #FFD700; margin-bottom: 20px;">
  <p>1. Weighting function <strong> is important for training</strong>. For perceptual signals, it balances the importance of different frequency components. It should be tuned based on data characteristics. </p>
  <p>2. Noise schedule <strong>is far less important to the training objective</strong> and affects the training efficiency.</p>
  <p style="margin: 0;">3. The network output proposed by flow matching nicely balances ${\bf x}$- and ${\epsilon}$-prediction, similar to ${\bf v}$-prediction.</p>
</div>



## Diving deeper into samplers

In this section, we discuss different kinds of samplers in more detail.

### Reflow operator

The Reflow operation in Flow Matching connects noise and data points to sample in a straight line.
One can obtain these data noise pairs by running a deterministic sampler from noise.
A model can then be trained to directly predict the data given the noise avoiding the need for sampling.
In the diffusion literature the same approach was the one of the first distillation techniques <d-cite key="luhman2021knowledge"></d-cite>.




### Deterministic sampler vs. stochastic sampler

So far we mainly cover the deterministic sampler of diffusion models or flow matching. An alternative is to use stochastic samplers such as the DDPM sampler <d-cite key="ho2020denoising"></d-cite>. The key is to realize that, the effect of a small step of DDIM update can be canceled out by a small step of forward diffusion update in distribution. To see why it is true, let's take a look at a 2D example. Starting from the same mixture of Gaussians distribution, we either apply a reverse DDIM update, or a diffusion update:
{% include figure.html path="assets/img/2025-04-28-distill-example/particle_movement.gif" class="img-fluid" %}
For each individual sample, the two updates are very different. The reverse DDIM update consistently drags every sample away from the modes of the distribution, while the diffusion update is purely random. However, aggregating all samples together, the distributions after the updates are the same, thereby validating our claim. That means we can run DDIM update with a large step then followed by a "renoising" step, which matches the effect of running DDIM update with a smaller step. 

<!-- If we flip the sign of the drift update and add another diffusion update: $${\bf z}_{t+\Delta t} = {\bf z}_t + s \nabla_{\bf z} \log p_t({\bf z}) + \sqrt{2s}{\bf e}$$, the effect of the two updates gets canceled out, so that the distribution remains unchanged. The DDPM sampler or its variants essentially add certain amount of these two updates on top of the DDIM sampler at every time step. The benefit is that if the model prediction is not perfectly accurate, the diffusion update helps correct the error. -->
<!-- The formal proof requires some manipulation of Fokker-Planck equation <d-cite key="song2020score"></d-cite>.  -->
<!-- The drift update is about stretching or flattening the distribution, whereas the diffusion update is about smoothing or reducing the curvature of the distribution.   -->

In fact, performing one DDPM sampling step going from $\lambda_t$ to $\lambda_t + \Delta\lambda$ is exactly equivalent to performing one DDIM sampling step to $\lambda_t + 2\Delta\lambda$, and then renoising to $\lambda_t + \Delta\lambda$ by doing forward diffusion. DDPM thus reverses exactly half the progress made by DDIM in terms of the log signal-to-noise ratio. However, the fraction of the DDIM step to undo by renoising is a hyperparameter which we are free to choose, and which has been called the level of _churn_ by <d-cite key="karras2022elucidating"></d-cite>. The effect of adding churn to our sampler is to diminish the effect on our final sample of our model predictions made early during sampling, and to increase the weight on later predictions. This is shown in the Figure below

<div class="l-page">
  <iframe src="{{ 'assets/html/2025-04-28-distill-example/churn.html' | relative_url }}" frameborder='0' scrolling='no' height="600px" width="100%"></iframe>
</div>

Here we ran different samplers for 100 sampling steps using a cosine noise schedule and v-prediction <d-cite key="salimansprogressive"></d-cite>. Ignoring nonlinear interactions, the final sample produced by the sampler can be written as a weighted sum of predictions made during sampling and noise. The weights of these predictions are shown on the y-axis for different diffusion times shown on the x-axis. DDIM results in an equal weighting of v-predictions for this setting, as shown by Salimans & Ho, whereas DDPM puts more emphasis on predictions made towards the end of sampling. Also see <d-cite key="lu2022dpm"></d-cite> for analytic expressions of these weights in the x and $\epsilon$ parameterizations.

## From Diffusion Models to Flow Matching and back

So far, we have shown that the equivalence of the flow matching sampler and the DDIM sampler. 
We have also shown that the weightings appearing in flow matching and diffusion models can all be expressed in a general framework by expressing them in terms of log-SNR. 
This should (hopefully!) have convinced you that the frameworks are identical. 
But how easily can you move from one framework to the other? 
Below, we derive <strong>exact formula</strong> to move from a diffusion model to a flow matching perspective and vice-versa. 

### Diffusion Models framework hyperparameters

We have stated in the overview that "A diffusion process gradually destroys an observed data $$ \bf{x} $$ over time $$t$$". But what is this gradual process? It can be fully described by the following evolution equation

$$
\begin{equation}
\mathrm{d} {\bf z}_t = f_t {\bf z}_t \mathrm{d} t + g_t \mathrm{d} {\bf z} ,
\end{equation}
$$

where $$\mathrm{d} {\bf z}$$ is an <em> infinitesimal Gaussian</em> <d-footnote>If you want to  be fancy this is usually referred to as a Brownian motion in the literature. </d-footnote>

Looking at this representation, the free parameters are given by $f_t$ and $g_t$. From the diffusion model perspective, the generative process is given by the reverse of the forward process, whose formula is given by 

$$
\begin{equation}
\mathrm{d} {\bf z}_t = \left( f_t {\bf z}_t - \frac{1+ \eta_t^2}{2}g_t^2 \nabla \log p_t({\bf z_t}) \right) \mathrm{d} t + \eta_t g_t \mathrm{d} {\bf z} ,
\end{equation}
$$

where $\nabla \log p_t$ is the <em>score</em> of the forward process <d-footnote>This is why you might have noticed that some papers refer to diffusion models as "score-based generative models".</d-footnote>

Note that we have introduced an additional parameter $\eta_t$ which controls the amount of stochasticity at inference time. This is exactly the <em>churn</em> parameter introduced before. When discretizing the backward process we recover DDIM in the case $\eta_t = 0$ and DDPM in the case $\eta_t = 1$. So to summarize: 

<div style="padding: 10px 10px 10px 10px; border-left: 6px solid #FFD700; margin-bottom: 20px;">
  Diffusion model frameworks can be entirely determined by three hyperparameters  
  <p>1. $f_t$ which controls how much we forget the original data in the forward process. </p>
  <p>2. $g_t$ which controls how much noise we input into the samples in the forward process. </p>
  <p style="margin: 0;">3. $\eta_t$ which controls the amount of stochasticity at inference time. </p>
</div>

### Flow Matching framework hyperparameters

Now let's turn to flow matching and its degrees of freedom. We consider a slightly more general setting than in the overview and introduce the following interpolation

$$
\begin{equation}
{\bf z}_t = \alpha_t {\bf x} + \sigma_t {\bf z} .
\end{equation}
$$

This is a specific case of the general <em>stochastic interpolation</em><d-cite key="liu2022flow,albergo2023stochastic"></d-cite>.
In that case, the free parameters are given by $\alpha_t$ and $\sigma_t$. From the flow matching perspective, the generative process is by the following trajectory

$$
\begin{equation}
\mathrm{d} {\bf z}_t = (v_t({\bf z_t}) - \varepsilon_t^2 \nabla \log p_t({\bf z_t})) \mathrm{d} t + \varepsilon_t \mathrm{d} {\bf z} .
\end{equation}
$$

Note that we have introduced an additional parameter $\varepsilon_t$ which controls the amount of stochasticity at inference time. 

<div style="padding: 10px 10px 10px 10px; border-left: 6px solid #FFD700; margin-bottom: 20px;">
  Flow matching frameworks can be entirely determined by three hyperparameters  
  <p>1. $\alpha_t$ which controls the data component in the interpolation. </p>
  <p>2. $\sigma_t$ which controls the noise component in the interpolation. </p>
  <p style="margin: 0;">3. $\varepsilon_t$ which controls the amount of stochasticity at inference time. </p>
</div>

### Equivalence of the points of view

Despite their clear similarities it is not immediately clear how to link the diffusion model framework and the flow matching one. 
Below, we provide formulae which give a one-to-one mapping between the two frameworks. In short:

<div style="padding: 10px 10px 10px 10px; border-left: 6px solid #FFD700; margin-bottom: 20px;">
  Diffusion model and flow matching are just one change of variable away!
</div>

Given a diffusion model framework, i.e. hyperparameters $f_t, g_t, \eta_t$ one can define 

$$
\begin{equation}
\alpha_t = \exp\left(\int_0^t f_s \mathrm{d}s\right) , \qquad \sigma_t = \left(\int_0^t g_s^2 \exp\left(-2\int_0^s f_u \mathrm{d}u\right) \mathrm{d} s\right)^{1/2} , \qquad \varepsilon_t = \eta_t g_t . 
\end{equation}
$$

Doing so, the noising process induced by the flow matching and the diffusion framework as well as the generative trajectories!
Similarly, given a flow matching framework, i.e. hyperparameters $\alpha_t, \sigma_t, \varepsilon_t$ one can define 

$$
f_t = \partial_t \log(\alpha_t) , \qquad g_t = 2 \alpha_t \sigma_t \partial_t (\sigma_t / \alpha_t) , \qquad \eta_t = \varepsilon_t / (2 \alpha_t \sigma_t \partial_t (\sigma_t / \alpha_t)) . 
$$

We have the similar conclusion, that under this transformation, diffusion models and flow matching frameworks coincide. 
To sum up, leaving aside training issues and the choice of the sampler, there is no fundamental differences between the two approaches.
