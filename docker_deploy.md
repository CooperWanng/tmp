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
- 离线安装
  ```
  device-mapper-persistent-data.x86_64 0:0.8.5-3.el7_9.2
  lvm2.x86_64 7:2.02.187-6.el7_9.5
  yum-utils.noarch 0:1.1.31-54.el7_8               
  device-mapper.x86_64 7:1.02.170-6.el7_9.5
  device-mapper-event.x86_64 7:1.02.170-6.el7_9.5
  device-mapper-event-libs.x86_64 7:1.02.170-6.el7_9.5       
  device-mapper-libs.x86_64 7:1.02.170-6.el7_9.5
  lvm2-libs.x86_64 7:2.02.187-6.el7_9.5
  
  container-selinux-2.119.2-1.911c772.el7_8.noarch.rpm
  docker-buildx-plugin-0.10.4-1.el7.x86_64.rpm
  containerd.io-1.6.21-3.1.el7.x86_64.rpm
  docker-ce-23.0.6-1.el7.x86_64.rpm
  docker-ce-cli-23.0.6-1.el7.x86_64.rpm
  fuse-overlayfs-0.7.2-6.el7_8.x86_64.rpm
  slirp4netns-0.4.3-4.el7_8.x86_64.rpm
  fuse3-libs-3.6.1-4.el7.x86_64.rpm
  docker-compose-plugin-2.17.3-1.el7.x86_64.rpm
  docker-ce-rootless-extras-23.0.6-1.el7.x86_64.rpm
  
  rpm -ivh *.rpm

  ```
- docker服务配置
  ```

systemctl start docker systemctl enable docker

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

systemctl restart docker # 重启docker

  ```
- push、pull
  ```

# 将镜像打新tag标记到私有仓库后再推送

docker tag <image>:<tag> <host>:<port>/<image>:<tag>
docker push <host>:<port>/<image>:<tag>

# 拉取镜像

docker pull <host>:<port>/<image-name>:<image-tag>

  ```
