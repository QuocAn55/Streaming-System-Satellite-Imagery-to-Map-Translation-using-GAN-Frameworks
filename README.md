# Streaming-System-Satellite-Imagery-to-Map-Translation-using-GAN-Frameworks

## Abstract
This paper proposes a novel approach to enhancing search and rescue operations in forests by using a GAN-powered Streaming System Satellite Imagery to Map Translation model. Dense foliage and complex terrain often hinder visibility, making traditional cameras ineffective in identifying trails. To address this, the model utilizes Generative Adversarial Networks (GANs) to convert raw satellite imagery into accurate maps that highlight hidden forest paths. It also incorporates a real-time streaming system using Kafka and PySpark to integrate data from multiple drones and sensors, ensuring dynamic and comprehensive map generation. The combined system significantly improves situational awareness, enabling faster and more efficient rescue missions.

## Dataset
We collected high-resolution satellite imagery through the Google Maps Static API, which enabled us to gather images from a wide range of global geographic regions. This approach provided a diverse dataset featuring various landscapes, terrain types, and environmental settings—essential for effectively training and assessing the Streaming Real-time Satellite Imagery to Map Translation system based on GAN frameworks and distributed learning. In total, the curated dataset includes 2,000 image pairs consisting of satellite views and their respective map representations.

## Baseline model
### Cycle Generative Adversarial Network (CycleGAN)
CycleGAN, based on the original GAN proposed by Goodfellow et al., enables image-to-image translation without requiring paired training data. It uses two generators (G and F) and two discriminators (Dx and Dy) to learn mappings between two image domains. The model translates an input image to a new domain and then reconstructs it back to the original, minimizing the difference between the original and reconstructed images. This architecture allows CycleGAN to perform effective image translation even when corresponding input-output image pairs are not available.
<p align="center">
  <img width="600" src="https://drive.google.com/file/d/1kZscipUvJKI8sRRcaYY2yf2uj7nW9mlm/view?usp=sharing" alt="CGAN_Architecture">
  <br>
  <em>Figure 1: Cycle Generative Adversarial Network architecture.</em>
</p>


### Image-to-image translation with a conditional GAN(Pix2Pix)
The original GAN maps random noise z to a realistic output image G(z), but lacks control over the generated content. This makes it difficult to produce specific outputs. Conditional GAN (cGAN) addresses this limitation by conditioning the generation on both noise z and an input image x, allowing control over the output. The generator learns to produce realistic images G(z|x) that correspond to x, while the discriminator ensures that the generated image is both realistic and relevant to the input. This makes cGANs effective for image translation tasks.

## Experimental Results
This experiment evaluated Pix2Pix and CycleGAN for translating satellite imagery into maps. While both models performed well, Pix2Pix consistently produced more accurate and detailed maps, closely resembling ground truth and proving more useful for forest search and rescue scenarios. CycleGAN, although generally effective, introduced some distortions. Overall, Pix2Pix was found to be the more suitable model for this task, highlighting the importance of model selection in high-stakes applications like search and rescue.

## Proposed System
The core of the Streaming Real-time System for Satellite Imagery to Map Translation is a sophisticated architecture that processes image data from multiple sources—such as drones—using Kafka and PySpark. The system enables real-time integration and translation of image streams to generate dynamic, up-to-date maps for search and rescue in dense forests.

<p align="center">
  <img width="600" src="https://drive.google.com/file/d/1kZscipUvJKI8sRRcaYY2yf2uj7nW9mlm/view?usp=drive_link" alt="Streaming_system">
  <br>
  <em>Figure 2: Our proposed streaming system.</em>
</p>

Images are first Base64 encoded for platform-independent transmission via Kafka. Kafka, serving as a robust distributed message broker, manages high-throughput, fault-tolerant data streams from drones and satellites using its publish-subscribe model.
PySpark, a distributed computing framework, is used to process the incoming image streams at scale, ensuring efficient resource use across computing nodes. Once processed, the Base64-encoded images are decoded and input into a trained GAN model for real-time map translation. The system generates accurate maps that reveal hidden trails and critical features needed in rescue missions.
