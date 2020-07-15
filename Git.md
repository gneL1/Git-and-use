# Git
## 创建代码仓库
&emsp;&emsp;安装完成后，在 **开始** 里找到 **Git Bash** 并打开。  
* 配置身份，这样在提交的时候，**Git** 就知道是谁提交的。  
```git
git config --global user.name "Tony"
git config --global user.email "tony@gmail.com"
```
![图片示例](https://github.com/gneL1/AndroidStudy/blob/master/photos/Git/Init/git_1.PNG)

* 创建代码仓库  
&emsp;&emsp;仓库(repository)是用于保存版本管理所需信息的地方，所有本地提交的代码都会被提交到代码仓库中，如果有需要还可以推送到远程仓库中。  
&emsp;&emsp;这里给```MaterialDesign```项目建立一个代码仓库，先进入```MaterialDesign```项目的目录下。  
![图片示例](https://github.com/gneL1/AndroidStudy/blob/master/photos/Git/Init/git_2.PNG)

&emsp;&emsp;在此目录中输入下面命令：  
```git
git init
```
&emsp;&emsp;这样就完成了创建代码仓库的操作  
![图片示例](https://github.com/gneL1/AndroidStudy/blob/master/photos/Git/Init/git_3.PNG)

&emsp;&emsp;仓库创建完成后，会在```MaterialDesign```项目的根目录下生成一个隐藏的git目录，这个目录就是用来记录本地所有的Git操作的，可以通过```ls -al```命令查看。  
![图片示例](https://github.com/gneL1/AndroidStudy/blob/master/photos/Git/Init/git_4.PNG)

如果想删除本地仓库，只需要删除这个目录就行了。
