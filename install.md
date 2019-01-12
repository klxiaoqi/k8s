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
---
# 安装
---

> 在所有机器上，以root用户执行以下命令

## apt支持HTTPS源

```
apt-get update && apt-get install -y apt-transport-https
```

## 安装curl工具

```
apt-get install curl
```
## 增加google的安装源 key
```
curl -s https://packages.cloud.google.com/apt/doc/apt-key.gpg | apt-key add -
```
> 如果此方式失败，请手动获取 https://packages.cloud.google.com/apt/doc/apt-key.gpg 文件，存储在某目录，例如 /home/iota/k8s下，然后执行
> `apt-key add /home/iota/k8s/apt-key.gpg`

## 添加kubernetes的安装源镜像
> 使用的是ustc的镜像

```
cat <<EOF >/etc/apt/sources.list.d/kubernetes.list
deb http://mirrors.ustc.edu.cn/kubernetes/apt kubernetes-xenial main
EOF
```
## 安装 kubelet kubeadm kubectl

```
apt-get update
kubernetes-cni=0.5.1-00 kubelet=1.8.2-00 kubeadm=1.8.2-00 kubectl=1.8.2-00
```

## 获取kubernetes环境所需要的基础镜像
> 需要拉取可用的镜像，并打标签。利用的是蜂巢资源

    1 拉取所需镜像
    
```
    docker pull hub.c.163.com/ap6108/kubernetes-dashboard-init-amd64:v1.0.1
    docker pull hub.c.163.com/juranzhijia/kubernetes-dashboard-amd64:v1.7.1
    docker pull hub.c.163.com/k8s163/etcd-amd64:3.0.17
    docker pull hub.c.163.com/zhijiansd/k8s-dns-kube-dns-amd64:1.14.5
    docker pull hub.c.163.com/zhijiansd/k8s-dns-sidecar-amd64:1.14.5
    docker pull hub.c.163.com/zhijiansd/k8s-dns-dnsmasq-nanny-amd64:1.14.5
    docker pull hub.c.163.com/conformance/kube-apiserver-amd64:v1.8.2
    docker pull hub.c.163.com/conformance/kube-controller-manager-amd64:v1.8.2
    docker pull hub.c.163.com/conformance/kube-scheduler-amd64:v1.8.2
    docker pull hub.c.163.com/conformance/kube-proxy-amd64:v1.8.2
    docker pull hub.c.163.com/conformance/pause-amd64:3.0
```
    2 更改标签，以便kubeadm可以拉取到
    
    
