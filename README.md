# Kinetics-400迷你数据集
[English](/README_en.md) | 简体中文

该数据集旨在解决的问题：参照Kinetics-400数据格式，训练基于自己数据的视频理解模型。

## 数据集介绍

Kinetics-400是视频领域benchmark常用数据集，详细介绍可以参考其官方网站[Kinetics](https://deepmind.com/research/open-source/kinetics)。整个数据集包含400个类别，全部文件大概需要135G左右的存储空间，下载起来比较困难。

Tiny-Kinetics-400同样包含400个类别，每个类别下仅有两条视频数据，分为train与val，可用于调试一些视频理解模型。

具体对比如下：

| 数据集            | 训练条数 | 验证条数 | 大小 |
| ----------------- | -------- | -------- | ---- |
| Kinetics-400      | 234619   | 19761    | 135G |
| Tiny-Kinetics-400 | 400      | 400      | 420M |

## Tiny-Kinetics-400下载

目前提供了百度网盘的下载方式：

| 下载方式 | 链接                                                         |
| -------- | ------------------------------------------------------------ |
| 百度云    | [BaiduCloud](https://pan.baidu.com/s/1kpyLj4CZym_2hp-RzY1kDg?pwd=pigr )|
| Google   | [GoogleDrive](https://drive.google.com/drive/folders/1OVDtdqNnOrzZ6PfoWMUNrsqvPijWHMCD?usp=sharing)|

## 抽帧Extract Frames

通常在训练视频理解模型时，会提前对视频文件进行抽帧，以此来加速训练过程。这里提供了抽帧脚本，且满足以下条件：

- 每个视频只抽取300帧
- 如果整个视频多于300帧，直接舍弃之后的视频帧
- 如果整个视频少于300帧，复制最后的视频帧以填充至300帧

使用方式：

```shell
python ./tools/extract_frames.py --source_dir ~/data/tiny-kinetics-400 ~/data/kinetics400_30fps_frames
```

将meta文件移到视频帧目录下：

```shell
mv ./annotations/tiny_train.csv ~/data/kinetics400_30fps_frames/
mv ./annotations/tiny_val.csv ~/data/kinetics400_30fps_frames/
```

最终的目录结构如下：

```
kinetics400_30fps_frames/
├── abseiling/
│   ├──_4YTwq0-73Y_000044_000054
│   │  ├──frame_00001.jpg
│   │  ├──...
│   ├──...
├──...
├── tiny_train.csv
├── tiny_val.csv
```


## 参考

- [PaddleVideo](https://github.com/PaddlePaddle/PaddleVideo/blob/develop/docs/zh-CN/dataset/k400.md)
- [video-contrastive-learning](https://github.com/amazon-research/video-contrastive-learning)

