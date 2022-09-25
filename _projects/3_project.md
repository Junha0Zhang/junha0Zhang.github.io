---
layout: page
title: 3D MRI-optoacoustic image registration
description: Deep learning based, fully automatic
img: assets/img/background_regi.jpg
importance: 3
category: Medical Imaging
---
Multispectral optoacoustic tomography (MSOT) is an imaging technology that generates high-resolution optical images in biological tissues. It allows measurements of higher spatial resolution than conventional diffuse optical methods, while being non-invasive and non-ionizing. However, it suffers from comparably poor soft-tissue or anatomical contrast. To study the images from anatomical perspective in research, registration is usually required with MRI. 

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/MRI.jpg" title="MRI" class="img-fluid rounded z-depth-1" %}
    </div>
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/pbb.jpg" title="pbb" class="img-fluid rounded z-depth-1" %}
    </div>
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/aoi.jpg" title="aoi" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    On the left, the template of mouse MRI transverse view. Middle, 3D PBB-dyed optoacoustic image maximum intenisity projection (MIP). Right, 3D AOI-dyed optoacoustic image MIP. 
</div>

The co-registration between these two imaging modalities is currently done mannually via software such as PMOD, or semi-automatically via some algorithm. Either way, there is a lot of mannual work required even for the latter. Since both images are 3D and very different in appearance, the process can be time-consuming and painful unfortunately. Thus, a fully automatic pipeline would be so great! 

The solution involves with the segmentation of brain in each imaging modality through U-net, and then the registration between two brain masks (DL-based or optimization-based can both do the job!). The error function can be chosen as RMSE, BCE, Dice, or you can explore your own to optimize the prediction.  
<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/pipeline.jpg" title="pipeline" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    The pipeline of registration between MSOT and MRI. The U-net can be 3D or 2D according to the image types. The registration CNN is trained to predict a transformation matrix. 
</div>

Of course, directly expanding 2D U-net to 3D is not that simple becasue 3D volumetric data contains a lot more information than 2D. Since annonated 3D medical images are usually very limited in number, this will easily lead to overparameterization. So besides regular data augmentation like rotation, translation, and scaling, we use Generative Adversarial Networks (GANs) such as DCGAN and cycleGAN to generate realistic images. This helps us boost the number of training data and fight against overparameterization.  

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/real_1.jpg" title="real_1" class="img-fluid rounded z-depth-1" %}
    </div>
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/fake.jpg" title="fake" class="img-fluid rounded z-depth-1" %}
    </div>
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/real_2.jpg" title="real_2" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    There are two real optoacoustic images and a fake one. Can you tell which is the fake? According to literature, the data augmentation can increase the network performance by 20%.
</div>


