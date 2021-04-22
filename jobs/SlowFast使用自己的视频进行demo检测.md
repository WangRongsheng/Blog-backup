## 按照官网步骤安装环境

https://github.com/facebookresearch/SlowFast/blob/master/INSTALL.md

## 编写json文件

在`slowfast/demo/AVA/`下创建一个新文件`ava.json`

```json
{"bend/bow (at the waist)": 0, "crawl": 1, "crouch/kneel": 2, "dance": 3, "fall down": 4, "get up": 5, "jump/leap": 6, "lie/sleep": 7, "martial art": 8, "run/jog": 9, "sit": 10, "stand": 11, "swim": 12, "walk": 13, "answer phone": 14, "brush teeth": 15, "carry/hold (an object)": 16, "catch (an object)": 17, "chop": 18, "climb (e.g., a mountain)": 19, "clink glass": 20, "close (e.g., a door, a box)": 21, "cook": 22, "cut": 23, "dig": 24, "dress/put on clothing": 25, "drink": 26, "drive (e.g., a car, a truck)": 27, "eat": 28, "enter": 29, "exit": 30, "extract": 31, "fishing": 32, "hit (an object)": 33, "kick (an object)": 34, "lift/pick up": 35, "listen (e.g., to music)": 36, "open (e.g., a window, a car door)": 37, "paint": 38, "play board game": 39, "play musical instrument": 40, "play with pets": 41, "point to (an object)": 42, "press": 43, "pull (an object)": 44, "push (an object)": 45, "put down": 46, "read": 47, "ride (e.g., a bike, a car, a horse)": 48, "row boat": 49, "sail boat": 50, "shoot": 51, "shovel": 52, "smoke": 53, "stir": 54, "take a photo": 55, "text on/look at a cellphone": 56, "throw": 57, "touch (an object)": 58, "turn (e.g., a screwdriver)": 59, "watch (e.g., TV)": 60, "work on a computer": 61, "write": 62, "fight/hit (a person)": 63, "give/serve (an object) to (a person)": 64, "grab (a person)": 65, "hand clap": 66, "hand shake": 67, "hand wave": 68, "hug (a person)": 69, "kick (a person)": 70, "kiss (a person)": 71, "lift (a person)": 72, "listen to (a person)": 73, "play with kids": 74, "push (another person)": 75, "sing to (e.g., self, a person, a group)": 76, "take (an object) from (a person)": 77, "talk to (e.g., self, a person, a group)": 78, "watch (a person)": 79}
```

## 修改yaml文件

打开 `/slowfast/demo/AVA/`中打开`SLOWFAST_32x2_R101_50_50.yaml`

```html
TRAIN:
  ENABLE: False
  DATASET: ava
  BATCH_SIZE: 16
  EVAL_PERIOD: 1
  CHECKPOINT_PERIOD: 1
  AUTO_RESUME: True
  CHECKPOINT_FILE_PATH: "/home/slowfast/configs/AVA/c2/SLOWFAST_32x2_R101_50_50.pkl"  #path to pretrain model
  CHECKPOINT_TYPE: pytorch
DATA:
  NUM_FRAMES: 32
  SAMPLING_RATE: 2
  TRAIN_JITTER_SCALES: [256, 320]
  TRAIN_CROP_SIZE: 224
  TEST_CROP_SIZE: 256
  INPUT_CHANNEL_NUM: [3, 3]
DETECTION:
  ENABLE: True
  ALIGNED: False
AVA:
  BGR: False
  DETECTION_SCORE_THRESH: 0.8
  TEST_PREDICT_BOX_LISTS: ["person_box_67091280_iou90/ava_detection_val_boxes_and_labels.csv"]
SLOWFAST:
  ALPHA: 4
  BETA_INV: 8
  FUSION_CONV_CHANNEL_RATIO: 2
  FUSION_KERNEL_SZ: 5
RESNET:
  ZERO_INIT_FINAL_BN: True
  WIDTH_PER_GROUP: 64
  NUM_GROUPS: 1
  DEPTH: 101
  TRANS_FUNC: bottleneck_transform
  STRIDE_1X1: False
  NUM_BLOCK_TEMP_KERNEL: [[3, 3], [4, 4], [6, 6], [3, 3]]
  SPATIAL_DILATIONS: [[1, 1], [1, 1], [1, 1], [2, 2]]
  SPATIAL_STRIDES: [[1, 1], [2, 2], [2, 2], [1, 1]]
NONLOCAL:
  LOCATION: [[[], []], [[], []], [[6, 13, 20], []], [[], []]]
  GROUP: [[1, 1], [1, 1], [1, 1], [1, 1]]
  INSTANTIATION: dot_product
  POOL: [[[2, 2, 2], [2, 2, 2]], [[2, 2, 2], [2, 2, 2]], [[2, 2, 2], [2, 2, 2]], [[2, 2, 2], [2, 2, 2]]]
BN:
  USE_PRECISE_STATS: False
  NUM_BATCHES_PRECISE: 200
SOLVER:
  MOMENTUM: 0.9
  WEIGHT_DECAY: 1e-7
  OPTIMIZING_METHOD: sgd
MODEL:
  NUM_CLASSES: 80
  ARCH: slowfast
  MODEL_NAME: SlowFast
  LOSS_FUNC: bce
  DROPOUT_RATE: 0.5
  HEAD_ACT: sigmoid
TEST:
  ENABLE: False
  DATASET: ava
  BATCH_SIZE: 8
DATA_LOADER:
  NUM_WORKERS: 2
  PIN_MEMORY: True

NUM_GPUS: 1
NUM_SHARDS: 1
RNG_SEED: 0
OUTPUT_DIR: .
# 修改部分在这！！！
#TENSORBOARD:
#  MODEL_VIS:
#    TOPK: 2
DEMO:
  ENABLE: True
  LABEL_FILE_PATH: "/home/slowfast/demo/AVA/ava.json"
  INPUT_VIDEO: "/home/slowfast/Vinput/2.mp4"
  OUTPUT_FILE: "/home/slowfast/Voutput/1.mp4"

  DETECTRON2_CFG: "COCO-Detection/faster_rcnn_R_50_FPN_3x.yaml"
  DETECTRON2_WEIGHTS: detectron2://COCO-Detection/faster_rcnn_R_50_FPN_3x/137849458/model_final_280758.pkl
```

下面这一行代码存放的是输入视频的位置，当然`Vinput`这个文件夹是我自己建的
```html
INPUT_VIDEO: "/home/slowfast/Vinput/2.mp4"
```
下面这一行代码存放的是检测后视频的位置，当然`Voutput`这个文件夹是我自己建的
```html
OUTPUT_FILE: "/home/slowfast/Voutput/1.mp4"
```

## 下载预训练模型

下载地址：https://github.com/facebookresearch/SlowFast/blob/master/MODEL_ZOO.md

下载`AVA`部分下的`MAP`为`29.1`的模型，并放在`/slowfast/configs/AVA/c2/`下

修改`/slowfast/demo/AVA/`下文件`SLOWFAST_32x2_R101_50_50.yaml`里修改如下：
```html
TRAIN:
  ENABLE: False
  DATASET: ava
  BATCH_SIZE: 16
  EVAL_PERIOD: 1
  CHECKPOINT_PERIOD: 1
  AUTO_RESUME: True
  CHECKPOINT_FILE_PATH: "/home/slowfast/configs/AVA/c2/SLOWFAST_32x2_R101_50_50.pkl"  #path to pretrain model
  CHECKPOINT_TYPE: pytorch
```

## 开始运行

```html
cd /slowfast/

python tools/run_net.py --cfg demo/AVA/SLOWFAST_32x2_R101_50_50.yaml
```

## 参考

https://blog.csdn.net/WhiffeYF/article/details/113527759

https://www.bilibili.com/video/BV1Pt4y1B7N9

https://space.bilibili.com/28018062
