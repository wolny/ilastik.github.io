---
layout: documentation
title: FIJI import/export plugin
tagline: Import and Export with a FIJI plugin
category: "Documentation"
group: "basic-documentation"
weight: 1
---

# ilastik Import Export plugin in FIJI
This plugin allows you to save images opened in FIJI directly to the hdf5 format preferred by ilastik. While this conversion is beneficial for any large dataset, we especially recommend it for _multipage tiffs_. After you save the file and process it with ilastik, you can use the same plugin to load the results for further post-processing in FIJI.

## Installation
In FIJI, go to Help->Update... In the dialog that appeares, click the "Manage update sites" button. In the list of update sites, select "ilastik Import Export". You should now see ilastik_HDF5.jar in your updater window.
<div class="row">
<div class="col-md-6">
<a href="snapshots/update_sites.png" data-toggle="lightbox"><img src="snapshots/update_sites.png" width="100%" class="img-responsive" /></a>
</div>
 <div class="col-md-6">
<a href="snapshots/ImageJ_Updater.png" data-toggle="lightbox"><img src="snapshots/ImageJ_Updater.png" width="100%" class="img-responsive" /></a>
</div>
</div>

## From FIJI to ilastik
<div class="row">
 <div class="col-md-6">
<a href="snapshots/fiji_export_cropped.png" data-toggle="lightbox"><img src="snapshots/fiji_export_cropped_scale2.png" width="100%" class="img-responsive" /></a>
</div>
 <div class="col-md-6">
This is how you find the right export option from within FIJI. It will warn you to be careful with the axes order, but don't worry, if you get it wrong you can still correct it on import in ilastik.
</div>
</div>

## ilastik
<p>
<div class="row">
<div class="col-md-6">
<a href="snapshots/ilastik_import_cropped_full.png" data-toggle="lightbox"><img src="snapshots/ilastik_import_cropped_scale2.png" width="100%" class="img-responsive" /></a>
</div>
<div class="col-md-6">
Open the file as usual. If the axis order is wrong, as shown in this figure (tzyxc instead of txyzc), change it in this dialogue.
</div>
</div>
</p>

Train the classifier in ilastik as you usually would (see [Pixel Classification workflow]({{site.baseurl}}/documentation/pixelclassification/pixelclassification.html) docs if you are not sure how to proceed). Once you are happy with the results, switch to the export applet. 

<div class="row">
<div class="col-md-6">
<a href="snapshots/pc_training.png" data-toggle="lightbox"><img src="snapshots/pc_training_scale2.png" width="100%" class="img-responsive" /></a>
</div>
<div class="col-md-6">
<a href="snapshots/pc_export.png" data-toggle="lightbox"><img src="snapshots/pc_export_scale2.png" width="100%" class="img-responsive" /></a>
</div>
</div>
<br>

Depending on your post-processing, export **Probabilities** or **Simple Segmentation**. You can control the export source by the "Source" dropdown menu. For probability maps you can either leave all settings at default, or, if you need to save space, convert the results to unsigned int 8-bit and rescale them from [0.0, 1.0] interval to [0, 255].

## From ilastik to FIJI

<div class="row">
<div class="col-md-6">
<a href="snapshots/fiji_import_cropped_full.png" data-toggle="lightbox"><img src="snapshots/fiji_import_cropped_scale2.png" width="100%" class="img-responsive" /></a>
</div>


<div class="col-md-6">
<p>
Using the same plugin, you can now load your results into FIJI by selecting "ilastik HDF5" in the File->Import menu. Two options are available: load (and display) the raw pixel values or load and display the image with a lookup-table (LUT). 
</p>
<p>
<a href="snapshots/fiji_load_dialogue_only.png" data-toggle="lightbox"><img src="snapshots/fiji_load_dialogue_only.png" width="50%" class="img-responsive" /></a>
</p>
<p>
For <b>Probabilities</b>, choose <b>Load Raw</b>. <br>
For <b>Segmentation</b>, choose <b>Load LUT</b>.<br>
If you loaded the segmentation and the image looks black, you probably loaded it as raw. Try again with a LUT.
</p>
</div>
</div>
If you load Probabilities, you should see something like the left image. For Simple Segmentation with a lookup-table you should see the right image.
<div class="row">
<div class="col-md-6">
<a href="snapshots/fiji_loaded_pmaps_cropped_full.png" data-toggle="lightbox"><img src="snapshots/fiji_loaded_pmaps_cropped_scale2.png" width="100%" class="img-responsive" /></a>
</div>
<div class="col-md-6">
<a href="snapshots/fiji_loaded_ss_cropped_full.png" data-toggle="lightbox"><img src="snapshots/fiji_loaded_ss_cropped_scale2.png" width="100%" class="img-responsive" /></a>
</div>
