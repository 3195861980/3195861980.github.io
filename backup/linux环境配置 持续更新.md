#  前要说明
前两天在阿里云免费领取了一台长达一年的云服务器，主要用来跑一些自己写的小项目和开源项目，配环境是一个头疼的事情，以防以后忘记，下面来记录一下。

# JAVA环境
>  现在java跑的大多的都是Spring boot 项目，需要配置的东西包如下

- JDK  -> 我这边采用JDK17 有很多新特性，而且Spring3 都是基于17封装的
- MAVEN -> 依赖管理的打包工具。目前最新的稳定版 3.9.8

这边用到一个工具 **[SDKMAN](https://sdkman.io/)**

下面给出两个系统安装  **[SDKMAN](https://sdkman.io/)** 的指令

1.ubentu
```shell
echo 'export SDKMAN_DIR="/opt/sdkman"' >> ~/.bashrc
source ~/.bashrc
apt update
apt-get install  zip unzip
curl -s "https://get.sdkman.io" | bash
source "$SDKMAN_DIR/bin/sdkman-init.sh"
``` 
2.centos
```shell
echo 'export SDKMAN_DIR="/opt/sdkman"' >> ~/.bashrc
source ~/.bashrc
yum update
yum install  zip unzip
curl -s "https://get.sdkman.io" | bash
source "$SDKMAN_DIR/bin/sdkman-init.sh"
``` 
> 修改 **SDKMAN_DIR**  进行自定义安装路径
> 查看 **[SDKMAN](https://sdkman.io/)** 是否安装成功   -> sdk version

![image](https://github.com/3195861980/3195861980.github.io/assets/38883647/5e95f622-b269-4167-801e-f766a4dc5f05)

 

安装JDk 
```shell
sdk install java 17.0.11-tem
```
> 查看JDK是否安装成功    java  --version

![image](https://github.com/3195861980/3195861980.github.io/assets/38883647/b95f1aa3-a6ea-4fe0-8b31-3a01c7d65ae0)

安装MAVEN
```shell
sdk install maven  3.9.8
```
> 查看MAVEN是否安装成功   mvn  --version
 
![image](https://github.com/3195861980/3195861980.github.io/assets/38883647/a538e766-6ab0-4dd0-ae47-d991e2c9b641)

#  python
1. 下载python安装包 
[地址抵达](https://www.python.org/ftp/python/) 这里面可以选择需要的版本 
2. 使用 wget命令 获取安装包 下载**.tgz** 文件 即可
如下
```shell
wget https://www.python.org/ftp/python/3.9.7/Python-3.9.7.tgz

``` 
3. 解压
```shell
tar -zxvf Python-3.9.7.tgz

``` 
4. 安装
```shell
cd Python-3.9.7
./configure --prefix=/usr/local/python3
make && make install

``` 
等待安装完成

5. 建立软连接
```shell
ln -s /usr/local/python3/bin/python3.9 /usr/bin/python
ln -s /usr/local/python3/bin/pip3.9 /usr/bin/pip
``` 
参考博文 [链接1](https://blog.csdn.net/qq_42571592/article/details/122902266)


#  node
1.通过包管理器
```  shell
sudo apt-get install nodejs
sudu yum install nodejs
```
2.  通过官方命令  
``` shell

# installs nvm (Node Version Manager)
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.7/install.sh | bash

# download and install Node.js (you may need to restart the terminal)
nvm install 20

# verifies the right Node.js version is in the environment
node -v # should print `v20.15.0`

# verifies the right NPM version is in the environment
npm -v # should print `10.7.0`
```
3. 通过docker

``` shell
# NOTE:
# Docker is not a Node.js package manager. Please ensure it is already installed
# on your system. Follow official instructions at https://docs.docker.com/desktop/
# Docker images are provided officially at https://github.com/nodejs/docker-node/

# pulls the Node.js Docker image
docker pull node:20-alpine

# verifies the right Node.js version is in the environment
docker run node:20-alpine node -v # should print `v20.15.0`

# verifies the right NPM version is in the environment
docker run node:20-alpine npm -v # should print `10.7.0`
```

# go
1.通过包管理器 
``` shell
dnf  install go
yum install go
apt-get install go

```
2. 官网下载 
官网下载linux 版本的 .tar 文件
解压tar文件
配置环境变量
``` shell
export PATH=$PATH:/usr/local/go/bin

source ~/.bashrc
source ~/.bashrc

``` 


# 数据库 

##  mysql 
1.包管理器 
我使用的是alibaba linux3 可用的包管理器有yum 和dnf 
``` shell 
dnf install mysql
yum install mysql
#  ubentu
apt-get install mysql-server

```
2.通过docker

##

### 1\. 拉取 MySQL Docker 镜像

从 Docker Hub 拉取 MySQL 官方镜像：

```bash
sudo docker pull mysql:latest
```

### 2\. 运行 MySQL 容器

使用以下命令启动一个 MySQL 容器。你可以根据需要自定义 `MYSQL_ROOT_PASSWORD` 和其他环境变量：

```bash
sudo docker run --name mysql-container -e MYSQL_ROOT_PASSWORD=my-secret-pw -d mysql:latest
```

### 3\. 检查 MySQL 容器状态

确保容器已成功启动：

```bash
sudo docker ps
```

你应该会看到 MySQL 容器正在运行。

### 4\. 连接到 MySQL 容器

你可以通过 `docker exec` 命令连接到运行中的 MySQL 容器并访问 MySQL 客户端：

```bash
sudo docker exec -it mysql-container mysql -u root -p
```

系统将提示你输入在启动容器时设置的 `MYSQL_ROOT_PASSWORD`。输入密码后，你将进入 MySQL 命令行界面。

### 5\. 持久化数据（可选）

为了确保数据在容器重启或删除时不丢失，可以将 MySQL 数据目录挂载到主机目录：

```bash
sudo docker run --name mysql-container -e MYSQL_ROOT_PASSWORD=my-secret-pw -v /my/own/datadir:/var/lib/mysql -d mysql:latest
```

在这个命令中，`/my/own/datadir` 是主机上的目录，将用来持久化 MySQL 数据。

### 6\. 配置网络（可选）

如果你需要配置自定义网络以便其他容器或主机访问 MySQL，可以创建一个 Docker 网络并将 MySQL 容器连接到该网络：

```bash
# 创建自定义网络
sudo docker network create my-network

# 运行 MySQL 容器并连接到自定义网络
sudo docker run --name mysql-container --network my-network -e MYSQL_ROOT_PASSWORD=my-secret-pw -d mysql:latest
```



##  redis
安装 Redis，可以通过以下步骤完成：

### 1\. 更新系统

首先，确保你的系统是最新的：

```bash
sudo yum update -y
```

### 2\. 安装编译工具和依赖

Redis 需要一些编译工具和依赖包：

```bash
sudo yum install -y gcc make
```

### 3\. 下载 Redis 源码

前往 Redis 官方网站下载最新版本的 Redis 源码，或者使用 `wget` 命令下载：

```bash
wget http://download.redis.io/releases/redis-6.2.6.tar.gz
```

注意：可以替换 `6.2.6` 为 Redis 的最新版本号。

### 4\. 解压源码包

解压下载的 Redis 源码包：

```bash
tar xzf redis-6.2.6.tar.gz
cd redis-6.2.6
```

### 5\. 编译 Redis

进入 Redis 源码目录后，编译 Redis：

```bash
make
```

编译完成后，可以通过运行以下命令来测试编译是否成功：

```bash
make test
```

### 6\. 安装 Redis

编译完成后，安装 Redis：

```bash
sudo make install
```

### 7\. 配置 Redis

默认情况下，Redis 的配置文件位于 `redis-6.2.6` 目录中，名为 `redis.conf`。你可以根据需要编辑此配置文件。

例如，可以使用以下命令编辑配置文件：

```bash
sudo nano redis.conf
```

### 8\. 运行 Redis

可以直接从命令行启动 Redis：

```bash
redis-server redis.conf
```

### 9\. 设置 Redis 为后台服务

为了方便管理，可以将 Redis 配置为后台服务。首先，创建一个系统服务文件：

```bash
sudo nano /etc/systemd/system/redis.service
```

在文件中添加以下内容：

```ini
[Unit]
Description=Redis In-Memory Data Store
After=network.target

[Service]
User=nobody
Group=nogroup
ExecStart=/usr/local/bin/redis-server /path/to/redis.conf
ExecStop=/usr/local/bin/redis-cli shutdown
Restart=always

[Install]
WantedBy=multi-user.target
```

确保将 `/path/to/redis.conf` 替换为你的实际 Redis 配置文件路径。

### 10\. 启动并启用 Redis 服务

启动 Redis 服务：

```bash
sudo systemctl start redis
```

设置 Redis 开机自启：

```bash
sudo systemctl enable redis
```

### 11\. 检查 Redis 状态

确保 Redis 服务已成功启动并正在运行：

```bash
sudo systemctl status redis
```


##  docker
### 1\. 安装 Docker

如果尚未安装 Docker，可以使用以下命令进行安装：

```bash
sudo yum install -y yum-utils
sudo yum-config-manager --add-repo https://download.docker.com/linux/centos/docker-ce.repo
sudo yum install -y docker-ce docker-ce-cli containerd.io
```

### 2\. 启动 Docker 并设置开机自启动

```bash
sudo systemctl start docker
sudo systemctl enable docker
```



## nginx
1\. 更新系统

首先，确保你的系统是最新的：

```bash
sudo yum update -y
```

### 2\. 安装 EPEL 仓库

Nginx 包通常包含在 EPEL（Extra Packages for Enterprise Linux）仓库中，因此需要先安装 EPEL 仓库：

```bash
sudo yum install -y epel-release
```

### 3\. 安装 Nginx

使用 `yum` 命令安装 Nginx：

```bash
sudo yum install -y nginx
```

### 4\. 启动 Nginx

安装完成后，启动 Nginx 服务：

```bash
sudo systemctl start nginx
```

### 5\. 设置 Nginx 开机自启

确保 Nginx 服务在系统启动时自动启动：

```bash
sudo systemctl enable nginx
```

### 6\. 检查 Nginx 状态

确保 Nginx 服务正在运行：

```bash
sudo systemctl status nginx
```

如果一切正常，你应该会看到 Nginx 正在运行的状态。

### 7\. 配置防火墙

如果你的服务器上启用了防火墙，需要允许 HTTP 和 HTTPS 流量通过防火墙：

```bash
sudo firewall-cmd --permanent --zone=public --add-service=http
sudo firewall-cmd --permanent --zone=public --add-service=https
sudo firewall-cmd --reload
```

### 8\. 测试 Nginx

在浏览器中访问你的服务器 IP 地址（或域名），你应该会看到默认的 Nginx 欢迎页面，地址格式为：[http://your\_server\_ip/](http://your%5C_server%5C_ip/)

### 9\. 配置 Nginx

Nginx 的主配置文件位于 `/etc/nginx/nginx.conf`，站点配置文件通常位于 `/etc/nginx/conf.d/` 目录中。你可以根据需要编辑这些配置文件。

例如，可以使用以下命令编辑主配置文件：

```bash
sudo nano /etc/nginx/nginx.conf
```

编辑站点配置文件：

```bash
sudo nano /etc/nginx/conf.d/default.conf
```

每次修改配置文件后，重新加载 Nginx 以应用更改：

```bash
sudo systemctl reload nginx
```

