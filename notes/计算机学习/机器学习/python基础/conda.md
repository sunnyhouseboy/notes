主要负责管理：python版本，底层科学库，隔离环境
# 一、使用
## 1、验证环境
`conda --version`
## 2、创建环境
`conda create -n myenv python=3.10`
含义：
- `myenv` = 环境名字
- `python=3.10` = 指定版本
## 3、激活环境
`conda activate myenv`
## 4、安装包
`conda install numpy`
适合（环境管理和数学/基础库）：
- numpy
- PyTorch（torch）
- scipy
- pandas
- matplotlib
## 5、查看环境
`conda env list`
## 6、删除环境
`conda remove -n myenv --all`
## 7、退出环境
`conda deactivate`
## 8、保存环境
`conda env export > environment.yml`
保存的是Python包，Python版本，系统依赖
## 9、环境复现
`conda env create -f environment.yml`
环境名会保存在environment.yml中，再用环境名激活环境
如果冲突可用`conda env create -f environment.yml -n new_name`
然后用新名字激活环境
## 10、查看所有创建的环境
`conda info --envs`
## 11、更改环境安装位置以及镜像
找到`E:\soft\conda\.condarc`
写入：
`channels:`
`   https://mirrors.tuna.tsinghua.edu.cn/anaconda/pkgs/main`
`   https://mirrors.tuna.tsinghua.edu.cn/anaconda/pkgs/r`
   `defaults`

`show_channel_urls: true`

`envs_dirs:`
  `E:/soft/conda/envs`
`pkgs_dirs:`
  `E:/soft/conda/pkgs`
## 12、查看当前环境里面的包
  
  `conda list`
# 二、常用包安装
