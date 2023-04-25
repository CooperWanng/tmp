# Docker

一、docker安装(可访问外网)
- 安装依赖
  ```
  yum install -y yum-utils device-mapper-persistent-data lvm2
  ```
- 添加docker官方仓库
  ```
  yum-config-manager --add-repo https://download.docker.com/linux/centos/docker-ce.repo
  ```
- 安装docker-ce
  ```
  yum install -y docker-ce
  ```
- docker服务配置
  ```
  systemctl start docker
  systemctl enable docker
  ```

二、docker私有仓库搭建
- 确保私有仓库服务器上安装了docker
- 容器化部署私有仓库
  ```
  docker pull registry:2
  
  # 运行容器
  docker run -itd \
  -p 5000:5000 \
  --restart=always \
  --name=your-registry-name \
  -v ${PATH}:/var/lib/registry \
  registry:2
  ```
- docker配置仓库(http)
  ```
  # 在需要使用仓库的docker服务器上进行配置
  # /etc/docker/ 下创建daemon.json文件
  {
    "insecure-registries": ["<your-server-ip>:<port>"]
  }
  
  systemctl restart docker  # 重启docker
  ```
- push、pull
  ```
  # 将镜像打新tag标记到私有仓库后再推送
  docker tag <image>:<tag> <host>:<port>/<image>:<tag>
  docker push <host>:<port>/<image>:<tag>
  
  # 拉取镜像
  docker pull <host>:<port>/<image-name>:<image-tag>
  ```
