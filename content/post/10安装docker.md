---
title: "安装docker"
slug: "安装docker"
date: "2024-03-25"
created: "2024-03-25"
tags: ["docker"]
---



# 1.CentOS安装docker



## 1.卸载旧版本

```
yum remove docker \
                  docker-client \
                  docker-client-latest \
                  docker-common \
                  docker-latest \
                  docker-latest-logrotate \
                  docker-logrotate \
                  docker-selinux \
                  docker-engine-selinux \
                  docker-engine
```





## 2.安装依赖

```
 yum install -y yum-utils
```

## 3.添加 `yum` 软件源

```
yum-config-manager     --add-repo     https://mirrors.aliyun.com/docker-ce/linux/centos/docker-ce.repo
sed -i 's/download.docker.com/mirrors.aliyun.com\/docker-ce/g' /etc/yum.repos.d/docker-ce.repo
```

## 4.安装docker

```
 yum install docker-ce docker-ce-cli containerd.io
```

## 5.启动服务

```
systemctl enable docker
systemctl start docker
systemctl status docker
```

## 6.测试docker是否安装成功

```
#查看版本信息
[root@ntp-01 ~]# docker --version
Docker version 26.1.4, build 5650f9b

[root@ntp-01 ~]# docker run --rm hello-world
Unable to find image 'hello-world:latest' locally
latest: Pulling from library/hello-world
2db29710123e: Pull complete 
Digest: sha256:2498fce14358aa50ead0cc6c19990fc6ff866ce72aeb5546e1d59caac3d0d60f
Status: Downloaded newer image for hello-world:latest

Hello from Docker!
This message shows that your installation appears to be working correctly.

To generate this message, Docker took the following steps:
 1. The Docker client contacted the Docker daemon.
 2. The Docker daemon pulled the "hello-world" image from the Docker Hub.
    (amd64)
 3. The Docker daemon created a new container from that image which runs the
    executable that produces the output you are currently reading.
 4. The Docker daemon streamed that output to the Docker client, which sent it
    to your terminal.

To try something more ambitious, you can run an Ubuntu container with:
 $ docker run -it ubuntu bash

Share images, automate workflows, and more with a free Docker ID:
 https://hub.docker.com/

For more examples and ideas, visit:
 https://docs.docker.com/get-started/



```





# 2.安装docker-compose

```
curl -L https://github.com/docker/compose/releases/download/1.27.4/docker-compose-`uname -s`-`uname -m` > /usr/local/bin/docker-compose

chmod +x /usr/local/bin/docker-compose

[root@ntp-01 ~]# docker --version
Docker version 26.1.4, build 5650f9b
[root@ntp-01 ~]# docker-compose --version
docker-compose version 1.27.4, build 40524192
[root@ntp-01 ~]# ls -l /usr/local/bin/
total 11936
-rwxr-xr-x. 1 root root 12218968 Jun  7 09:07 docker-compose
[root@ntp-01 ~]# 

```



# 3.镜像加速

```
mkdir -p /etc/docker
tee /etc/docker/daemon.json <<-'EOF'
{
  "registry-mirrors": ["https://gkseqe2l.mirror.aliyuncs.com"]
}
EOF

systemctl daemon-reload
systemctl restart docker
```

1.过往工作经历
IT工程师
 主要职责：安装维护服务器硬件、优化系统性能、保障系统稳定与安全、
并且参与数据中心设备维护及库存管理。
第二份工作，技术支持工程师
  主要职责：快速响应客户咨询、解决技术问题
（如资源配置、网络延迟、安全威胁等）、编写更新知识库文档。

### 3. 遇到的问题及解决方案
- **问题**：例如，在第二份工作中遇到DoS攻击导致服务中断。
- **解决方法**：立即启动应急响应计划，利用防火墙规则阻挡恶意流量，同时分析日志文件定位攻击源并采取措施防止未来发生类似事件。
- **收获**：通过这些经历提高了紧急情况下的应对能力，增强了网络安全意识和技术处理能力。

### 4. 个人发展规划
短期目标：快速熟悉公司的工作流程，提高解决速度，提升自己在云平台架构设计和运维方面的技能。
长期目标：希望能够成为一名技术领导者，并为公司创造更大价值。

5. 对腾讯的意向度
兴趣点：腾讯作为中国领先的互联网公司之一，拥有众多高科技产品和良好的就业环境。来这里不仅可以接触到最新的技术和理念，还能获得更多的职业发展机会。

贡献：我相信我的技能和经验可以为腾讯带来积极的影响，特别是在提高IT基础设施效率和客户服务体验方面。

6. 服务态度
原则：始终以用户为中心，提供快速、专业的技术支持，确保客户满意度。
行为：积极主动地解决问题，即使面对复杂或紧急情况也能保持冷静，确保服务质量不受影响。

### 7. 为什么来深圳
原因：深圳是中国的科技创新中心之一，来这里不仅可以接触到最新的技术和理念，还能获得更多的职业发展机会。

### 8. 有什么想问的
- **问题**：对于腾讯来说，目前最重视的技术趋势是什么？公司在未来一年内有哪些重点发展方向？

希望这些回答能够帮助你准备面试或者自我介绍。如果你有更具体的需求或想要进一步细化某个部分，请随时告诉我！