# git 常用命令
## 一、第一次上传项目到 GitHub
> 适用于：
>
> - 新建项目
> - 本地代码第一次上传 GitHub
> - 初始化 Git 仓库
---
## 1. 初始化 Git 仓库
```bash
git init
# 让当前文件夹变成 Git 仓库
# 会生成一个隐藏的 .git 文件夹
```
## 2. 添加所有文件到暂存区
```bash
git add .
# 添加当前目录下所有文件
# "." 表示当前目录
```
## 3. 提交一次版本记录
```bash
git commit -m "Initial commit"
# 提交一次版本
# -m 后面是提交说明
# "Initial commit" 一般表示第一次提交
```
## 4. 设置主分支名称为 main
```bash
git branch -M main
# 把当前分支名称改成 main
# 现在 GitHub 默认主分支通常都是 main
```
## 5. 连接 GitHub 远程仓库
```bash
git remote add origin  https://github.com/sunnyhouseboy/notes.git
# 添加远程仓库连接  
# origin 是远程仓库默认名字
```
## 6. 推送代码到 GitHub
```bash
git push -u origin main
# 上传 main 分支到 GitHub
# -u 表示建立默认关联
# 后面再 push 时可以直接 git push
```
# 二、以后最常用的 Git 命令
## 1. 查看文件状态
```bash
git status
# 查看哪些文件被修改
# 查看哪些文件未提交
```
## 2. 添加所有修改
```bash
git add .
# 添加所有修改到暂存区
```
## 3. 提交修改
```bash
git commit -m "修改说明"
# 提交代码版本
```
## 4. 上传到 GitHub
```bash
git push
# 推送到远程仓库
```
# 三、拉取 GitHub 最新代码
## 拉取远程仓库更新
```bash
git pull
# 下载 GitHub 最新代码
# 并自动合并到本地
```
# 四、查看提交记录
```bash
git log
# 查看历史提交记录
```
# 五、查看远程仓库地址
```bash
git remote -v
# 查看当前连接的 GitHub 仓库
```
# 六、删除远程仓库连接
```bash
git remote remove origin
# 删除当前 GitHub 仓库连接
```
# 七、克隆 GitHub 仓库
```bash
git clone 仓库地址
# 下载整个 GitHub 仓库
```
# 八、创建新分支
```bash
git branch 分支名
# 创建分支
```
# 九、切换分支
```bash
git checkout 分支名
# 切换到指定分支
```
# 十、创建并切换分支（常用）
```bash
git checkout -b 分支名
# 创建并立即切换
```
# 十一、查看当前分支
```bash
git branch
# 查看所有分支
# 当前分支前面会有 *
```
# 十二、忽略不需要上传的文件
创建：
```
.gitignore
```
例如：
```
# Python缓存
__pycache__/

# 虚拟环境
venv/

# IDE配置
.idea/

# 日志文件
*.log
```
# 十三、git代理
## 1.检查 Git 是否走代理
```bash
git config --global --get http.proxy
```
## 2.设置代理
```bash
git config --global http.proxy http://127.0.0.1:7897
git config --global https.proxy http://127.0.0.1:7897
```
## 3.取消代理
```bash
git config --global --unset http.proxy
git config --global --unset http.proxy
```