---
title: git基本使用
tags: [git]
categories: [git]
---
# Git

git是一个开源的分布式版本控制系统

![78952a3d9ed12b0ab9dfd13ca4c512f.png](/images/1605855011997933.png)

## 三个区域

​	工作区：处理工作的区域

​	暂存区：已完成的工作的临时存放区域，等待被提交

​	Git仓库:  最终存储区域

## 四种状态

未跟踪：不被Git所管理的文件

已修改：表示修改了文件，但还没有把结果放到暂存区

已暂存：表示对已修改文件的当前版本做了标记

已提交： 表示文件已经安全地保存在本地的Git仓库中

![image-20221215171854018](/images/image-20221215171854018.png)



## 分支

切换分支前一定要先提交



## 开源协议

GPL：

​	不允许修改后和衍生的代码作为闭源的商业软件发布和销售

​	例子：Linux

MIT：

​	目前限制最少的协议，唯一条件是必须包含原作者的许可信息

​	例子：jQuery、Node.js



## 远程仓库

上传协议：SSH、HTTPS



### SSH

实现本地仓库和Github之间免登录的加密数据传输

SSH Key 由两部分组成，分别是：

​	id_rsa (私钥文件，存放于客户端的电脑中即可)

​	id_rsa.pub（公钥文件，需要配置到Github中）