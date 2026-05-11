#### 安装依赖包
yum install -y yum-utils device-mapper-persistent-data lvm2
#### 设置阿里云docker-ce镜像源
yum-config-manager --add-repo https://mirrors.aliyun.com/docker-ce/linux/centos/docker-ce.repo
#### docker-ce安装
yum install -y docker-ce
#### 启动docker并设置开机自启
#启动docker命令
systemctl start docker
#设置开机自启命令
systemctl enable docker
#查看docker版本命令
docker version
