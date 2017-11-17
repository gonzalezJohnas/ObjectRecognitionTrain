## ObjectRecognitionTrain ##

This is a simple wrapper of the [tensorflow tutorial](https://www.tensorflow.org/tutorials/image_retraining) for object recognition reusing pretrained model such as InceptionV3, MobileNet.


### Dependencies ###
This module was tested only on Linux machine and depends on the following :

-	Yarp
-	TensorFlow
-	OpenCV

Optionally a Cuda environment to launch on a GPU and accelerate the process.

### General description ###
As explained in the TensorFlow tutorial, reusing existing architecture for object recognition can be done by retraining the last layer. All the previous architecture remain identical, it can be seen as a generic features extractor. On this "feature code" we can retrain the output layer according to our needs.

So this module provide an Yarp rpc control to create the directory hierarchy in order to match the requirements to retrain the chosen architecture.

You can have a deeper insight on the approach with this [paper](https://arxiv.org/pdf/1310.1531v1.pdf).

### Yarp Input/Output ###
**RPC commands**:

-	Add `<number_of_images>` `<name_label>` => Add **N** images to the dataset with associated label.
-	Train => Launch the training with the specified parameters

**Inputs**:

- /objectRecognitionTrain/imageRGB:i => Yarp image port where images are taken

**Outputs**:

- NONE

## How to use it ##
All the parameters are computed from the objectRecognitionTrain.ini file.

The parameters are the one used in TensorFlow :

**Mandatory**

- **image_dir** => The directory where the dataset will be created
- **output_graph** => Full path and name to save the new graph (ex /tmp/output_graph.pb)
- **model_name** => Name of the architecture to use
- **output_labels** => Full path and name to save the labels associted with the graph (ex /tmp/output_labels.txt)

**Optional**

- **architecture** => Which architecture to reuse (InceptionV3, MobileNet)
- **learning_rate** => The increase in backprogation step for the weights
- **how_ many_ training_steps** => Specify number of training steps to perform
- **random_brightness** => Specify with percentage values that control how much of each of the distortions is applied to each image
- **random_scale** => Specify with percentage values that control how much of each of the distortions is applied to each image
- **random_crop**  => Specify with percentage values that control how much of each of the distortions is applied to each image
- **flip_left_right** => Boolean value to
- **model_dir** => Where to find the model graph (default /tmp/imagenet, it will be automaticly download by the script if not found).

## Model_name possible values : 
To use the mobileNet architecture you have to specify it like this  **mobilenet_<number_weight>_<image_size>** where : 
- number_weight can be in  {0.25|0.50|0.75|1}
- image_size can be in {224|192|168|128}

To use [inceptionV3](https://arxiv.org/abs/1512.00567) just write **inception_v3**


## Log and Debug ##
By default all the summaries of the training rpocess are saved into **/tmp/retrain_logs**. With [tensorboard](https://www.tensorflow.org/get_started/summaries_and_tensorboard) you can visualize the different metrics of the training process.
