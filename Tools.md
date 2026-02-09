
```
 zip file.pdf.zip --out file.zip -s 40m

 cat file.z* > newFile.zip
 unzip -q newFile.zip
```


[广告拦截](https://github.com/gorhill/uBlock/releases)


# Git

```
feat:
fix:
docs:
style:
refactor:
perf:
test:
chore
```

Git 中所有数据在存储前都计算校验和，然后以校验和来引用。


Git有三种状态，你的文件可能处于其中之一：已提交（committed）、已修改（modified）和已暂存（staged）。分别对应项目的三个工作区域的概念：Git仓库、工作目录以及暂存区域。

基本的 Git 工作流程如下:
1. 在工作目录中修改文件。
2. 暂存文件，将文件的快照放入暂存区域。
3. 提交更新，找到暂存区域的文件，将快照永久性存储到 Git 仓库目录

获取帮助
```
git help <verb>
git <verb> --help
man git-<verb>
```

Git配置分为三个级别
1. --system ：/etc/gitconfig 文件
2. --global ：~/.gitconfig 或 ~/.config/git/config 
3. local： 当前项目的.git/config
   

```
git config --global user.name "Qu Chunhe"
git config --global user.email quchunhe@example.com

git config --list
git config user.name
```



.gitignore
```
*.a
  # but do track lib.a, even though you're ignoring .a files above
  !lib.a
  # only ignore the TODO file in the current directory, not subdir/TODO
  /TODO
  # ignore all files in the build/ directory
  build/
  # ignore doc/notes.txt, but not doc/server/arch.txt
  doc/*.txt
  # ignore all .pdf files in the doc/ directory
  doc/**/*.pdf
 
```
[A collection of .gitignore templates](https://github.com/github/gitignore)




```
git init
git clone git@github.com:QuChunhe/study.git Study

git status
git status -s

git add README.md
git commit -m "first commit"

git rm --cached README

git mv README.md README

git remote add origin git@github.com:QuChunhe/blogs.git
git push -u origin master

git status

git remote add origin git@github.com:QuChunhe/blogs.git
git push -u origin master

git log
```



```
git diff
git diff --staged
```


```
git log

git log -p -3

git log --stat
```


```
git commit -m 'initial commit'
git add forgotten_file
 git commit --amend
```


There are several ways 
to do this. Many people find dedicated Git GUI tools such as Sourcetree (macOS and Windows) or 
Sublime Merge (Linux, macOS, and Windows) to be the easiest and most intuitive way to handle merge 
conflicts. Other people prefer to resolve merge conflicts manually, using Git terminal commands and 
a text editor. GitLab users have another option: you can use GitLab’s built-in graphical merge conflict 
resolution tool.


```
git clone --recursive git://
git submodule update --init
```
# Maven

```
 mvn dependency:tree

 mvn dependency:resolve -Dclassifier=sources
```

```
pdftocairo -r 300 -png \\infile % 将生成的pdf文件转换为png图像
```
# Gradle

[Gradle](https://gradle.org/releases/)

~/.gradle/gradle.properties
```
org.gradle.java.home=C:\\Program Files\\corretto-1.8.0_402
```

```
vim 
GRADLE_HOME=/usr/local/gradle-6.7
export PATH=${GRADLE_HOME}/bin:$PATH
export GRADLE_HOME

```
# SBT

[https://www.scala-sbt.org/download.html](https://www.scala-sbt.org/download.html)


YApi旨在为开发、产品、测试人员提供更优雅的接口管理服务。可以帮助开发者轻松创建、发布、维护 API

# IDEA

在后面添加：-Dfile.encoding=utf-8



# Tools

[](https://www.mindshow.fun/#/home)

[合并代码](https://winmerge.org/downloads/)
[draw.io]()