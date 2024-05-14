---
name: 3D reconstruction of garments from a single RGB image
image: /assets/img/uv-map-3d-garment-reconstruction/logo.png
tools: [GAN, Deep Learning, Computer Vision, 3D, AI]
description: Deep learning model that learns garment dynamics and is able to reconstruct 3D garments from just a single RGB image.
---

# UV-based reconstruction of 3D garments from a single RGB image

Research project done at Human Pose Recovery and Behavior Analysis (HuPBA) group from the Computer Vision Center (CVC) in Barcelona. [Paper](https://www.researchgate.net/publication/358120826_UV-based_reconstruction_of_3D_garments_from_a_single_RGB_image) accepted to IEEE International Conference on Automatic Face and Gesture Recognition (FG 2021) and [Poster](https://sergioescalera.com/wp-content/uploads/2021/12/FG2021-UV-map-garment-reconstruction-poster.pdf) awarded with a Google Best Poster Award.

## Introduction
Inferring 3D shapes from a single viewpoint is an essential human vision feature extremely difficult for computer vision machines. Despite the advances in the field of 3D human reconstruction, most
research has concentrated only on unclothed bodies and faces, but modelling and recovering garments have remained notoriously tricky. We are interested in UV maps compared to other 3D surface 
representations such as meshes, point clouds or voxels, which are the ones commonly used in other 3D deep learning models. In this paper we adapt the LGGAN [1] architecture to predict
garment UV map from the input image. We also introduce 3D loss functions to improve the surface quality.

## UV Maps
The model has the novelty to use UV maps to represent 3D data. Garments are registered on top of SMPL [2] mesh to have homogeneous topology at both training and inference time. The UV coordinates 
are discrete points, thus UV maps have empty gaps between vertices. 
We use image inpainting techniques to estimate the values of the empty spaces and we use displacement UV maps that store garment vertices as an offset over the estimated SMPL body vertices.

## RGB to UV Map Translation - LGGAN Architecture
The model is based on the LGGAN architecture.
![preview](/assets/img/uv-map-3d-garment-reconstruction/LGGAN-Overview-ConditionBody.png)

- LGGAN is conditioned on body UV map and garment UV semantic segments.
- Global decoder G_g is responsible to predict low frequency details (overall shape).
- Local decoder G_l is responsible to learn specific dynamics w.r.t. each garment class.
- The amount of aggregation of global and local information is controlled by weight
decoder G_w through softmax.
- Class-specific discriminative feature learning branch classifies masked features to the
target garment class.
- Discriminator D receives the conditioning image (body UV map) and predicted
garment UV map to distinguish real data from fake.

## Class-Specific Local Generation Network
![preview2](/assets/img/uv-map-3d-garment-reconstruction/LGGAN-Local Generator.png)

- Shared latent code is upconvolved to form per-pixel features.
- Features are masked into specific branches by garment semantic labels.
- Garment-specific convolutions map the features to relative 3D coordinates.
- All branches are aggregated to form the final UV map.

## Generator Loss
- L1 loss on the
reconstructed UV map,
- Smooth L1 loss on the
reconstructed mesh,
- L2 loss on the surface
normals based on
nearest neighbor
matching,
- Laplacian smoothing
regularization,
- Edge length
regularizan.

## CLOTH3D++ Dataset [3]
- As dataset to train our network we use CLOTH3D++, the first
large-scale synthetic dataset of
3D clothed human sequences.
- Garments are simulated on top
of thousands of different human
pose sequences and body
shapes, generating realistic cloth
dynamics.
- It has over 2 million 3D samples
with a large variety of garment
types, topology, shape, size,
tightness and fabric. 

## Evaluation Metric
- We use surface-to-surface
(S2S) error [3], an extension
of the chamfer distance (CD),
that computes the distance
based on the nearest faces
rather than nearest vertices.
- As S2S evaluates the results
based on mesh format,
during evaluation we
unwrap UV map
representations into 3D
meshes.

## Results
![preview3](/assets/img/uv-map-3d-garment-reconstruction/LGGAN - Final Ablation Study - Qualitative.png)
![preview4](/assets/img/uv-map-3d-garment-reconstruction/results.png)

### Comparison with SMPLicit [4]
![preview5](/assets/img/uv-map-3d-garment-reconstruction/LGGAN - Final Comparison SMPLicit - Qualitative.png)

### References
[1] H. Tang, D. Xu, Y. Yan, P. H. S. Torr, and N. Sebe. Local class-specific and global image-level generative
adversarial networks for semantic-guided scene generation, CVPR, 2020.
[2] M. Loper, N. Mahmood, J. Romero, G. Pons-Moll, and M. J. Black. SMPL: A skinned multi-person linear
model. ACM Trans. Graphics (Proc. SIGGRAPH Asia), 34(6):248:1–248:16, Oct. 2015.
[3] M. Madadi, H. Bertiche, W. Bouzouita, I. Guyon, and S. Escalera. Learning cloth dynamics: 3d + texture
garment reconstruction benchmark. In Proceedings of the NeurIPS 2020 Competition and Demonstration
Track, PMLR, volume 133, pages 57–76, 2021.
[4] E. Corona, A. Pumarola, G. Alenya, G. Pons-Moll, and F. Moreno-Noguer. Smplicit: Topology-aware
generative model for clothed people, CVPR, 2021
