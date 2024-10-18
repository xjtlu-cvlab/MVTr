# An end-to-end tracking framework via multi-view and temporal feature aggregation [[paper]](https://doi.org/10.1016/j.cviu.2024.104203)

```
@article{YANG2024104203,
title = {An end-to-end tracking framework via multi-view and temporal feature aggregation},
journal = {Computer Vision and Image Understanding},
volume = {249},
pages = {104203},
year = {2024},
issn = {1077-3142},
doi = {https://doi.org/10.1016/j.cviu.2024.104203},
author = {Yihan Yang and Ming Xu and Jason F. Ralph and Yuchen Ling and Xiaonan Pan},
}
```

## Overview

The code and demonstration videos of the MVTr which is accepted by Computer Vision and Image Understanding (CVIU). The code is recommended to be trained on GPUs with memory equal to or higher than that of the RTX 3090.

## Dependencies

The programme uses the following libraries:  
python 3.7+  
pytorch 1.7.1 & tochvision 0.8.2  
numpy  
matplotlib  
pillow  
opencv-python  
kornia  
motmetrics  
matlab & matlabengine

Also you should go to `multiview_detector/models/ops` and run `bash mask.sh` to build the deformable transformer (forked from [Deformable DETR](https://github.com/fundamentalvision/Deformable-DETR)).

## Data Preparation

The datasets need to be downloaded from their official websites before running the program.  
Wildtrack: https://www.epfl.ch/labs/cvlab/data/data-wildtrack/  
Multiviewx: https://github.com/hou-yz/MVDet/  
MVPerception: https://pan.baidu.com/s/1J3279-G4Nyl7_n0T4lfaDg?pwd=9mqn (password: 9mqn)  
By default, all datasets are put in `Data/`. The `Data/` folder should look like this  
Data  
├── MultiviewX/  
│ └── ...  
└── Wildtrack/  
│ └── ...  
└── MVPerception/  
└── ...  
To generate the MOT file, run `generate_mvmot_from_mvd.py` and make the following modifications:

- Use `ground_plane('wildtrack')` for the Wildtrack dataset,
- Use `ground_plane('multiviewx')` for the MultiviewX dataset,
- Use `ground_plane('mvperception')` for the MVPerception dataset.

Afterward, manually copy the frames you want to test from `gt.txt` and save them as `gt_test.txt`. Or you can download the default test ground truth files `gt_test.txt` and `gt.txt` directly from the following [[baidu(password: 33yz)]](https://pan.baidu.com/s/1qgcv_q6kXMbcxkcdiedaNA?pwd=33yz).

## Training and testing

For training and testing, you can run the following commands in Python:

- To train on Wildtrack dataset: `python Myproject.py -d Wildtrack`
- To train on Multiviewx dataset: `python Myproject.py -d Multiviewx`
- To train on MVPerception dataset: `python Myproject.py -d MVPerception`

Please note that the code is implemented based on `batch size = 1` due to the limited memory of our computer. Please do not change the batch size, as it may result in bugs (even if your GPU memory is greater than that of the RTX 3090).

## Pre-Trained Models

The pre-trained models can be download from the [[baidu(password: x8hd)]](https://pan.baidu.com/s/1vjJLh31ebEly6hwFXluxaw?pwd=x8hd ).
You need to place the pre-trained models in the "logs" folder.
The programme can be run with the pre-trained models for testing:

- To test on Wildtrack dataset: `python Myproject.py -d Wildtrack` and use `model.load_state_dict(torch.load(f'logs\\MultiviewDetectorWildetrack.pth'))`
- To test on Multiviewx dataset: `python Myproject.py -d Multiviewx` and use `model.load_state_dict(torch.load(f'logs\\MultiviewDetectorMultiviewX.pth'))`
- To test on MVPerception dataset: `python Myproject.py -d MVPerception` and use `model.load_state_dict(torch.load(f'logs\\MultiviewDetectorMVPerception.pth'))`
