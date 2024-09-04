---
layout: page
title: Ed-Fed
description: A generic federated learning framework
img: assets/img/Ed-Fed.JPG
importance: 1
related_publications: true
---

Federated learning (FL) has evolved as a prominent method for edge devices to cooperatively create a unified prediction model while securing their sensitive training data local to the device. Despite the existence of numerous research frameworks for simulating FL algorithms, they do not facilitate comprehensive deployment for automatic speech recognition tasks on heterogeneous edge devices. This is where Ed-Fed, a comprehensive and generic FL framework, comes in as a foundation for future practical FL system research.

**What is Federated Learning?**

<div class="row justify-content-sm-center">
    <div class="col-sm-4 mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/Ed-Fed.JPG" title="Ed-fed" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    Our Ed-Fed Framework: Depicting the essential components - server, client, and communication protocol. The green dotted lines represent interactions between client devices and the client selection algorithm. Clients send necessary information for the algorithm, and the server notifies them of their selection status. Red cross shows the clients not selected for FL round. Blue lines indicate the transmission of global weights from the server to clients in each round. The brown dotted line illustrates the interaction with the server strategy algorithm, where selected clients send weights that are aggregated to form the global weights.
</div>

The above figure shows a general FL setting. It consists of a set of clients (edge devices) and a server. The server maintains a global model, whose copy is initially sent to a subset of clients. These clients train their local model using the local data and communicate back the updated weights to the server. The server aggregates the weights using a strategy. This process is repeated for several rounds until the global model achieves a better accuracy.

**Ed-Fed Framework:**

Now, we will go through our Ed-Fed framework{% cite sasindran2023ed %}. We first discuss the methodology for facilitating on-device training and weight updation of models in the clients, followed by a brief overview on the communication protocol and the server-side algorithms used.

**Client**

<div class="row justify-content-sm-center">
    <div class="col-sm-8 mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/FL_tflite_new.JPG" title="Ed-fed" class="img-fluid rounded z-depth-1" %}
    </div>
        <div class="col-sm-4 mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/Android_app.JPG" title="Android_application" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
(a) Model with eight functions that allow us to successfully train the model on the device, and perform FL related functions for the clients in both single system simulation and Android based clients (b) Android application developed for FL
</div>

The above Figure depicts the optimized model with eight signature functions that allow us to successfully train the model on the device, and perform FL related functions in the mobile devices. Along with the existing signature functions such as train, evaluate, save, load, and calculate_loss, we build three new signature functions:

Get_1D_weights: reshapes an N-dimensional weight tensor from each node in the model graph to a 1-D array and returns a list of 1-D arrays.

Get_nodenames_shapes: returns all the node names as well as the actual tensor shapes.

Set_weights: reshape the aggregated 1-D weight array to N-D tensor and reloads it into the model.

**Communication protocol**

We use the gRPC communication protocol to ensure efficient communication between the server and clients. gRPC, like many RPC systems, is built on the concept of establishing a service, which describes the methods that can be called remotely with their input and return types. Protocol buffers are the most common interface definition language (IDL) used by gRPC to describe both the service interface and the message structure of the payloads. In our framework, three RPCs were used. “CommunicatedText” is the first, which is used to send the current context of the client and server. “GetGlobalWeights” is the second, which is used to send the current global FL weights to the clients who have been chosen for training. The final one is “GetFLWeights”, which is used to share the aggregated weights between the server and client.

**Server**

On the server side, there are two major components: the Client selection and Aggregation strategy.

Client selection involves selecting k clients out of N available clients. In case of waiting time optimised client selection algorithms, the clients should be selected in such a way that the overall waiting time of the clients is minimised, while ensuring fairness in the selection of clients. The weight aggregation is an integral part of FL.

The server strategy algorithms aggregates the weights obtained from the selected k clients by choosing algorithms such as FedAvg , and the updated weights are sent back to the clients.

**Results**

<div class="row">
    <div class="col-sm-6 mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/Avg-WER.JPG" title="results1" class="img-fluid rounded z-depth-1" %}
    </div>
    <div class="col-sm-6 mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/Validation_accuracy.jpg" title="results2" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
Performance of Ed-Fed on Automatic Speech Recogntion (ASR) and Image classification tasks: The performance of global model at each round is assessed using the global validation set, with the reported average 
 metric used for evaluation.
</div>

The results obtained from running Ed-Fed on system-based simulations for ASR and image classification tasks is given in the above figure. Here, we compared the impact of using various server strategy algorithms and the best one for each tasks.

<div class="row">
    <div class="col-sm-6 mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/Phone_results.JPG" title="results3" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
Evaluation of Ed-Fed Performance on Android-based Mobile Phones for ASR tasks
</div>

The above figures depicts the findings obtained on deployment of our Ed-Fed framework on multiple phones. The experiment is carried for 8 rounds on 4 mobile devices. In each round, 3 clients are selected. The round 0 in the figure refers to the initial global weights. All the checkpoints that are obtained at the end of each FL round are put to the test on a global test set. As could be predicted, the WER declines as the number of FL rounds grow. For more details, kindly have a look at our paper {% cite sasindran2023ed %} and reach out to me.


{% endraw %}
