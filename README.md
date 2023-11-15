# Segment Anything Model for Medical Image Analysis: an Experimental Study

[![arXiv Paper](https://img.shields.io/badge/arXiv-2304.10517-orange.svg?style=flat)](https://arxiv.org/abs/2304.10517)

#### By [Maciej Mazurowski](https://sites.duke.edu/mazurowski/), Haoyu Dong, Hanxue Gu, Jichen Yang, [Nicholas Konz](https://nickk124.github.io/) and Yixin Zhang.

This is the official repository for our paper: [Segment Anything Model for Medical Image Analysis: an Experimental Study](https://www.sciencedirect.com/science/article/pii/S1361841523001780), recently published in Medical Image Analysis, where we evaluated Meta AI's Segment Anything Model (SAM) on many medical imaging datasets. 

## Installation

The code requires installing SAM's repository [Segment Anything (SAM)](https://github.com/facebookresearch/segment-anything.git). The model and dependencies can be found at SAM's repository, or you can install them with

```
git clone https://github.com/facebookresearch/segment-anything.git
cd segment-anything; pip install -e .
```

Optionally, we have included code to evaluate [Reviving Iterative Training with Mask Guidance for Interactive Segmentation (RITM)](https://arxiv.org/abs/2102.06583) on the datasets. All you need to do to use our code for this is to clone their repository locally:

```
git clone https://github.com/yzluka/ritm_interactive_segmentation
```

## Getting start
First, download SAM's model checkpoint 
```
wget https://dl.fbaipublicfiles.com/segment_anything/sam_vit_h_4b8939.pth
```

If you want to run SAM (and competing methods) with iterative prompts, run the code with:
```
python3 prompt_gen_and_exec_v1.py --num-prompt XXX --model sam/ritm
```
where it will ask you to enter the dataset you wish to evaluate on.

Optionally, to run RITM, you need to download its weights via:
```
wget https://github.com/saic-vul/ritm_interactive_segmentation/releases/download/v1.0/coco_lvis_h32_itermask.pth
```


If you want to run SAM with the 5 mode proposed in the paper, run the code with:
```
python3 prompt_gen_and_exec_v2_allmode.py 
```
The 5 mode strategy includes (also shown in Figure 1, [![arXiv Paper](https://img.shields.io/badge/arXiv-2304.10517-orange.svg?style=flat)](https://arxiv.org/abs/2304.10517)):
- 1 point at the center of the **largest** component
- 1 point at the center of **each** component (put at most 3 points)
- 1 box sharply around the **largest** component
- 1 box sharply around **each** component (put at most 3 boxes)
- 1 box covers **all** object

## Obtaining datasets from our paper

TODO

## Adding custom datasets
To evaluate your own dataset, you need to format the dataset as: 
```
  XXX:
     images:
        abc.png
        def.png
        ...
     masks:
        abc.png
        def.png
        ...
```
where images and masks should have the same name.

## News
- 1 We have released our experimental results with detailed numerical numbers that were used to make figures in our paper; these tables are under the subfolder /experimental_results_tables.

## Citation
If you find our work to be useful for your research, please cite our paper:
```
@article{mazurowski2023segment,
  title={Segment anything model for medical image analysis: an experimental study},
  author={Mazurowski, Maciej A and Dong, Haoyu and Gu, Hanxue and Yang, Jichen and Konz, Nicholas and Zhang, Yixin},
  journal={Medical Image Analysis},
  volume={89},
  pages={102918},
  year={2023},
  publisher={Elsevier}
}
```
