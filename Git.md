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

***

## 提交本地代码
&emsp;&emsp;使用```add```和```commit```命令。  
&emsp;&emsp;```add```用于把想要提交的代码添加进来，```commit```则是真正执行提交操作。

* 添加单个文件，如添加```build.grade```文件：  
```git
git add build.gradle
```

* 添加某个目录，如添加整个```app```目录下的所有文件：  
```git
git add app
```

* 一次性添加所有文件，只需要在```add```后面加上一个点：  
```git
git add .
```

* ```MaterialDesign```项目下所有文件都添加好后，可以进行提交：  
```git
git commit -m "First commit"
```
&emsp;&emsp;注意，在```commit```命令的后面，一定要通过```-m```参数加上提交的描述信息，没有描述信息的提交被认为是不合法的。  

***

## 忽略文件
&emsp;&emsp;先cd到```MultiMediaTest```项目下，```git init```创建代码仓库。  
&emsp;&emsp;```build```目录下的文件都是编译项目时自动生成的，不应该将这部分文件添加到版本控制中。  
&emsp;&emsp;**Git** 允许用户将指定的文件或目录排除在版本控制之外，它会检查代码仓库的目录下是否存在一个名为```.gitignore```的文件。如果存在，就去一行行读取这个文件中的内容，并把每一行指定的文件或目录排除在版本控制之外。注意，```.gitignore```中指定的文件或目录是可以使用```*```通配符的。  
&emsp;&emsp;**Android Studio** 在创建项目的时候会自动创建出两个```.gitignore```文件，一个在根目录下面，一个在```app```模块下面。  

* 根目录下的```.gitignore```:  
![图片示例](https://github.com/gneL1/AndroidStudy/blob/master/photos/Git/mid/gitignore_1.PNG)  
&emsp;&emsp;除了```*.iml```表示指定任意以```.iml```结尾的文件，其他都是指定的具体的文件名或者目录名，上面配置中的所有内容都不会被添加到版本控制中，因为基本是一些由 **IDE** 自动生成的配置。  

* ```app```模块下面的```.gitignore```：  
![图片示例](https://github.com/gneL1/AndroidStudy/blob/master/photos/Git/mid/gitignore_2.PNG)  
&emsp;&emsp;```app```模块下大多是编写的代码，因此默认情况下只有其中的```build```目录不会被添加到版本控制中。  
&emsp;&emsp;  
&emsp;&emsp;也可以对以上两个文件进行任意修改。比如说```app```模块下的所有测试文件都只是给自己使用的，并不想把它们添加到版本控制中，就可以修改```app/.gitignore```文件中的内容：  
```
/build
/src/test
/src/androidTest
```
&emsp;&emsp;所有测试文件都是放在这两个目录下的。  
&emsp;&emsp;  
先```add```将所有文件添加：  
```git
git add .
```
执行```commit```命令完成提交：  
```git
gir commit -m "First commit."
```

***

## 查看修改内容
* 使用 **Git** 查看自上次提交后文件修改的内容：  
```git
git status
```
![图片示例](https://github.com/gneL1/AndroidStudy/blob/master/photos/Git/mid/git_status_1.PNG)  
&emsp;&emsp;这里 **Git** 提示目前项目中没有任何可提交的文件，因为刚刚才提交过。  
&emsp;&emsp;  
修改下```MainActivity```中的内容：  
```kotlin
class MainActivity : AppCompatActivity() {
    override fun onCreate(savedInstanceState: Bundle?) {
        ......
        Btn_notification.setOnClickListener {
            ......
            Log.d("MainActivity","跳转成功")
        }
        ......
```
这里在按钮的点击事件中添加一行日志打印代码。  
&emsp;&emsp;  
&emsp;&emsp;重新输入```git status```命令：  
![图片示例](https://github.com/gneL1/AndroidStudy/blob/master/photos/Git/mid/git_status_2.PNG)  
&emsp;&emsp;**Git** 提醒```MainActivity.kt```这个文件已经发生了更改。  

* 查看更改的内容：  
```git
git diff
```
&emsp;&emsp;这样可以查看所有文件的更改内容。如果只想查看```MainActivity.kt```这个文件的更改内容，可以在后面加上完整的文件路径：  
```git
git diff app/src/main/java/com/example/multimediatest/MainActivity.kt
```
![图片示例](https://github.com/gneL1/AndroidStudy/blob/master/photos/Git/mid/git_diff_1.PNG)  
&emsp;&emsp;变更部分最左侧的加号代表新添加的内容。如果有删除内容的话，会在左侧用减号表示。  

***

## 撤销未提交的修改
* 撤销未使用```git add```缓存的代码  
上面一节给```MainActivity```添加了一行日志打印，如果想要撤销这个修改，可以使用```checkout```命令：  
```git
git checkout app/src/main/java/com/example/multimediatest/MainActivity.kt
```
&emsp;&emsp;执行了命令后，对```MainActivity.kt```这个文件所做的一切修改就应该都被撤销了，重新执行```git status```命令检查。  
![图片示例](https://github.com/gneL1/AndroidStudy/blob/master/photos/Git/mid/git_checkout.PNG)  
&emsp;&emsp;可以看到，当前项目没有任何可提交的文件，说明撤销操作确实成功了。  
&emsp;&emsp;这种撤销方式只设用于那些还没有执行过```add```命令的文件，如果某个文件已经被添加过了，这种方式就无法撤销更改的内容。  

* 撤销使用了```git add```缓存了的代码  
给```MainActivity```添加一行日志打印，然后输入命令：  
```git
gir add .
```
&emsp;&emsp;把所有修改的文件都进行添加，输入```git status```检查：  
![图片示例](https://github.com/gneL1/AndroidStudy/blob/master/photos/Git/mid/git_reset_1.PNG)  
&emsp;&emsp;再执行一次```checkout```命令，```MainActivity```仍然处于已填加状态。  
&emsp;&emsp;  
&emsp;&emsp;对于已添加的文件，应该先对其取消添加，然后才可以撤回提交。取消添加使用的是```reset```命令。  
```git
git reset HEAD app/src/main/java/com/example/multimediatest/MainActivity.kt
```
&emsp;&emsp;再运行一次```git status```命令，可以看到```MainActivity.kt```这个文件重新变回了为添加状态，此时就可以执行```checkout```命令将修改的内容撤销了。  
![图片示例](https://github.com/gneL1/AndroidStudy/blob/master/photos/Git/mid/git_reset_2.PNG) 

***

## 查看提交记录
```git
git log
```
![图片示例](https://github.com/gneL1/AndroidStudy/blob/master/photos/Git/mid/git_log_1.PNG)  
&emsp;&emsp;每次提交记录都会包含提交```id```、提交人、提交日期以及提交描述这4个信息。  
&emsp;&emsp;  
&emsp;&emsp;当提交记录非常多，只想看其中一条记录，可以在命令中指定该纪录的```id```：  
```git
git log f2b2f069c41aded5c9f69ee33d53879513782e34
```
&emsp;&emsp;也可以在命令中通过指定参数查看最近的几次提交，比如```-1```表示只想看到最后一次的提交记录：  
```git
git log -1
```

***

## 分支的用法
为什么需要分支？  
&emsp;&emsp;比如现在开发一张ZE地图，整了个```v1```版本的地图发布出去了，然后现在我开始做```v2```版本的新关卡。新关卡整到一半，有玩家跟我反馈```v1```版本有个重大bug会导致游戏崩溃，要我赶紧修复。如果我现在没有使用分支功能，而是直接在主干线上开发的地图，想要修完bug后就直接拿去玩，那意味着这整到一半的新关卡也被同时发布了。  
&emsp;&emsp;而使用了分支功能，我只需要在发布```v1```版本的时候建立一个分支，然后在主干线上继续开发```v2```版本的新关卡，当```v1```版本出现bug，就在分支线上进行修改，然后发布新的```v1_1```版本，并将修改后的代码合并到主干线上的```v2```版本。这样就解决了```v1```版本存在的bug，而且保证了主干线上的地图也已经修复了这些bug，当```v2```版本发布时，就不会有同样的bug存在了。  
&emsp;&emsp;  
* 查看当前版本库有哪些分支：  
```git
git branch
```
![图片示例](https://github.com/gneL1/AndroidStudy/blob/master/photos/Git/pro/git_branch_1.PNG)  

* 创建一个分支：  
```git
git branch version1.0
```
使用```git branch```检查一下：  
![图片示例](https://github.com/gneL1/AndroidStudy/blob/master/photos/Git/pro/git_branch_2.PNG)  
&emsp;&emsp;```master```分支的前面有一个```*```号，说明目前的代码还是在```master```分支上。  

* 切换分支：  
```git
git checkout version1.0
```
使用```git branch```检查一下  
![图片示例](https://github.com/gneL1/AndroidStudy/blob/master/photos/Git/pro/git_branch_3.PNG)  
&emsp;&emsp;需要注意，在```version1.0```分支上修改并提交的代码将不会影响到```master```分支。同理，在```master```分支上修改并提交的代码也不会影响```version1.0```分支。如果在```version1.0```分支上修复了一个 **bug** ，在```master```分支上这个 **bug** 仍然是存在的。  

* 合并分支：  
```git
git checkout master
git merge version1.0
```
![图片示例](https://github.com/gneL1/AndroidStudy/blob/master/photos/Git/pro/git_merge_1.PNG)  
&emsp;&emsp;先切换到```master```分支，然后通过```merge```命令，把在```version1.0```分支上修改并提交的内容合并到```master```分支上。合并分支的时候可能会出现代码冲突的情况。  

* 删除分支：  
```git
gir branch -d version1.0
```
![图片示例](https://github.com/gneL1/AndroidStudy/blob/master/photos/Git/pro/git_delete_1.PNG)

***

## 与远程版本库协作
&emsp;&emsp;使用 **Git** 进行团队开发，需要有一个远程的版本库，团队成员都从这个版本库中获取最原始的代码，然后各自进行开发，并且以后每次提交的代码都同步到远程版本库上。要经常从版本库中获取最新代码，不然容易出现冲突。  
&emsp;&emsp;比如现在有一个远程版本库的 **Git** 地址是```git@github.com:gneL1/Git-and-use.git```  

* 将代码下载到本地：  
```git
git clone git@github.com:gneL1/Git-and-use.git
```
![图片示例](https://github.com/gneL1/AndroidStudy/blob/master/photos/Git/pro/git_clone_1.PNG)  
```clone```完成后的文件夹：  
![图片示例](https://github.com/gneL1/AndroidStudy/blob/master/photos/Git/pro/git_clone_2.PNG)  
&emsp;&emsp;  

* 把本地修改的内容同步到远程版本库上：  
```git
git push origin master
```
&emsp;&emsp;```origin```部分指定的是远程版本库的 **Git**地址，```master```部分指定的是同步到哪一个分支上，上述代码完成了将本地代码同步到```git@github.com:gneL1/Git-and-use.git```这个版本库的```master```分支上。  
&emsp;&emsp;注意，要先```cd```到本地仓库的所在目录，然后将修改的内容```commit```到本地仓库后，```push```命令才会生效。  
&emsp;&emsp;```push```命令通过对比```commit```的记录，如果本地仓库新增了与远程仓库不同的代码，就把多出来的```commit```给推上去。如果本地仓库的分支的最新版本和远程的```commit```有冲突，就需要解决冲突。  

下面是没有```commit```直接执行```push```命令：  
![图片示例](https://github.com/gneL1/AndroidStudy/blob/master/photos/Git/pro/git_push_1.PNG)  
&emsp;&emsp;```Everything up-to-date```表示本地代码仓库推给远程仓库的文件都是最新的。之前修改的代码都还在工作区，本地代码仓库和远程仓库的代码一样，没东西可以推送。需要先```add```到暂存区，然后```commit```到本地代码仓库，再```push```就会把本地代码仓库的修改代码推送给远程仓库。  
&emsp;&emsp;  
先```add```再```commit```最后```push```：  
![图片示例](https://github.com/gneL1/AndroidStudy/blob/master/photos/Git/pro/git_push_2.PNG)  
&emsp;&emsp;可以看到推送是成功的。  
&emsp;&emsp;  
* 将远程版本库上的修改同步到本地：  
```git
git fetch origin master
```
&emsp;&emsp;```fetch```会将远程版本库上的代码同步到本地，不过同步下来的代码并不会合并到任何分支上，而是会存放到一个```origin/master```分支上。  
![图片示例](https://github.com/gneL1/AndroidStudy/blob/master/photos/Git/pro/git_fetch_1.PNG)  
&emsp;&emsp;可以通过```diff```命令查看远程版本库上到底修改了哪些东西。  
```git
git diff origin/master
```
![图片示例](https://github.com/gneL1/AndroidStudy/blob/master/photos/Git/pro/git_fetch_2.PNG)  

&emsp;&emsp;再调用```merge```命令将```origin/master```分支上的修改合并到主分支上  
```git
git merge origin/master
```
![图片示例](https://github.com/gneL1/AndroidStudy/blob/master/photos/Git/pro/git_fetch_3.PNG)   
&emsp;&emsp;  
&emsp;&emsp;而```pull```命令相当于将```fetch```和```merge```两个命令放在一起执行了，它可以从远程版本库上获取最新的代码并且合并到本地。  
```git
git pull origin master
```
![图片示例](https://github.com/gneL1/AndroidStudy/blob/master/photos/Git/pro/git_pull_1.PNG)  
&emsp;&emsp;  
* 实际工作情况中的提交代码：  
&emsp;&emsp;先```commit```然后```pull```再```push```。```pull```是为了拉取到远程版本库中的最新代码，不然直接```push```很可能会与别人的代码产生冲突。如果有问题就可以自己在本地直接解决。  
&emsp;&emsp;  
* ```Fork```：  
&emsp;&emsp;```Fork```可以将项目复制到自己的账号下，再使用```git clone```命令将它克隆到本地，这样就可以在现有代码的基础上自由添加功能并提交了。  
