
# Adaptive Distillation
This repository is the main source code for the [paper](https://arxiv.org/abs/2110.09674) titled: "Adaptive Distillation: Aggregating Knowledge from Multiple Paths for Efficient Distillation". This paper has been published in [BMVC2021](https://www.bmvc2021-virtualconference.com/conference/papers/paper_1528.html).

To reproduce the experiments with CIFAR-100 dataset, please follow the instructions below:

Install packages.
```
conda create -n AdaptiveDistillation python=3.7 -y
conda activate AdaptiveDistillation
conda install pytorch==1.7.0 torchvision==0.8.1 cudatoolkit==11.0 -c pytorch -y

pip install mmcv-full==1.3.8 -f https://download.openmmlab.com/mmcv/dist/cu110/torch1.7.0/index.html

pip install -r requirements.txt
```
Please note that, this repository is based on mmclassification package version `0.13.0`. Hence this particular version should be installed. Newer versions might work, but has not been tested.

## Running Experiments

### Run experiements on single GPU
```
python tools/train.py configs/kd/cifar100/<config-file> --options model.backbone.norm_cfg.type='BN'
```
For instance for the case of distillation from the ResNet50 to ResNet18 with equal contribution from different paths you can run:
```bash
python tools/train.py configs/kd/cifar100/kd_resnet18_resnet50_cifar100_equal --options model.backbone.norm_cfg.type='BN'
```

### Run experiements on multiple GPU
```
./tools/dist_train.sh configs/kd/cifar100/<config-file> <num_gpus> --options data.samples_per_gpu=<num_samples>
```
For instance, to reproduce our results use 4 GPUs and num_samples 32 for the same setting you can use:
```
./tools/dist_train.sh configs/kd/cifar100/kd_resnet18_resnet50_cifar100_equal 4 --options data.samples_per_gpu=32
```

## Citation
Please use the following bibitem for citing our work Adaptive Distillation:
```
@article{chennupati2021adaptive,
  title={Adaptive Distillation: Aggregating Knowledge from Multiple Paths for Efficient Distillation},
  author={Chennupati, Sumanth and Kamani, Mohammad Mahdi and Cheng, Zhongwei and Chen, Lin},
  journal={British Machine Vision Conference (BMVC)},
  year={2021}
}
```
The Paper can be accessed from [here](https://arxiv.org/abs/2110.09674)

## Acknowledgement
The backbone of this repository is forked from [mmclassification repository](https://github.com/open-mmlab/mmclassification) from [OpenMMLab](https://github.com/open-mmlab)
