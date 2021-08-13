---
name: Face Interpolator
tools: [VAE, CVAE, Deep Learning, Computer Vision, AI]
image: /assets/img/face_interpolator/face.png
description: Generative model for face edition software with named parameters using CVAE.
---

# Face Interpolator

For more details please visit [project's site](https://github.com/jdecid/face-interpolator).

Learning reusable feature representations from large unlabeled datasets allows us to modify these representations. It is also essential to be concerned about their meaning up to a certain degree of explainability. Using this idea and image generation approaches, we can create artificial images of a specific domain constrained with any properties that we want. Also, having the feature representation of a real-world object allows us to modify a real object's properties. By doing that, we can check how it would look like if we apply some modifications.

Face Interpolator is an API service that allows users to alter an image of a face by modifying certain attributes. Through this intelligent system, users have the opportunity to see how good they look with different hairstyles, glasses, facial expressions, among many other possible usages.

![preview](/assets/img/face_interpolator/overview.png)

This project tries to make artificial intelligence techniques for image editing accessible to everyone through an easy API interaction. We believe that the businesses that will make more profit out of this application will be small businesses that don't have either the knowledge or the resources to build this kind of application on their own, and even independent image editors or graphic designers. We also created a demo example of a possible application, which is shown in the following image:

![preview_2](/assets/img/face_interpolator/interface.png)

The model is based on Conditional Variational Autoencoders (CVAE), a Deep Learning method that can learn in an unsupervised manner efficient data representations (encoding) in a latent space and whose goal is to mimic a probability distribution (usually a Gaussian) to sample from. Model was trained using data from the CelebA dataset.

The interpolated images extracted from this release still lack this sense of reality. The system outputs blurred versions of the given image. Nonetheless, the system has been developed to be easily adapted to new improvements in the model to overcome these kinds of issues in future releases. In fact, we have already analyzed some alternatives, such as using Vector Quantized VAEs (VQ-VAE) since they seem to achieve a better representation of the given image.

![preview_3](/assets/img/face_interpolator/example.png)

Developed together with **Jordi Armengol**, **Josep de Cid** and **David Hilazo**.
