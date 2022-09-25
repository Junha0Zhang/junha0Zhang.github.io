---
layout: page
title: HoloRegi
description: Patient registration with HoloLens 2
img: assets/img/background_neuronavigation.jpg
importance: 3
category: Neuronavigation
---

Neuronavigation is technologies used by neurosurgeons to navigate inside the patient's skull by registering medical images and the physical world. At the neurosurgery OR in University Hospital Zurich, the geometry of the physical world is scanned by infrared system from Zeiss and the registration is done using software provided by BrainLab and Medtronic. They are highly delicate devices and are unaffordable for some hospitals. They are also sometimes inconvenient to work with because they take a long time to implement and the quality of registration can vary a lot. 

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/neurosurgery.jpg" title="neurosurgery" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    A typical neuronavigation system using infrared in the OR. A mechanical part with four infrared balls is clamped to the head of the patient and detected. The software registers the 3D mesh reconstructed from MRI with the scanned data from infrared.
</div>

In current solution with Hololens-based neuronavigation, a pointer is used to indicate several points on both the hologram (mesh reconstructed from MRI and shown on the glasses) and the patient in the same order to register the hologram. There are several issues with this approach: 

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
    Neuronavigation developed by Augmedit. On the left, the generated MRI mesh. Middle, planning before neurosurgery. Right, guidance during neurosurgery.
</div>

With the novel technology of mixed reality, we implemente a new neuronavigation system based on HoloLens 2, where the hologram of medical images is superimposed on the real patient using an automatic registration algorithm. By enabling research mode on Hololens 2, we get access to 8 avaliable sensor streams including IR, visual light, and depth. We use these data streams to reconsturct the patient's head in the real world coordinate and register that with patient's MRI. With more data accessible, our solution makes it much easier for surgeons to plan and navigate intracranial neurosurgeries.


<div class="row justify-content-sm-center">
    <div class="col-sm-8 mt-3 mt-md-0">
        {% include figure.html path="assets/img/test_patient.jpg" title="test patient" class="img-fluid rounded z-depth-1" %}
    </div>
    <div class="col-sm-4 mt-3 mt-md-0">
        {% include figure.html path="assets/img/test_phantom.jpg" title="test phantom" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    Left: The test result on real patient in the OR. According to the feedback from surgeon, we have achieved clinical accuracy. Right: Test on phantom head. Because there is no noise around (such as the mouth tubing or hair), the registration is (and should be) nearly perfect.
</div>

Instead of registering images with only 5 paired landmarks, we directly register the entire face of the patient to the face of the reconstructed MRI mesh. With powerful cloud copmputing like Azure, the automatic registration is done within 5 seconds. The average registration error is only 2.5mm, enabling accurate neuronavigation and planning for surgeons. In general, we substantially improve the current solution by building a fast, accurate, and stable workflow.  

