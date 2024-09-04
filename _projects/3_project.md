---
layout: page
title: Smart client selection
description: A smart client selection algorithm for FL
img: assets/img/Ondevicelearning.JPG
importance: 3
related_publications: true
---

<div class="row justify-content-sm-center">
    <div class="col-sm-4 mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/Ondevicelearning.JPG" title="ODT" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption"> On-device learning
</div>

FL approach has emerged as a leading decentralized paradigm for training machine learning models, utilizing local data available on multiple client devices and thus ensuring data privacy and security. The distributed nature of FL offers immense potential for scalable and privacy-preserving model training across vast network of edge devices, such as mobile phones, and IoT devices.

One of the key challenges in FL revolves around the effective selection of suitable k clients from N available clients to participate in the training process, given their diverse hardware and specifications. This may potentially result in varying model training time among various devices. In a conventional FL setup, the server awaits model updates from all participating clients before proceeding to the next step. However, this synchronous nature of FL creates a potential bottleneck, as the overall FL process is slowed down by the variability in the training time required by each client.
This variability arises from factors such as the computational power of client devices and communication delays during the transfer of model weights to the server. These delays, commonly referred to as the ``straggler effect",  are primarily caused by clients with weaker network connections or limited computational capabilities. In FL, straggler devices refer to the participating client devices that take longer to complete their computations and send updates to the central server. This delay can cause synchronization problems and slow down the overall FL process. 

**Motivation**

At present, the most common client selection approach devised in FL setups involves the random selection of k clients from a pool of N clients. This approach works well in FL when there are no straggler devices. However, excluding straggler devices and choosing only resource-rich devices for a FL round to tackle this issue can undermine the generalization capabilities of the global model and fairness in the learning process. Therefore, this chapter seeks an answer to one important question - Is it possible to cleverly (or nicely) choose the k clients such that the difference in training time among clients is minimum. Also, there is a certain randomness associated with training time taken by the client devices, and this makes the whole process challenging. For instance, the system memory might either get freed up to speed up the training time or might reduce to slowdown. There can be events where the training process itself might be removed by the operating system (OS) due to lack of memory. We observe that system resources and training time share a non-linear relationship. This idea inspired us to use tools like neural network models to understand the hidden and complex relationships between the resource capabilities with the training time requirements. 

**Our client selection algorithm**
Considering the challenges involved in selecting the clients in FL to reduce the waiting times and efficiently managing straggler devices, we develop a resource-aware waiting time optimized
client selection algorithm aimed at tackling these challenges. Our algorithm considers the resources accessible on each client device and assigns tasks adaptively based on their specific
capabilities. Our approach Resource-aware waiting time optimized client selection algorithm comprises of three key phases - extraction of resource information, neural reward generation
using neuralUCB, and the implementation of a resource-aware waiting time optimized algorithm.

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
