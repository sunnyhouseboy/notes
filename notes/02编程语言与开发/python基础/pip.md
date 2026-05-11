# 一、、安装包
`pip install torch torchvision`
适合（深度学习框架和最新AI库）：
- torchvision
- transformers
- diffusers
# 二、uv
主要负责：安装 Python 包（替代 pip），快速解析依赖，生成依赖文件
## 1、安装
windows+cmd，输入：`winget install astral-sh.uv`
或打开powershell，输入：`irm https://astral.sh/uv/install.ps1 | iex`
## 2、安装包
`uv pip install torch torchvision`
## 3、保存依赖
`uv pip freeze > requirements.txt`
保存的是当前环境的python包清单
## 4、复现环境
`uv pip install -r requirements.txt`
# 三、常用包安装
## 1、PyTorch
`pip install torch torchvision torchaudio`
