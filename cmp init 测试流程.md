**{1} 安装包的流程**
- rpm -qa | grep nokia-imp
- rpm -e nokia-imp-xxx.x.xxxxxxxx.xxx-x.noarch
- download package & install package 
- rpm -i nokia-imp-xxx.x.xxxxxxxx.xxx-x.noarch.rpm

**{2} 启动BTSMED**

- cd /opt/imp/Version/cli/bin/
- 切换账户 su Nemuadmin 
- cd cli/bin
- ./imp-cli-control.sh start
- btsmed init --btsmedId <btsmedId>
- btsmed>btsmed start
- 
**{3} 停止BTSMED**
- cd /opt/imp/Version/cli/bin/

./imp-cli-control.sh start

- btsmed>btsmed stop
- **./imp-cli-control.sh stop**

查看BTSMED状态 
- btsmed>btsmed state

**{4} 查看相应的配置信息 
btsmed>config set --dn /BTSMED-1/CERTH-1/CMP-1**

**配置证书caSubjectName eeSubjectName** 


```
caCertificateUpdateTime:1
caSubjectName : C=CN, O=Nokia, CN=FOR_TEST_CA1_1_1
cmpPreSharedKey:LJTS-dsMF-JsGY-2gK9
cmpRefNum:10546
eeSubjectName:O=Nokia,CN=BTSMEDCLI
neCertificateUpdateTime :2
serverHost:10.159.218.215
serverPath pkix
serverPort:8081

```
CMP Initialize


```
btsmed>cmp initialize
```
查看所有的配置信息 

```
config list --dn all
```

--测试 btsmed import config 

```
btsmed config import --path Invalid_parameter.xml
```


