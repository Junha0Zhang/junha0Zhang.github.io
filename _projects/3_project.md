---
layout: page
title: 3D MRI-optoacoustic image registration
description: Deep learning based, fully automatic
img: assets/img/3.jpg
importance: 3
category: Medical Imaging
---
Multispectral optoacoustic tomography (MSOT) is an imaging technology that generates high-resolution optical images in biological tissues. It allows measurements of higher spatial resolution than conventional diffuse optical methods, while being non-invasive and non-ionizing. However, it suffers from comparably poor soft-tissue or anatomical contrast. To study the images from anatomical perspective in research, registration is usually required with MRI. 

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/MRI.jpg" title="example image" class="img-fluid rounded z-depth-1" %}
    </div>
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/pbb.jpg" title="example image" class="img-fluid rounded z-depth-1" %}
    </div>
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/aoi.jpg" title="example image" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    Caption photos easily. On the left, a road goes through a tunnel. Middle, leaves artistically fall in a hipster photoshoot. Right, in another hipster photoshoot, a lumberjack grasps a handful of pine needles.
</div>

The co-registration between these two imaging modalities is currently done mannually via software such as PMOD, or semi-automatically via some algorithm. Either way, there is a lot of mannual work required even for the latter. Since both images are 3D and very different in appearance, the process can be time-consuming and painful unfortunately. Thus, a fully automatic pipeline would be so great! 

The solution involves with the segmentation of brain in each imaging modality through U-net, and then the registration between two brain masks (DL-based or optimization-based can both do the job!). The error function can be chosen as RMSE, BCE, Dice, or you can explore your own to optimize the prediction.  
<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/pipeline.jpg" title="example image" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    The pipeline of registration between MSOT and MRI. The U-net can be 3D or 2D according to the image types. The registration CNN is trained to predict a transformation matrix. 
</div>

Of course, directly expanding 2D U-net to 3D is not that simple becasue 3D volumetric data contains a lot more information than 2D. Since annonated 3D medical images are usually very limited in number, this will easily lead to overparameterization. So besides regular data augmentation like rotation, translation, and scaling, we use Generative Adversarial Networks (GANs) such as DCGAN and cycleGAN to generate realistic images. This helps us boost the number of training data and fight against overparameterization.  


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


