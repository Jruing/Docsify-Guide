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


## 安装mongosh

1. 下载

    ```
    wget https://downloads.mongodb.com/compass/mongodb-mongosh-2.0.2.x86_64.rpm
    ```

2. 安装

    ```
    rpm -iv mongodb-mongosh-2.0.2.x86_64.rpm
    ```

3. 配置用户

    > mongodb内置的用户角色
    >
    > 1. **read**：允许读取文档。
    >
    >     ```markdown
    >     { role: "read", db: "library", collection: "books" }
    >     ```
    >
    > 2. **readWrite**：允许读取和写入文档。
    >
    >     ```markdown
    >     { role: "readWrite", db: "library", collection: "books" }
    >     ```
    >
    > 3. **dbAdmin**：允许管理数据库。
    >
    >     ```markdown
    >     { role: "dbAdmin", db: "library" }
    >     ```
    >
    > 4. **userAdmin**：允许管理用户。
    >
    >     ```markdown
    >     { role: "userAdmin", db: "library" }
    >     ```
    >
    > 5. **clusterAdmin**：允许管理集群配置和元数据。
    >
    >     ```markdown
    >     { role: "clusterAdmin", db: "admin" }
    >     ```
    >
    > 6. **readAnyDatabase**：允许读取任何数据库的文档。
    >
    >     ```markdown
    >     { role: "readAnyDatabase", db: "library" }
    >     ```
    >
    > 7. **readWriteAnyDatabase**：允许读取和写入任何数据库的文档。
    >
    >     ```markdown
    >     { role: "readWriteAnyDatabase", db: "library" }
    >     ```
    >
    > 8. **dbAdminAnyDatabase**：允许管理任何数据库。
    >
    >     ```markdown
    >     { role: "dbAdminAnyDatabase", db: "library" }
    >     ```
    >
    > 9. **userAdminAnyDatabase**：允许管理任何数据库的用户。
    >
    >     ```markdown
    >     { role: "userAdminAnyDatabase", db: "library" }
    >     ```
    >
    > 10. **clusterAdminAnyDatabase**：允许管理任何数据库的集群配置和元数据。
    >
    >     ```markdown
    >     { role: "clusterAdminAnyDatabase", db: "library" }
    >     ```

    ```
    # 进入mongodb服务
    mongosh
    # 进入admin数据库
    use admin
    # 创建用户
    db.createUser({
      user: "adminUser",
      pwd: "adminPassword123",
      roles: [
        { role: "userAdminAnyDatabase", db: "admin" },
        { role: "dbAdminAnyDatabase", db: "admin" },
        { role: "readWriteAnyDatabase", db: "admin" }
      ]
    }
    # 校验用户密码
    db.auth("adminUser","adminPassword123")
    
    ```

    