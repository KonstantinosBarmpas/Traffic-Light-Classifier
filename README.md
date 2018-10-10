# **Traffic Light Classifier**

## Traffic Light Classifier - My part for Udacity's "Self-Driving Car Engineer Nanodegree" Capstone project.

---

[sim_result1]: ./imgs/sim_result1.png
[sim_result2]: ./imgs/sim_result2.png
[sim_result3]: ./imgs/sim_result3.png
[sim_result4]: ./imgs/sim_result4.png
[sim_result5]: ./imgs/sim_result5.png
[sim_result6]: ./imgs/sim_result6.png
[sim_result7]: ./imgs/sim_result7.png
[sim_result8]: ./imgs/sim_result8.png
[sim_result9]: ./imgs/sim_result9.png
[sim_result10]: ./imgs/sim_result10.png
[sim_result11]: ./imgs/sim_result11.png
[sim_result12]: ./imgs/sim_result12.png

[sim_result_ext1]: ./imgs/sim_result_ext1.png
[sim_result_ext2]: ./imgs/sim_result_ext2.png
[sim_result_ext3]: ./imgs/sim_result_ext3.png
[sim_result_ext4]: ./imgs/sim_result_ext4.png
[sim_result_ext5]: ./imgs/sim_result_ext5.png
[sim_result_ext6]: ./imgs/sim_result_ext6.png
[sim_result_ext7]: ./imgs/sim_result_ext7.png


[carla_result1]: ./imgs/carla_result1.png
[carla_result2]: ./imgs/carla_result2.png
[carla_result3]: ./imgs/carla_result3.png
[carla_result4]: ./imgs/carla_result4.png
[carla_result5]: ./imgs/carla_result5.png

[carla_result_ext1]: ./imgs/carla_result_ext1.png
[carla_result_ext2]: ./imgs/carla_result_ext2.png
[carla_result_ext3]: ./imgs/carla_result_ext3.png
[carla_result_ext4]: ./imgs/carla_result_ext4.png

**Introduction**

During Udacity's "Self-Driving Car Engineer Nanodegree" Capstone project, my part of the project was to design the two Traffic Light Classifier models for the two modes (simulator and site).

**Files**

This repo contains instructions of how I trained the models, my results, comments on the results, tips and of course the model .pb files.

**Training Process -- Instructions**

Choice of the pre-trained model and the model's technique:

For our models, I used the Tensorflow object detection API as described in the tutorial below:

https://pythonprogramming.net/introduction-use-tensorflow-object-detection-api-tutorial/

After seaching on the web, I've decided that a good compromise of accuracy and execution time is the SSD_mobilnet and for that reason I chose the ssd_mobilenet_v1_coco_2017_11_17 pre-trained model.

To get started clone the Tensorflow API repo:

https://github.com/tensorflow/models/tree/master/research/object_detection

--------------Datasets------------------:

To train the model, I used the train dataset and to test it the test dataset. More accurately, I used the TFRecord files on each data set as described in the tutorial.

-----------------Training---------------:

Set up:

1) Go to models - > research -> object_detection
2) In the data folder put the train.record and test.record files you want to use
3) In the training folder configure the pipeline (basically the number of steps and learning rate)
3) Go to models - > research -> object_detection ->legacy
4) In the data folder put the train.record and test.record files you want to use
5) In the training folder configure the pipeline (basically the number of steps and learning rate)

Train:

1) Open terminal
2) Navigate to models -> research (cd models -> cd research)
3) Execute the following:
```
protoc object_detection/protos/*.proto --python_out=.
export PYTHONPATH=$PYTHONPATH:`pwd`:`pwd`/slim
```
4) Go to object_detection folder (cd object_detection) and the to legacy (cd legacy)
5) Execute the folllowing:

```
python3 train.py --logtostderr --train_dir=training/ --pipeline_config_path=training/pipeline.config
```

After the model is trained:

1) Move the three last saved files from the training folder in legacy to the training file in training folder in object_detection.
2) Open terminal
3) Navigate to models - > research -> object_detection
4) Execute to save the graph:

```
        python3 export_inference_graph.py \
            --input_type image_tensor \
            --pipeline_config_path training/pipeline.config \
            --trained_checkpoint_prefix training/YOUR-LAST-SAVE-MODEL(eg model.ckpt-20000)\
            --output_directory A-NEW-NAME-DIRECTORY
            
```
            
--------------Test the model------------------:

1) Open the Jupyter notebook in the object_detection folder
2) Change the models name
3) Run all cells

--------------Important notes------------------------:

1) I trained the simulation model for 40000 steps tried to make it work for both simulator but I did not succeed that. The reason seems to be the training data are completely different since we have on the one hand real data and on the other hand digitally created data. Generally, the model serve their purpose really well and trying to generalize them is beyond the scope of this project although completely possible.

The final results are both trained for 20000 steps. 10000 steps were enough for both models but I did an extra 10000 steps for better results.

Simulation model is stored in sim_v4
Carla model is stored in carla_v4

(Please use the correct name if you want to run them in your program)

2) The Udacity's Carla car runs only Tensorflow v3. It is important to export the frozen graph in Tensorflow v4 in order to the .pb files to be compatible with the Carla's version. To do that use the tensorflow API for v4 by navigating to the file models and execute:
```
git checkout f7e99c0

```

3) The models were trained in Amazon AWS g3.4 large instance.
Visit:

https://aws.amazon.com

You may find it useful to use FileZilla to transfer your data in the instance.
Visit:

https://filezilla-project.org


**Results for the two modes**

Successful results of sim_v4:

![sim_result1]

![sim_result2]

![sim_result3]

![sim_result4]

![sim_result5]

![sim_result6]

![sim_result7]

![sim_result8]

![sim_result9]

![sim_result10]

![sim_result11]

![sim_result12]

Successful results of carla_v4:

![carla_result1]

![carla_result2]

![carla_result3]

![carla_result4]

![carla_result5]

**Results for other images**

I tested the two models in images unrelated to the two models. The two models although they had trained with no general data could recognize large amount of them with the sim_v4 model to be better.

Here are some successful results of sim_v4:

![sim_result_ext1]

![sim_result_ext2]

![sim_result_ext3]

![sim_result_ext4]

![sim_result_ext5]

![sim_result_ext6]

![sim_result_ext7]

Here are some successful results of carla_v4:

![carla_result_ext1]

![carla_result_ext2]

![carla_result_ext3]

![carla_result_ext4]

---


