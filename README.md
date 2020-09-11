# Pomegranate-Appearance-Grading-Based-on-Faster-RCNN
<br />
**Note: due to exceeding the usage limit of GitHub LFS, the latest version of supporting materials cannot be updated in this repository in time. Please download the materials from Google drive at this link:**
**https://drive.google.com/drive/folders/1HOJ0ZmreVresB6f0Y8jmILv3_hvjUurx?usp=sharing**<br />
**Sorry for the inconvenience.**
<br />
<br />
<br />
<br />
<br />
<br />
<br />
<br />
**Readme** for this project: <br />
<br />
There are 2 main folders (or compressed files for backup) for this project. They are: <br />
<br />
**1. mmdetection-master**<br />
This is the work folder of the 'Pomegranate Appearance Quality Recognition System' in this project based on MMDetection. It has main parts includes: <br />
<br />
(a) GUI.py----The executable file (i.e. system GUI) of this system. To run this file normally, the environment which supports MMDetection-master must be configured. Before running, check if the paths of work configuration files in run() is correct for your PC. <br />
<br />
(b) data/fruits/images----The Pomegranate image dataset for training & testing.  <br />
In path data/fruits, the folder test1_label & train1_label includes the .xml annotations for the dataset. The file train.json & test.json are the coco format annotations converted by xml2coco.py. For mmdetection, we actually use the coco format annotations. <br />
<br />
(c) work_dirs/faster_rcnn_r50_fpn_1x_coco/epoch_12.pth----The model embedded in system (i.e. faster rcnn+ResNet50+FPN) in our project.  <br />
<br />
(d) configs/faster_rcnn/faster_rcnn_r50_fpn_1x_coco.py----The configuration file for system model training & detection. If the system cannot work normally, check in this file about the configuration paths of each work files in your PC. <br />
<br />
**Noticed that: For all codes in 'mmdetection-master' should be run in the correct environment which supports mmdetection-master. The guideline of configure the environment can be seen in: <br />
https://github.com/open-mmlab/mmdetection <br />
(Noticed that it must be the environment of 'master' branch/version of mmdetection.)**<br />
<br />
<br />
<br />
<br />
**2. compare**<br />
This is the work folder of codes for training & performance testing of two comparison models (i.e. faster rcnn+ResNet50 & faster rcnn+VGG16) in this project developed based on lab source codes. It has main parts includes:<br />
<br />
(a) folder 'logs_vgg' & 'logs_resnet'----The output path of saving trained comparison models.<br />
There are 2 completed comparison models in these 2 folders separately already, which are:<br />
VGG16: Epoch85-Total_Loss0.3951-Val_Loss0.3538.pth<br />
ResNet50: Epoch85-Total_Loss0.1797-Val_Loss0.1788.pth<br />
<br />
(b) folder 'accuracy'----Includes main codes for testing model performance, performance outputs also generates in 'output' in this path.<br />
<br />
(c) folder 'RESULTS_examples'----Includes 2 examples of testing performance output of comparison model which we trained in the project.<br />
<br />
<br />
To build (i.e. train) and test a comparison model, try to follow this general folow:<br />
(Enrironment: torch >= 1.2.0)<br />
<br />
**Training the model:**<br />
1. Set path of Pomegranate image dataset in data_config.py
*(*We have use data/fruits/images folder in 'mmdetection-master' as the path of Pomegranate image dataset.)*<br />
2. Set corresponding classes in data_process/data_annotation.py----using .xml annotations to generate .txt annotations<br />
*(*We have use data/fruits/test1_label & data/fruits/train1_label folders in 'mmdetection-master' as the path of .xml annotations.)*<br />
3. Set the classes you use in model_data/voc_classes.txt (i.e. G1,G2,G3)<br />
4. Sey NUM_CLASSES in train.py to the number of positive classes (i.e. 3 grades)<br />
5. Set 'Configuration of training' in train.py<br />
6. Run train.py to start training a VGG/ResNet50 model<br />
<br />
**Testing the performance of a choosed model：**<br />
1. Set configuration of the test (e.g. model path, category of model, confidence...) in frcnn.py<br />
2. Run accuracy/get_ground_true.py----get the ground truth<br />
3. Run accuracy/predict_all_for_calculate.py---get the detection result<br />
4. Run accuracy/main.py----get PR curve, AP & mAP and other performance outputs, saves in 'accuracy/output' folder.<br />
