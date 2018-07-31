在运行ET测试脚本的时候,可以使用Verify Job的方式来单独的调试某一个Case
1.打开Verify job网址
http://hztdci01.china.nsn-net.net/view/IMP_GIT/job/IMP_ET_VERIFY/
2.点击 Build with Parameters


选择如何获取RPM包
如何需要使用TRUNK上的包，请在HOW_TO_GET_RPM的下拉框中选择wget

如果需要使用开发提供的knife包，请在HOW_TO_GET_RPM的下拉框中选择copy


输入rpm包的获取地址或commit id
如果使用TRUNK上的包，且在第三步中已选择wget。请在TRUNK的job上找到所需的rpm包版本，并在KNIFE_LINK_OR_COMMIT_ID的表框中填入该RMP包的下载链接。
TRUNK链接：
http://hztdci01.china.nsn-net.net/view/IMP_GIT_TRUNK/job/IMP_GIT_TRUNK_RPM_PACKAGE/

如果使用开发提供的knife包，且在第三步中已选择copy。请在KNIFE_LINK
_OR_COMMIT_ID的表框中填入对应ticket的commit id。

输入ET case的测试版本

如果需要调试ticket上的case，，请在ET_CASE_REFSPEC的表框中输入该ticket的版本号。
如果需要直接运行已经提交的case，请在ET_CASE_REFSPEC的表框中输入如下命令：
如需运行master分支上已有的case：refs/heads/master
如需运行17A分支上已有的case：refs/heads/maintenance/17A
输入运行ET case的命令
如果希望运行单个case，在ET_COMMAND的表框中填入如下命令：
pybot -L trace -t 'case name' -d ./log .
（单引号中替换为你需要运行的case名称）
如果希望运行某个suite里所有的case，在ET_COMMAND的表框中填入如下命令：
pybot -L trace -s 'suite name' -d ./log .
（单引号中替换为你需要运行的suite名称）
如果希望运行压力池中所有的case，在ET_COMMAND的表框中填入如下命令：
pybot -L trace --listener RobotListener -e status-debug -e feature-LTE3875* -d ./log .
开始构建
点击开始构建，便可在build history中看到你所提交的构建，等待构建完成就可看到case运行结果。