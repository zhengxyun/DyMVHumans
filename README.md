
<h1 align="center">PKU-DyMVHumans: A Multi-View Video Benchmark for High-Fidelity Dynamic Human Modeling</h1>

<div align="center">
    <a href="https://github.com/zhengxyun" target='_blank'>Xiaoyun Zheng</a>, 
    <a href="https://github.com/leviome" target='_blank'>Weili Liao</a>, 
    <p>xufeng Li</p>, 
    <a href="https://jianbojiao.com" target='_blank'>Jianbo Jiao</a>, 
    <a href="https://github.com/rongjiewang" target='_blank'>Rongjie Wang</a>, 
    <a href="https://www.art.pku.edu.cn/szdw/qzjs/cysjyysglx/gf/index.htm" target='_blank'>Feng Gao</a>, 
    <a href="https://www.cs.cityu.edu.hk/~shiqwang" target='_blank'>Shiqi Wang</a>, 
    <a href="https://www.ece.pku.edu.cn/info/1046/2147.htm" target='_blank'>Ronggang Wang</a>*
</div>
<br />

[Shunyuan Zheng](https://shunyuanzheng.github.io)<sup>1&dagger;</sup>, [Boyao Zhou](https://yaourtb.github.io)<sup>2</sup>, [Ruizhi Shao](https://dsaurus.github.io/saurus)<sup>2</sup>, [Boning Liu](https://liuboning2.github.io)<sup>2</sup>, [Shengping Zhang](http://homepage.hit.edu.cn/zhangshengping)<sup>1*</sup>, [Liqiang Nie](https://liqiangnie.github.io)<sup>1</sup>, [Yebin Liu](https://www.liuyebin.com)<sup>2</sup>

<p><sup>1</sup>Harbin Institute of Technology &nbsp;&nbsp;<sup>2</sup>Tsinghua Univserity
<br><sup>*</sup>Corresponding author &nbsp;&nbsp;<sup>&dagger;</sup>Work done during an internship at Tsinghua Univserity<p>


### [Project page](https://pku-dymvhumans.github.io/) · [Paper](https://arxiv.org) 

<br />

![colored_mesh (1)](assets/overview.png)

## Overview

PKU-DyMVHumans is a versatile human-centric dataset designed for high-fidelity reconstruction and rendering of dynamic human performances in markerless multi-view capture settings. It comprises 32 humans across 45 different dynamic scenarios, each featuring highly detailed appearances and complex human motions. 

![colored_mesh (1)](assets/snapshot.png)

Inspired by recent advancements in neural radiance field (NeRF)-based scene representations, we carefully set up an off-the-shelf framework that is easy to provide those state-of-the-art NeRF-based implementations and benchmark on PKU-DyMVHumans dataset. It is paving the way for various applications like fine-grained foreground/background decomposition, high-quality human reconstruction and photo-realistic novel view synthesis of a dynamic scene.


![colored_mesh (1)](assets/usage.png)

Details are described in our paper:

> PKU-DyMVHumans: A Multi-View Video Benchmark for High-Fidelity Dynamic Human Modeling
>
> Xiaoyun Zheng, Liwei Liao, Xufeng Li, Jianbo Jiao, Rongjie Wang, Feng Gao, Shiqi Wang, Ronggang Wang.
>
>
> CVPR 2024 ([arxiv](https://arxiv.org/))


## Usage

### Download Instructions

The dataset can be directly downloaded from the following links.

**Part1**: [Baidu Pan](https://pan.baidu.com/s/1bqEfh2GbaKf1GTVeMABDtA) (code: xxju), (8 scenarios) can be directly used for benchmarks in fine-grained foreground/background decomposition, 3D human reconstruction and novel view synthesis. 

**Part2**: [Baidu Pan](https://pan.baidu.com/s/1dAD6d1sQ5skJHg1OBv2MRA?pwd=3i2p) (code: 3i2p), (37 scenarios) contains video sequences of the dataset.

**Note that by downloading the datasets, you acknowledge that you have read the agreement, understand it, and agree to be bound by them**:

> 1. The PKU-DyMVHumans dataset is made available only for non-commercial research purposes. Any other use, in particular any use for commercial purposes, is prohibited.
>
> 2. You agree not to further copy, publish or distribute any portion of the dataset. 
>
> 3. Peking University reserves the right to terminate your access to the dataset at any time.

### Dataset format

For each scene, we provide the multi-view images (`./case_name/per_view/cam_*/images/`), the coarse foreground with RGBA channels (`./case_name/per_view/cam_*/images/`), as well as the coarse foreground segmentation (`./case_name/per_view/cam_*/pha/`), which are obtained using [BackgroundMattingV2](https://github.com/PeterL1n/BackgroundMattingV2). 

To make the benchmarks easier compare with our dataset, we save different data formats (i.e., [Surface-SOS](https://github.com/zhengxyun/Surface-SOS), [NeuS](https://github.com/Totoro97/NeuS), [NeuS2](https://github.com/19reborn/NeuS2), [Instant-ngp](https://github.com/NVlabs/instant-ngp), and [3D-Gaussian](https://github.com/graphdeco-inria/gaussian-splatting)) of PKU-DyMVHumans at **Part1** and write a document that describes the data process. 


```
.
|--- <case_name>
|   |--- cams                    
|   |--- videos
|   |--- per_view                
|   |--- per_frame              
|   |--- data_ngp       
|   |--- data_NeuS
|   |--- data_NeuS2
|   |--- data_COLMAP
|   |--- <overview_fme_*.png>
|--- ...

```

Optionally, camera parameters are provided in `./case_name/cams/`, the `*_cam.txt` files are for example :

```
extrinsic
-0.9870368172239224 -0.022593485597630164 -0.15889573893915476 0.2776553077243575 
0.023645162225597843 0.9587670058488046 -0.28320793562159163 0.6898850210976338 
0.1587426462794277 -0.2832937749126657 -0.9458041072801162 4.304908547693294 
0.0 0.0 0.0 1.0 

intrinsic
1795.4695513117783 0.0 960.0 
0.0 1908.5821699983292 540.0 
0.0 0.0 1.0 

<depth_value1> <depth_value2> <depth_value3> <depth_value4>  # depth range and interval 
```

### Case Naming Rules

To filter the scenarios to be downloaded depending on the purpose, you can take advantage of the format of the case names. The case name contains information regarding the duration, action, scenarios type, peeple per frame, and the gender. For instance,

![colored_mesh (1)](assets/names.png)

### Scripts

We provide several scripts in this repo for you to experiment with our dataset. More detailed instructions are included in the files.

* `data_preprocess.sh`: Per view image overview, and save the image sequence and matting results.
* `process2colmap2neus.sh`: process2colmap2neus.sh: Init data format for NeuS/NeuS2. 
* `process2nerf.sh`: Init data format for Instant-ngp/torch-ngp.

Also, we provide a converter script `run_colmap.sh`, using the open source [COLMAP](https://colmap.github.io/) software to extract SfM information and the necessary camera data.

**Note that** all require Python 3.7 or higher to be installed?and make sure that you have installed [COLMAP](https://colmap.github.io/) and that it is available in your PATH. If you are using a video file as input, also be sure to install [FFmpeg](https://www.ffmpeg.org/) and make sure that it is available in your PATH.


## Benchmarks

### Run the [NeuS](https://github.com/Totoro97/NeuS) on PKU-DyMVHumans

NeuS supports the data format provided by **data_NeuS**.

```
.
 <data_NeuS>
|---000000 # frame
|   |---images
|   |   |---000.png
|   |   |---001.png
|   |   |---...
|   |---mask
|   |   |---000.png
|   |   |---001.png
|   |   |---...
|   |---cameras_sphere.npz
|---...

```

### Run the [NeuS2](https://github.com/19reborn/NeuS2) on PKU-DyMVHumans

NeuS2 supports the data format provided by **data_NeuS2**.

```
.
<data_NeuS2>
|---images
|   |---000000 # target frame of the scene
|   |   |---image_c_000_f_000000.png
|   |   |---image_c_001_f_000000.png
|   |   |---...
|   |---000005
|   |   |---image_c_000_f_000000.png
|   |   |---image_c_001_f_000000.png
|   |   |---...
|   |---...
|---train
|   |---transform_000000.json
|   |---transform_000005.json
|   |---<transform_*.json>
|---test
|   |---transform_000000.json
|   |---transform_000005.json
|   |---<transform_*.json>
|---transform_000000.json
|---transform_000005.json
|---<transform_*.json>

```

### Run the [Instant-ngp](https://github.com/NVlabs/instant-ngp)/[torch-ngp](https://github.com/ashawkey/torch-ngp) on PKU-DyMVHumans

Instant-ngp supports the data format provided by **data_ngp**.

```
.
<data_ngp>
|---000000 # frame
|   |---images
|   |   |---image_c_000_f_000000.png
|   |   |---image_c_001_f_000000.png
|   |   |---...
|   |---transform_test.json
|   |---transform_train.json
|   |---transform_val.json
|---...

```

### Run the [Surface-SOS](https://github.com/zhengxyun/Surface-SOS) or [3D-Gaussian](https://github.com/graphdeco-inria/gaussian-splatting) on PKU-DyMVHumans

Surface-SOS/3D-Gaussian supports the data format provided by **data_COLMAP**.

```
.
<data_COLMAP>
|---000000 # frame
|   |---images
|   |   |---image_c_000_f_000000.png
|   |   |---image_c_001_f_000000.png
|   |   |---...
|   |---masks
|   |   |---image_c_000_f_000000.png
|   |   |---image_c_001_f_000000.png
|   |   |---...
|   |---sparse
|   |   |---cameras.bin
|   |   |---images.bin
|   |   |---points3D.bin
|---...

```


## Citation

If you find this repo is helpful, please cite:

```

@article{zheng2024PKU-DyMVHumans,
  title={PKU-DyMVHumans: A Multi-View Video Benchmark for High-Fidelity Dynamic Human Modeling},
  author={Zheng, Xiaoyun and Liao, Liwei and Li,Xufeng and Jiao, Jianbo and Wang, Rongjie and Gao, Feng and Wang, Shiqi and Wang, Ronggang},
  journal={IEEE Conference on Computer Vision and Pattern Recognition (CVPR)},
  year={2024}
}

```

## Acknowledgements

This repository is partly based on [COLMAP](https://colmap.github.io/), [BackgroundMattingV2](https://github.com/PeterL1n/BackgroundMattingV2), 
[NeuS](https://github.com/Totoro97/NeuS), [NeuS2](https://github.com/19reborn/NeuS2), [Instant-ngp](https://github.com/NVlabs/instant-ngp), [torch-ngp](https://github.com/ashawkey/torch-ngp), [3D-Gaussian](https://github.com/graphdeco-inria/gaussian-splatting), and [Surface-SOS](https://github.com/zhengxyun/Surface-SOS). 

We appreciate their contributions to the community.

## Contact

Xiaoyun Zheng (xyun_z@stu.pku.edu.cn)


