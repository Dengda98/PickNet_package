## （脚本重整理）PickNet —— 基于深度卷积网络的地震波初至拾取模型

+ Original Author: Xiao Zhuowei ([@MrXiaoXiao](https://github.com/MrXiaoXiao))

+ Modified by: Zhu Dengda ([@Dengda98](https://github.com/Dengda98))

--------------------------------------------------------
> Show the greatest respect to my senior, [@MrXiaoXiao](https://github.com/MrXiaoXiao).
>
> It was not until I myself experienced the pain that Xiao had endured that I understood:
> 
> Communicate with those who truly possess the skills and who truly care about you, rather than with those who merely seek to take credit for the achievements and then bite you back. 


原`picknet`程序是一系列脚本，未组织成`Python`安装包的形式，
故使用上会有不便，这里我做出一些修改，使之可以以`Python`包
的形式安装，**而不再要求运行在`picknet`源码路径**。这些调整
主要是为了方便我自定义拾取输入的数据。

## 下载 
1. 克隆库（体积很小，只是一些文本文件）
    ```
    git clone https://github.com/Dengda98/PickNet_package
    ```

2. 下载 picknet 程序包
    由于包含模型文件，体积较大，我压缩后上传到科技云盘，可点击 [链接](https://pan.cstcloud.cn/s/1THLjV9QRaE) 下载。
    
    下载后运行以下命令解压（解压后压缩包可删除）
    ```
    tar -xzvf picknet_modified_by_ZDD.tar.gz
    ```

    此时整个目录结构应该如下所示 ：
    ```
    .
    ├── README.md
    ├── docs
    ├── gpl-3.0.txt
    ├── picknet
    └── setup.py
    ```


## 安装方法
基本的依赖包要求详见`docs/`内的介绍，其中是原程序包的使用
说明。在虚拟环境中安装好依赖包后，在当前目录下运行
```
pip install -v .
```
即可在当前虚拟环境中安装`picknet`包。

## 修改部分 
+ 源码文件的导入改为相对导入，并给每个子文件夹添加`__init__.py`
文件，使之成为一个子包；
+ 增加`setup.py`，其中简要地包括了必要的一些参数；
+ 增加`MANIFEST.in`，使得安装包的过程中能将模型文件加入安装目录
+ 将原始的说明文档放入`docs/`目录；
+ 对`fcn.tester.Tester`类的`run`函数增加`raw_output`选项，使得
可以选择是否保存`picknet`模型的原始输出，以减少存储空间占用。
【picknet运行时的内存占用问题目前没空修改，注意每次不传入大体积数据即可】


## 关于使用
这里保留原始的配置文件方式以及运行方式。  

+ **`picknet`配置文件**  
  运行以下命令可打印出`picknet`安装包中的参考配置文件以及
  模型文件目录:
  ```
    python -m picknet.print 
  ```
  会输出5个路径：
  ```
  DEFAULT_P_CONFIG: [...]  # 拾取初至P波的配置文件
  DEFAULT_S_CONFIG: [...]  # 拾取初至S波的配置文件
  P_WAVE_MODEL:     [...]  # 拾取初至P波的模型目录
  S_WAVE_MODEL:     [...]  # 拾取初至S波的模型目录
  RUN_PY_SCRIPT:    [...]  # 运行`python -m picknet.run`的脚本路径
  ```
  故可将`picknet`参考配置文件复制到本地进行自定义修改，而模型文件可填入
  配置文件中的`save_dir`关键字。

+ **运行**  
  原说明文档中的脚本运行方式可简单替换为 
  ```
    python -m picknet.run [...]  # 后续参数设定方法不变
  ```

+ **自定义运行脚本**  
  在以上输出的路径中还包括`RUN_PY_SCRIPT`，故可复制该脚本到本地，
  再进行修改，以自定义拾取的输入数据，当然运行的方式也变为
  ```
    python -u [自定义运行脚本] [...]  # 后续参数设定方法不变
  ```

## Citation  
Wang, J.\*, **Xiao, Z.**\*, Liu, C., Zhao, D., & Yao, Z. (2019). Deep learning for picking seismic arrival times. Journal of Geophysical Research: Solid Earth, 124, 6612– 6624. https://doi.org/10.1029/2019JB017536
