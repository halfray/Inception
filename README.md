# Inception 
 使用vagrant创建虚拟环境,并通过Cloudera Manager 离线安装Hadoop集群

 *将需要部署的离线文件放到cloudera目录下的repo,rpm和parcel文件夹中


### 通过vagrant完成的虚拟机环境准备
在Vagrantfile中创建了4台虚拟机

- guest - 配合ansible用于在其他机器上进行环境安装
- cluster-master - 服务器主节点用于启动cloudera server
- cluster-slave1 - 从节点1
- cluster-slave2 - 从节点2

 操作系统使用centos 6.9 可以配合安装CDH5.x

*其中主节点需要运行5G的内存，从节点需要3G的内存，否则在本地无法运行*

### 通过ansible 完成的部署环境准备工作
- 环境准备
1. 关闭selinux
2. 关闭iptables
3. 安装ntp服务

- 账户准备 
1. 创建需要部署用的账号: 当前为root (必须制定密码: 当前为root)
2. 打通各账号服务器之间的免密ssh登录服务

- 拷贝离线文件 
1. copy文件到部署服务器
2. 执行rpm文件
3. 在master节点上启动db服务和server服务

### 通过Cloudera Manager安装界面进行安装
- 访问: http://192.168.42.11:7180 

   用户名: admin 密码: admin
- 不需要再勾选安装oracle java
- 服务器主机为: 192.168.42.[11-13]
- 其他基本默认即可 


### 执行命令
vagrant up

#### 查考文档
http://www.jianshu.com/p/0fb35ca8f95f
