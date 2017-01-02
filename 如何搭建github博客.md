搭建github博客采用hexo来搭建静态博客

参考资料[https://wsgzao.github.io/post/hexo-guide/#了解Hexo]

2.安装Hexo 
npm install hexo-cli -g
npm install hexo hexo --save

3.初始化hexo 
$ hexo init <folder>
$ cd <folder>
$ npm install


4.预览 hexo server 成功之后可以登录 localhost:4000

5.简写命令
 hexo n 生成文章
 hexo s 本地发布预览效果
 hexo g 生成public 静态文件

6.我喜欢用我自己觉得喜欢的样式来进行装饰
 使用方法参考[http://moxfive.coding.me/yelee/1.Getting-Started/i18n.html]

要点:1.首先 git clone 下来主题 
2.重点的重点：需要配置 _config.yml 需要指定theme的来源 
然后要执行 这个命令 hexo clean && hexo s 不要忘记

在github上建立一个仓库 username.github.io为仓库名 
然后切换到所在的博客的目录下使用命令hexo g 生成public文件夹 

【重点】特别注意生成了public文件夹之后 你需要将public文件夹下面的所有的静态资源文件放入到刚才建立的仓库下去 然后提交到github仓库上去 
访问的URL[weipingQin.github.io]


