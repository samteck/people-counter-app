# Project Write-Up

Edge computing has a very promising future as more and more data needs to be processed near to its generations and inferencing should be taken as fast as possible.

In terms of computer vision the video feed gathered from the camera takes considerable amount of time and bandwidth to be uploaded to cloud. So its better to do inferencing at the edge itself.

## Conversion from Frozen model to IR

wget http://download.tensorflow.org/models/object_detection/faster_rcnn_inception_v2_coco_2018_01_28.tar.gz

tar -xvf faster_rcnn_inception_v2_coco_2018_01_28.tar.gz

cd faster_rcnn_inception_v2_coco_2018_01_28

python /opt/intel/openvino/deployment_tools/model_optimizer/mo.py --input_model frozen_inference_graph.pb --tensorflow_object_detection_api_pipeline_config pipeline.config --tensorflow_use_custom_operations_config /opt/intel/openvino/deployment_tools/model_optimizer/extensions/front/tf/faster_rcnn_support.json --reverse_input_channels

## Explaining Custom Layers

OpenVINO optimises already present Models in frameworks like TensorFlow, caffe, etc. When we use this models out of the box the speed and memory usage will be pretty high.

So we need to optimise these models to IR which can be fed to Inference Engine.

But during the process of optimization using Model Optimizer, MO searches for any layers which are not present in the list of Known layers, those layers are called custom layers

## Comparing Model Performance

These we less use of memory and FPS inferred also increased after we converted the forzen model to IR.

## Assess Model Use Cases

This can be used extensively in Smart City scenario in which we will be having cameras all over the city (side walks, stations, subways, etc) and we can calculate density of people at these places.

## Assess Effects on End User Needs

The lighting condistions should be good for proper inference, we also need to check how these models perform in Infrared video (night survelliance)
