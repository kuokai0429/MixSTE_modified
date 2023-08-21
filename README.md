# A modified version of MixSTE

Modified from official implementation of CVPR 2022 paper (**MixSTE**) and official implementation of CVPR 2022 oral paper (**PoolFormer**).

> - **MixSTE** ([Github Link](https://github.com/JinluZhang1126/MixSTE.git)) <br>
> [MixSTE: Seq2seq Mixed Spatio-Temporal Encoder for 3D Human Pose Estimation in Video](https://arxiv.org/abs/2203.00859)
> - **PoolFormer** ([Github Link](https://github.com/sail-sg/poolformer.git)) <br>
> [PoolFormer: MetaFormer Is Actually What You Need for Vision (CVPR 2022 Oral)](https://arxiv.org/abs/2111.11418)

**Note:**
> Here are core codes of our work. This work is based on the [VideoPose3D](https://github.com/facebookresearch/VideoPose3D), some fundamental codes canbe found there. At the same time, We are organizing codes and prepare to submit to the [mmpose](https://github.com/open-mmlab/mmpose) as soon as possible.

<br>

<p align="center"> <img src="./assets/SittingDown_s1.gif" width="80%"> </p> 
<p align="center"> Visualization of our method and ground truth on Human3.6M </p>

<br>

## 訓練資料集 Dataset

The Human3.6M dataset and HumanEva dataset setting follow the [VideoPose3D](https://github.com/facebookresearch/VideoPose3D).
Please refer to it to set up the Human3.6M dataset (under ./data directory).

The MPI-INF-3DHP dataset setting follows the [MMPose](https://github.com/open-mmlab/mmpose).
Please refer it to set up the MPI-INF-3DHP dataset (also under ./data directory).

<br>

## 資料集型態轉換 Prepare Human3.6M Dataset

```bash
cd data
python prepare_data_h36m.py --from-archive h36m.zip
cd ..
```

<br>


## 模型預測 Run Inference

**Input video length (frames) should be greater than receptive field (81, 243..).**

```bash
cd inference
python infer_video_d2.py --cfg COCO-Keypoints/keypoint_rcnn_R_101_FPN_3x.yaml --output-dir output --image-ext mp4 input
cd ..

cd data
python prepare_data_2d_custom.py -i ../inference/output -o myvideos
cd ..

python run.py --custom_2d -d custom -k myvideos -f 81 -s 81 -c checkpoint --evaluate best_epoch.bin --render --viz-subject myvideos.mp4 --viz-action custom --viz-camera 0 --viz-export output --viz-video ./inference/input/myvideos.mp4 --viz-output output.mp4 --viz-size 6
( python run.py --custom_2d -d custom -k myvideos -f 243 -s 243 -c checkpoint --evaluate checkpoint_cpn_243f_paper.bin --render --viz-subject myvideos.mp4 --viz-action custom --viz-camera 0 --viz-export output --viz-video ./inference/input/myvideos.mp4 --viz-output output.mp4 --viz-size 6 )

```

<br>


## 模型訓練 Training

```bash
python run.py -k cpn_ft_h36m_dbb -b 2048 -f 81 -s 81 -l log/run -c checkpoint -gpu 0,1 --export-training-curves
( python run.py -k cpn_ft_h36m_dbb -b 1024 -f 243 -s 243 -l log/run -c checkpoint -gpu 0,1 --export-training-curves )
```

<br>

## 結果視覺化 Visulization

Please refer to the https://github.com/facebookresearch/VideoPose3D#visualization.

<br>

## 其他

Check Note.txt for detailed command guidance.

<br>

## Acknowledgement

Thanks for the baselines, we construct the code based on them:

* PoolFormer
* MixSTE
* VideoPose3D
* SimpleBaseline
