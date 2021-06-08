---
title: Managing pipelines
layout: redirect
weight: 45

aliases:
  - /predictive-analytics/web-app/#managing-pipelines
---

The **Pipelines** page allows you to manage your ONNX pipelines. 

A pipeline represents an end-to-end workflow that encapsulates any pre-processing or post-processing steps that need to be performed in addition to invoking a machine learning model. A pipeline must include a machine learning model, whereas the inclusion of a pre-processing or post-processing step is optional. If an ONNX model requires pre-processing or post-processing steps, the corresponding pre-processing/post-processing resources must be uploaded via the **Resources** page. These pre-processing/post-processing resources are represented using python scripts which must follow the conventions defined below. A pipeline's end-to-end workflow can be depicted using the following sequence:

Input data > Pre-processing > ONNX model > Post-processing > Output data

When a pre-processing step is part of a pipeline, the input data is first processed by the pre-processing script. The pre-processed data is then passed on to the model and finally the outputs from the model are processed by the post-processing script. The output generated by the post-processing script is returned as the final output.

>**Info:** 
<br>1. The pre-processing/post-processing scripts must contain a python function named **process** which takes in just one argument. The processing logic should be contained in this function. Any inputs to these scripts can be accessed using the argument of the **process** function.
<br>2. The **process** function of any pre-processing script must return a *Dictionary* with the keys containing the input field names of the model and its corresponding values containing the pre-processed data. 
<br>3. If there is a post-processing script, the outputs of the ONNX model will be the input to the **process** function of the post-processing script which may or may not return an output depending on the use case.

Pipeline management functionality includes:

* Adding pipelines
* Deleting pipelines
* Viewing pipeline properties

Click **Pipelines** in the navigator, to open the **Pipelines** page. 

![Pipelines](/images/zementis/zementis-pipelines.PNG)


### Adding pipelines

To add a new pipeline, perform the following steps:

1. Click **Add Pipeline** in the **Pipelines** page. 
2. In the **Add Pipeline** wizard, enter the name of the pipeline you want to create followed by choosing your ONNX model.<br>
![Add pipeline](/images/zementis/zementis-add-pipeline.png)
3. Select the pre-processing and post-processing resources if you have any or leave them empty.<br>
Click **Apply** to create the new pipeline.

Once your pipeline is created successfully, you will see a corresponding confirmation message. The new pipeline will be added to the list of pipelines.

### Deleting pipelines

To delete a pipeline, click the delete icon on its card and confirm the deletion.  

Once a pipeline is deleted, it will be removed permanently from your list of pipelines. 

### Viewing pipeline properties

To view the properties of a pipeline, click the info icon <img src="/images/zementis/zementis-info-icon.png" alt="Info" style="display:inline-block; margin:0"> on its card. 

![Pipeline properties](/images/zementis/zementis-pipeline-details.png)
Properties include the name of the pipeline with the name of the ONNX model and pre-processing/post-processing resources which are part of this pipeline.