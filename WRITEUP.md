# Project Write-Up

## Explaining Custom Layers

The process of adding custom layers depends on the framework used to build these layers.

- For Caffe and Tensorflow, one option is to register custom layers as extension
- For caffe another option could be to calculate the output shape of the layer (requires caffe)
- In Tensorflow you can replace the unsupported subgraph with another subgraph

Potential Reasons for adding the custom layers could include some layer that is essential for the model and is not supported by OpenVINO.
This new layer is efficient in terms of performance.

## Comparing Model Performance

There are two main metrics that are to be seen here.
1. Accuracy
2. Speed

Accuracy can be simply measured by comparing the results with human labelled data.

For speed we can measure the inference time.

After conversion, 

- Accuracy decreases (but is negligible) because of decrease in floating point precision.

- Speed increases because of freezing, fusion and quantization.

- The size of the model also decreases, e.g. in my case the preprocessing block was removed.

|System |Accuracy (mAP)  |Time (ms)  |Size (MB)  |
|---|---|---|---|
|Original   |21   |55   |28   |
|OpenVINO Optimization   |21   |48   |26   |


## Assess Model Use Cases

- **Customer Interest**
We can see how much time customers are spending near a specific category

- **Security**
Let's say a person is near the cashier, this is the time when one can stay alert, rest of the time there's less risk

- **Frequency of People Entering**
Consider a small pathway or something similar, we are interested if it will suffice, i.e. if the person entering increase a lot, we might look for an alternative way.


## Assess Effects on End User Needs

Lighting, model accuracy, and camera focal length/image size have different effects on a
deployed edge model. The potential effects of each of these are as follows, 

- Lighting may be required all the times, e.g. in cloudy situation hunmans can see fine, but the camera quality suffers

- User will need a cctv camera, placed correctly near the region of interest.

- Model needs to be accurate enough, also testing of the required threshold may be needed.

## Model Research

Tried various models, such as SSDv1, SSDv2, FRCNN. SSDv1 was the fastest, also you need to tune the probability threshold value for each model in order to get optimal results.
