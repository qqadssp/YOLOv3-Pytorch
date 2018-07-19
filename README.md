# YOLOv3-Pytorch

This is an implementation of YOLOv3 in Pytorch, it is base on the code [marvis](https://github.com/marvis/pytorch-yolo3). Here are some [introductions](https://pjreddie.com/darknet/yolo/), the [origin implementation](https://github.com/pjreddie/darknet) and [paper](https://pjreddie.com/media/files/papers/YOLOv3.pdf).

Some notes about source code of origin yolov3:
1. Sourse code files are in three folders, 'examples', 'include' and 'src', not just in 'src'  

2. The function 'int main(argc, *argv)' is in 'examples/darknet.c', it took me a lot of time to find it.

3. Majority implementation of the algrothms in the paper are in 'src/yolo_layer.c', it is much like a loss layer, rather than a data-processing layer.

4. Original author use independent logistic classifiers, which are just sigmoid function, and binary cross-entropy loss for class prediction, that is right, and use sum of squared error loss for width and height of bounding box, that is also right. But for location of bounding box, logistic classifiers are used as a coordinate predictor, which are just sigmoid function, and binary cross-entropy are used again, accroding to the encoding method of locations and the source code in 'yolo_layer.c', instead of squared error loss which is in the text description following the bounding box encoding fomula in the paper.

## Requirment

python 2.7  
pytorch 0.4  

## Train

1. Download this repo and VOC dataset  
'''
git clone git@github.com:qqadssp/YOLOv3-Pytorch  
cd YOLOv3-Pytorch  
wget https://pjreddie.com/media/files/VOCtrainval_11-May-2012.rar  
tar xf VOCtrainval_11-May-2012.rar  
'''
2. Generate Labels for VOC  
'''
 python voc_label.py  
'''
3. Modify cfg in cfg/voc.data for Pascal Data  
'''
train = <path-to-voc>/2012_train.txt  
valid = <path-to-voc>/2012_val.txt  
'''
4. Download Pretrained Convolutional Weights  
'''
wget https://pjreddie.com/media/files/darknet53.conv.74  
'''
5. Train the Model  
'''
python train.py cfg/voc.data cfg/yolov3-voc.cfg darknet53.conv.74  
'''
## Detect

Download Pretrained Weitghts and Detect  
'''
wget https://pjreddie.com/media/files/yolov3.weights  
python detect.py cfg/yolov3.cfg yolov3.weights data/dog.jpg  
'''
