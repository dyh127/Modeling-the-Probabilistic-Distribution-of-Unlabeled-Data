Please email me (dyh.ustc.uts@gmail.com) if you want the code and dataset.

# AAAI2021
code for Modeling the Probabilistic Distribution of Unlabeled Data for One-shot Medical Image Segmentation


## Prerequisites
* Python 3.6
* Tensorflow 1.14.0
* Cuda 10.0

## Datasets
* CANDI and ABIDE_benchmark are in the 'data' folder. please untar them.

## Training
1. Shape registration network and Intensity alignment network:

a. Training the shape registration network:

* setting up the datapath and dataname in ```job.sh```
* run the code in the ```job.sh```:
```
python shape_deformation_learning.py --data-path $datapath --dataname $dataname --log-path $logpath --log-name 'shape_deformation_learning' --mode 'forward'
python shape_deformation_learning.py --data-path $datapath --dataname $dataname --log-path $logpath --log-name 'shape_deformation_learning' --mode 'backward'
```

b. Training the intensity alignment network:

* setting up the forward and backword pretrained model in ```intensity_deformation_learning.py line162-169```,
* run the code in the ```job.sh```:
```
python intensity_deformation_learning.py --data-path $datapath --dataname $dataname --log-path $logpath --log-name 'intensity_deformation_learning'
```

2. Shape VAE and Intensity VAE training in ```MPDUD```

a. Training the shape VAE:
* setting up the datapath and dataname in ```job.sh```
* setting up the leaned registration networks path in ```shape_distri_modeling.py line148 or line151```
* run the code in the ```job.sh```:
```
python shape_distri_modeling.py --data-path $datapath --dataname $dataname
```

b. Training the intensity VAE:
* setting up the datapath and dataname in ```job.sh```
* setting up the leaned registration networks path in ```intensity_distri_modeling.py line147-154```
* run the code in the ```job.sh```:
```
python intensity_distri_modeling.py --data-path $datapath --dataname $dataname
```

3. Segmentation network training:
* setting up the datapath and dataname in ```job.sh```
* setting up the leaned VAE networks path in ```segmenter.py line221-232```
* run the code in the ```job.sh```:
```
python segmenter.py --data-path $datapath --dataname $dataname
```

## Evaluate
* setting up the datapath and dataname in ```job.sh```
* setting up the learned segmentation network path in ```job.sh```
* run the code in the ```job.sh```:
```
python segmenter.py --data-path $datapath --dataname $dataname --evaluate --resume $evalmodel
```
