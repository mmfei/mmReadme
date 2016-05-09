#查看远程仓库(别人提交的)

git remote -v; #可以看到仓库的完整url

#添加新的远程仓库

git remote add 仓库名 https://github.com/mmfei/web-development-environment-for-mac.git;

#提交到远程仓库(真实的github地址)

1) 在本地创建一个远程仓库
git remote add origin https://github.com/mmfei/web-development-environment-for-mac.git;

git push origin master;

