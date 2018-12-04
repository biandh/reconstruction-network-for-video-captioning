# reconstruction-network-for-video-captioning

This project tries to implement *RecNet* proposed on **[Reconstruction Network for Video Captioning](http://openaccess.thecvf.com/content_cvpr_2018/papers/Wang_Reconstruction_Network_for_CVPR_2018_paper.pdf)** in **CVPR 2018**.



## Requirements

* Ubuntu 16.04
* CUDA 9.0
* cuDNN 7.3.1
* Java 1.8
* Python 2.7.12
  * PyTorch 1.0
  * Other python libraries specified in requirements.txt



## How to use

### Step 1. Setup python virtual environment

```
$ pip install virtualenv
$ virtualenv .env
$ source .env/bin/activate
(.env) $ pip install --upgrade pip
(.env) $ pip install -r requirements.txt
```


### Step 2. Prepare Data

1. Extract feature vectors of datasets by following instructions in [here](https://github.com/hobincar/awesome-video-dataset), and locate them at `~/<dataset>/features/<network>.hdf5`
   
   > e.g. InceptionV4 feature vectors of MSVD dataset will be located at `~/data/MSVD/features/InceptionV4.hdf5`.

2. Set hyperparameters in `config.py` and split the dataset into train / val / test dataset by running following command.
   
   ```
   (.env) $ python -m scripts.split
   ```
   

### Step 3. Train

1. Set hyperparameters in `config.py`.
2. Run
   ```
   (.env) $ python train.py
   ```


### Step 4. Inference

1. Set hyperparameters in `config.py`.
2. Run
   ```
   (.env) $ python run.py
   ```


## Result

### Comparison with original paper

* MSVD

  |   | BLEU4 | METEOR | CIDEr | ROUGE_L |
  | :---: | :---: | :---: | :---: | :---: |
  | Ours (global) | 40.7 | 27.3 | 34.4 | 61.9 |
  | Paper (local) | 52.3 | 34.1 | 69.8 | 80.7 |
<!--
[Ours (global)]: RecNet | MSVD tc-30 mc-5 sp-uniform | ENC InceptionV4 sm-28 | DEC lstm-1 at-128 dr-0.5-0.5 tf-1.0 lr-1e-05-wd-1e-05 op-amsgrad | REC LSTM lr-1e-06-wd-1e-05 op-adam | EMB 468 dr-0.5 sc-1 | bs-100 | cp-50.0 | 181117-18:32:22
-->

* MSR-VTT

  |   | BLEU4 | METEOR | CIDEr | ROUGE_L |
  | :---: | :---: | :---: | :---: | :---: |
  | Ours | - | - | - | - |
  | Paper (local) | 39.1 | 26.6 | 59.3 | 42.7 |


### loss

![image](https://user-images.githubusercontent.com/17702664/49371473-e364d480-f73a-11e8-809b-107ed321e841.png)


### evaluation metrics (BLEU, METEOR, CIDEr, and ROUGE_L)

![image](https://user-images.githubusercontent.com/17702664/49371614-6b4ade80-f73b-11e8-8cec-e0e4dc6b8fb8.png)


## TODO

* Add C3D feature vectors.
* Implement a local reconstructor network.
* Add MSR-VTT dataset.
