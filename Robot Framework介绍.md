
Robot Framework 是一款基于 Python 的功能自动化测试框架。它具备良好的可扩展性，支持关键字驱动，可以同时测试多种类型的客户端或者接口，可以进行分布式测试执行。主要用于轮次很多的验收测试和验收测试驱动开发（ATDD）。

- 安装 Rebot 

需要安装python环境 我们这边的测试环境有个NBS的模拟器来模拟上层组件NetAct发送数据。在下载NBS的时候已经把python环境打包进去了。

安装NBS模拟器

```
make nbs
```

- 使用python的包管理器来安装framework库 
```
pip install robotframework
```
-在安装IDE之前,你需要将你的pip升级一下 
```
pip install --upgrade pip 
```

安装RebotFramework的IDE
```
pip install robotframework-ride
```
安装实现代码高亮的组件pygments

```
 pip install pygments
```

- 安装成功后,执行如下命令,打开IDE 
```
ride.py
```
- 如下图,这就是对应的rebot case 编辑的IDE编译器

![image](https://note.youdao.com/yws/public/resource/b1b84aba5a7f6c84f38e2859198afaef/xmlnote/885E694D34194A66BF943E7A1BC45AFB/6178)


编写测试用例的时候,使用F5来查询关键字。



输入关键字“open”进行搜索，查询到一个“Open Browser”的关键字，点击这个关键字，就出现了它的用法和说明

- 相关的语法 

**标量变量:${scalar}**

当在测试数据中使用标量变量时，它们将被分配的值所代替

**列表变量: @{LIST}**

列表变量是复合变量，可以分配多个值给它

**数字变量:${80}**

变量语法可以用来创建一个全是整型和浮点型的数字：整型${80}、浮点型${3.14}


编写完一个case之后,运行的信息会生成三个文件:Output.xml,Log.html,Report.html 通过浏览器去查看对应的case有无通过。

![image](https://images0.cnblogs.com/i/311516/201407/271805068381521.png)


例子:这是项目中一个完整的Robot Case文件 

一个case由两部分组将 一个是robot case 还有对应的 ACC【XML流程图】
case 可以理解成是一个黑盒测试，相当于我设置一些输入的参数和我期望的输出结果。然后跑case的时候去运行你写的代码

Force Tags 中标注的 feature-LTE4934-E-i    release-LTE19 是对应的ACC 

```
*** Settings ***
Suite Setup       NE Start Up For Security
Suite Teardown    Stop NE And Switch To Hostname
Force Tags        owner-david.xu    team-OSS&EMS SG5    feature-LTE4934-E-i    release-LTE19
Resource          ${CURDIR}/resources/Common_Resources.robot

*** Variables ***
${S_RESULT_SUCCEED}    2
${S_RESULT_FAILED}    4
${S_DEL_CERTIFICATE_IND}    URI-1/SESSION-1/DEL_CERTIFICATE_IND

*** Test Cases ***
Manager Request CACERT Delete And NE Reply Success To Agent
    [Tags]    acc-LTE4934-E-i.1.1    type-normal    status-RT
    [Setup]    Clear Nbs Message Buffer
    ${operation id}    Set Variable    ${EVENTID()}
    Manager Send Provision Request With Parameters To Agent    Deleta_ca_file.xml    ${operation id}
    ${distname}    NE Receive Request From Agent And Reply    ${S_DEL_CERTIFICATE_IND}
    NE Send NE MO Result To Agent    ${distname}    ${S_RESULT_SUCCEED}    result_mo=DEL_CERTIFICATE_RESULT-1
    Validate Manager Received Feedback From Agent    ${operation id}
    NE Receive Remove MO Message From Agent And Send Back Removed MO    ${distname}    DEL_CERTIFICATE_RESULT-1

Manager Request CACERT Delete And NE Reply Failed To Agent
    [Tags]    acc-LTE4934-E-i.1.2    type-exception    status-RT
    [Setup]    Clear Nbs Message Buffer
    ${operation_id}=    Set Variable    ${EVENTID()}
    Manager Send Provision Request With Parameters To Agent    Deleta_ca_file.xml    ${operation id}
    ${distname}    NE Receive Request From Agent And Reply    ${S_DEL_CERTIFICATE_IND}
    NE Send NE MO Result To Agent    ${distname}    ${S_RESULT_FAILED}    result_mo=DEL_CERTIFICATE_RESULT-1
    Validate Manager Received Feedback From Agent    ${operation_id}    not_ok    1 failed    'ne3s.common.operationFailed'    'Received Failed from NE'
    NE Receive Remove MO Message From Agent And Send Back Removed MO    ${distname}    DEL_CERTIFICATE_RESULT-1

```


相关参考资料:

http://robotframework.org/

http://robotframework.org/robotframework/latest/RobotFrameworkUserGuide.html#id484

http://www.cnblogs.com/fnng/category/598667.html


参考书籍:

Selenium 2自动化测试实战 基于Python语言
