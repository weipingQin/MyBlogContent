docker是一个容器，它像一个虚拟机类似，可以在上面运行各种不同的程序。
而且不使用的时候直接可以停止容器。

我们项目中主要是在测试环境下使用，测试的时候有各种各样不同的环境，可以在启动多个docker container 然后和宿主机建立对应关系，因为docker容器和宿主机是隔离掉的，在docker上运行，并抓取日志。和宿主机mount一个文件夹，然后就可以多个容器里跑应用，在宿主机中直接抓取测试的日志。不需要使用容器的时候，直接可以stop,remove容器。即插即用，非常方便，比虚拟机轻量，效率高。

其他有类似的产品，比如LXC.

测试环境docker搭建 

一个公司中有其他同学设置了相应的环境变量的时候，就可以使用scp将配置文件 bashrc拷贝下来 

```
 scp root@10.106.218.35:/root/.bashrc /root/.bashrc
```
我在bashrc里设置了一个docker的别名 dockerMe 来替代这一串很长的命令，当我运行dockerMe的时候就相对应的输入了对应的 命令，很方便。

```
alias dockerMe='docker exec -it btsmedContainer /bin/bash'
```
docker官方文档请参考 

https://docs.docker.com/engine/reference/commandline/docker/

- 检查docker版本 
```
docker version
```

- 下载docker images 
```
docker pull <dockerImageName>
```
example:

```
docker pull archive.docker-registry.eecloud.nsn-net.net/btsmed/imp-redhat:latest
```
当拉取image识别的时候可以设置代理 


```
mkdir -p /etc/systemd/system/docker.service.d
echo '[Service]' > /etc/systemd/system/docker.service.d/http-proxy.conf
echo 'Environment="HTTP_PROXY=http://10.144.1.10:8080/" "https_proxy=http://10.144.1.10:8080"' >> /etc/systemd/system/docker.service.d/http-proxy.conf
systemctl daemon-reload
service docker restart
```

- 检查image的详细信息 
```
docker images
```

- 移除images 
```
docker rmi <dockerImageID>
or
docker rmi <imageREPOSITORY>:<imageTAG>
```

```
example: docker rmi archive.docker-registry.eecloud.nsn-net.net/btsmed/imp-redhat:latest
```

- 创建一个container 
```
docker run --privileged --name=<containerName> -itd <dockerImageName> /bin/bash

example: docker run --privileged --name=container1 -itd archive.docker-registry.eecloud.nsn-net.net/btsmed/imp-redhat:latest /bin/bash

```

- 将对应的宿主机做一个mount 
```
docker run --privileged --name=<containername> -v <localpath>:<containerpath> -itd <dockerimage> /bin/bash
```

```
example: docker run --privileged --name=container1 -v /home/workspace:/data -itd archive.docker-registry.eecloud.nsn-net.net/btsmed/imp-redhat:latest /bin/bash
```

- 检查mount的路径对应关系
```
docker inspect -f "{{ .Mounts }}" 'dfcee' (CONTAINER ID)
```

- 登录容器
```
docker exec -it <containerName> /bin/bash

ssh root@containerIp (the password is root by default)
```

```
example: docker exec -it container1 /bin/bash
```

- 检查正在运行的容器 
```
docker ps
```

- 停止容器
```
docker stop <containerName>
example: docker stop container1
```

- 移除容器
```
docker rm <containerName>

example: docker rm container1
```

- 在Docker中添加一张网卡
```
docker network create --driver=bridge network1
docker network connect network1 container1
```



