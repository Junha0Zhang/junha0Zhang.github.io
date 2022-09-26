---
layout: page
title: Automatic anatomical analysis of MRI
description: A comprehensive pipeline inspired by morphology, pix2pix GAN, and SVM
img: assets/img/brain_mri.jpg
importance: 2
category: Medical Imaging
---
At the request of doctors, I measure the skull thicknesses and scalp-to-cortex distances at four different locations (sphenoid, parietal, etc.) from MRI scans. The data is further categorized in terms of gender and age to study the distribution. This geometric information is important to transcranial imaging modalities involved with optics and ultrasound because they have limited depth and resolution for functional imaging. 

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/infared.jpg" title="example image" class="img-fluid rounded z-depth-1" %}
    </div>
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/ultrasound.jpg" title="example image" class="img-fluid rounded z-depth-1" %}
    </div>
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/transcranial_oat.jpg" title="example image" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    Left: transcranial near-infrared optical tomography. Middle: transcranial ultrasound. Right: transcranial optoacoustic tomography. Both optical and ultrasound waves will be heavily attenuated and distorted during the propagation. That's why we measure those distances to find the optimal solutions of imaging in future clinical practice.
</div>

Segmentation of skull and calculating its thickness profile from T1 MRI are generally very challenging because bones are black along with air in the scans. The first solution is using morphological transformations to extract the surface of inner and outer surfaces of the skull and calculating the 95% Hausdorff distance of the outer surface. The same procedure is applied to the scalp and cortex. By registering each MRI to a template in advance, we can make sure that we are measuring the same location for each sample. And thanks to the API of 3D Slicer, we can process a batch of scans automatically.

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/measurement.jpg" title="example image" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    This image can also have a caption. It's like magic.
</div>

Another solution, which is getting interesting, is using machine/deep learning to segment the skull from MRI. In this project, I calculate a feature-descripting vector (descriptor) for each voxel (3D pixel) of the images based on the (pre-registered) location and neighbor intensities. By training present paired MRI-CT dataset with support vector machine, we optimize the weights that classify each voxel as skull or non-skull. This method works well with limited number of training data like paired MRI-CT. Another possible solution is directly using 3D U-net to segment the skull, which needs to be investigated further.    


<div class="row justify-content-sm-center">
    <div class="col-sm-8 mt-3 mt-md-0">
        {% include figure.html path="assets/img/SVM.jpg" title="example image" class="img-fluid rounded z-depth-1" %}
    </div>
    <div class="col-sm-4 mt-3 mt-md-0">
        {% include figure.html path="assets/img/SCD.jpg" title="example image" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    Left and middle: the MRI scan and its predicted skull segmentation. Right: the calculated scalp-to-cortex distance map. As people age, this value should increase because the brain is shrinking.
</div>

Even more interestingly, I am currently trying to construct a generative adversarial network (GAN) inspired by pix2pix GAN to directly translate 3D MRI to CT, and then segment the skull by plain thresholding. A test result is shown below, but the result is a bit unstable. Perhaps I need to keep tuning the hyperparameters, so stay updated!   
<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/MRI_CT.jpg" title="example image" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    Left: original MRI for test. Middle: paired CT as ground truth. Right: synthesized CT from the MRI. We then segment out the skull from thresholding. This approach is a bit unstable now and this is way better than average.
</div>
