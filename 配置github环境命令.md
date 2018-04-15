1.配置github: 先设置用户名和信息
git config --global user.name "weipingQin"
git config --global user.email "995308963@qq.com"

2.生成key命令 
ssh-keygen -t rsa -C "995308963@qq.com"

3.非常重要的一点:将本地的密钥识别 
ssh-add ~/.ssh/id_github_rsa

4.执行命令 看是否识别 
ssh -T git@github.com

5.出现 welcome to Git@github 表示成功 

6.其他资料[http://www.jianshu.com/p/fbbf6efb50ba]


FAQ:
1.配置多个git账号的时候出现这问题:git:could not open a connection to your authentication agent问题的解决（重新绑定私钥）

解决方法:

### 1> ssh-agent bash 
### 2> ssh-add /c/Users/wqin/.ssh/id_github_rsa



