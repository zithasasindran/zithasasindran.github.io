---
layout: page
title: MobileASR
description: A resource-aware on-device training methodology for ASR models on mobilephones
img: assets/img/Ed-Fed.JPG
importance: 2
related_publications: true
---

<div class="row justify-content-sm-center">
    <div class="col-sm-4 mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/Ondevicelearning.JPG" title="ODT" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption"> On-device learning
</div>

On-device training is a process of training machine learning models directly on the user’s device, such as a mobile phone, without relying on cloud-based infrastructure as shown in the figure. The idea is to preserve data privacy by keeping sensitive data on the user’s device such as audio containing personally identifiable information. Over time, as the user interacts with the system, the model fine-tunes its recognition capabilities to align specifically with the unique nuances of that user’s speech. This personalized adaptation enhances the accuracy and efficiency of the speech recognition system, delivering a more customized and user-centric experience. Additionally, on-device training not only preserves user privacy but also aligns with the growing emphasis on data security and user control over personal information.
However, implementing such functionalities on mobile devices is limited by factors such as CPU speed, memory, and storage availability, as well as the quality of on-device training data due to the use of cheap sensor hardware. Hence, training the models on mobile devices requires efficient algorithms that can handle the available limited resources available. Furthermore, the personalization process should not affect the device’s normal functioning including consuming too much energy, as this can negatively impact the user experience. As a result, training ASR models on lightweight systems is a challenge in itself. A wide range of real-world problems can benefit from implementing a on-device training framework for ASR models on mobile phones. For instance, it can facilitate the adaptation of the user’s voice for voice-controlled home automation or assistive technologies for individuals with speech impairments.

<div class="row justify-content-sm-center">
    <div class="col-sm-8 mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/ODT_module.JPG" title="Ed-fed" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
Model with dix functions that allow us to successfully train the model on the device
</div>

**Module for deployment**
A crucial step involves the conversion of the baseline ASR model into a memory-efficient and optimized format suitable for deployment on mobile platforms. We employed six key functions to interact with the model when deployed on devices and these functions are used to specify the inputs, such as training data, inference data, and the path to the checkpoint file, as well as the outputs, including loss values and the output probability matrix, as illustrated in the above figure. These functions can be customized based on our requirement. For instance, we built a function to extract the CTC loss value. Additionally, we utilize another function to retrieve parameter information from the model, which is subsequently employed in our resource-efficient model selection approach. The train function is responsible for effectively training the model on a batch or mini-batch of inputs, ensuring that training can be conducted directly on the mobile device.


<div class="row">
    <div class="col-sm-6 mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/RAM_utilization.JPG" title="results1" class="img-fluid rounded z-depth-1" %}
    </div>
    <div class="col-sm-6 mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/Training_results.JPG" title="results2" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
(a)RAM utilization (b)The WER trend across epochs for two training rounds
</div>


**Results**
We examined the impact of training on the memory of a OnePlus 7T phone that ran on Android 10 and had 5.3GB of available RAM out of 8GB. Our resource-aware model selection algorithm selected the best sub-model for training. We evaluate our on-device training procedure on multiple accents. We conduct our experiment on the dataset for accents for training and testing the model. Figure (b) shows the WER trend versus epochs for the first round of training. The trend indicates that WER values are monotonically decreasing with the increase in training epochs. The * symbol denotes the epoch where, the minimum metric value (WER) or when the battery percentage or RAM is below the threshold is obtained and the checkpoints are saved for the next round. We see that the steepest decrease in metric value is in the initial round. This happens when the model sees user data for the first time. As we continue, the average WER goes down more slowly. The speed of this improvement depends on the data we use. If we have new words or phrases in the data for a round, the model learns more and the test set WER gets better. Interestingly, we did not find any specific pattern related to accents or gender. It appears like these factors are influenced more by the data we use in each round rather than following a set pattern. This highlights the importance of using different data in every round. When the model encounters varied data each time, it learns better and becomes more personalized to the user's voice and unique characteristics.

For more details, kindly have a look at our paper {% cite sasindran2023mobileasr %} and reach out to me for further details.
