  # Monocular 3D Object Detection with Bounding Box Denoising in 3D by Perceiver

  ## Project Page

https://xianpeng919.github.io/monoxiver

## Abstract

The main challenge of monocular 3D object detection is the accurate localization of 3D center. Motivated by a new and strong observation that this challenge can be remedied by a 3D-space local-grid search scheme in an ideal case, we propose a stage-wise approach, which combines the information flow from 2D-to-3D (3D bounding box proposal generation with a single 2D image) and 3D-to-2D (proposal verification by denoising with 3D-to-2D contexts) in a top-down manner. Specifically, we first obtain initial proposals from off-the-shelf backbone monocular 3D detectors. Then, we generate a 3D anchor space by local-grid sampling from the initial proposals. Finally, we perform 3D bounding box denoising at the 3D-to-2D proposal verification stage. To effectively learn discriminative features for denoising highly overlapped proposals, this paper presents a method of using the Perceiver I/O model to fuse the 3D-to-2D geometric information and the 2D appearance information. With the encoded latent representation of a proposal, the verification head is implemented with a self-attention module. Our method, named as MonoXiver, is generic and can be easily adapted to any backbone monocular 3D detectors. Experimental results on the well-established KITTI dataset and the challenging large-scale Waymo dataset show that MonoXiver consistently achieves improvement with limited computation overhead.

## 1. Installation

Please refer to [INSTALL.md](install.md).

## 2. Training and Testing

### 2.1. Prepare data

1) Download [KITTI](http://www.cvlibs.net/datasets/kitti/eval_object.php?obj_benchmark=3d) dataset and organize data 
 following the [official instructions](https://mmdetection3d.readthedocs.io/en/latest/)
  in mmdetection3D. Then generate data by running:
  
```
python custom_create_mono3d_data_tools/create_data.py kitti --root-path ./data/kitti --out-dir ./data/kitti --extra-tag kitti
```

2) Prepare pretrained checkpoints and put it in the ./ckpts folder.

### 2.2. Train and test models

Training: see [ddd_mmdet_train.sh](./scripts/ddd_mmdet_train.sh)

```
./scripts/ddd_mmdet_train.sh [relative_config_filename] [remove_old_if_exist_0_or_1] [name_tag] [gpus] [nb_gpus] [port] [resume_dir]
```

Testing: see [ddd_mmdet_test.sh](./scripts/ddd_mmdet_test.sh)

```
./scripts/ddd_mmdet_test.sh [relative_config_filename] [ckpt_dir] [mode] [gpus] [nb_gpus] [port]
```

## 3. Checkpoints

### 3.1 Pretrained RPN head

|    Model     | Link      |
| ------- | --------- |
| MonoCon (3-Class) | [Link](https://github.com/Xianpeng919/monoxiver/releases/download/monoxiver/monocon_pretrained_rpn_3cls.pth) |
| MonoCon (Car-only) | [Link](https://github.com/Xianpeng919/monoxiver/releases/download/monoxiver/monocon_pretrained_rpn_car.pth) |

### 3.2 MonoXiver Checkpoint
|         | AP40@Easy | AP40@Mod. | AP40@Hard | Link      |
| ------- | --------- |-----------|-----------|-----|
| MonoXiver |  29.20  | 22.54   | 19.53 | [Model](https://github.com/Xianpeng919/monoxiver/releases/download/monoxiver/monoxiver.pth) |

## Contact

Please feel free to report issues here and/or any related problem to Xianpeng Liu (xliu59~at~ncsu~dot~edu).







