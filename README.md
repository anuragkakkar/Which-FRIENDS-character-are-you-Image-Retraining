# Which-FRIENDS-character-are-you-Image-Retraining-

This is an image retrained model based on Tensorflow. The pre-trained model used is Inception model. 
You can have fun with this model by asking the it which FRIENDS character you resemble.
It uses the Inception model to train the images.
Use this [CodeLab](https://codelabs.developers.google.com/codelabs/tensorflow-for-poets/) by Google as a guide. 
Also this [tutorial](https://www.tensorflow.org/hub/tutorials/image_retraining) is quite helpful, it tells you about various terms and things you are going to use in this image classifier. 

## Requirements

* [docker](https://www.docker.com/products/docker-toolbox)
* [tensorflow](https://www.tensorflow.org/install/)
* [python](https://www.python.org/downloads/)

## Usage 

All the commands have to be given in docker.

First we need to choose our working directory. In my case, it is tf_files. Also if you want to use tensorboard, you can publish.
For example, 
```
docker run -it \
  --publish 6006:6006 \
  --volume ${HOME}/tf_files:/tf_files \
  --workdir /tf_files \
  tensorflow/tensorflow:1.1.0 bash
```

You just need to make a "classifier" directory with images inside each individual folder.
For example
```
 [any_path]/friends/chandler bing/image1.jpg
 [any_path]/friends/ross geller/image2.jpg
 [any_path]/friends/monica geller/image3.jpg
 [any_path]/friends/phoebe/image4.jpg
```

## Training process
 
The following code will download and extract the "inception" model (a pre-trained model) inside the inception folder before training.
Just give appropriate file and folder name. You can also give number of training steps and learning rate.
For example,
```
 python retrain.py \
  --bottleneck_dir=bottlenecks \
  --how_many_training_steps=4000 \
  --model_dir=inception \
  --summaries_dir=training_summaries/04_August_2018 \
  --learning_rate=0.005 \
  --output_graph=retrained_graph_for_friends.pb \
  --output_labels=retrained_labels_for_friends.txt \
  --image_dir=friends
``` 

## Guessing process

You just need to put your image in the test folder and use label_image.py to get the result.
For example
```
 python label_image.py /[any_path]/test/Matthew-Perry-Friends-NBC-060115-1276x850.jpg tf_files/retrained_graph_for_friends.pb
```

## Example of result
```
 python label_image.py /tf_files/test/Matthew-Perry-Friends-NBC-060115-1276x850.jpg tf_files/retrained_graph_for_friends.pb
 chandler bing (score = 0.67296)
 ross geller (score = 0.18219)
 joey (score = 0.11796)
 phoebe (score = 0.01084)
 monica geller (score = 0.01076)
 rachael greene (score = 0.00529)
```
P.s. You can use better images to train your model for better results! I was able to find/mass download these images only which are not great but still can be used.

## For more information

* [TensorFlow website](https://www.tensorflow.org)
* [TensorFlow White Papers](https://www.tensorflow.org/about/bib)
* [TensorFlow Model Zoo](https://github.com/tensorflow/models)
* [TensorFlow MOOC on Udacity](https://www.udacity.com/course/deep-learning--ud730)
* [TensorFlow course at Stanford](https://web.stanford.edu/class/cs20si)

Learn more about the TensorFlow community at the [community page of tensorflow.org](https://www.tensorflow.org/community) for a few ways to participate.

