---
layout: page
title: MobileASR
description: A resource-aware on-device training methodology for ASR models on mobilephones
img: assets/img/Ed-Fed.JPG
importance: 2
related_publications: true
---



On-device training is a process of training machine learning models directly on the user’s device, such as a mobile phone, without relying on cloud-based infrastructure as shown in the figure. The idea is to preserve data privacy by keeping sensitive data on the user’s device such as audio containing personally identifiable information. Over time, as the user interacts with the system, the model fine-tunes its recognition capabilities to align specifically with the unique nuances of that user’s speech. This personalized adaptation enhances the accuracy and efficiency of the speech recognition system, delivering a more customized and user-centric experience. Additionally, on-device training not only preserves user privacy but also aligns with the growing emphasis on data security and user control over personal information.
However, implementing such functionalities on mobile devices is limited by factors such as CPU speed, memory, and storage availability, as well as the quality of on-device training data due to the use of cheap sensor hardware. Hence, training the models on mobile devices requires efficient algorithms that can handle the available limited resources available. Furthermore, the personalization process should not affect the device’s normal functioning including consuming too much energy, as this can negatively impact the user experience. As a result, training ASR models on lightweight systems is a challenge in itself. A wide range of real-world problems can benefit from implementing a on-device training framework for ASR models on mobile phones. For instance, it can facilitate the adaptation of the user’s voice for voice-controlled home automation or assistive technologies for individuals with speech impairments.
