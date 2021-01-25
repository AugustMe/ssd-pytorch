# ssd-pytorch

### 主要环境
torch == 1.2.0

### 需要修改的地方

1. 首先，将自己准备的图片和对应的标签分别放入VOCdevkit/VOC2007/JPEGImages和VOCdevkit/VOC2007/Annotations，ImageSets文件夹不需要动，该文件夹用于存放后面运行py文件生成的txt。将数据集准备好后，运行voc2ssd.py（根据自己的需要修改生成训练集、测试集的比例），分别在/ImageSets/Main/生成train.txt、trainval.txt、val.txt和test.txt。

2. 然后，运行voc_annotation.py，生成2007_train.txt、2007_val.txt和2007_test.txt，如果有的txt为空，表示前期运行voc2ssd.py时，代码中数据比例配比的问题，根据自己的需要进行修改即可。

3. 修改utils/config.py里面num_classes,这里必须要进行修改。model_data/voc_classes.txt，修改成自己数据集的类，并在model_data文件夹下存放预训练好的权重文件。

4. 运行训练代码，python train.py

### 参考

https://github.com/bubbliiiing/ssd-pytorch
