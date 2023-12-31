# wctYOLOv5.11

### YOLOv5.11 of wct



![pipeline](pipeline.png)

## Introduction

Just a easy test

More detailed can be found in [github](https://github.com/ultralytics/yolov5) code.

## Main Results

Now, this code don't have a complent results.

<div align="center">
    <img src="acdm.png" height="500px" />
</div>

The self-supervised model's attention is focused on the key parts of the scene objects and has a better grasp of the feature information, avoiding the problem of feature redundancy and excessive computational costs.

<div align="center">
    <img src="vss.png" height="500px" />
</div>

### YOLOv5.11 Model

| name | train epochs | input resolution | output resolution | acc@1 | model | chang time |
| :---: | :---: | :---: | :---: | :---: | :---: | :---: |
|  YOLOv5.11  | 200 | 640x640 | 640x640 |  91.92  | 2023.9.27 | [models](models/yolov5s.yaml) | 

### ImageNet-1K Pre-trained Model

| name | pre-train epochs | pre-train resolution | fine-tune resolution | acc@1 | pre-trained model |
| :---: | :---: | :---: | :---: | :---: | :---: |
| SwinMIM-Large | 800 | 224x224 | 224x224 | 85.4 | [google](https://drive.google.com/file/d/1DCELfGormJK0xbMU2A-mvBWZStSbDUfd/view?usp=sharing)/[config](configs/MIM_finetune__swin_large__img224_window14__800ep.yaml) | 
## Installation

 The requirements are listed in the `requirement.txt` file. To create your own environment, an example is:

```bash
use pip and requirements, and then, use train.py and test.py, or you can use minglinghang
```
This work used the State Farm dataset which can be downloaded from this [Kaggle competition](https://www.kaggle.com/c/state-farm-distracted-driver-detection).
## Train

 The training continues by using a pretrained model from our work, an example is:

```bash
python main.py  --cfg configs/SLDDBD_patchsize32_swin_ratio0.5_img224_statefarm_110ep.yaml --pretrained SLDDBD_patchsize32_swin_ratio0.5_img224_statefarm_110ep.pth --data-path dataset --local_rank 0 --batch-size 32
```
 New training using the MIM pretrained model:, an example is:

```bash
python main.py  --cfg configs/MIM_finetune__swin_large__img224_window14__800ep.yaml --pretrained MIM_finetune__swin_large__img224_window14__800ep.pth --data-path dataset --local_rank 0 --batch-size 32
```


## Evaluation

The evaluation configurations can be adjusted at `main_eval.py`.
Get the confusion matrix results you need in the confusion matrix folder.

```bash
cd eval
python main_eval.py --eval  --cfg configs/SLDDBD_patchsize32_swin_ratio0.5_img224_statefarm_110ep.yaml  --resume ./SLDDBD_patchsize32_swin_ratio0.5_img224_statefarm_110ep.pth --local_rank 0 --data-path  dataset
```

## Inference

Print the detection results of the weights model and output the txt file.


```bash
cd eval
python inference.py --cfg configs/SLDDBD_patchsize32_swin_ratio0.5_img224_statefarm_110ep.yaml  --resume ./SLDDBD_patchsize32_swin_ratio0.5_img224_statefarm_110ep.pth --local_rank 0
```
You can modify the inference code to customize the inference categories and data input path.

## Citation

If you are interested in this work, please cite the following work:

```
@article{zhang2023novel,
  title={A Novel Driver Distraction Behavior Detection Method Based on Self-Supervised Learning With Masked Image Modeling},
  author={Zhang, Yingzhi and Li, Taiguo and Li, Chao and Zhou, Xinghong},
  journal={IEEE Internet of Things Journal},
  year={2023},
  publisher={IEEE}
}
```

## Acknowledgments

Our work is based on [Swin Transformer](https://github.com/microsoft/Swin-Transformer).  We appreciate the previous open-source repository [Swin Transformer](https://github.com/microsoft/Swin-Transformer).


