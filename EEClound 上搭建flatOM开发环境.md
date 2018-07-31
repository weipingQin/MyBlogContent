最新项目地址:

```
ssh://<yourname>@gerrit.nsn-net.net:29418/LTEBTSOM/BTS_SC_NE3SADAPT_OAM
```

登录你自己的 EE clound  

1.先准备相关环境 包括LXC 

https://confluence.int.net.nokia.com/display/MANO/Cloud


2.mout Linsee的环境 

```
mkdir -p /build/ltesdkroot 
edit /etc/rc.d/rc.local file add two lines
mount -t nfs hzchon10.china.nsn-net.net:/vol/hzchon10_bin/build/build /build
mount -t nfs hzchon11.china.nsn-net.net:/vol/hzchon11_ltesdk/ltesdkroot/ltesdkroot /build/ltesdkroot

perform command chmod +x /etc/rc.d/rc.local

```

---


1.首先要在linux机器上建立一个自己的用户 


```
user add <yourname>
```

2.在/var/fpwork/root下建立一个自己的项目文件夹 将你的代码放到root文件夹下 

3.设置项目权限 


```
chmod 777 
```

4.配置git相关的权限 
具体配置git的相关问题 请参考如下文档
https://confluence.int.net.nokia.com/display/DevOffice/01+Clone+and+Config#id-01CloneandConfig-1Addkey

```
git remote set-url origin ssh://wqin@gerrit.nsn-net.net:29418/LTEBTSOM/BTS_SC_Ne3sAdapter_OAM
```

```
git config user.name wqin

git config user.email weiping.qin@nokia-sbell.com

curl -o .git/hooks/commit-msg http://hzgitv01.china.nsn-net.net/tools/hooks/commit-msg
chmod u+x ./.git/hooks/commit-msg

```

5.clone 相应的项目 


```
git clone ssh://wqin@gerrit.nsn-net.net:29418/LTEBTSOM/BTS_SC_NE3SADAPT_OAM
```
6.编译代码 
编译前需要做相关的配置 


```
1. 找到mfo的路径 code/mfo/pkgfile.d
2. vi ne3sadapt.pkgfile
3. domxml 加到这个位置depends_on=(
                              lim
                              liboam
                              bmmeta
                              ltemeta
                              ccsmocks
                              oamtoolkit
                              gtest
                              domxml
                           )
```


-   编译相关命令请参考如下文档 

https://confluence.int.net.nokia.com/pages/viewpage.action?pageId=658955996

```
mfo/mfo -o $(pwd) build ne3sadapt --arch x86_64 -C ne3sadapt_source=$(pwd)/BTS_SC_NE3SADAPT_OAM

```
具体建立LXC的步骤
请参考如下文档 

https://hackmd.io/eM10QIM8QdCYA2bTjMAtag?view

- sct存放的路径
```
/var/fpwork/root/FlatOM/BTS_SC_NE3SADAPT_OAM/integration/sct
```

- ACC存放的路径
```
/var/fpwork/root/FlatOM/BTS_SC_NE3SADAPT_OAM/integration/acc
```
- nbs的版本需要更新到最新版本
```
pip install --upgrade --trusted-host 10.69.239.163 --disable-pip-version-check -i http://10.69.239.163/ nbs==trunk.3.6.1 --user -U --timeout 60
```
- 再运行 
```
  bash /var/fpwork/jancao/code/ne3sadapt/integration/sct/script/deploy_library_for_LXC.sh

```
的时候 需要联网下载对应的rebot库文件,需要container上网 

- 在host机器上配置上网 
```
iptables -t nat -F POSTROUTING
iptables -t nat -A POSTROUTING -o eth0 -j MASQUERADE
iptables -A INPUT -m state --state ESTABLISHED,RELATED -j ACCEPT
iptables -A FORWARD -i eth0 -o nat -m state --state RELATED,ESTABLISHED -j ACCEPT
iptables -A FORWARD -i nat -o eth0 -j ACCEPT
```

- 运行一个测试的case 注意:需要将nbs的版本升级到最新版的跑case 

```
 pybot -L trace -t CM Upload Configuration To Manager .
```
 
