title: 什么？OSS存储你还在用FastDFS？MinIO了解一下！！！
author: strongant
tags: 'OSS，Java,云存储'
date: 2020-05-05 15:13:09
---

## 什么是MinIO ？

根据官方定义：

  1. MinIO 是在 Apache License v2.0 下发布的对象存储服务器。 它与 Amazon S3 云存储服务兼容。 它最适合存储非结构化数据，如照片，视频，日志文件，备份和容器/ VM 映像。 对象的大小可以从几 KB 到最大 5TB。

2. MinIO 服务器足够轻，可以与应用程序堆栈捆绑在一起，类似于 NodeJS，Redis 和 MySQL。
3. 一种高性能的分布式对象存储服务器，用于大型数据基础设施。它是机器学习和其他大数
   据工作负载下 Hadoop HDFS 的理想 s3 兼容替代品。



## 为什么需要MinIO？

1. Minio 有良好的存储机制
2. Minio 有很好纠删码的算法与擦除编码算法
3. 拥有RS code 编码数据恢复原理
4. 公司做强做大时，数据的拥有重要性，对数据治理与大数据分析做准备。
5. 搭建自己的一套文件系统服务,对文件数据进行安全保护。
6. 拥有自己的平台，不限于其他方限制。



## MinIO 和其他OSS存储解决方案各有什么优缺点？
  这里主要针对Ceph、Minio、FastDFS 热门的存储解决方案进行比较。
  ### Ceph
  **优点**
  * 成熟
  * 红帽继子，ceph创始人已经加入红帽
  * 国内有所谓的ceph中国社区，私人机构，不活跃，文档有滞后，而且没有更新的迹象。
  * 从git上提交者来看，中国有几家公司的程序员在提交代码，星辰天合，easystack, 腾讯、阿里基于ceph在做云存储，但是在开源社区中不活跃，阿里一位叫liupan的有参与
  * 功能强大
  * 支持数千节点
  * 支持动态增加节点，自动平衡数据分布。（TODO，需要多长时间，add node时是否可以不间断运行）
  * 可配置性强，可针对不同场景进行调优
    

  **缺点**
    学习成本高，安装运维复杂。

  ### Minio
  **优点**
  * 学习成本低，安装运维简单，开箱即用
  * 目前minio论坛推广给力，有问必答
  * 有java客户端、js客户端
  * 数据保护：分布式Minio采用 纠删码来防范多个节点宕机和位衰减bit rot。分布式Minio至少需要4个硬盘，使用分布式Minio自动引入了纠删码功能。
  * 一致性：Minio在分布式和单机模式下，所有读写操作都严格遵守read-after-write一致性模型。


   **缺点**
   * 社区不够成熟，业界参考资料较少
   * 不支持动态增加节点，minio创始人的设计理念就是动态增加节点太复杂，后续会采用其它方案来支持扩容。
  ### FastDFS
  fastdfs是阿里余庆做的一个个人项目，在一些互联网创业公司中有应用，没有官网，不活跃，6个contributors。



  ## 如何安装使用MinIO？
  ### 基于 Docker 容器使用
  * 稳定版
  ```shell
docker pull minio/minio
docker run -p 9000:9000 minio/minio server /data
  ```
  * 尝鲜版
  ```shell
docker pull minio/minio:edge
docker run -p 9000:9000 minio/minio:edge server /data
  ```

### 基于 Mac Homebrew 使用
```
brew install minio/stable/minio
minio server /data
```
### 下载二进制文件安装使用

| 操作系统    | CPU架构      | 地址                                                      |
| :---------- | :----------- | :-------------------------------------------------------- |
| Apple macOS | 64-bit Intel | https://dl.min.io/server/minio/release/darwin-amd64/minio |

```shell
chmod 755 minio
./minio server /data
```

### GNU/Linux

#### 下载二进制文件

| 操作系统  | CPU架构      | 地址                                                     |
| :-------- | :----------- | :------------------------------------------------------- |
| GNU/Linux | 64-bit Intel | https://dl.min.io/server/minio/release/linux-amd64/minio |

```shell
chmod +x minio
./minio server /data
```

### 微软Windows系统

#### 下载二进制文件

| 操作系统        | CPU架构 | 地址                                                         |
| :-------------- | :------ | :----------------------------------------------------------- |
| 微软Windows系统 | 64位    | https://dl.min.io/server/minio/release/windows-amd64/minio.exe |

```shell
minio.exe server D:\Photos
```

### FreeBSD

#### Port

使用 [pkg](https://github.com/freebsd/pkg)进行安装。

```shell
pkg install minio
sysrc minio_enable=yes
sysrc minio_disks=/home/user/Photos
service minio start
```

### 使用源码安装

采用源码安装仅供开发人员和高级用户使用,如果你还没有Golang环境， 请参考 [How to install Golang](https://golang.org/doc/install).

```shell
go get -u github.com/minio/minio
```



## 使用MinIO浏览器进行验证



安装后使用浏览器访问[http://127.0.0.1:9000](http://127.0.0.1:9000/)，如果可以访问，则表示minio已经安装成功。

![](https://tva1.sinaimg.cn/large/007S8ZIlgy1gehkyhi60yj31330neaan.jpg)



## 使用MinIO客户端 `mc`进行验证

`mc` 提供了一些UNIX常用命令的替代品，像ls, cat, cp, mirror, diff这些。 它支持文件系统和亚马逊S3云存储服务。 更多信息请参考 [mc快速入门](https://docs.min.io/docs/minio-client-quickstart-guide)  - https://docs.min.io/docs/minio-client-quickstart-guide 。

## 已经存在的数据

当在单块磁盘上部署MinIO server,MinIO server允许客户端访问数据目录下已经存在的数据。比如，如果MinIO使用`minio server /mnt/data`启动，那么所有已经在`/mnt/data`目录下的数据都可以被客户端访问到。

上述描述对所有网关后端同样有效。

## 了解更多

- [MinIO纠删码入门](https://docs.min.io/docs/minio-erasure-code-quickstart-guide)
- [`mc`快速入门](https://docs.min.io/docs/minio-client-quickstart-guide)
- [使用 `aws-cli`](https://docs.min.io/docs/aws-cli-with-minio)
- [使用 `s3cmd`](https://docs.min.io/docs/s3cmd-with-minio)
- [使用 `minio-go` SDK](https://docs.min.io/docs/golang-client-quickstart-guide)
- [MinIO文档](https://docs.min.io/)