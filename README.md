# DeepFashion-MultiModal

<img src="./assets/logo.png" width="96%">

**DeepFashion-MultiModal** is a large-scale high-quality human dataset with rich multi-modal annotations. It has the following properties:
1. It contains 44,096 high-resolution human images, including 12,701 full body human images.
2. For each full body images, we **manually annotate** the human parsing labels with 24 classes.
3. For each full body images, we **manually annotate** the keypoints.
4. We extract densepose for each human image.
5. Each image is **manually annotated** with attributes for both clothes shapes and textures.
6. We provide a textual description for each image.

DeepFashion-MultiModal can be applied to text-driven human image generation, text-guided human image manipulation, skeleton-guided human image generation, human pose estimation, human image captioning, multi-modal learning for human images, human attribute recognition, human parsing prediction, and etc. The dataset is proposed in [Text2Human](https://github.com/yumingj/Text2Human).

## Overview of Annotations
<img src="./assets/dataset_overview.png" width="100%">

You can download the following links:

| Path | Size | Files | Format | Description
| :--- | :---- | ----: | :----: | :----------
| [DeepFashion-MultiModal](xxxx) | ~20 GB | 420,002 | | Main folder
| &boxvr;&nbsp; [image](xxxx) | ~2 GB | 44,096 | JPG | images from DeepFashion of size 750&times;1101
| &boxvr;&nbsp; [parsing](xxx) | 11 MB | 12,701 | PNG | manually annotated parsing labels
| &boxvr;&nbsp; [keypoints](xxx) | 11 MB | 2 | TXT | manually annotated keypoints
| &boxvr;&nbsp; [densepose](xxx) | 11 MB | 44,096 | PNG | extracted densepose
| &boxvr;&nbsp; [labels](xxx) | 11 MB | 3 | TXT | three texts for shape, fabric, and color annotations
| &boxvr;&nbsp; [textual descriptions](xxx) | 11 MB | 1 | JSON | textual descriptions for each image

## Human Parsing Label
* Mask labels are defined as follows:

| Label list | | | |
| ------------ | ------------- | ------------ | ------------ |
| 0: 'background' | 1: 'top' | 2: 'outer' | 3: 'skirt' |
| 4: 'dress' | 5: 'pants' | 6: 'leggings' | 7: 'headwear' |
| 8: 'eyeglass' | 9: 'neckwear' | 10: 'belt' | 11: 'footwear' |
| 12: 'bag' | 13: 'hair' | 14: 'face' | 15: 'skin' |
| 16: 'ring' | 17: 'wrist wearing' | 18: 'socks' | 19: 'gloves' |
| 20: 'necklace' | 21: 'rompers' | 22: 'earrings' | 23: 'tie' |

* You can read the labels using the following code:

```python
from PIL import Image
import numpy as np

segm = Image.open(f)
segm = np.array(segm) # shape: [750, 1101]
```

# KeyPoints
* For each human image, we provide 21 keypoints. The keypoints are defined as follows:

<img src="./assets/keypoints_definition.png" width="20%">

* The `keypoints_loc.txt` file contains the coordinates of the keypoints. The format is as follows:
```
<img name> <x_1> <y_1> <x_2> <y_1> ... <x_21> <y_21>
```
&ensp; If the keypoints are not present, the keypoint is (-1, -1).

* The `keypoints_vis.txt` file indicates the visibility of the keypoints. The format is as follows:
```
<img name> <v_1> <v_2> ... <v_21>
```
&ensp; If the keypoint is visible, the value is 0. If the keypoint is present but hidden by other parts, the value is 1. If the keypoint is not present, the value is 2.

# DensePose
* We extract DensePose using this [repo](https://github.com/facebookresearch/DensePose). Please refer to this repo for more details.

# Labels
* The definitions of shape annotations:
```
  0. sleeve length: 0 sleeveless, 1 short-sleeve, 2 medium-sleeve, 3 long-sleeve, 4 not long-sleeve, 5 NA
  1. lower clothing length: 0 three-point, 1 medium short, 2 three-quarter, 3 long, 4 NA
  2. socks: 0 no, 1 socks, 2 leggings, 3 NA
  3. hat: 0 no, 1 yes, 2 NA
  4. glasses: 0 no, 1 eyeglasses, 2 sunglasses, 3 have a glasses in hand or clothes, 4 NA
  5. neckwear: 0 no, 1 yes, 2 NA
  6. wrist wearing: 0 no, 1 yes, 2 NA
  7. ring: 0 no, 1 yes, 2 NA
  8. waist accessories: 0 no, 1 belt, 2 have a clothing, 3 hidden, 4 NA
  9. neckline: 0 V-shape, 1 square, 2 round, 4 standing, 5 lapel, 6 suspenders, 7 NA
  10. outer clothing a cardigan?: 0 yes, 1 no, 2 NA
  11. upper clothing covering navel: 0 no, 1 yes, 2 NA

  Note: 'NA' means the relevant part is not visible.
```

* The format of shape annotations:
```
  <img_name> <shape_0> <shape_1> ... <shape_11>
```

* The definitions of fabric annotations:
```
  0 denim, 1 cotton, 2 leather, 3 furry, 4 knitted, 5 chiffon, 6 other, 7 NA

  Note: 'NA' means the relevant part is not visible.
```

* The format of fabric annotations:
```
  <img_name> <upper_fabric> <lower_fabric> <outer_fabric>
```

* The definitions of color annotations:
```
  0 floral, 1 graphic, 2 striped, 3 pure color, 4 lattice, 5 other, 6 color block, 7 NA

  Note: 'NA' means the relevant part is not visible.
```

* The format of color annotations:
```
  <img_name> <upper_color> <lower_color> <outer_color>
```

## Papers using our dataset
* (SIGGRAPH 2022) **Text2Human: Text-Driven Controllable Human Image Generation**, Yuming Jiang et al. [[Paper](xxx)], [[Code](xxx)]
* (arXiv 2022) **StyleGAN-Human: A Data-Centric Odyssey of Human Generation**, Jianglin Fu et al. [[Paper](https://arxiv.org/pdf/2204.11823.pdf)], [[Code](https://github.com/stylegan-human/StyleGAN-Human)], [[Project Page](https://stylegan-human.github.io/)]

## Citation

If you find this dataset useful for your research and use it in your work, please consider cite the following papers:

```bibtex
@article{jiang2022text2human,
  title={Text2Human: Text-Driven Controllable Human Image Generation},
  author={Jiang, Yuming and Yang, Shuai and Qiu, Haonan and Wu, Wayne and Loy, Chen Change and Liu, Ziwei},
  journal={ACM Transactions on Graphics (TOG)},
  volume={41},
  number={4},
  articleno={162},
  pages={1--11},
  year={2022},
  publisher={ACM New York, NY, USA},
  doi={10.1145/3528223.3530104},
}

@inproceedings{liuLQWTcvpr16DeepFashion,
 author = {Liu, Ziwei and Luo, Ping and Qiu, Shi and Wang, Xiaogang and Tang, Xiaoou},
 title = {DeepFashion: Powering Robust Clothes Recognition and Retrieval with Rich Annotations},
 booktitle = {Proceedings of IEEE Conference on Computer Vision and Pattern Recognition (CVPR)},
 month = {June},
 year = {2016}
 }
```