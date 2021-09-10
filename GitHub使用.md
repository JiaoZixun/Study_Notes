# 上传项目

```c++
//1.在本地文件夹添加依赖
git init
//2.添加文件进入缓存区
git add .//(空格.表示添加全部，也可以单独添加某一文件)
//3.对本次提交的注释，可以直接写
git commit -m "xxxx"
//4.更改提交方式，使用ssh
git remote add origin xxxxxx
//5.提交分支
git push -u origin main//(主分支为main)
//强制提交
git push -u origin master -f
```

# 常用操作

```c++
//查看状态
git status
    
//查看项目提交方式（有https和ssh两种）
git remote -v
    
//移除旧的提交方式
git remote rm origin

//添加新的提交方式
git remote add origin git@xxx.git  

//清除缓存
git rm -r --cached 
    
//进入目录
cd
    
//查看文件夹中文件
ls
    
//进入文件编辑
vi 文件名
//vim操作，进入编辑模式
o
//退出编辑模式
esc
//推出并保存
:wq
//推出不保存
:q!
    
//切换分支
git  checkout master
    
//合并分支
git  merge dev
    
//更新远程分支列表
git remote update origin --prune

//查看所有分支
git branch -a

//删除远程分支Chapater6
git push origin --delete Chapater6

//删除本地分支 Chapater6
git branch -d  Chapater6
```

