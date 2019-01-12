# 环境准备
---
## 主机
可以用虚拟机（VirtualBox/Ubuntu 16.04），桥接网络，规划IP地址。例如：

|hostname|ip	|  |
| ------| ----- |---|
|iota-m1|10.8.25.100|kubernetes master|
|iota-n1|10.8.25.150|node|
| ... |    |   |

## 基础准备
规划好节点名称和ip，并修改所有机器的/etc/hosts文件，添加必要的记录
例如：

```

10.8.25.100 iota-m1
10.8.25.150 iota-n1

```
> 在所有机器上，以root用户执行以下命令

## apt支持HTTPS源

```
apt-get update && apt-get install -y apt-transport-https
```
