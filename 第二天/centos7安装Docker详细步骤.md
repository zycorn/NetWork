# centos7安装Docker详细步骤

标签（空格分隔）： Docker安装

---

## 安装前必读
在安装 Docker 之前，先说一下配置，我这里是Centos7
Linux 内核：官方建议 3.10 以上，3.8以上貌似也可。
注意：本文的命令使用的是 root 用户登录执行，不是 root 的话所有命令前面要加 sudo
### 1.查看当前的内核版本
> uname -r

![image_1g3vk8u1ckvn3j7sas1obttqj9.png-905.1kB][1]
### 2.使用 root 权限更新 yum 包（生产环境中此步操作需慎重，看自己情况，学习的话随便搞）
> yum -y update

### 3.卸载旧版本（如果之前安装过的话）
> yum remove docker  docker-common docker-selinux docker-engine

## 安装步骤
### 1.安装需要的软件包， yum-util 提供yum-config-manager功能，另两个是devicemapper驱动依赖
> yum install -y yum-utils device-mapper-persistent-data lvm2

### 2.设置 yum 源
> yum-config-manager --add-repo http://mirrors.aliyun.com/docker-ce/linux/centos/docker-ce.repo

![image_1g3vkr3g7191r1tb510o26ivsmt9.png-1011.6kB][2]
> 如上图，表示安装成功

### 3.查看可用docker版本有哪些
> yum list docker-ce --showduplicates | sort -r

![image_1g3vktcht1bm017491q7ga4u1pvpm.png-1019kB][3]
### 4.选择一个版本并安装
> yum -y install docker-ce-18.03.1.ce

### 5.出现下图说明安装成功
![image_1g3vl5kd1jd21i58fca1and15pi1g.png-999.3kB][4]
### 6.启动 Docker 并设置开机自启
> systemctl start docker
systemctl enable docker

![image_1g3vl77ft1imuqev1bt11o5ra8p9.png-999.2kB][5]


  [1]: http://static.zybuluo.com/corn/8gj2g6lg8gbo1eee102lrq5t/image_1g3vk8u1ckvn3j7sas1obttqj9.png
  [2]: http://static.zybuluo.com/corn/4k213wwbop5ttas9krziok6c/image_1g3vkr3g7191r1tb510o26ivsmt9.png
  [3]: http://static.zybuluo.com/corn/3fp72j8h3m4wkhb6lfig6f6e/image_1g3vktcht1bm017491q7ga4u1pvpm.png
  [4]: http://static.zybuluo.com/corn/6jmyal2oyqdgrnnf6sx90502/image_1g3vl5kd1jd21i58fca1and15pi1g.png
  [5]: http://static.zybuluo.com/corn/qv6zux0km21u56nweghdr5yg/image_1g3vl77ft1imuqev1bt11o5ra8p9.png