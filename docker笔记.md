# docker笔记

> ### 安装
>
> 桌面版：https://www.docker.com/products/docker-desktop
> 服务器版：https://docs.docker.com/engine/install/#server
>
> https://docker.easydoc.net/

1、安装桌面版时会天才cmd框安装WSL2，这个安装时间有点长

2、window安装程序里开启Hyper-V、windows虚拟机监控程序平台、适用于Linux的Windows子系统、容器。

3、桌面版程序的docker Engine里添加镜像源加速地址

"registry-mirrors": [
    "https://5tqw56kt.mirror.aliyuncs.com",
    "https://k3x0o754.mirror.aliyuncs.com",
    "https://docker.hpcloud.cloud",
    "https://docker.m.daocloud.io",
    "https://docker.1panel.live",
    "http://mirrors.ustc.edu.cn",
    "https://docker.chenby.cn",
    "https://docker.ckyl.me",
    "http://mirror.azure.cn",
    "https://hub.rat.dev"
  ]



```json
{
    "registry-mirrors": [
        "https://docker.m.daocloud.io",
        "https://mirrors.tuna.tsinghua.edu.cn/docker-hub/"
    ]
}
```



### 镜像加速源

| 镜像加速器          | 镜像加速器地址                       |
| ------------------- | ------------------------------------ |
| Docker 中国官方镜像 | https://registry.docker-cn.com       |
| DaoCloud 镜像站     | http://f1361db2.m.daocloud.io        |
| Azure 中国镜像      | https://dockerhub.azk8s.cn           |
| 科大镜像站          | https://docker.mirrors.ustc.edu.cn   |
| 阿里云              | https://ud6340vz.mirror.aliyuncs.com |
| 七牛云              | https://reg-mirror.qiniu.com         |
| 网易云              | https://hub-mirror.c.163.com         |
| 腾讯云              | https://mirror.ccs.tencentyun.com    |

```
"registry-mirrors": ["https://registry.docker-cn.com"]
```



Docker 是一款流行的容器化平台，以下是一些常用的 Docker 命令：

### 镜像相关命令

- **docker pull**：用于从镜像仓库中拉取指定的镜像，如`docker pull ubuntu:latest`，表示拉取最新版的 Ubuntu 镜像。
- **docker images**：列出本地已有的镜像，可通过此命令查看镜像的名称、标签、ID 等信息。
- **docker rmi**：删除本地的镜像，例如`docker rmi ubuntu:latest`，会删除指定标签的 Ubuntu 镜像。

### 容器相关命令

- **docker run**：用于创建并运行一个容器，如`docker run -itd --name my_ubuntu ubuntu:latest /bin/bash`，表示以交互模式在后台运行一个名为`my_ubuntu`的容器，基于`ubuntu:latest`镜像，并在容器启动时执行`/bin/bash`命令。
- **docker ps**：列出正在运行的容器，加上`-a`参数可以列出所有容器，包括已停止的容器。
- **docker stop**：停止指定的运行中的容器，如`docker stop my_ubuntu`，会停止名为`my_ubuntu`的容器。
- **docker start**：启动已停止的容器，`docker start my_ubuntu`可将名为`my_ubuntu`的容器启动。
- **docker exec**：在运行的容器中执行命令，例如`docker exec -it my_ubuntu /bin/bash`，可以进入`my_ubuntu`容器的命令行界面。
- **docker rm**：删除指定的容器，若容器正在运行，需要先停止容器才能删除，可使用`-f`参数强制删除运行中的容器。

### 网络相关命令

- **docker network create**：创建自定义网络，如`docker network create my_network`，会创建一个名为`my_network`的网络。
- **docker network ls**：列出所有的 Docker 网络。
- **docker network connect**：将容器连接到指定网络，`docker network connect my_network my_ubuntu`可将`my_ubuntu`容器连接到`my_network`网络。

### 数据卷相关命令

- **docker volume create**：创建数据卷，`docker volume create my_volume`会创建一个名为`my_volume`的数据卷。
- **docker volume ls**：列出所有的数据卷。
- **docker volume rm**：删除指定的数据卷。



这些只是 Docker 的一部分常用命令，通过这些命令可以方便地管理 Docker 镜像、容器、网络和数据卷等资源。