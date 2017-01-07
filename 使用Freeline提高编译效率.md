现在用AndroidStudio的时候 用Gradle进行项目构建实在是太慢了，据说蚂蚁金服出了一个freeline的构建会使得项目构建速度快很多，于是今天尝试了一下。

1.首先很重要的是你必须要去配置你的AndroidSDK，千万不要忘记了，今天配置SDK的时候遇到了很坑的问题。
出现了问题：
`mac 配置环境变量出现export `=' not a valid identifier`
`解决方法：很简单，原来是配置SDK的时候 = 左右两边多了空格`
2.freeline首先要进行初始化 freeline init 提示配置失败需要升级到./gradlew initFreeline
3.`编译找不到project_description.json文件`
`解决方法:执行 ./gradlew checkBeforeCleanBuild`
4.`下载更新的时候一直显示0% `
`使用命令  gradle initFreeline -Pmirror (建议直接使用这个) 加上这个参数 -Pmirror优先访问国内的镜像`
5.第一次编译的时候全量编译
`python freeline.py -f`
6.调试应用的时候 使用
`python freeline.py -d`
7.参考资料[http://www.jianshu.com/p/46418dd38218]

