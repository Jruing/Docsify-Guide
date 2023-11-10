# Centos 7 安装Mongodb社区版

## 准备环境

> 1. 操作系统：Centos 7
> 2. 安装包：https://fastdl.mongodb.org/linux/mongodb-linux-x86_64-rhel70-7.0.3.tgz
> 3. windows 可视化工具：Studio 3T（原robot 3t）/ Dbeaver CE

## 安装

1. 下载

    ```
    wget -O mongodb.tgz https://fastdl.mongodb.org/linux/mongodb-linux-x86_64-rhel70-7.0.3.tgz
    ```

2. 解压

    ```
    tar zxf mongodb.tgz
    ```

3. 创建配置文件 `mongodb.conf`

    ```
    # 数据库数据存放路径
    dbpath=/root/mongodb-linux-x86_64-rhel70-7.0.3/data/db
    # mongodb pid文件路径
    pidfilepath=/var/log/mongodb/master.pid 
    # mongodb日志存放路径
    logpath=/root/mongodb-linux-x86_64-rhel70-7.0.3/data/log/mongodb.log
    # 是否追加方式写入日志，默认True
    logappend=true
    # 端口
    port=27017
    # 是否认证
    auth=true
    # 以守护进程的方式在后台执行
    fork=true
    # 主机ip
    bind_ip=0.0.0.0
    ```

4. 启动服务

    ```
    [root@VM-24-9-centos bin]# ./mongod -f mongodb.conf  --fork
    about to fork child process, waiting until server is ready for connections.
    forked process: 30287
    child process started successfully, parent exiting
    ```

    