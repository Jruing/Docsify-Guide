# Centos 7 编译安装Python

## 环境准备

> 操作系统：Centos 7
>
> 版本：Python 3.12

## 下载

```
wget https://www.python.org/ftp/python/3.12.0/Python-3.12.0.tgz
```

## 编译安装

```
# 安装依赖
yum -y install gcc zlib zlib-devel libffi libffi-devel readline-devel openssl-devel openssl11 openssl11-devel

# 解压
tar -zxvf Python-3.12.0.tgz
cd cd Python-3.12.0/
# 编译安装
./configure --prefix=/usr/python --with-ssl
make && make install
# 软连接
ln -s /usr/python/bin/python3 /usr/bin/python3
ln -s /usr/python/bin/pip3 /usr/bin/pip3
```

## 验证

```
[python@localhost nomarl_env]$ python3
Python 3.12.0 (main, Nov 15 2023, 08:35:30) [GCC 4.8.5 20150623 (Red Hat 4.8.5-44)] on linux
Type "help", "copyright", "credits" or "license" for more information.
>>> 


[python@localhost nomarl_env]$ pip3 -V
pip 23.2.1 from /usr/python/lib/python3.12/site-packages/pip (python 3.12)
```

