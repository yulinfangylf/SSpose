## Pretraining SSpose Model

The following table provides pretrained checkpoints and logs.
| | SSpose-B|
| :---: | :---: |
| pretrained checkpoints| [download](https://drive.google.com/file/d/1gNlMpxUSpDrtxDKM3OmSda4h1IaqBUu-/view?usp=drive_link) |
| logs | [download](https://drive.google.com/file/d/153wF7AUlgNFiQnz_0lX-8OLTY9aAjge7/view?usp=drive_link) |

## Usage

### Install
- Clone this repo:

```bash
git clone https://github.com/yulinfangylf/SSpose
cd SSpose
```

- Create a conda environment and activate it:
```bash
conda create -n SSpose python=3.7
conda activate SSpose
```

- Install `Pytorch==1.8.0` and `torchvision==0.9.0` with `CUDA==11.1`

```bash
conda install pytorch==1.8.0 torchvision==0.9.0 cudatoolkit=11.1 -c pytorch -c conda-forge
```

- Install `timm==0.3.2`

```bash
pip install timm==0.3.2
```

### Data preparation

You can download the ImageNet-1K [here](https://image-net.org) and prepare the ImageNet-1K follow this format:
```tree data
imagenet
  ├── train
      ├── class1
      │   ├── img1.jpeg
      │   ├── img2.jpeg
      │   └── ...
      ├── class2
      │   ├── img3.jpeg
      │   └── ...
      └── ...
```

### Training
To pretrain SSpose Model with multi-node distributed training, run the following on 3 nodes with 8 GPUs each:

```bash
python distributed_pretrain.py \
    --job_dir ${JOB_DIR} \
    --nodes 3 \
    --batch_size 128 \
    --model sspose_convvit_base_patch16 \
    --norm_pix_loss \
    --mask_ratio 0.75 \
    --epochs 800 \
    --warmup_epochs 40 \
    --blr 1.5e-4 --weight_decay 0.05 \
    --data_path ${IMAGENET_DIR}
```
