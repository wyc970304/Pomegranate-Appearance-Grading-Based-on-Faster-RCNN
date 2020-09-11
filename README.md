# Pomegranate-Appearance-Grading-Based-on-Faster-RCNN

**Note: due to exceeding the usage limit of GitHub LFS, the latest version of supporting materials cannot be updated in this repository in time. Please download the materials from Google drive at this link:**

**Sorry for the inconvenience.**








**Readme** for this project:

There are 2 main folders (or compressed files for backup) for this project. They are:

1. mmdetection-master
This is the work folder of the 'Pomegranate Appearance Quality Recognition System' in this project based on MMDetection. It has main parts includes:

(a) GUI.py----The executable file (i.e. system GUI) of this system. To run this file normally, the environment which supports MMDetection-master must be configured. Before running, check if the paths of work configuration files in run() is correct for your PC. 

(b) data/fruits/images----The Pomegranate image dataset for training & testing. 
In path data/fruits, the folder test1_label & train1_label includes the .xml annotations for the dataset. The file train.json & test.json are the coco format annotations converted by xml2coco.py. For mmdetection, we actually use the coco format annotations.

(c) work_dirs/faster_rcnn_r50_fpn_1x_coco/epoch_12.pth----The model embedded in system (i.e. faster rcnn+ResNet50+FPN) in our project. 

(d) configs/faster_rcnn/faster_rcnn_r50_fpn_1x_coco.py----The configuration file for system model training & detection. If the system cannot work normally, check in this file about the configuration paths of each work files in your PC.

Noticed that: For all codes in 'mmdetection-master' should be run in the correct environment which supports mmdetection-master. The guideline of configure the environment can be seen in: 
https://github.com/open-mmlab/mmdetection 
(Noticed that it must be the environment of 'master' branch/version of mmdetection.)




2. compare
This is the work folder of codes for training & performance testing of two comparison models (i.e. faster rcnn+ResNet50 & faster rcnn+VGG16) in this project developed based on lab source codes. It has main parts includes:

(a) folder 'logs_vgg' & 'logs_resnet'----The output path of saving trained comparison models.
There are 2 completed comparison models in these 2 folders separately already, which are:
VGG16: Epoch85-Total_Loss0.3951-Val_Loss0.3538.pth
ResNet50: Epoch85-Total_Loss0.1797-Val_Loss0.1788.pth

(b) folder 'accuracy'----Includes main codes for testing model performance, performance outputs also generates in 'output' in this path.

(c) folder 'RESULTS_examples'----Includes 2 examples of testing performance output of comparison model which we trained in the project.


To build (i.e. train) and test a comparison model, try to follow this general folow:
(Enrironment: torch >= 1.2.0)

Training the model:
1. Set path of Pomegranate image dataset in data_config.py
(*We have use data/fruits/images folder in 'mmdetection-master' as the path of Pomegranate image dataset.)
2. Set corresponding classes in data_process/data_annotation.py----using .xml annotations to generate .txt annotations
(*We have use data/fruits/test1_label & data/fruits/train1_label folders in 'mmdetection-master' as the path of .xml annotations.)
3. Set the classes you use in model_data/voc_classes.txt (i.e. G1,G2,G3)
4. Sey NUM_CLASSES in train.py to the number of positive classes (i.e. 3 grades)
5. Set 'Configuration of training' in train.py
6. Run train.py to start training a VGG/ResNet50 model

Testing the performance of a choosed model：
1. Set configuration of the test (e.g. model path, category of model, confidence...) in frcnn.py
2. Run accuracy/get_ground_true.py----get the ground truth
3. Run accuracy/predict_all_for_calculate.py---get the detection result
4. Run accuracy/main.py----get PR curve, AP & mAP and other performance outputs, saves in 'accuracy/output' folder.
