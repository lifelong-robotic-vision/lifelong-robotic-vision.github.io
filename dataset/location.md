---
title: OpenLORIS-Location
layout: info
Edit: 2020-11-15
toc: false
commentable: false
protected: true
mathjax: true
---



# OpenLORIS-Location Dataset

>(L)ifel(O)ng (R)obotic V(IS)ion (**OpenLORIS**) - Location Dataset (**OpenLORIS-Location**) is designed for the research of indoor visual localization. It contains contains variant illumination and viewpoints, severe dynamic elements, repetitive features and daily changed items.

## Dataset download
> Our dataset can be downloaded at [OpenLORIS-Location dataset](https://github.com/lifelong-robotic-vision/OpenLORIS-Location). The dataset is an open dataset, and we welcome contribution of data from third parties.  Please contact [Fei Qiao](mailto:qiaofei@tsinghua.edu.cn) for more details.
> Our project using OpenLORIS-Location dataset for training can be found at [RaP-Net](https://github.com/ivipsourcecode/RaP-Net)
Please see the details in our paper below. You can also open an issue [here](https://github.com/ivipsourcecode/RaP-Net/issues) for any questions.

## Motivation
Visual localization aims to estimate the camera pose of a given image taken in a mapped area. It is a fundamental problem for many artificial intelligence applications. Although localization in urban environments archives good performance, indoor localization is still a non-trivial task. For indoor visual localization, the challenges come from repetitive features like carpet, textures and visually identical pillars, and dynamic objects like moving people and moved furniture. And the main reason causing such gap is that the feature extraction in indoor environment is not reliable.  Localization needs reliable features extracted from static/stable regions. 

The regions with different semantic attributes should not play equal importance. For example, by apply semantic segmentation, features in buildings regions are distinct and stable in urban scenes. However, it is hard to define the static and dynamic attributes of items in indoor environment, such as desks and chairs. Thus, **attention** mechanism can be adopted to solve such hard problem. Common strategies for training attention are applying metric learning, which need to construct triplet-type dataset. The ideal datasets to train such network should contain less viewpoints but large illumination changes, dynamic occlusions. Pictures describing the same location should be in different visual conditions. Unfortunately, we can not directly extract images from existing indoor image datasets to construct a training and validation dataset. For example, InLoc dataset [1] is introduced to SfM and relocalization and it contains large viewpoint changes, limited illumination changes, and less dynamic disturbance. The Bicocca dataset [2] is recorded in a relative short time period and contains less dynamic elements and illumination changes. They are excellent choice to evaluate the performance but can not be used to train.

To help the research about indoor localization , we introduce a new indoor image  dataset, refered as OpenLORIS-Location. The dataset is composed of 94 locations, and each location contains several images taken at different time with various kinds of indoor interferences. Part of the data are derived from the OpenLORIS-Scene dataset, while others are newly collected in various indoor scenes. 

More description of the dataset can be found in [this paper](https://arxiv.org/abs/2012.00234):

> Dongjiang Li et al. "RaP-Net: A Region-wise and Point-wise Weighting Network to Extract Robust Features for Indoor Localization." arXiv preprint arXiv:2012.00234, 2020.

If you find our dataset and related project useful in your research, please consider citing:

    @article{li2020RaPNet,
        title={ {RaP-Net}: A Region-wise and Point-wise Weighting Network to Extract Robust Features for Indoor Localization},
        author={Dongjiang Li and Jinyu Miao and Xuesong Shi and Yuxin Tian and Qiwei Long and Tianyu Cai and Ping Guo and Hongfei Yu and Wei Yang and Haosong Yue and Qi Wei and Fei Qiao},
        journal={arXiv preprint arXiv:2012.00234},
        year={2020}
    }


## Data collection
Data is collected in the indoor environments. We extracted 30 localizations from former published OpenLORIS-Scene dataset. We propose a incremental extracting method to build our new dataset and figure below gives us an illustration for extracting the locations from each scene of OpenLORIS-Scene dataset. For each scene, we regard the position of the first RGB image from the first sequence as the first location. For the rest images in the scene, we impose the limitations of displacement and direction to decide its location. Euclidean distances and the changes of Euler angles are calculated between the position of current images and all existing locations. If the closest distance and orientation are both less than the pre-defined threshold, the current
image is added into the corresponding location. To make sure images belonging to different locations have little overlap
information, a new image is regarded as a new location only if it was far from existing locations or it had a large viewpoint
change compared to existing locations. Figure below (b) shows some samples extracted from OpenLORIS-Scene.

![dataset-location](dataset-location.jpg)

On the other hand, in order to enlarge the training and validation data, we collect 64 new locations. Those data are all taken by cameras on cellphones and most of them keep almost the same viewpoint, but they contain appearance changes and dynamic occlusions as shown in figure above (c).

## Data description
>The dataset is composed of 93 locations. Images in each locations describe the same real-world place but in different visual conditions.

Our released dataset is a collection of $93$ distinct locations including $1553$ RGB images.  To the best of our knowledge, it is the first dataset of real-world indoor scenes that can be used for training attention mechanisms. In the 45 locations of office, home and corridor, there are moderate scene changes and significant illumination changes. In the other 48 locations of market, restaurant and station, illumination is relatively stable but there are many people and dynamic objects.


| Scene | Locations* | Images   | Main challenges |
| :-------------: |:-------------:| :-------------:|:-------------:|
| office | 6+6 | 270 |illumination changes |
| home | 9+7 | 232 |moved furnitures |
| corridor | 12+5 | 291 |large illumination changes |
| market | 23+8 | 527 |high dynamics |
| restaurant | 5+4 | 135 |high dynamics |
| station | 8+0 | 98 |dynamics, repetitive patterns |
| **Total** | **63+30** | **1553** | |

\* (newly collected locations + derived from OpenLORIS-Scene dataset)


## Data structure

ourDataset  
  | ------ Scene#1  
  | ------ | ------ Location#1  
  | ------ | ------ | ------ 001.jpg  
  | ------ | ------ | ------ ...  
  | ------ | ------ | ------  XXX.jpg  
  | ------ | ------ Location#2  
  | ------ | ------ | ------ ...  
  | ------ Scene#2  
  | ------ | ------  ...  
--->

## References

[1] H. Taira, M. Okutomi, T. Sattler, M. Cimpoi, M. Pollefeys, J. Sivic, T. Pajdla, and A. Torii, “Inloc: Indoor visual localization with dense matching and view synthesis,” in Proceedings of the IEEE/CVF Conference on Computer Vision and Pattern Recognition (CVPR), 2018, pp. 7199–7209.

[2] RAWSEEDS, “Robotics advancement through web-publishing of sensorial and elaborated extensive data sets (project FP6-IST-045144),” 2007-2009. [Online]. Available: http://www.rawseeds.org/rs/datasets


