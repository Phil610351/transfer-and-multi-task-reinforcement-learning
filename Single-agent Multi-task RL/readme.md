# Multi-task RL
This directory contains the source code of Single-agent Multi-task baselines and benchmarks. 

## Contents

1. Baselines
2. Benchmarks
3. Setup
4. Usage
5. Acknowledgements

## Baselines

We have covered the implementation of these following multi-task methods, which are common used baselines presented in recent papers. Some implementation are citing from @mtrl

### Network-Architecture:

- **Soft-Modularization** - https://arxiv.org/abs/2003.13661v2 

### Gradient-based:
- **GradDrop** -  [https://arxiv.org/abs/2010.06808](https://arxiv.org/abs/2010.06808) 
- **PCGrad** - [https://arxiv.org/abs/2001.06782](https://arxiv.org/abs/2001.06782) 
- **CAGrad** - [https://arxiv.org/abs/2110.14048](https://arxiv.org/abs/2110.14048) 

### Others:

+ **CARE** -  https://arxiv.org/abs/2102.06177
+ **MTSAC**
+ **MTMHSAC**

## Benchmarks

We run multi-task algorithm in the benchmarks: Metaworld, MuJoCo. Please follow the results below.

// some introduction to multi-task MuJoCo.

// some introduction to Metaworld.

## Setup

+ Clone the repository: `git clone git@gitlab.example.com:ytp/transfer-and-multi-task-reinforcement-learning.git`.
+ Install dependencies: `pip install -r requirements.txt`

## Usage(TODO)

All experiments were written in `PyTorch 1.7` and can be trained with different flags (hyper-parameters) when running each training script. We briefly introduce some important flags below. 

| Flag Name     | Usage                                                                                                                                    | Comments                                                                            |
|---------------|------------------------------------------------------------------------------------------------------------------------------------------|-------------------------------------------------------------------------------------|
| `network`     | choose multi-task network: `split, mtan`                                                                                                 | both architectures are based on ResNet-50; only available in dense prediction tasks |
| `dataset`     | choose dataset: `nyuv2, cityscapes`                                                                                                      | only available in dense prediction tasks                                            |
| `weight`      | choose weighting-based method: `equal, uncert, dwa, autol`                                                                               | only `autol` will behave differently when set to different primary tasks            |
| `grad_method` | choose gradient-based method: `graddrop, pcgrad, cagrad`                                                                                 | `weight` and `grad_method` can be applied together                                  |
| `task`        | choose primary tasks: `seg, depth, normal` for NYUv2, `seg, part_seg, disp` for CityScapes, `all`: a combination of all standard 3 tasks | only available in dense prediction tasks                                            |
| `with_noise`  | toggle on to add noise prediction task for training (to evaluate robustness in auxiliary learning setting)                               | only available in dense prediction tasks                                            |
| `subset_id`   | choose domain ID for CIFAR-100, choose `-1` for the multi-task learning setting                                                          | only available in CIFAR-100 tasks                                                   |
| `autol_init`  | initialisation of Auto-Lambda, default `0.1`                                                                                             | only available when applying Auto-Lambda                        |
| `autol_lr`    | learning rate of Auto-Lambda, default `1e-4`  for NYUv2 and `3e-5` for CityScapes                                                        | only available when applying Auto-Lambda                       |

Training Auto-Lambda in Multi-task / Auxiliary Learning Mode:
```
python trainer_dense.py --dataset [nyuv2, cityscapes] --task [PRIMARY_TASK] --weight autol --gpu 0   # for NYUv2 or CityScapes dataset
python trainer_cifar.py --subset_id [PRIMARY_DOMAIN_ID] --weight autol --gpu 0   # for CIFAR-100 dataset
```

Training in Single-task Learning Mode:
```
python trainer_dense_single.py --dataset [nyuv2, cityscapes] --task [PRIMARY_TASK]  --gpu 0   # for NYUv2 or CityScapes dataset
python trainer_cifar_single.py --subset_id [PRIMARY_DOMAIN_ID] --gpu 0   # for CIFAR-100 dataset
```

*Note: All experiments in the original paper were trained from scratch without pre-training.*

## Citation
If you found this code/work to be useful in your own research, please considering citing the following:

```
@article{,
  title={},
  author={},
  journal={},
  year={}
}
```

## Acknowledgement



## Contact
If you have any questions, please contact 