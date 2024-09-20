In the field of Additive Manufacturing (AM), ensuring the mechanical integrity of printed parts is critical. X-ray Computed Tomography (X-CT) is frequently employed for non-destructive evaluation of porosity and structural defects within AM samples. Traditional 2D methods, however, often miss critical volumetric details, especially when classifying fine structures like pores. To overcome this limitation, we have developed a workflow utilizing both unsupervised and supervised 3D Deep Learning (DL) models for voxel-wise classification of porosity.

The process begins by scanning AM parts, using X-CT to create high-resolution volumetric datasets. The high complexity of these datasets demands advanced techniques for accurate anomaly detection, such as identifying small or irregularly shaped pores.

3D Patch-Based Approach:
The method uses a 3D patch-based approach, where the large volumetric X-CT dataset is broken down into smaller 64x64x64 voxel patches. This allows neural networks to process manageable chunks of data without sacrificing critical volumetric information.

Model Training – Supervised and Unsupervised:
We utilize both supervised and unsupervised learning models for voxel-wise classification. For the supervised models, we train on annotated data using a custom loss function (focal Tversky loss) that addresses the imbalance between pore and non-pore voxels, as the numerosity of non-pore voxels is much greated than pore-voxels. In the unsupervised approach, models like the Variational Autoencoder (VAE) learn from unlabelled data to identify anomalies based on reconstruction error. The VAE model is trained to compress 3D patches of X-CT data into a lower-dimensional latent space, and then reconstruct the original patch from this compressed representation. The key idea is that the VAE learns to capture the normal patterns in the training data. When presented with anomalous structures like pores, the reconstruction will deviate from the original input.
![targe1](/images/pore_segmentation/dl_1.png)

Implemented models: 
For the supervised models, we employed UNet, MSS-UNet, UNet++, and UNet 3+, all of which are based on variations of the popular encoder-decoder architecture for semantic segmentation tasks. On the unsupervised side, we implemented Variational Autoencoders (VAE), along with its more advanced versions ceVAE, gmVAE, and vqVAE. 

Post-Processing of unsupervised models:
Unsupervised models, while powerful, often blur critical details, especially near sample surfaces. To counteract this, we apply a post-processing algorithm, based on the derivative of the output, that corrects the voxel-wise anomaly scores, refining the results to highlight porosity with greater clarity.

Re-training of supervised models: In the re-training phase, the best-performing unsupervised model, ceVAE, was used to generate labels for the supervised models. This allowed us to create a fully unsupervised pipeline by using the anomaly scores from the ceVAE model as training labels for the supervised models. The supervised models were then retrained from scratch using these labels instead of the original annotated data. This procedure aimed to verify if the UNet-family could have reasonable performance by using labels produced with an unsupervised model, freeing the supervised model of any manual or heuristic annotation.

![targe2](/images/pore_segmentation/dl_2.png)

This 3D-based approach has shown to provide more accurate and reliable detection of porosity in AM parts, if compared to the Otsu-based thresholding method. The best approach resulted to be the unsupervised one, if properly post-processed. Moreover, by re-training the unsupervised models, it was proven that the UNet-family of networks has limitation, even considering recent variations of the base architecture. 

![targe3](/gifs/pore/defects.gif)

For more details, check out our open-source framework [here](https://github.com/snipdome/nn_3D-anomaly-detection) and explore the extensive analysis in our [article](https://arxiv.org/abs/2305.07894).