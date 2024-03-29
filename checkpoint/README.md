# A revised version of MixSTE

Revised from official implementation of CVPR 2022 paper (**MixSTE**) and official implementation of CVPR 2022 oral paper (**PoolFormer**).

> - **MixSTE** ([Github Link](https://github.com/JinluZhang1126/MixSTE.git)) <br>
> [MixSTE: Seq2seq Mixed Spatio-Temporal Encoder for 3D Human Pose Estimation in Video](https://arxiv.org/abs/2203.00859)
> - **PoolFormer** ([Github Link](https://github.com/sail-sg/poolformer.git)) <br>
> [PoolFormer: MetaFormer Is Actually What You Need for Vision (CVPR 2022 Oral)](https://arxiv.org/abs/2111.11418)

**Note:**
> Here are core codes of our work. This work is based on the [VideoPose3D](https://github.com/facebookresearch/VideoPose3D), some fundamental codes canbe found there. At the same time, We are organizing codes and prepare to submit to the [mmpose](https://github.com/open-mmlab/mmpose) as soon as possible.

<br>

<p align="center"> <img src="./assets/SittingDown_s1.gif" width="80%"> </p> 
<p align="center"> Visualization of our method and ground truth on Human3.6M </p>

## Environment

The code is conducted under the following environment:

* Ubuntu 18.04
* Python 3.6.10
* PyTorch 1.8.1
* CUDA 10.2

You can create the environment as follows:

```bash
conda env create -f requirements.yml
```

## Dataset

The Human3.6M dataset and HumanEva dataset setting follow the [VideoPose3D](https://github.com/facebookresearch/VideoPose3D).
Please refer to it to set up the Human3.6M dataset (under ./data directory).

The MPI-INF-3DHP dataset setting follows the [MMPose](https://github.com/open-mmlab/mmpose).
Please refer it to set up the MPI-INF-3DHP dataset (also under ./data directory).

## Evaluation

* [ ] Download the checkpoints from [Baidu Disk](https://pan.baidu.com/s/1Gu7ItpkU0Q7SF_QVmlQ15A)(wnjf);

Then run the command below (evaluate on 243 frames input):

> python run.py -k cpn_ft_h36m_dbb -c <checkpoint_path> --evaluate <checkpoint_file> -f 243 -s 243

## Training from scratch

Training on the 243 frames with two GPUs:

>  python run.py -k cpn_ft_h36m_dbb -f 243 -s 243 -l log/run -c checkpoint -gpu 0,1

if you want to take place of attention module with more efficient attention design, please refer to the rela.py, routing_transformer.py, and linearattention.py. These efficient design are coming from previous works:

- https://github.com/rishikksh20/rectified-linear-attention
- https://github.com/lucidrains/routing-transformer
- https://arxiv.org/abs/2006.04768

## Visulization

Please refer to the https://github.com/facebookresearch/VideoPose3D#visualization.

## Acknowledgement

Thanks for the baselines, we construct the code based on them:

* PoolFormer
* MixSTE
* VideoPose3D
* SimpleBaseline

<br>

```BibTeX
@InProceedings{Zhang_2022_CVPR,
    author    = {Zhang, Jinlu and Tu, Zhigang and Yang, Jianyu and Chen, Yujin and Yuan, Junsong},
    title     = {MixSTE: Seq2seq Mixed Spatio-Temporal Encoder for 3D Human Pose Estimation in Video},
    booktitle = {Proceedings of the IEEE/CVF Conference on Computer Vision and Pattern Recognition (CVPR)},
    month     = {June},
    year      = {2022},
    pages     = {13232-13242}
}
```

```Bibtex
@inproceedings{yu2022metaformer,
  title={Metaformer is actually what you need for vision},
  author={Yu, Weihao and Luo, Mi and Zhou, Pan and Si, Chenyang and Zhou, Yichen and Wang, Xinchao and Feng, Jiashi and Yan, Shuicheng},
  booktitle={Proceedings of the IEEE/CVF Conference on Computer Vision and Pattern Recognition},
  pages={10819--10829},
  year={2022}
}
```
