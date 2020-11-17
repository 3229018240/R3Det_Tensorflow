# R<sup>3</sup>Det: Refined Single-Stage Detector with Feature Refinement for Rotating Object

[![License](https://img.shields.io/badge/License-Apache%202.0-blue.svg)](https://opensource.org/licenses/Apache-2.0)
[![arXiv](http://img.shields.io/badge/cs.CV-arXiv%3A1908.05612-B31B1B.svg)](https://arxiv.org/abs/1908.05612)

## Abstract
[R<sup>3</sup>Det](https://arxiv.org/abs/1908.05612) and [R<sup>3</sup>Det++](https://arxiv.org/abs/2004.13316) are based on [Focal Loss for Dense Object Detection](https://arxiv.org/pdf/1708.02002.pdf), and it is completed by [YangXue](https://yangxue0827.github.io/).

**We also recommend a tensorflow-based [rotation detection benchmark](https://github.com/yangxue0827/RotationDetection), which is led by [YangXue](https://yangxue0827.github.io/).**

<!-- Techniques:      -->
<!-- - [x] [ResNet](https://arxiv.org/abs/1512.03385), [MobileNetV2](https://arxiv.org/abs/1801.04381), [EfficientNet](https://arxiv.org/abs/1905.11946) -->
<!-- - [x] [RetinaNet-H, RetinaNet-R](https://arxiv.org/abs/1908.05612) -->
<!-- - [x] [R<sup>3</sup>Det: Feature Refinement Module (FRM)](https://arxiv.org/abs/1908.05612) -->
<!-- - [x] [R<sup>3</sup>Det++: Instance Level Denoising (InLD)](https://arxiv.org/abs/2004.13316) -->
<!-- - [x] [IoU-Smooth L1 Loss](https://arxiv.org/abs/1811.07126) -->
<!-- - [x] [Circular Smooth Label (CSL)](https://arxiv.org/abs/2003.05597) -->
<!-- - [x] [Densely Coded Label (DCL)]() -->
<!-- - [x] [mmdetection version](https://github.com/SJTU-Thinklab-Det/r3det-on-mmdetection) is released -->
<!-- - [x] Dataset support: DOTA, HRSC2016, ICDAR2015, ICDAR2017 MLT, UCAS-AOD, FDDB, OHD-SJTU, SSDD++ -->
<!-- - [x] [OHDet: Object Heading Detection](https://github.com/SJTU-Thinklab-Det/OHDet_Tensorflow) -->

## Pipeline
![5](pipeline.png)

## Latest Performance
### DOTA1.0 (Task1)
| Model |    Backbone    |    Training data    |    Val data    |    mAP   | Model Link | Anchor | Angle Pred. | Reg. Loss| Angle Range | lr schd | Data Augmentation | GPU | Image/GPU | Configs |      
|:------------:|:------------:|:------------:|:---------:|:-----------:|:----------:|:-----------:|:-----------:|:-----------:|:---------:|:---------:|:---------:|:---------:|:---------:|:---------:|    
| [RetinaNet-H](https://arxiv.org/abs/1908.05612) | ResNet50_v1d 600->800 | DOTA1.0 trainval | DOTA1.0 test | 65.73 | [Baidu Drive (jum2)](https://pan.baidu.com/s/19-hEtCGxLfYuluTATQJpdg) | H | Reg. | smooth L1 | 90 | 2x | × | 3X GeForce RTX 2080 Ti | 1 | [cfgs_res50_dota_v4.py](./libs/configs/DOTA1.0/baseline/cfgs_res50_dota_v4.py) |
| [RetinaNet-H](https://arxiv.org/abs/1908.05612) | ResNet50_v1d 600->800 | DOTA1.0 trainval | DOTA1.0 test | 64.17 | [Baidu Drive (j5l0)](https://pan.baidu.com/s/1Qh_LE6QeGsOBYqMzjAESsA) | H | Reg. | smooth L1 | **180** | 2x | × | 3X GeForce RTX 2080 Ti | 1 | [cfgs_res50_dota_v15.py](./libs/configs/DOTA1.0/baseline/cfgs_res50_dota_v15.py) |
| [R<sup>3</sup>Det](https://arxiv.org/abs/1908.05612) | ResNet50_v1d 600->800 | DOTA1.0 trainval | DOTA1.0 test | 70.66 | [Baidu Drive (30lt)](https://pan.baidu.com/s/143sGeLNjXzcpxi9GV7FVyA) | H + R | Reg. | smooth L1 | 90 | 2x | × | 3X GeForce RTX 2080 Ti | 1 | [cfgs_res50_dota_r3det_v1.py](./libs/configs/DOTA1.0/r3det/cfgs_res50_dota_r3det_v1.py) |
| [R<sup>3</sup>Det*](https://arxiv.org/abs/1908.05612) | ResNet101_v1d 600->800 | DOTA1.0 trainval | DOTA1.0 test | 73.79 | [Baidu Drive (d7qp)](https://pan.baidu.com/s/1GnRbedKDfpgeYB1rUlwObQ) | H + R | Reg. | iou-smooth L1 | 90 | 3x | √ | 4X GeForce RTX 2080 Ti | 1 | [cfgs_res101_dota_r3det_v19.py](./libs/configs/DOTA1.0/r3det/cfgs_res101_dota_r3det_v19.py) |
| [R<sup>3</sup>Det*](https://arxiv.org/abs/1908.05612) | ResNet152_v1d 600->800 | DOTA1.0 trainval | DOTA1.0 test | 74.54 | [Baidu Drive (73bc)](https://pan.baidu.com/s/1WElLJwx15Gmu_gWUj4gE3A) | H + R | Reg. | iou-smooth L1 | 90 | 3x | √ | 4X GeForce RTX 2080 Ti | 1 | [cfgs_res152_dota_r3det_v25.py](./libs/configs/DOTA1.0/r3det/cfgs_res152_dota_r3det_v25.py) |
| [R<sup>3</sup>Det](https://arxiv.org/abs/1908.05612) | ResNet152_v1d 600->MS (+Flip) | DOTA1.0 trainval | DOTA1.0 test | 76.23 (+0.24) | [model](https://drive.google.com/file/d/1GkpiSPN-cAnvDISk5d4kjrV3Tqti_mbj/view?usp=sharing) | H + R | Reg. | iou-smooth L1 | 90 | 4x | √ | 3X GeForce RTX 2080 Ti | 1 | [cfgs_res152_dota_r3det_v3.py](./libs/configs/DOTA1.0/r3det/cfgs_res152_dota_r3det_v3.py) |     
<!-- | [CSL](https://arxiv.org/abs/2003.05597) | ResNet50_v1 600->800 | DOTA1.0 trainval | DOTA1.0 test | 65.69 | [Baidu Drive (kgr3)](https://pan.baidu.com/s/1gvkLhyoIMqVKWsSK38wyrw) | H | **Cls.: Gaussian (r=6, w=1)** | smooth L1 | 180 | 2x | × | 3X GeForce RTX 2080 Ti | 1 | [cfgs_res50_dota_v1.py](./libs/configs/DOTA1.0/csl/cfgs_res50_dota_v1.py) | -->
<!-- | [CSL](https://arxiv.org/abs/2003.05597) | ResNet50_v1 600->800 | DOTA1.0 trainval | DOTA1.0 test | 67.38 | [Baidu Drive (g3wt)](https://pan.baidu.com/s/1nrIs-oYA53qQzlPjqYkMJQ) | H | **Cls.: Gaussian (r=1, w=10)** | smooth L1 | 180 | 2x | × | 3X GeForce RTX 2080 Ti | 1 | [cfgs_res50_dota_v45.py](./libs/configs/DOTA1.0/csl/cfgs_res50_dota_v45.py) | -->
<!-- | [CSL](https://arxiv.org/abs/2003.05597) | ResNet50_v1 600->800 | DOTA1.0 trainval | DOTA1.0 test | 68.73 | [Baidu Drive (3a4t)](https://pan.baidu.com/s/1yC-b9Y4ZVgVkQvpPRRLmhw) | H | **Cls.: Pulse (w=1)** | smooth L1 | 180 | 2x | × | 2X GeForce RTX 2080 Ti | 1 | [cfgs_res50_dota_v41.py](./libs/configs/DOTA1.0/csl/cfgs_res50_dota_v41.py) | -->
<!-- | [DCL]() | ResNet50_v1 600->800 | DOTA1.0 trainval | DOTA1.0 test | 67.39 | [Baidu Drive (p9tu)](https://pan.baidu.com/s/1TZ9V0lTTQnMhiepxK1mdqg) | H | **Cls.: BCL (w=180/256)** | smooth L1 | 180 | 2x | × | 3X GeForce RTX 2080 Ti | 1 | [cfgs_res50_dota_dcl_v5.py](./libs/configs/DOTA1.0/dcl/cfgs_res50_dota_dcl_v5.py) | -->
<!-- | **[R<sup>3</sup>Det-DCL]()** | ResNet50_v1 600->800 | DOTA1.0 trainval | DOTA1.0 test | 71.21| [Baidu Drive (jueq)](https://pan.baidu.com/s/1XR31i3T-C5R16giBxQUNWw) | H->R | **Cls.: BCL (w=180/256)** | iou-smooth L1 | 90->180 | 2x | × | 3X GeForce RTX 2080 Ti | 1 | [cfgs_res50_dota_r3det_dcl_v1.py](./libs/configs/DOTA1.0/r3det_dcl/cfgs_res50_dota_r3det_dcl_v1.py) | -->

[R<sup>3</sup>Det*](https://arxiv.org/abs/1908.05612): R<sup>3</sup>Det with two refinement stages      
**Due to the improvement of the code, the performance of this repo is gradually improving, so the experimental results in other configuration files are for reference only.**        

### Visualization
![1](demo1.png)

## My Development Environment
**docker images: docker pull yangxue2docker/yx-tf-det:tensorflow1.13.1-cuda10-gpu-py3**      
1、python3.5 (anaconda recommend)               
2、cuda 10.0                     
3、[opencv(cv2)](https://pypi.org/project/opencv-python/)       
4、[tfplot 0.2.0](https://github.com/wookayin/tensorflow-plot) (optional)            
5、tensorflow-gpu 1.13                              

## Download Model
### Pretrain weights
1、Please download [resnet50_v1](http://download.tensorflow.org/models/resnet_v1_50_2016_08_28.tar.gz), [resnet101_v1](http://download.tensorflow.org/models/resnet_v1_101_2016_08_28.tar.gz), [resnet152_v1](http://download.tensorflow.org/models/resnet_v1_152_2016_08_28.tar.gz), [efficientnet](https://github.com/tensorflow/tpu/tree/master/models/official/efficientnet), [mobilenet_v2](https://storage.googleapis.com/mobilenet_v2/checkpoints/mobilenet_v2_1.0_224.tgz) pre-trained models on Imagenet, put it to data/pretrained_weights.       
2、**(Recommend in this repo)** Or you can choose to use a better backbone (resnet_v1d), refer to [gluon2TF](https://github.com/yangJirui/gluon2TF).    
* [Baidu Drive](https://pan.baidu.com/s/1GpqKg0dOaaWmwshvv1qWGg), password: 5ht9.          
* [Google Drive](https://drive.google.com/drive/folders/1BM8ffn1WnsRRb5RcuAcyJAHX8NS2M1Gz?usp=sharing)      

## Compile
```  
cd $PATH_ROOT/libs/box_utils/cython_utils
python setup.py build_ext --inplace (or make)

cd $PATH_ROOT/libs/box_utils/
python setup.py build_ext --inplace
```

## Train 

1、If you want to train your own data, please note:  
```     
(1) Modify parameters (such as CLASS_NUM, DATASET_NAME, VERSION, etc.) in $PATH_ROOT/libs/configs/cfgs.py
(2) Add category information in $PATH_ROOT/libs/label_name_dict/label_dict.py     
(3) Add data_name to $PATH_ROOT/data/io/read_tfrecord_multi_gpu.py  
```     

2、Make tfrecord     
For DOTA dataset:      
```  
cd $PATH_ROOT/data/io/DOTA
python data_crop.py
```  

```  
cd $PATH_ROOT/data/io/  
python convert_data_to_tfrecord.py --VOC_dir='/PATH/TO/DOTA/' 
                                   --xml_dir='labeltxt'
                                   --image_dir='images'
                                   --save_name='train' 
                                   --img_format='.png' 
                                   --dataset='DOTA'
```      

3、Multi-gpu train
```  
cd $PATH_ROOT/tools
python multi_gpu_train_r3det.py
```

## Test
```  
cd $PATH_ROOT/tools
python test_dota_r3det_ms.py --test_dir='/PATH/TO/IMAGES/'  
                             --gpus=0,1,2,3,4,5,6,7  
                             -ms (multi-scale testing, optional)
                             -s (visualization, optional)
``` 

**Notice: In order to set the breakpoint conveniently, the read and write mode of the file is' a+'. If the model of the same #VERSION needs to be tested again, the original test results need to be deleted.**      

## Tensorboard
```  
cd $PATH_ROOT/output/summary
tensorboard --logdir=.
``` 

![3](images.png)

![4](scalars.png)

## Citation

If this is useful for your research, please consider cite.

```
@article{yang2020arbitrary,
    title={Arbitrary-Oriented Object Detection with Circular Smooth Label},
    author={Yang, Xue and Yan, Junchi},
    journal={European Conference on Computer Vision (ECCV)},
    year={2020}
    organization={Springer}
}

@article{yang2019r3det,
    title={R3Det: Refined Single-Stage Detector with Feature Refinement for Rotating Object},
    author={Yang, Xue and Liu, Qingqing and Yan, Junchi and Li, Ang and Zhang, Zhiqiang and Yu, Gang},
    journal={arXiv preprint arXiv:1908.05612},
    year={2019}
}

@article{yang2020scrdet++,
    title={SCRDet++: Detecting Small, Cluttered and Rotated Objects via Instance-Level Feature Denoising and Rotation Loss Smoothing},
    author={Yang, Xue and Yan, Junchi and Yang, Xiaokang and Tang, Jin and Liao, Wenglong and He, Tao},
    journal={arXiv preprint arXiv:2004.13316},
    year={2020}
}

@inproceedings{yang2019scrdet,
    title={SCRDet: Towards more robust detection for small, cluttered and rotated objects},
    author={Yang, Xue and Yang, Jirui and Yan, Junchi and Zhang, Yue and Zhang, Tengfei and Guo, Zhi and Sun, Xian and Fu, Kun},
    booktitle={Proceedings of the IEEE International Conference on Computer Vision (ICCV)},
    pages={8232--8241},
    year={2019}
}

@inproceedings{xia2018dota,
    title={DOTA: A large-scale dataset for object detection in aerial images},
    author={Xia, Gui-Song and Bai, Xiang and Ding, Jian and Zhu, Zhen and Belongie, Serge and Luo, Jiebo and Datcu, Mihai and Pelillo, Marcello and Zhang, Liangpei},
    booktitle={Proceedings of the IEEE Conference on Computer Vision and Pattern Recognition (CVPR)},
    pages={3974--3983},
    year={2018}
}

```

## Reference
1、https://github.com/endernewton/tf-faster-rcnn   
2、https://github.com/zengarden/light_head_rcnn   
3、https://github.com/tensorflow/models/tree/master/research/object_detection    
4、https://github.com/fizyr/keras-retinanet     


