1.配置github: 先设置用户名和信息
git config --global user.name "weipingQin"
git config --global user.email "995308963@qq.com"

2.生成key命令 
ssh-keygen -t rsa -C "995308963@qq.com"

3.非常重要的一点:将本地的密钥识别 
ssh-add ~/.ssh/id_github_rsa

4.执行命令 看是否识别 
ssh -T git@github.com

出现 welcome to Git@github 表示成功 

