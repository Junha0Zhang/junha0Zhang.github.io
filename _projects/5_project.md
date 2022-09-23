---
layout: page
title: project 5
description: Patient registration with HoloLens 2
img: assets/img/1.jpg
importance: 3
category: Neuronavigation
---

Neuronavigation is technologies used by neurosurgeons to navigate inside the patient's skull by registering medical images and the physical world. At neurosurgery OR in University Hospital Zurich, the geometry of the physical world is scanned by infrared system from Zeiss and the registration is done using software provided by BrainLab and Medtronic. They are highly delicate devices and are unaffordable for some hospitals. They are also sometimes inconvenient to work with because they take a long time to implement and the quality of registration can vary a lot. 

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/neurosurgery.jpg" title="neurosurgery" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    A typical neuronavigation system using infrared in the OR. A mechanical part with four infrared balls is clamped to the head of the patient and detected.
</div>

In current solution with Hololens-based neuronavigation, a pointer is used to indicate several points on both the hologram and the patient in the same order to register the hologram. There are several issues with this approach: 

1. It is time-consuming: The surgeon needs to manually indicate all the facial landmarks. And if one makes a mistake in the process, he/she has to start pointing all over again.
2. It has large errors: According to report, the average fiducial registration error of this approach is about 8.5mm, which can be large for clinical accuracy.
3. It is unstable: the quality of registration heavily depends on the accuracy of picked point pairs.  

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/MRI_mesh.jpg" title="MRI mesh" class="img-fluid rounded z-depth-1" %}
    </div>
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/neurosurgical_planning.jpg" title="neurosurgical planning" class="img-fluid rounded z-depth-1" %}
    </div>
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/neurosurgical_guidance.jpg" title="neurosurgical guidance" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    Neuronavigation developed by Augmedit from the Netherlands. On the left, the generated MRI mesh. Middle, planning before neurosurgery. Right, guidance during neurosurgery.
</div>

With the novel technology of mixed reality, we implemente a new neuronavigation system based on HoloLens 2, where the hologram of medical images is superimposed on the real patient using an automatic registration algorithm. By enabling research mode on Hololens 2, we get access to 8 avaliable sensor streams including IR, visual light, and depth. We use these data streams to reconsturct the patient's head in the real world coordinate and register that with patient's MRI. With more data accessible, uur solution makes it much easier for surgeons to plan and navigate intracranial neurosurgeries.


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


The code is simple.
Just wrap your images with `<div class="col-sm">` and place them inside `<div class="row">` (read more about the <a href="https://getbootstrap.com/docs/4.4/layout/grid/">Bootstrap Grid</a> system).
To make images responsive, add `img-fluid` class to each; for rounded corners and shadows use `rounded` and `z-depth-1` classes.
Here's the code for the last row of images above:

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
