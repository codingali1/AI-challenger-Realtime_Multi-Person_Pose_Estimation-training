# AI-challenger-Realtime_Multi-Person_Pose_Estimation

# Training

1. Download the original project [Realtime multi-person](https://github.com/ZheC/Realtime_Multi-Person_Pose_Estimation#training) and add the files in my repository and put them in the `training`directory.
2. Run `cd training`; Download the AI-challenger dataset and put the images in dataset/COCO/images/, keypoints annotations in dataset/COCO/annotations/ and COCO official toolbox in dataset/COCO/coco/.
```
dataset/AI_challenge/train/
--------------------/train/keypoint_train_images_20170902/
--------------------/train/keypoint_train_annotations_20170909.json
```
3. Python `ai2coco_art_json.py`to transform the annotation format of the AI-challenger dataset to the  MS COCO annotation format. The final annotation file is `coco_artkeypoint_train_annotations_20170909.json`
4. Run my_getANNO.m in matlab to convert the annotation format from json to mat in dataset/AI_challenge/mat/
5. Run my_genCOCOMask.m in matlab to obatin the mask images for unlabeled person. You can use 'parfor' in matlab to speed up the code.(I use the human bbox as the segmentation annotations)
6. Run python my_genLMDB.py to generate your LMDB.
7. Download our modified caffe: [caffe_train](https://github.com/CMU-Perceptual-Computing-Lab/caffe_train). Compile pycaffe. It will be merged with caffe_rtpose (for testing) soon.
8. Run python setLayers.py --exp 1 to generate the prototxt and shell file for training.
9. Download [VGG-19 model](https://gist.github.com/ksimonyan/3785162f95cd2d5fee77), we use it to initialize the first 10 layers for training.
10. Run bash train_pose.sh 0,1 (generated by setLayers.py) to start the training with two gpus.

# Citation
Please cite the paper in your publications if it helps your research:
```
@inproceedings{cao2017realtime,
  author = {Zhe Cao and Tomas Simon and Shih-En Wei and Yaser Sheikh},
  booktitle = {CVPR},
  title = {Realtime Multi-Person 2D Pose Estimation using Part Affinity Fields},
  year = {2017}
  }
            
@inproceedings{wei2016cpm,
  author = {Shih-En Wei and Varun Ramakrishna and Takeo Kanade and Yaser Sheikh},
  booktitle = {CVPR},
  title = {Convolutional pose machines},
  year = {2016}
  }
```
