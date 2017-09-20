# docker
学习docker，配置lnmp环境

SECURECRT  

docker-machine  ls  
docker-machine  ip  

192.168.99.100  

默认的用户名和密码是： docker/tcuser  

一、镜像加速
http://29c4b907.m.daocloud.io  
Docker 中国官方镜像加速https://3vziuflx.mirror.aliyuncs.com  

1.如果你已经通过docker-machine创建了虚拟机的话  
docker-machine ssh default   
sudo sed -i "s|EXTRA_ARGS='|EXTRA_ARGS='--registry-mirror=加速地址 |g" /var/lib/boot2docker/profile   
exit   
docker-machine restart default  


sudo sed -i "s|EXTRA_ARGS='|EXTRA_ARGS='--registry-mirror=https://3vziuflx.mirror.aliyuncs.com |g" /var/lib/boot2docker/profile

sudo sed -i "s|EXTRA_ARGS='|EXTRA_ARGS='--registry-mirror=http://29c4b907.m.daocloud.io |g" /var/lib/boot2docker/profile
2.创建一台安装有Docker环境的Linux虚拟机，指定机器名称为default，同时配置Docker加速器地址。

docker-machine create --engine-registry-mirror=https://3vziuflx.mirror.aliyuncs.com -d virtualbox default
查看机器的环境配置，并配置到本地，并通过Docker客户端访问Docker服务。

docker-machine env default
eval "$(docker-machine env default)"
docker info



3.创建我们自己的镜像.

docker commit -m="Added json pip" -a="Smith" \
012dee14d242 ouruser/webapp:v2


二、本机构建docker的win环境

1.虚拟机设置共享文件夹，把项目根目录（E:/phpworkspace/LightLampV2）挂载到/data，把接收日志文件的目录的挂载到/lightlamp

2.利用docker-compose进行安装（结合编写的dockerfile文件）
运行docker-toolbox后，进入到在含有docker-compose.yml的目录下运行
docker-compose  up --build


3.配置本机的apache反向代理
<VirtualHost *:80>
   
   DocumentRoot "E:/phpworkspace/LightLampV2/public"
   ServerName wap.lightlamp.com
   ServerAlias m.lightlamp.com admin.lightlamp.com api.lightlamp.com www.lightlamp.com
   ProxyPass / http://192.168.99.100:1800/
   ProxyPassReverse / http://192.168.99.100:1800/
   ProxyPreserveHost On

</VirtualHost>

4.查看容器并进入
cd  /e/proj/lightlamp/redis
docker build -t tredis .
docker run -idt tredis /bin/bash
6b6ac80a75cc4270f73a994c470a0e3e5125329047e34f38c12ce5018e74bc3d
docker attach 6b6ac80a75cc4270f73a994c470a0e3e5125329047e34f38c12ce5018e74bc3d
