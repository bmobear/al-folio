---
layout: default
title: viva
description: Visual Variation Learning for Object Recognition
img: /assets/img/2019_viva_6.png
---

<h2 class="page-title">Visual Variation Learning for Object Recognition</h2>


+ We propose visual variation learning to improve object recognition with convolutional neural networks (CNN). While a typical CNN regards visual variations as nuisances and marginalizes them from the data, we speculate that some variations are informative. 
+ We study the impact of visual variation as an auxiliary task, during training only, on classification and similarity embedding problems. 
+ Our key contribution is that, at the cost of visual variation annotation during training only, CNN enhanced with visual variation learning learns better object representations.


<div class="pub_img center" width="100%">
    <img width="50%" src="{{ site.baseurl }}/assets/img/2019_viva_7.png"/>
    <p class="darkcaption">
    Gradient-weighted class activation mapping (<a href="http://doi.acm.org/10.1109/ICCV.2017.74">Grad-CAM</a>) on iLab-2M test data. Both object instances are misclassified as car on ResNet without variation learning and correctly classified as van and monster on ResNet with variation learning (ResNet+Pose). The heatmaps on the second row highlight regions of the image that activate the incorrect class on ResNet and on the third row hightligh regions that activates the correct class on ResNet+Pose. ResNet+Pose is more tuned to the shape of an object across poses and focuses on distinctive features of each category (flat front of the van and oversized wheels of the monster truck).
    </p>
</div>


<div class="citation">
    Visual Variation Learning for Object Recognition. Jatuporn Toy Leksut, Jiaping Zhao, Laurent Itti; <em>Image and Vision Computing</em>, 2020 <br><br>

    [DOI: <a href="https://doi.org/10.1016/j.imavis.2020.103912" target="_blank">10.1016/j.imavis.2020.103912</a>][<a href="{{ site.baseurl }}/assets/pdf/viva_preprint.pdf" target="_blank">Preprint</a>]
</div>

---

### Data

#### iLab-20M
The iLab-20M dataset is a large-scale controlled, parametric dataset of toy vehicle objects under variations of viewpoint, lighting, and background. The dataset is produced by placing a physical object on a turntable and using multiple cameras located on a semicircular arc over the table. 

+ 15 categories: boat, bus, car, equipment, f1car, helicopter, military, monster truck, pickup truck, plane, semi truck, tank, train, UFO, and van 
+ 718 object instances
+ 88 different viewpoints (11 elevations x 8 azimuths)
+ 5 lighting conditions
+ 3 camera focus settings
+ 14--40 background images
+ 22 million images total

<div class="pub_img center" width="100%">
    <img width="100%" src="{{ site.baseurl }}/assets/img/page_viva_ilab2m.png"/>
    <p class="darkcaption">
    The iLab dataset provides toy vehicle images from 15 categories in various viewpoints, lighting conditions, and backgrounds.
    </p>
</div>

<div class="citation">
    iLab-20M: A Large-Scale Controlled Object Dataset to Investigate Deep Learning. Ali Borji, Saeed Izadi, Laurent Itti; The IEEE Conference on Computer Vision and Pattern Recognition (CVPR), 2016 <br><br>


    [DOI: <a href="https://doi.org/10.1109/CVPR.2016.244" target="_blank">10.1109/CVPR.2016.244</a>]
    [<a href="http://openaccess.thecvf.com/content_cvpr_2016/html/Borji_iLab-20M_A_Large-Scale_CVPR_2016_paper.html" target="_blank">Open Access</a>]
</div>

#### iLab-80M
The iLab-80M is an augmented set of the iLab-20M adding random crops and scales. The augmentation ensures that the number of images per category is well balanced, resulting in 5.5 million images per category and a total of 82.7 million images for the whole set. 

In addition, the original `960x720` images are cropped around each object and rescaled to `256x256`.

#### iLab-2M
The iLab-2M is a subset of iLab-80M sampled for experiments conducted in this work. In iLab-2M, data vary only in pose variation, while other visual variations are kept constant.
+ 30 poses (5 elevations x 6 azimuths)
+ 1.2M training images, 270K validation images, 270K test images

<div class="link-button"><a href="http://ilab.usc.edu/ilab2m/iLab-2M.tar.gz">Download iLab-2M</a></div>

<div class="pub_img center" width="100%">
    <img width="50%" src="{{ site.baseurl }}/assets/img/2019_viva_6.png"/>
</div>

#### iLab-2M-Light
The iLab-2M-Light is an extension of the iLab-2M that includes lighting conditions as an additional visual variation.
+ 30 poses (same as iLab-2M)
+ 5 lighting conditions
+ 1.36M training images, 316K validation images, 316K test images

<div class="link-button"><a href="http://ilab.usc.edu/ilab2m/iLab-2M-Light.tar.gz">Download iLab-2M-Light</a></div>



---

### Methods

#### 1. Variation Classification


<div class="pub_img center" width="100%">
    <img width="50%" src="{{ site.baseurl }}/assets/img/2019_viva_multilayer.png"/>
    <p class="darkcaption">
    A multi-layer variation-injected CNN built on top of <a href="http://doi.acm.org/10.1145/3065386">AlexNet</a>. AlexNet is enclosed inside the left box. All additional components on the right are part of the variation classification module. Dotted lines represent injection connections that connect intermediate conv/pool layers to transformation (fc) units. Outputs of transformation units are summed into variation scores.
    </p>
</div>


#### 2. Variation Embedding Learning


<div class="pub_img center" width="100%">
    <img width="50%" src="{{ site.baseurl }}/assets/img/2019_viva_tripletcnn.png"/>
    <p class="darkcaption">
    A conceptual diagram of an embedding network. The main AlexNet network takes an anchor input and produces class probability scores. For Siamese setting, the second network in the middle takes a second input of the same object instance but with either similar or dissimilar pose. For triplet setting, the second and the third network takes one similar pose and one dissimilar pose. Both auxiliary networks output an embedding vector representing a point in pose embedding space.
    </p>
</div>

---

### Experimental Results

#### Multi-Layer Injections

<script src="https://cdn.plot.ly/plotly-latest.min.js"></script>
<div><div id="aa9bd88a-0542-4ae8-93c2-6119aeb9ace1" style="height: 380px; width: 600px;" class="plotly-graph-div"></div><script type="text/javascript">window.PLOTLYENV=window.PLOTLYENV || {};window.PLOTLYENV.BASE_URL="https://plot.ly";
if (document.getElementById("aa9bd88a-0542-4ae8-93c2-6119aeb9ace1")) {
    Plotly.newPlot("aa9bd88a-0542-4ae8-93c2-6119aeb9ace1", [{"name": "I<sub>0</sub>", "whiskerwidth": 0.4, "fillcolor": "rgba(253, 231, 37, 0.7)", "uid": "efb8a6bb-1ebc-47b2-bf85-a21a1b1df2c2", "y": [82.60035333642261, 81.93422729379056, 81.72570088044485, 80.6258688600556, 81.71158190454125], "hoveron": "points", "boxpoints": "all", "type": "box", "line": {"color": "black", "width": 1}, "marker": {"color": "#fde725", "line": {"color": "gray", "width": 1}, "size": 5}, "hoverinfo": "y", "jitter": 0}, {"name": "I<sub>[1]</sub>", "whiskerwidth": 0.4, "fillcolor": "rgba(191, 223, 37, 0.7)", "uid": "522d9fb8-73d6-4c11-b142-f24ec7d0b904", "y": [81.70108317886933, 77.77818002780353, 82.1825764596849, 81.87702734012974, 81.48024791473587], "hoveron": "points", "boxpoints": "all", "type": "box", "line": {"color": "black", "width": 1}, "marker": {"color": "#bfdf25", "line": {"color": "gray", "width": 1}, "size": 5}, "hoverinfo": "y", "jitter": 0}, {"name": "I<sub>[12]</sub>", "whiskerwidth": 0.4, "fillcolor": "rgba(123, 210, 81, 0.7)", "uid": "09170b2d-703b-45f1-a89b-a4af9a0ea6e6", "y": [81.94870829471733, 82.96780873493977, 82.79838102409639, 83.51374246987952, 83.29869960611677], "hoveron": "points", "boxpoints": "all", "type": "box", "line": {"color": "black", "width": 1}, "marker": {"color": "#7bd251", "line": {"color": "gray", "width": 1}, "size": 5}, "hoverinfo": "y", "jitter": 0}, {"name": "I<sub>[123]</sub>", "whiskerwidth": 0.4, "fillcolor": "rgba(69, 191, 112, 0.7)", "uid": "6f30edb7-e030-489e-8462-f8e3dcf31a3b", "y": [83.31209453197404, 85.51936109823912, 83.82906626506023, 84.33771142261352, 84.07741543095459], "hoveron": "points", "boxpoints": "all", "type": "box", "line": {"color": "black", "width": 1}, "marker": {"color": "#45bf70", "line": {"color": "gray", "width": 1}, "size": 5}, "hoverinfo": "y", "jitter": 0}, {"name": "I<sub>[1234]</sub>", "whiskerwidth": 0.4, "fillcolor": "rgba(35, 168, 132, 0.7)", "uid": "0a2ecd59-fab9-4d06-8ba3-92724a265c23", "y": [83.20565917516218, 84.04193697868396, 84.51836190917517, 84.29173424467099, 85.21960437905469], "hoveron": "points", "boxpoints": "all", "type": "box", "line": {"color": "black", "width": 1}, "marker": {"color": "#23a884", "line": {"color": "gray", "width": 1}, "size": 5}, "hoverinfo": "y", "jitter": 0}, {"name": "I<sub>[12345]</sub>", "whiskerwidth": 0.4, "fillcolor": "rgba(33, 144, 141, 0.7)", "uid": "afafea56-bc57-42d1-a207-af8e9d8d7a88", "y": [85.19136642724744, 84.34350382298425, 83.58578544949027, 83.99776992585728, 86.163765639481], "hoveron": "points", "boxpoints": "all", "type": "box", "line": {"color": "black", "width": 1}, "marker": {"color": "#21908d", "line": {"color": "gray", "width": 1}, "size": 5}, "hoverinfo": "y", "jitter": 0}, {"name": "I<sub>[2345]</sub>", "whiskerwidth": 0.4, "fillcolor": "rgba(42, 120, 142, 0.7)", "uid": "a9c87354-686f-421e-b67c-cfc4d6a69e1b", "y": [84.13389133456904, 85.27608028266914, 84.8347717794254, 84.21570898980536, 84.089000231696], "hoveron": "points", "boxpoints": "all", "type": "box", "line": {"color": "black", "width": 1}, "marker": {"color": "#2a788e", "line": {"color": "gray", "width": 1}, "size": 5}, "hoverinfo": "y", "jitter": 0}, {"name": "I<sub>[345]</sub>", "whiskerwidth": 0.4, "fillcolor": "rgba(53, 94, 141, 0.7)", "uid": "f407e9f6-c067-4388-9883-8f05e69fed3a", "y": [83.66434487951807, 84.5035188832252, 83.3399704587581, 84.74897184893419, 83.6904106811863], "hoveron": "points", "boxpoints": "all", "type": "box", "line": {"color": "black", "width": 1}, "marker": {"color": "#355e8d", "line": {"color": "gray", "width": 1}, "size": 5}, "hoverinfo": "y", "jitter": 0}, {"name": "I<sub>[45]</sub>", "whiskerwidth": 0.4, "fillcolor": "rgba(65, 67, 135, 0.7)", "uid": "f5762d34-e5e1-4737-b097-7f5c880a4433", "y": [84.6132124652456, 84.20991658943467, 84.1009470574606, 83.44893999073216, 84.68597949490268], "hoveron": "points", "boxpoints": "all", "type": "box", "line": {"color": "black", "width": 1}, "marker": {"color": "#414387", "line": {"color": "gray", "width": 1}, "size": 5}, "hoverinfo": "y", "jitter": 0}, {"name": "I<sub>[5]</sub>", "whiskerwidth": 0.4, "fillcolor": "rgba(72, 35, 116, 0.7)", "uid": "624f41a5-6b17-43cd-96b6-c92ac0cef5f5", "y": [84.30549119555144, 85.5957483781279, 85.63774328081557, 85.03569566728453, 83.62886642724744], "hoveron": "points", "boxpoints": "all", "type": "box", "line": {"color": "black", "width": 1}, "marker": {"color": "#482374", "line": {"color": "gray", "width": 1}, "size": 5}, "hoverinfo": "y", "jitter": 0}, {"name": "Ensemble", "marker": {"color": [0, 1, 2, 3, 4, 5, 6, 7, 8, 9], "symbol": "pentagon", "line": {"color": "black", "width": 1}, "size": 14, "colorscale": [[0.0, "#fde725"], [0.1, "#bfdf25"], [0.2, "#7bd251"], [0.30000000000000004, "#45bf70"], [0.4, "#23a884"], [0.5, "#21908d"], [0.6000000000000001, "#2a788e"], [0.7000000000000001, "#355e8d"], [0.8, "#414387"], [0.9, "#482374"], [1.0, "#440154"]]}, "type": "scatter", "line": {"color": "lightgrey", "width": 2}, "uid": "9600ed2d-a648-4cbb-adcf-6080340a53ef", "x": ["I<sub>0</sub>", "I<sub>[1]</sub>", "I<sub>[12]</sub>", "I<sub>[123]</sub>", "I<sub>[1234]</sub>", "I<sub>[12345]</sub>", "I<sub>[2345]</sub>", "I<sub>[345]</sub>", "I<sub>[45]</sub>", "I<sub>[5]</sub>"], "hoverinfo": "y", "y": [84.40903035217794, 84.68923772011121, 85.97225440222428, 87.39971906858202, 87.02067886932345, 87.66834163577386, 87.23463565801669, 87.29690396200185, 87.23282553290083, 88.10313368860055]}], {"autosize": false, "margin": {"t": 20, "pad": 4, "l": 50, "r": 50, "b": 50}, "legend": {"font": {"color": "black", "family": "Old Standard TT, serif", "size": 14}}, "width": 600, "yaxis": {"title": {"text": "Test Accuracy", "font": {"color": "grey", "family": "Arial, sans-serif", "size": 14}}, "ticks": "outside", "tick0": 80, "range": [80, 89], "tickfont": {"color": "black", "family": "Old Standard TT, serif", "size": 14}, "hoverformat": ".2f", "showticklabels": true, "dtick": 1, "nticks": 7, "automargin": true, "linecolor": "black", "mirror": "ticks", "showline": true}, "height": 380, "xaxis": {"linecolor": "black", "ticks": "outside", "showline": true, "mirror": true, "tickfont": {"color": "black", "family": "Old Standard TT, serif", "size": 14}, "showticklabels": true}}, {"showLink": false, "plotlyServerURL": "https://plot.ly", "linkText": "Export to plot.ly"}); 
}
</script></div>

#### Loss Weight Assignment

<script src="https://cdn.plot.ly/plotly-latest.min.js"></script><div>
    <div id="6d59faba-8537-4830-853f-d56d131e0272" style="height: 300px; width: 450px;" class="plotly-graph-div"></div><script type="text/javascript">window.PLOTLYENV=window.PLOTLYENV || {};window.PLOTLYENV.BASE_URL="https://plot.ly";
if (document.getElementById("6d59faba-8537-4830-853f-d56d131e0272")) {
    Plotly.newPlot("6d59faba-8537-4830-853f-d56d131e0272", [{"name": "Ensemble", "marker": {"color": "red", "symbol": "pentagon", "line": {"color": "black", "width": 1}, "size": 12}, "type": "scatter", "line": {"color": "lightgrey", "dash": "dash", "width": 3}, "uid": "02e1983e-f491-41ba-a030-6a8de07b5262", "x": [0, 0.1, 0.2, 0.3, 0.4, 0.5, 0.6, 0.7, 0.8, 0.9], "mode": "lines+markers", "hoverinfo": "y", "y": [84.49, 86.71, 87.15, 87.19, 87.87, 88.52, 89.35, 89.86, 91.06, 91.15]}, {"type": "scatter", "line": {"color": "orange"}, "uid": "159407eb-abea-4201-aa70-241318bf43db", "x": [0, 0.1, 0.2, 0.3, 0.4, 0.5, 0.6, 0.7, 0.8, 0.9], "y": [81.91, 84.75, 84.98, 84.92999999999999, 85.57, 86.05, 87.24, 87.22, 88.36999999999999, 87.89], "showlegend": false, "mode": "lines"}, {"type": "scatter", "x": [0, 0.1, 0.2, 0.3, 0.4, 0.5, 0.6, 0.7, 0.8, 0.9], "fillcolor": "orange", "uid": "f15d953b-bf13-4e52-aa3c-50f157a2329b", "line": {"color": "orange"}, "fill": "tonexty", "y": [81.15, 84.15, 84.52, 84.11, 85.03, 85.55, 86.3, 87.06, 87.95, 87.19000000000001], "showlegend": false, "mode": "lines"}, {"name": "Average", "marker": {"color": "black", "line": {"color": "black", "width": 1}, "size": 8}, "type": "scatter", "line": {"color": "brown", "dash": "dot", "width": 3}, "uid": "1432fb89-2331-4425-9866-d1f8ca9afff4", "x": [0, 0.1, 0.2, 0.3, 0.4, 0.5, 0.6, 0.7, 0.8, 0.9], "mode": "lines+markers", "hoverinfo": "y", "y": [81.53, 84.45, 84.75, 84.52, 85.3, 85.8, 86.77, 87.14, 88.16, 87.54]}], {"autosize": false, "margin": {"t": 20, "pad": 2, "l": 50, "r": 50, "b": 40}, "legend": {"x": 0.6, "y": 0.05, "font": {"color": "black", "family": "Arial, sans-serif", "size": 14}}, "width": 450, "yaxis": {"title": {"text": "Test Accuracy", "font": {"color": "grey", "family": "Arial, sans-serif", "size": 14}}, "zeroline": false, "linecolor": "black", "ticks": "outside", "automargin": true, "mirror": true, "showline": true, "tickfont": {"color": "black", "family": "Old Standard TT, serif", "size": 14}, "showticklabels": true}, "height": 300, "xaxis": {"title": {"text": "Auxiliary (pose) weight ratio", "font": {"color": "black", "family": "Old Standard TT, serif", "size": 14}}, "zeroline": false, "dtick": 0.1, "ticks": "outside", "automargin": true, "linecolor": "black", "mirror": true, "showline": true, "tickfont": {"color": "black", "family": "Old Standard TT, serif", "size": 14}, "showticklabels": true}}, {"showLink": false, "plotlyServerURL": "https://plot.ly", "linkText": "Export to plot.ly"}); 
}
</script></div>


#### Extension to ResNet and DenseNet

<script src="https://cdn.plot.ly/plotly-latest.min.js"></script>
<div><div id="8ba3be2e-b8e1-47e5-8fe6-a0413f5fe02d" style="height: 300px; width: 600px;" class="plotly-graph-div"></div><script type="text/javascript">window.PLOTLYENV=window.PLOTLYENV || {};window.PLOTLYENV.BASE_URL="https://plot.ly";
if (document.getElementById("8ba3be2e-b8e1-47e5-8fe6-a0413f5fe02d")) {
    Plotly.newPlot("8ba3be2e-b8e1-47e5-8fe6-a0413f5fe02d", [{"name": "ResNet", "whiskerwidth": 0.4, "fillcolor": "rgba(191, 223, 37, 0.7)", "uid": "699c6b2c-4186-4d86-851e-688a013c3181", "y": [84.2, 82.05, 84.56, 83.39, 85.04], "hoveron": "points", "boxpoints": "all", "type": "box", "line": {"color": "#21908d", "width": 1}, "marker": {"color": "#bfdf25", "size": 5}, "hoverinfo": "y", "jitter": 0}, {"name": "ResNet+Pose", "whiskerwidth": 0.4, "fillcolor": "rgba(69, 191, 112, 0.7)", "uid": "31a6755d-67d4-4ba8-b39d-1e144f290a5b", "y": [86.56, 86.36, 87.24, 86.04, 86.71], "hoveron": "points", "boxpoints": "all", "type": "box", "line": {"color": "#355e8d", "width": 1}, "marker": {"color": "#45bf70", "size": 5}, "hoverinfo": "y", "jitter": 0}, {"name": "DenseNet", "whiskerwidth": 0.4, "fillcolor": "rgba(42, 120, 142, 0.7)", "uid": "a0b7a142-314c-4d8b-a307-9e5ba5624c1b", "y": [84.27, 83.74, 83.86, 82.02, 84.06], "hoveron": "points", "boxpoints": "all", "type": "box", "line": {"color": "#355e8d", "width": 1}, "marker": {"color": "#2a788e", "size": 5}, "hoverinfo": "y", "jitter": 0}, {"name": "DenseNet+Pose", "whiskerwidth": 0.4, "fillcolor": "rgba(65, 67, 135, 0.7)", "uid": "32ae1bcf-953e-4349-8cce-a499ddbf1193", "y": [86.98, 87.2, 87.29, 89.03, 87.9], "hoveron": "points", "boxpoints": "all", "type": "box", "line": {"color": "#482374", "width": 1}, "marker": {"color": "#414387", "size": 5}, "hoverinfo": "y", "jitter": 0}, {"name": "emsemble", "marker": {"color": ["#bfdf25", "#45bf70", "#2a788e", "#414387"], "symbol": "pentagon", "line": {"color": ["#21908d", "#355e8d", "#355e8d", "#482374"], "width": 1}, "size": 12}, "type": "scatter", "x": ["ResNet", "ResNet+Pose", "DenseNet", "DenseNet+Pose"], "uid": "493d5596-5725-47c3-a51e-dc7a6568dce5", "mode": "markers", "hoverinfo": "y", "y": [86.04, 88.68, 84.89, 89.97]}], {"autosize": false, "margin": {"t": 20, "pad": 4, "l": 50, "r": 50, "b": 40}, "legend": {"font": {"color": "black", "family": "Old Standard TT, serif", "size": 14}}, "width": 600, "yaxis": {"title": {"text": "Test Accuracy", "font": {"color": "grey", "family": "Old Standard TT, serif", "size": 14}}, "showline": true, "linecolor": "lightgrey", "mirror": "ticks", "tickfont": {"color": "black", "family": "Old Standard TT, serif", "size": 14}, "hoverformat": ".2f", "showticklabels": true}, "height": 300, "xaxis": {"linecolor": "lightgrey", "ticks": "outside", "showline": true, "mirror": true, "tickfont": {"color": "black", "family": "Old Standard TT, serif", "size": 12}, "showticklabels": true}}, {"showLink": false, "plotlyServerURL": "https://plot.ly", "linkText": "Export to plot.ly"}); 
}
</script></div>

#### Extension to Lighting Variation

<script src="https://cdn.plot.ly/plotly-latest.min.js"></script><div>
    <div id="d2467e7e-e88c-49c4-b52c-aeb7aa1b4f73" style="height: 300px; width: 600px;" class="plotly-graph-div"></div><script type="text/javascript">window.PLOTLYENV=window.PLOTLYENV || {};window.PLOTLYENV.BASE_URL="https://plot.ly";
if (document.getElementById("d2467e7e-e88c-49c4-b52c-aeb7aa1b4f73")) {
    Plotly.newPlot("d2467e7e-e88c-49c4-b52c-aeb7aa1b4f73", [{"name": "I<sub>[0]</sub>", "whiskerwidth": 0.4, "fillcolor": "rgba(252, 207, 37, 0.7)", "uid": "dab3ec88-22e9-49c9-a7b8-a8b0766ed6ba", "y": [78.25, 79.91, 79.62, 77.88, 79.16], "hoveron": "points", "boxpoints": "all", "type": "box", "line": {"color": "#cb4679", "width": 1}, "marker": {"color": "#fccf25", "size": 5}, "hoverinfo": "y", "jitter": 0}, {"name": "I<sub>[5]</sub>+Light", "whiskerwidth": 0.4, "fillcolor": "rgba(242, 133, 75, 0.7)", "uid": "ef7adcab-0851-4cd6-bbee-a1cb0194f635", "y": [82.56, 82.11, 82.93, 81.33, 82.5], "hoveron": "points", "boxpoints": "all", "type": "box", "line": {"color": "#8f0da4", "width": 1}, "marker": {"color": "#f2854b", "size": 5}, "hoverinfo": "y", "jitter": 0}, {"name": "I<sub>[5]</sub>+Pose", "whiskerwidth": 0.4, "fillcolor": "rgba(176, 42, 144, 0.7)", "uid": "af1b2171-ba69-41ca-ac6e-56ce944706ba", "y": [85.25, 84.72, 85.6, 84.69, 85.17], "hoveron": "points", "boxpoints": "all", "type": "box", "line": {"color": "#8f0da4", "width": 1}, "marker": {"color": "#b02a90", "size": 5}, "hoverinfo": "y", "jitter": 0}, {"name": "I<sub>[5]</sub>+Pose+Light", "whiskerwidth": 0.4, "fillcolor": "rgba(106, 0, 168, 0.7)", "uid": "4d9dcf31-c48c-4826-bfcd-f80492e3a732", "y": [85.35, 85.44, 85.92, 86.22, 85.54], "hoveron": "points", "boxpoints": "all", "type": "box", "line": {"color": "#40049d", "width": 1}, "marker": {"color": "#6a00a8", "size": 5}, "hoverinfo": "y", "jitter": 0}, {"name": "emsemble", "marker": {"color": ["#fccf25", "#f2854b", "#b02a90", "#6a00a8"], "symbol": "pentagon", "line": {"color": ["#cb4679", "#8f0da4", "#8f0da4", "#40049d"], "width": 1}, "size": 12}, "type": "scatter", "x": ["I<sub>[0]</sub>", "I<sub>[5]</sub>+Light", "I<sub>[5]</sub>+Pose", "I<sub>[5]</sub>+Pose+Light"], "uid": "5c190366-3471-41fd-aa4d-b0fcc1904c5c", "mode": "markers", "hoverinfo": "y", "y": [80.54, 83.9, 86.75, 87.33]}], {"autosize": false, "margin": {"t": 20, "pad": 4, "l": 50, "r": 50, "b": 40}, "legend": {"font": {"color": "black", "family": "Old Standard TT, serif", "size": 14}}, "width": 600, "yaxis": {"title": {"text": "Test Accuracy", "font": {"color": "grey", "family": "Old Standard TT, serif", "size": 14}}, "showline": true, "linecolor": "lightgrey", "mirror": "ticks", "tickfont": {"color": "black", "family": "Old Standard TT, serif", "size": 14}, "hoverformat": ".2f", "showticklabels": true}, "height": 300, "xaxis": {"linecolor": "lightgrey", "ticks": "outside", "showline": true, "mirror": true, "tickfont": {"color": "black", "family": "Old Standard TT, serif", "size": 14}, "showticklabels": true}}, {"showLink": false, "plotlyServerURL": "https://plot.ly", "linkText": "Export to plot.ly"}); 
}
</script></div>



#### Variation Embedding Learning

<script src="https://cdn.plot.ly/plotly-latest.min.js"></script>
<div><div id="d8e71513-388d-42cb-894e-b50eb11bfc30" style="height: 300px; width: 600px;" class="plotly-graph-div"></div><script type="text/javascript">window.PLOTLYENV=window.PLOTLYENV || {};window.PLOTLYENV.BASE_URL="https://plot.ly";
if (document.getElementById("d8e71513-388d-42cb-894e-b50eb11bfc30")) {
    Plotly.newPlot("d8e71513-388d-42cb-894e-b50eb11bfc30", [{"name": "I<sub>[0]</sub>", "whiskerwidth": 0.4, "fillcolor": "rgba(252, 207, 37, 0.7)", "uid": "aa6c448f-2307-49ac-8f8b-173283947ffa", "y": [79.42, 81.84, 79.35, 80.49, 80.97], "hoveron": "points", "boxpoints": "all", "type": "box", "line": {"color": "#fca736", "width": 1}, "marker": {"color": "#fccf25", "size": 5}, "hoverinfo": "y", "jitter": 0}, {"name": "I<sub>[5]</sub>+Siamese", "whiskerwidth": 0.4, "fillcolor": "rgba(35, 168, 132, 0.7)", "uid": "13abb75b-ba13-4b43-852c-4a94a87b96c9", "y": [82.32, 81.99, 82.48, 81.81, 81.47], "hoveron": "points", "boxpoints": "all", "type": "box", "line": {"color": "#355e8d", "width": 1}, "marker": {"color": "#23a884", "size": 5}, "hoverinfo": "y", "jitter": 0}, {"name": "I<sub>[5]</sub>+Triplet", "whiskerwidth": 0.4, "fillcolor": "rgba(53, 94, 141, 0.7)", "uid": "1848db03-c6a8-45c7-973e-487557b896c3", "y": [82.03, 82.25, 82.75, 81.67, 82.36], "hoveron": "points", "boxpoints": "all", "type": "box", "line": {"color": "#482374", "width": 1}, "marker": {"color": "#355e8d", "size": 5}, "hoverinfo": "y", "jitter": 0}, {"name": "emsemble", "marker": {"color": ["#fccf25", "#23a884", "#355e8d"], "symbol": "pentagon", "line": {"color": ["#fca736", "#355e8d", "#482374"], "width": 1}, "size": 12}, "type": "scatter", "x": ["I<sub>[0]</sub>", "I<sub>[5]</sub>+Siamese", "I<sub>[5]</sub>+Triplet"], "uid": "21f95915-edc8-4db1-9fe4-8d4ee1f29811", "mode": "markers", "hoverinfo": "y", "y": [82.53, 83.43, 83.61]}], {"autosize": false, "margin": {"t": 20, "pad": 4, "l": 50, "r": 50, "b": 40}, "legend": {"font": {"color": "black", "family": "Old Standard TT, serif", "size": 14}}, "width": 600, "yaxis": {"title": {"text": "Test Accuracy", "font": {"color": "grey", "family": "Old Standard TT, serif", "size": 14}}, "showline": true, "linecolor": "lightgrey", "range": [79, 84], "mirror": "ticks", "tickfont": {"color": "black", "family": "Old Standard TT, serif", "size": 14}, "hoverformat": ".2f", "showticklabels": true}, "height": 300, "xaxis": {"linecolor": "lightgrey", "ticks": "outside", "showline": true, "mirror": true, "tickfont": {"color": "black", "family": "Old Standard TT, serif", "size": 14}, "showticklabels": true}}, {"showLink": false, "plotlyServerURL": "https://plot.ly", "linkText": "Export to plot.ly"}); 
}
</script></div>



