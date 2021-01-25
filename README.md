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

### 权重文件下载
预训练权重从右侧Releases中下载：将ssd_weigths.pth放入model_data文件夹下面。当然，也可以不用预训练权重，注释掉train.py中相应的代码即可。


### 多卡报错问题
目前，程序中多卡训练会出现报错问题，尚未得到解决。因此，train.py和ssd.py中要指定0号卡进行训练。

'''
    return gather(outputs, output_device, dim=self.dim)
  File "/home/ubuntu/anaconda3/envs/zpytorch/lib/python3.6/site-packages/torch/nn/parallel/scatter_gather.py", line 68, in gather
    res = gather_map(outputs)
  File "/home/ubuntu/anaconda3/envs/zpytorch/lib/python3.6/site-packages/torch/nn/parallel/scatter_gather.py", line 55, in gather_map
    return Gather.apply(target_device, dim, *outputs)
  File "/home/ubuntu/anaconda3/envs/zpytorch/lib/python3.6/site-packages/torch/nn/parallel/_functions.py", line 54, in forward
    assert all(map(lambda i: i.is_cuda, inputs))
AssertionError
'''
