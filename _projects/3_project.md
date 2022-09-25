---
layout: page
title: 3D MRI-optoacoustic image registration
description: Deep learning based, fully automatic
img: assets/img/3.jpg
importance: 3
category: Medical Imaging
---
Multispectral optoacoustic tomography (MSOT) is an imaging technology that generates high-resolution optical images in biological tissues. It allows measurements of higher spatial resolution than conventional diffuse optical methods, while being non-invasive and non-ionizing. However, it suffers from comparably poor soft-tissue or anatomical contrast. To study the images from anatomical perspective in research, registration is usually required with MRI. 

The co-registration between these two imaging modalities is currently done mannually via software such as PMOD, or semi-automatically via some algorithm. Either way, there is a lot of mannual work required even for the latter. Since both images are 3D and very different in appearance, the process can be time-consuming and painful unfortunately. Thus, a fully automatic pipeline would be so great! 

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/1.jpg" title="example image" class="img-fluid rounded z-depth-1" %}
    </div>
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/3.jpg" title="example image" class="img-fluid rounded z-depth-1" %}
    </div>
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/5.jpg" title="example image" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    Caption photos easily. On the left, a road goes through a tunnel. Middle, leaves artistically fall in a hipster photoshoot. Right, in another hipster photoshoot, a lumberjack grasps a handful of pine needles.
</div>

Segmentation of skull and calculating its thickness profile from T1 MRI is generally very challenging because bones are black along with air in the scans. The first solution is using morphological transformations to extract the surface of inner and outer surfaces of the skull and calculating the 95% Hausdorff distance of the outer surface. The same procedure is applied to the scalp and cortex. By registering each MRI to a template in advance, we can make sure that we are measuring the same location for each sample. And thanks to the API of 3D Slicer, we can process a batch of scans automatically.

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/pipleline.jpg" title="example image" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    The pipeline of registration between MSOT and MRI. The U-net can be 3D or 2D according to the image types. The registration CNN is trained to predict a transformation matrix. 
</div>

Another solution, which is getting interesting, is using machine/deep learning to segment the skull from MRI. In this project, I calculate a feature-descripting vector (descriptor) for each voxel (3D pixel) of the images based on the (pre-registered) location and neighbor intensities. By training present paired MRI-CT dataset with support vector machine, we optimize the weights that classify each voxel as skull or non-skull. This method works well with limited number of training data, which is true for paired MRI-CT. Another possible solution is directly using 3D U-net to segment the skull, which needs to be investigated further.    


<div class="row justify-content-sm-center">
    <div class="col-sm-8 mt-3 mt-md-0">
        {% include figure.html path="assets/img/6.jpg" title="example image" class="img-fluid rounded z-depth-1" %}
    </div>
    <div class="col-sm-4 mt-3 mt-md-0">
        {% include figure.html path="assets/img/11.jpg" title="example image" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    You can also have artistically styled 2/3 + 1/3 images, like these.
</div>

Even more interestingly, I am currently trying to construct a generative adversarial network (GAN) inspired by pix2pix GAN to directly translate 3D MRI to CT, and then segment the skull by plain thresholding. A test result is shown below, but the result is a bit unstable. Perhaps I need to keep tuning the hyperparameters, so stay updated!   

{% raw %}
```html
<div class="row justify-content-sm-center">
    <div class="col-sm-8 mt-3 mt-md-0">
        {% include figure.html path="assets/img/6.jpg" title="example image" class="img-fluid rounded z-depth-1" %}
    </div>
    <div class="col-sm-4 mt-3 mt-md-0">
        {% include figure.html path="assets/img/11.jpg" title="example image" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
```
{% endraw %}
