# 环境离线安装

由于我们的服务器是离线的，所以安装环境也将是在离线情况下安装，这里就要求我们熟悉`pip`,`conda`的离线安装方法。

我们首先安装conda环境，在这里我已经预先下载好了miniconda的包位于`/mnt/data/analysis/downloads/./Miniconda3-py38_23.1.0-1-Linux-x86_64.sh`下，我们输入

```shell
bash /mnt/data/analysis/downloads/./Miniconda3-py38_23.1.0-1-Linux-x86_64.sh
```

一路enter确认安装即可，注意安装完后，我们需要刷新一下环境

```shell
source ~/.bashrc
```



## 1. pip离线安装

我们首先需要一台可以联网的linux服务器，要求系统最好是Ubuntu18.04, x86_64架构，这里推荐`恒源云`和`矩池云`。我们在可以联网的服务器上（这里我一般打开平台给的jupyter-lab实例，然后选择terminal免去登陆的烦恼）

然后我们使用pip download下载包的安装包

```shell
pip download Pyomic -d ./ 
```

例如`Pyomic`是我们要下载的包，`-d`指定了包的下载目录，`./`代表当前目录，然后会把这个包相关的所有依赖项一起下载下来，然后我们使用`sftp`传输到服务器上，我们建议文件传输好后，移动到`/mnt/data/leihu`目录下，`leihu`为你自己的用户名，因为`/mnt/data`目录有15TB

```shell
pip install --no-index --find-links='/mnt/data/analysis/downloads' /mnt/data/leihu/Pyomic-1.1.7-py3-none-any.whl
```

其中`--find-links`参数代表依赖项的安装目录，我提前准备了大量依赖项在`/mnt/data/analysis/downloads`下避免你们重复上传下载，但是如果你们要装新的包，可能还是得自己上传下载。

`/mnt/data/leihu/Pyomic-1.1.7-py3-none-any.whl`代表我们这次要装的包文件，通常是有`.whl`结尾的，但也不排除`.tar.gz`结尾。

## 2. Conda离线安装

Conda的离线安装比较简单，但是也比较烦，因为conda作为包管理工具，其实离线安装能力是比较弱的，并不能自动安装依赖，也可能是我不知道。所以如果不是这个包只能从conda安装，我还是建议用pip安装。

```shell
conda install --use-local /home/leihu/SEQ/gffcompare-0.12.6-h9f5acd7_0.tar.bz2
```

`--use-local`参数就是你的包的路径`/home/leihu/SEQ/gffcompare-0.12.6-h9f5acd7_0.tar.bz2`

conda的包下载我一般会在anaconda.org上搜索下载：https://anaconda.org/conda-forge/conda，然后选择适合linux以及x86_64架构的包进行下载。