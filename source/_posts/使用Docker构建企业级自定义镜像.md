title: 使用Docker构建企业级自定义镜像
author: strongant
tags: 'docker,镜像,harbor'
date: 2020-05-19 22:19:40
---

## 前言

  临下班前，楼主接到了一个需求，由于基础镜像标准发生变更，需要按照最新的Docker 镜像标准构建自己应用的自定义镜像。目前的标准是这样的：基础架构组只提供所有项目必须接入的3个公共镜像，这3个公共基础镜像包含了：JDK8、Skywalking、Arthas。对于各自业务组的应用如果还需要加入其它镜像，则由各个业务组自己基于基础架构组提供的公共镜像之上，再添加自定义的镜像，结构图如下：

  ![image.png](http://ww1.sinaimg.cn/large/bc9918a2gy1gey3efkciuj20pg0ksq4n.jpg)

## 构建步骤

### 编写Dockerfile

  基于最新的规范来看，我们需要编写一个Dockerfile，然后引用基础架构组提供的基础镜像，再加入应用需要的其他镜像。因此最终的 Dockerfile 文件如下：

```Dockerfile
FROM 基础镜像地址
RUN apk add 需要添加的自定义镜像
...
```



### 在Centos7下安装Docker环境



#### 卸载旧版本

较旧的 Docker 版本称为 docker 或 docker-engine 。如果已安装这些程序，请卸载它们以及相关的依赖项。

```
$ sudo yum remove docker \
         docker-client \
         docker-client-latest \
         docker-common \
         docker-latest \
         docker-latest-logrotate \
         docker-logrotate \
         docker-engine
```


####  安装 Docker Engine-Community

##### 使用 Docker 仓库进行安装

在新主机上首次安装 Docker Engine-Community 之前，需要设置 Docker 仓库。之后，您可以从仓库安装和更新 Docker。

**设置仓库**

安装所需的软件包。yum-utils 提供了 yum-config-manager ，并且 device mapper 存储驱动程序需要 device-mapper-persistent-data 和 lvm2。

```
$ sudo yum install -y yum-utils \
 device-mapper-persistent-data \
 lvm2
```

使用以下命令来设置稳定的仓库。

```
$ sudo yum-config-manager \
  --add-repo \
  https://download.docker.com/linux/centos/docker-ce.repo
```

#####  安装 Docker Engine-Community

安装最新版本的 Docker Engine-Community 和 containerd，或者转到下一步安装特定版本：

```
$ sudo yum install docker-ce docker-ce-cli containerd.io
```

如果提示您接受 GPG 密钥，请选是。

> **有多个 Docker 仓库吗？**
>
> 如果启用了多个 Docker 仓库，则在未在 yum install 或 yum update 命令中指定版本的情况下，进行的安装或更新将始终安装最高版本，这可能不适合您的稳定性需求。

Docker 安装完默认未启动。并且已经创建好 docker 用户组，但该用户组下没有用户。

**要安装特定版本的 Docker Engine-Community，请在存储库中列出可用版本，然后选择并安装：**

1、列出并排序您存储库中可用的版本。此示例按版本号（从高到低）对结果进行排序。

$ **yum list** docker-ce --showduplicates **|** **sort** -r

```docker-ce.x86_64  3:18.09.1-3.el7           docker-ce-stable
docker-ce.x86_64  3:18.09.0-3.el7           docker-ce-stable
docker-ce.x86_64  18.06.1.ce-3.el7           docker-ce-stable
docker-ce.x86_64  18.06.0.ce-3.el7           docker-ce-stable
```

2、通过其完整的软件包名称安装特定版本，该软件包名称是软件包名称（docker-ce）加上版本字符串（第二列），从第一个冒号（:）一直到第一个连字符，并用连字符（-）分隔。例如：docker-ce-18.09.1。

```shell
$ sudo yum install docker-ce-<VERSION_STRING> docker-ce-cli-<VERSION_STRING> containerd.io
```

启动 Docker。

```shell
$ sudo systemctl start docker
```

通过运行 hello-world 映像来验证是否正确安装了 Docker Engine-Community 。

```shell
$ sudo docker run hello-world
```

> 以上安装过程参考自： `https://www.runoob.com/docker/centos-docker-install.html`



### 开始构建应用自定义镜像



#### 根据 Dockerfile 文件进行自定义镜像的构建

  在Dockerfile 文件所在的目录下执行如下命令进行自定义镜像的构建：

  ```
  sudo docker build -f Dockerfile -t 你的自定义镜像名称 .
  ```



#### 推送到企业私有的镜像harbor之前进行登录

```
docker login 企业私有的harbor地址
输入用户名
输入密码
完成登录
```



#### 将构建完成的自定义镜像推送到企业私有的harbor

```
sudo docker push 你的自定义镜像名称
```

### 总结

  通过 1.编写自定义构建镜像的Dockerfile 2.安装Docker环境 3.构建自定义镜像 4.上传自定义镜像到harbor 以上4个步骤，我们便完成了应用自定义镜像的构建，后续我们自己的应用中直接使用自定义镜像即可，这样做的好处就是基于基础的镜像，我们可以随意组合，构建出满足自己应用的镜像，更灵活、镜像分层管理、可扩展。
