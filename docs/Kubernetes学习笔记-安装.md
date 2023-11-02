# Kubernetes学习笔记-安装

## 准备工作

> 操作系统：Centos 7.6
>
> 容器环境：Docker
>
> 所需工具：kubectl，minikube
>

## 安装Docker

```
# 安装yum工具包
yum -y install yum-utils
# 添加yum源
yum-config-manager --add-repo http://mirrors.aliyun.com/docker-ce/linux/centos/docker-ce.repo
# 安装docker社区版
yum install docker-ce
# 查看docker版本
docker -v
# 镜像加速（国内使用）
cat << EOF > /etc/docker/daemon.json 
{
    "registry-mirrors": [
        "https://mirror.ccs.tencentyun.com"
   ]
 }
EOF
# 重载配置
systemctl daemon-reload
# 启动docker服务
systemctl start docker
# 验证docker是否可以正常使用
[root@VM-24-9-centos ~]# docker ps
CONTAINER ID   IMAGE     COMMAND   CREATED   STATUS    PORTS     NAMES
```

## 安装kubectl

```
# 下载
wget "https://storage.googleapis.com/kubernetes-release/release/v1.18.8/bin/linux/amd64/kubectl"
# 赋权
chmod 777 kubectl 
# 添加到环境变量
mv kubectl /usr/local/bin
```

## 安装minikube

```shell
# 下载minikube
curl -LO https://storage.googleapis.com/minikube/releases/latest/minikube-linux-amd64
# 添加到环境变量
sudo install minikube-linux-amd64 /usr/local/bin/minikube

# 正常启动（如果使用root用户启动则需要追加 --force）
minikube start
# 指定minikube使用docker启动
minikube start --driver=docker
# 将docker设置为minikube启动时默认使用的驱动
minikube config set driver docker
```

## 验证

```
# 创建deployment
kubectl create deployment hello-node --image=registry.k8s.io/e2e-test-images/agnhost:2.39 -- /agnhost netexec --http-port=8080
# 查看pod
[root@VM-8-17-centos ~]# kubectl get pods
NAME                        READY   STATUS             RESTARTS   AGE
hello-node-6fd6f4b7-2fkxk   0/1     ImagePullBackOff   0          84m
```





