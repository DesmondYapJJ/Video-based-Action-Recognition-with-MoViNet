# Video-based-Action-Recognition-with-MoViNet

This is based on the official notebook for [MoViNets (Mobile Video Networks)](https://arxiv.org/pdf/2103.11511.pdf) by [Tensorflow](https://colab.research.google.com/github/tensorflow/models/blob/master/official/projects/movinet/movinet_tutorial.ipynb).

Pretrained models are provided by [TensorFlow Hub](https://tfhub.dev/google/collections/movinet/) and the [TensorFlow Model Garden](https://github.com/tensorflow/models/tree/master/official/projects/movinet), trained on [Kinetics 600](https://deepmind.com/research/open-source/kinetics) for video action classification. All Models use TensorFlow 2 with Keras for inference and training.

The following code notebook is ran on Google Colab.

The following steps will be performed:

1. [Running base model inference with TensorFlow Hub](#scrollTo=6g0tuFvf71S9&line=8&uniqifier=1)
2. [Running streaming model inference with TensorFlow Hub and plotting predictions](#scrollTo=ADrHPmwGcBZ5&line=4&uniqifier=1)
3. [Running a streaming TensorFlow Lite model for mobile](#scrollTo=W3CLHvubvdSI&line=3&uniqifier=1)

![jumping jacks plot](https://storage.googleapis.com/tf_model_garden/vision/movinet/artifacts/jumpingjacks_plot.gif)

<img src='https://drive.google.com/uc?id=1dkncoH5-yGRNdue-PFqVvKYxau9k0WnT'>

## Summary 

### Jumping Jacks
- MoViNet-A2-Base Model 
  - jumping jacks 0.9166438

- MoViNet-A2-Stream Model 
  - jumping jacks 0.9998123

-  MoViNet-A0-Stream TF Lite
  - jumping jacks 0.99030006

### Swimming Butterfly Stroke
- MoViNet-A2-Base Model 
  - swimming butterfly stroke 0.89739895

- MoViNet-A2-Stream Model 
  - swimming butterfly stroke 0.82453096

-  MoViNet-A0-Stream TF Lite
  - swimming butterfly stroke 0.6641578

Base models implement standard 3D convolutions without stream buffers. Base models are not recommended for fast inference on CPU or mobile due to limited support for tf.nn.conv3d. 

Stream model was expected to perform best for both jumping jacks and butterfly stroke action recognition, however this was not true for butterfly stroke. 

TF Lite model A0 has the lowest latency suitable for mobile, however it does have a lower accuracy most evident with butterfly stroke action recognition. Another possibility is that Kinetics 600 has four similar classes for swimming as compared to jumping jacks which are unique: 

- swimming backstroke
- swimming breast stroke
- swimming butterfly stroke
- swimming front crawl 

Top 5 predictions for TF Lite for swimming

- swimming butterfly stroke 0.6641578
- swimming front crawl 0.16218565
- swimming breast stroke 0.029098507
- jumping into pool 0.02509537
- swimming backstroke 0.01980626
