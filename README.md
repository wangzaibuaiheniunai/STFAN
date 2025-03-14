# STFAN

Code repo for the paper "Spatio-Temporal Filter Adaptive Network for Video Deblurring".&nbsp; [[arXiv]](https://arxiv.org/pdf/1904.12257.pdf) &nbsp; [[Project Page]](https://www.shangchenzhou.com/projects/stfan/)&nbsp;

<p align="center">
  <img width=95% src="https://user-images.githubusercontent.com/14334509/61511077-1b016200-aa28-11e9-94c1-63e97f55f093.png">
</p>

## Filter Adaptive Convolutional (FAC) Layer

The proposed filter adaptive convolutional (FAC) layer applies generated pixel variant filters to the features, In theory, the element-wise adaptive filters is five-dimensional ![](http://latex.codecogs.com/svg.latex?$h{\times}w{\times}c{\times}k{\times}k$)
. In practice, the dimension of the generated filter ![](http://latex.codecogs.com/svg.latex?$\mathcal{F}$)
 is ![](http://latex.codecogs.com/svg.latex?$h{\times}w{\times}ck^2$) and we reshape it into the five-dimensional filter. For each position ![](http://latex.codecogs.com/svg.latex?$(x,y,c_i)$) of input feature ![](http://latex.codecogs.com/svg.latex?$Q\in\mathds{R}^{h{\times}w{\times}c}$), a specific local filter ![](http://latex.codecogs.com/svg.latex?$\mathds{F}_{x,y,c_i}\in\mathcal{R}^{k{\times}k}$) (reshape from ![](http://latex.codecogs.com/svg.latex?$1{\times}1{\times}k^2$)) is applied to the region centered around ![](http://latex.codecogs.com/svg.latex?$Q_{x,y,c_i}$).
 
<p align="center">
  <img width=40% src="https://user-images.githubusercontent.com/14334509/68988034-36f90100-086c-11ea-9e57-93aca737d6d3.jpg">
</p>
 
<p>&#10148; The <strong>forward pass</strong> of the proposed Filter Adaptive Convolutional (FAC) Layer is as follows:</p>

<p align="center">
  <img width=70% src="https://user-images.githubusercontent.com/14334509/68988093-1aa99400-086d-11ea-9a92-8cef3026b11a.png">
</p>

<p>&#10148; The <strong>backward pass</strong> can be presented as:</p>

<p align="center">
  <img width=65% src="https://user-images.githubusercontent.com/14334509/68988094-2006de80-086d-11ea-9be0-d9758be6380e.png">
</p>

<p align="center">
  <img width=50% src="https://user-images.githubusercontent.com/14334509/68988097-22693880-086d-11ea-983e-c561b7421d26.png">
</p>
 
 ## Illustration of Alignment and Deblurring Processes by FAC layer
The frame alignment and deblurring are both spatially variant tasks. Using the proposed FAC layer, we consider these two processes as two filter adaptive convolution in feature domain. The convolution operation can transform the pixels of features, which can be used for frames alignment (a) and deblurring (b) using estimated corresponding filters.

<p align="center">
  <img width=70% src="https://user-images.githubusercontent.com/14334509/68987844-01064d80-0869-11ea-8f80-2ebb72619f39.jpg">
</p>

## Pretrained Models

You could download the pretrained model (21.5MB) of STFAN from [[Here]](https://hiteducn0-my.sharepoint.com/:f:/g/personal/sczhou_hit_edu_cn/EiVeE2qh_e5Omxa_JrfOj6UBXgSm13kyI3RHwUPnaDL9Hg?e=5YJFOx). 

(Note that the model does not need to unzip, just load it directly.)

## Prerequisites

- Linux (tested on Ubuntu 14.04/16.04)
- gcc 4.9+
- Python 2.7+
- Pytorch 0.4.1
- easydict
- tensorboardX

#### Installation

```
pip install -r requirements.txt
bash install.sh
```

## Get Started

Use the following command to train the neural network:

```
python runner.py 
        --phase 'train'\
        --data [dataset path]\
        --out [output path]
```

Use the following command to test the neural network:

```
python runner.py \
        --phase 'test'\
        --weights './ckpt/best-ckpt.pth.tar'\
        --data [dataset path]\
        --out [output path]
```
Use the following command to resume training the neural network:

```
python runner.py 
        --phase 'resume'\
        --weights './ckpt/best-ckpt.pth.tar'\
        --data [dataset path]\
        --out [output path]
```
You can also use the following simple command, with changing the settings in config.py:

```
python runner.py
```

## Results on the testing dataset and real blurry videos

Some results are shown in [[Project Page]](https://www.shangchenzhou.com/projects/stfan/).

## Citation
If you find STFANet, or FAC layer useful in your research, please consider citing:

```
@article{Zhou2019stfan,
  title={Spatio-Temporal Filter Adaptive Network for Video Deblurring},
  author={Zhou, Shangchen and Zhang, Jiawei and Pan, Jinshan and Xie, Haozhe and Zuo, Wangmeng and Ren, Jimmy},
  journal={arXiv preprint arXiv:1904.12257},
  year={2019}
}
```

## Contact

We are glad to hear if you have any suggestions and questions.

Please send email to shangchenzhou@gmail.com

## License

This project is open sourced under MIT license.
