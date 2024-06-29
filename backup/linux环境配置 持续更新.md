## 前要说明
前两天在阿里云免费领取了一台长达一年的云服务器，主要用来跑一些自己写的小项目和开源项目，配环境是一个头疼的事情，以防以后忘记，下面来记录一下。

## JAVA环境
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

暂时先写到java环境，其他的下次再补
## python


## node


## go



## 数据库 

###  mysql 



###  redis



##  docker



## nginx

最后更新时间 2024年6月30日03点22分