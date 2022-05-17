# 终端

**cmd + Cmder** 命令行 使用教程技巧 （全攻略）

参考教程：**https://blog.csdn.net/sunsineq/article/details/122818453**

【配合此地址安装：https://juejin.cn/post/6844903817851453453】

Cmder常用快捷键

- 利用Tab，自动路径补全；

- 利用Ctrl+T建立新页签；利用Ctrl+W关闭页签;

- Alt+Shift+1：开启cmd.exe

- Alt+Shift+2：开启powershell.exe

- Alt+Shift+3：开启powershell.exe (系统管理员权限)

  

- 利用Ctrl+Tab切换页签;

- Alt+F4：关闭所有页签

- Ctrl+1：快速切换到第1个页签

- Ctrl+n：快速切换到第n个页签( n值无上限)

- Alt + enter： 切换到全屏状态；

- Ctr+r 历史命令搜索





**管理员权限**的终端：

![image-20220515143936363](C:\Users\051129\AppData\Roaming\Typora\typora-user-images\image-20220515143936363.png) Win10可以直接 win+x 再按 a 键进入。





# Vscode

## vscode插件

> （较为全面）vscode编辑器插件总结： https://blog.csdn.net/luyu13141314/article/details/70238990
>
> （带图）前端必备vscode插件推荐https://blog.csdn.net/weixin_39886956/article/details/110212937



## vscode用户代码片段设置

==**将需要的代码转换为配置格式：https://snippet-generator.app/**==



> - 安装借鉴：https://blog.csdn.net/qq_40191093/article/details/82915028
>
> - vue的部分代码块提供：https://blog.csdn.net/weixin_34133829/article/details/93169471
>
> - 后续设置（将自定义的移到第一个）：https://blog.csdn.net/weixin_40579884/article/details/97165221
> - 详细补充讲解（不是以vue为例）：https://blog.csdn.net/maokelong95/article/details/54379046

### 二、配置步骤

1.在vscode中，Ctrl+shift+p 打开配置搜索框

2.搜索框内输入：配置用户代码片段 或者 Snippets，在下拉选项中选中配置用户代码片段选项，

3.在新打开的搜索下拉框中，选择或搜索需要配置的文件类型，以css为例，输入css，在下拉选项中，点击css.json进行编辑




### **四、代码片段置顶**

默认情况下，自定义代码片段在vscode中提示优先级较低，可以将代码片段优先级设为置顶

设置中，搜索：snippet，将 Snippet Suggestions 设置为 top

![img](https://img-blog.csdnimg.cn/2021033118382041.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80MDU3OTg4NA==,size_16,color_FFFFFF,t_70)





## VScode

CTRL+ h   可以调出当前页面替换

CTRL+ ~   可以调出控制台终端

CTRL+ b   调出侧边目录栏





# git

- 推送代码之前，要先pull，然后再push，确保目前修改的是最新版本的，才能避免冲突

- pull = fetch + merge 

  - 先 git fetch 【远程库地址别名（通常为origin）】【远程分支名】 

  - 再 git merge【远程库地址别名 / 远程分支名】 

  - fetch 是将远程的仓库抓取到本地 ,并存放到本地的origin/master分支上【如果远程仓库是存放在master分支上的话】

    ```
    【要想使用origin这个仓库别名之前，先需要git remote add origin (这里是每次的仓库地址，常用SSH链接)】
    
    【1】git fetch origin master
    【2】cat (本地的文件)
    	如果使用 cat 查看本地的工作区，是没有变化的
    【3】git checkout origin/master 
    	如果需要查看fetch抓取到的内容，需要切换到新增的本地分支 
    【4】cat (本地的文件)
    	再次使用 cat 查看（这里查看的不是本地的工作区，只是分支上的内容），能看到远程抓取下来的文件内容
    	
    【5】git checkout master
    	再次切换为主要的master的分支	
    【6】git merge origin/master
    	查看好远程仓库中修改的文件情况之后，确认无误就使用 merge 更新本地文件
    【7】cat (本地的文件)
    	再次使用 cat 查看本地的工作区，这里已经和远程仓库的内容合并了
    	
    ```

    

  - merge

> https://blog.csdn.net/zhuguanlin121/article/details/118415704
>
> https://blog.csdn.net/unique_perfect/article/details/104833391

命令解释：

| 命令                         | 描述                                                         |
| ---------------------------- | ------------------------------------------------------------ |
| cd + 你的远程仓库名          | 进入到远程仓库内（根据自己的仓库名输入）                     |
| git init                     | 初始话Git                                                    |
| git add .                    | 将工作区的文件添加到暂存区（“ . ”是当前目录下的所有文件，也可只输入文件夹名称） |
| git commit -m “你的提交信息” | 将暂存区的文件添加到本地仓库                                 |
| git push                     | 提交到远程仓库（可能需要你输入帐号和密码）                   |







----



![image-20220516223524400](C:\Users\051129\AppData\Roaming\Typora\typora-user-images\image-20220516223524400.png)

==**常用 Git 命令清单：http://www.ruanyifeng.com/blog/2015/12/git-cheat-sheet.html**==

![img](https://img12.360buyimg.com/ling/jfs/t1/57850/27/2864/109717/5d09d6fbE82192e63/ad0330a27b300c5f.jpg)



## 图解

![](https://img-blog.csdnimg.cn/20201217102052835.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3VuaXF1ZV9wZXJmZWN0,size_16,color_FFFFFF,t_70)



![在这里插入图片描述](https://img-blog.csdnimg.cn/20201217102041839.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3VuaXF1ZV9wZXJmZWN0,size_16,color_FFFFFF,t_70)

![在这里插入图片描述](https://img-blog.csdnimg.cn/20201217102028766.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3VuaXF1ZV9wZXJmZWN0,size_16,color_FFFFFF,t_70)



![在这里插入图片描述](https://img-blog.csdnimg.cn/20201217100310917.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3VuaXF1ZV9wZXJmZWN0,size_16,color_FFFFFF,t_70)





![在这里插入图片描述](https://img-blog.csdnimg.cn/20201217100241959.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3VuaXF1ZV9wZXJmZWN0,size_16,color_FFFFFF,t_70)





![在这里插入图片描述](https://img-blog.csdnimg.cn/20201217100301167.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3VuaXF1ZV9wZXJmZWN0,size_16,color_FFFFFF,t_70)

![在这里插入图片描述](https://img-blog.csdnimg.cn/20201217102107185.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3VuaXF1ZV9wZXJmZWN0,size_16,color_FFFFFF,t_70)







## 正常使用git bash

https://www.runoob.com/git/git-remote-repo.html

```
# 新建后对项目进行介绍   {或者直接这样新建：touch README.md}
echo "# test" >> README.md

【1】# 将该文件夹变成用git管理的本地仓库
git init

# 尝试将README.md到暂存区
git add README.md

【2】# 提交暂存区到仓库区，并添加代码提交信息
git commit -m "first commit"

# 强制重命名分支 
git branch -M main     

【3】# 添加远程仓库 
git remote add origin git@github.com:WenlinJi/test.git  #每次都会改变后面的部分

【4】# 把本地的 main 分支推送到 origin 服务器上
git push -u origin main
```

![](C:\Users\051129\AppData\Roaming\Typora\typora-user-images\image-20220516112425778.png)

如果后续本地仓库里修改了什么文件，再`git add commit push`三连即可。

```text
git status
git add .
git commit -m '添加展示图片和README说明'
git push origin gh-pagesgit
```



---



### 本地仓库搭建

创建本地仓库的方法有两种：一种是创建全新的仓库，另一种是克隆远程仓库。

**创建全新的仓库**，

> 点右上角**+**号处的**New repository**或者直接打开 https://github.com/new ；在`Repository name`处填写仓库名称，因为和后续网页展示的URL挂钩，建议取个可读性好点的名称，最后点绿色按钮**Create repository**，一个空的仓库就创建成功（不带`readme.md`和`.gitignore`），后续只需将本地仓库的代码推送到此处即可

1、需要用GIT管理的项目的根目录执行：

```
# 在当前目录新建一个Git代码库
$ git init
```

2、执行后可以看到，仅仅在项目目录多出了一个.git目录，关于版本等的所有信息都在这个目录里面。



**或者 采取克隆远程仓库：**

1、另一种方式是克隆远程目录，由于是将远程服务器上的仓库完全镜像一份至本地！

```
# 克隆一个项目和它的整个代码历史(版本信息)
$ git clone [url] 
# SSH 链接:  git@github.com:WenlinJi/first-personalweb.git
```

2、去 gitee 或者 github 上克隆一个测试！





### git分支操作

> git branch用法总结，查看、新建、删除、重命名：**https://www.jianshu.com/p/aea408814ebe**
>
> **git 中一些选项解释**
>
> **-d**  --delete：删除
>
> **-D**  --delete --force的快捷键
>
> **-f**  --force：强制
>
> **-m**  --move：移动或重命名
>
> **-M**  --move --force的快捷键
>
> **-r**  --remote：远程
>
> **-a**  --all：所有

1.首先切换到master分支上，确认工作目标是干净的，也没有需要[commit](https://so.csdn.net/so/search?q=commit&spm=1001.2101.3001.7020)的；

```
  查看分支：$ git branch
  查看状态：$ git status
```

2.新建远程分支

```
# 列出所有本地分支，星号(*)表示当前所在分支。现在的状态是成功创建的新的分支并且已经切换到新分支上。
git branch

# 列出所有远程分支
git branch -r

# 合并指定分支到当前分支
$ git merge [branch]


===========================================
# 本地新建一个分支，但依然停留在当前分支
git branch 【分支名】

# 本地新建一个分支，并切换到该分支
git checkout -b 【分支名】


本地创建分支成功后，我们会发现远程端并没有分支产生
· git status (查看文件状态)
· git add “test.txt” (添加推送文件)
· git status (再次文件状态)
· git commit -m “test.txt” (提交文件)


# 把新建的本地分支push到远程服务器，远程分支与本地分支同名（当然可以随意起名）：
$ git push origin 【分支名:分支名】
或者===>  git push origin 【分支名】 --set-upstream (推送)


//使用git branch -a查看所有分支，会看到remotes/origin/localbranch这个远程分支，说明新建远程分支成功。
```

3.删除远程分支

```
也可以使用：
$ git push origin --delete localbranch

这两种方式都可以删除指定的远程分支


===========================================
# 删除本地分支  ==》 附：当前所在的工作分支是不能够被删除的
$ git branch -d 【分支名】

· git 分支名 -d ：删除
· git 分支名 -D ：强制删除 （一般情况下不用）


# 删除远程分支
$ git push origin --delete 【分支名】
或者 $ git branch -dr [remote/branch]
或者 $ git branch -r -d origin/分支名

或者，我比较喜欢的简单方式，推送一个空分支到远程分支，其实就相当于删除远程分支：
$ git push origin :【分支名】


git branch -d -r <branchname>
删除远程分支，其中<branchname>为本地分支名
删除后，还要推送到服务器上才行，即git push origin :<branchname>
```







### 文件的四种状态

版本控制就是对文件的版本控制，要对文件进行修改、提交等操作，首先要知道文件当前在什么状态，不然可能会提交了现在还不想提交的文件，或者要提交的文件没提交上。

- Untracked: 未跟踪, 此文件在文件夹中, 但并没有加入到git库, 不参与版本控制. 通过git add 状态变为Staged.

- Unmodify: 文件已经入库, 未修改, 即版本库中的文件快照内容与文件夹中完全一致. 这种类型的文件有两种去处, 如果它被修改, 而变为Modified. 如果使用git rm移出版本库, 则成为Untracked文件

- Modified: 文件已修改, 仅仅是修改, 并没有进行其他的操作. 这个文件也有两个去处, 通过git add可进入暂存staged状态, 使用git  checkout 则丢弃修改过, 返回到unmodify状态, 这个git checkout即从库中取出文件, 覆盖当前修改 !

- Staged: 暂存状态. 执行git commit则将修改同步到库中, 这时库中的文件和本地文件又变为一致, 文件为Unmodify状态. 执行git reset HEAD filename取消暂存, 文件状态为Modified

  

#### 查看文件状态

上面说文件有4种状态，通过如下命令可以查看到文件的状态：

```
#查看指定文件状态
git status [filename]

#查看所有文件状态
git status
```





## 部署静态页面

**官方文档：**

> **https://docs.github.com/cn/pages/getting-started-with-github-pages/creating-a-github-pages-site**

- **`GitHub Pages`搭建过个人博客：【涉及其他git相关学习】**

==**https://zhuanlan.zhihu.com/p/69592043**==

> 本文不对`Git`做过多介绍，默认大家已经完成安装配置，没有的可以看看：[Git 安装配置](https://www.runoob.com/git/git-install-setup.html)和[Git 远程仓库(Github)](https://www.runoob.com/git/git-remote-repo.html)；小白可以看这篇指南快速了解下：[Git- 简明指南 - 助你入门 Git的简明指南，木有高深内容](http://rogerdudler.github.io/git-guide/index.zh.html)；想系统学习的可以看：[Git 教程- 廖雪峰的官方网站](https://www.liaoxuefeng.com/wiki/896043488029600)；想快速查找命令的可以看：[常用 Git 命令清单](https://github.com/guanguans/notes/blob/master/Git/常用Git命令清单.md)。
>
> 
>
> **新建仓库，添加内容：**
>
> ```text
> # 将该文件夹变成用git管理的本地仓库
> git init
> # 查看所有文件，多出 .git 文件
> ls -al
> # 新建后对项目进行介绍
> touch README.md
> # 新建后可以写入后续不想提交到GitHub上的文件
> touch .gitignore
> 
> # 列出所有本地分支和远程分支，仓库默认在 master 分支
> git branch -a
> # 新建并切换到 gh-pages 分支
> git checkout -b gh-pages
> # 显示有变更的文件
> git status
> # 删除 master 分支
> git branch -d master
> # 添加当前目录的所有文件到暂存区
> git add .
> # 提交暂存区到仓库区，并添加代码提交信息
> git commit -m 'first commit'
> 
> # 添加远程仓库
> git remote add origin git@github.com:WenlinJi/first-personalweb.git
> # 把本地的 gh-pages 分支推送到 origin 服务器上
> git push origin gh-pages
> ```
>
> 



- 狂神说：【视频加配套笔记】

视频：https://www.bilibili.com/video/BV1FE411P7B3?spm_id_from=333.337.search-card.all.click

笔记：https://mp.weixin.qq.com/s/Bf7uVhGiu47uOELjmC5uXQ



- **码云搭建：**

> https://blog.csdn.net/weixin_49455047/article/details/121714615
>
> https://blog.csdn.net/weixin_45697314/article/details/106170149





## SSH密钥获取

> **指导视频：**https://www.bilibili.com/video/BV1qT4y1v7n1/?spm_id_from=pageDriver

> **Gitee网站的参考教程：**https://gitee.com/help/articles/4181#article-header0

![image-20220414095107746](C:\Users\051129\AppData\Roaming\Typora\typora-user-images\image-20220414095107746.png)

> **Github添加SSH的地方:** https://github.com/settings/keys





## 最初一版学习

1. 从仓库中获取内容到本地

   ```
   git clone git@github.com:gin051129/gin051129.github.io.git
   ```

   

2. ==一定要到**工作区**（刚下载好的文件要点进去才是工作区）中打开D:\GitProject\gin051129.github.io==

   - 先查看是否要配置我是谁

     ```
     git config -l
     ```

     ![image-20220414100414950](C:\Users\051129\AppData\Roaming\Typora\typora-user-images\image-20220414100414950.png)

   3. 查看是否有人控制  //检查文件区别

      ```
      git status
      ```

      ![image-20220414100603057](C:\Users\051129\AppData\Roaming\Typora\typora-user-images\image-20220414100603057.png)

   4. ```
      git add .
      ```

      ```
      git commit -m "更新的注释："
      ```

      ```
      git push 
      ```


   > https://blog.csdn.net/bjbz_cxy/article/details/116703787



# 系统自带快捷键

| 快捷键                     | 作用                 |
| :------------------------- | :------------------- |
| ctrl  + shift + b          | 显示微软自带的表情   |
| Win+V                      | 打开剪贴板的历史记录 |
| Ctrl+Z                     | 撤销上一步的操作     |
| Ctrl+Y                     | 复原刚才撤销的操作   |
| Ctrl+X                     | 剪切的快捷键         |
| Win+G                      | 系统录屏             |
| Ctrl+L                     | 快速锁屏             |
| Win+空格【ctrl  + shift 】 | 切换输入法           |
|                            |                      |


​      

## **各种编辑器：**

光标确定开头，按住Shift再用鼠标确定结尾
Ctrl+A          全选
Ctrl+F          找关键词
Shift+字母   在英文小写和中文情况下直接大写字母



## **截图：**

Ctrl+F1    启动Snipsate截图
F2            将截图粘贴至桌面

（Win+Shift+S   自定义截图）



## **文件夹：**

Ctrl+Shift+N           快速新建文件夹
按住Ctrl拖动文件    快速复制文件
按住Alt双击文件     快速打开文件属性





# Typora使用技巧 



> ## windows快捷键：[#](https://www.cnblogs.com/hongdada/p/9776547.html#windows快捷键)
>
> - 无序列表：输入-之后输入空格
>
> - 有序列表：输入数字+“.”之后输入空格
>
> - 任务列表：-[空格]空格 文字
>
> - 标题：ctrl+数字
>
> - 表格：ctrl+t
>
> - 生成目录：`[TOC]`按回车
>
> - 选中一整行：ctrl+l
>
> - 选中单词：ctrl+d
>
> - 选中相同格式的文字：ctrl+e
>
> - 跳转到文章开头：ctrl+home
>
> - 跳转到文章结尾：ctrl+end
>
> - **搜索：ctrl+f**
>
> - 替换：ctrl+h
>
> - 引用：输入>之后输入空格
>
> - 代码块：ctrl+shift+k
>
> - 加粗：ctrl+b
>
> - 倾斜：ctrl+i
>
> - 下划线：ctrl+u
>
> - 删除线：alt+shift+5
>
> - 插入图片：直接拖动到指定位置即可或者ctrl+shift+i
>
> - 插入链接：ctrl + k
>
>   ![img](https://img2018.cnblogs.com/blog/443934/201810/443934-20181012170159282-378811511.png)

- Ctrl+Shift+f     全局搜索

- 高亮`==highlight==` 显示为 ==highlight==

- shift+tab 可以一键调节typora的代码缩进
- 定位到文字后，ctrl+加号/减号，可以放大/缩小文字
- ctrl+shift+加号/减号可以对整体页面进行放大/缩小
- ctrl+键盘右侧home定位到第一行，ctrl+end定位到文章末尾
- ctrl+shift+【   对段落标序号，或者数字加 "."即可
  ctrl+shift+ 】  对段落标小点（无序列表）
- ctrl+横排数字键n，可将字体设置为n级标题

1、先将复制网页到记事本后，再将记事本中的复制到word，结果，背景色是没有了但是网页上的图也没有了，只得文字和图片分开复制，图片直接复制到word，而文字单独用记事本处理后再复制到word，很繁琐！
2、复制网页到word后，再全选后点击字符底纹按钮，结果，文字部分的黑灰背景变得很淡的底纹，文字看得清了，图片也没有问题，但是文字和图片的外部还是黑灰色，而且文字的淡色底纹也让人觉得不完美，总之看着很不爽！

3、点击：格式——边框和底纹——底纹——“填充”选“无填充颜色”；“应用”选“段落”（若只是文字有黑灰底色，而文字和图片外部没有黑灰底色，则“应用”选“文字”即可）



# Linux虚拟机相关

ifconfig  -- linux中查ip
ipconfig -- Windows中查ip
设置--网络和Internet--更改适配器选项--VMnet8

“windows LOGO”键和字母“V”键，即可在剪贴板上查看自己复制的内容。

[O]pen Read-Only, (E)dit anyway
若是只读点键盘'o'；若是修改点键盘'e'

1.Ctrl + C 终止
2.Ctrl + D 退出
3.Ctrl + S 挂起
4.Ctrl + Q 解挂

![image-20220509191152959](C:\Users\051129\AppData\Roaming\Typora\typora-user-images\image-20220509191152959.png)





# Java相关

- Ctrl+Shift+R   IDEA中全局搜索替换

- Intellij Idea 代码自动补全：

  > 光标移动至代码最右边，Ctrl+Alt+V
  > 也可以;号前.var 也会补全

- 快速生成 doGet( ),doPost ( )方法，右键 Generate





# word

## Word如何设置第一页不显示页码

将光标移动到第一页的末尾，点击 布局-分隔符-分节符-下一页，这时候光标跳到第二页开头

![Word如何设置第一页不显示页码](https://exp-picture.cdn.bcebos.com/8b3643dd884ce54ac11ad658a3066b0193ddf794.jpg?x-bce-process=image%2Fresize%2Cm_lfit%2Cw_500%2Climit_1%2Fformat%2Cf_jpg%2Fquality%2Cq_80)

双击第二页页尾，取消“链接到前一节”

![Word如何设置第一页不显示页码](https://exp-picture.cdn.bcebos.com/5c9c964ce54a2f2708d219b1e00192dd3240f494.jpg?x-bce-process=image%2Fresize%2Cm_lfit%2Cw_500%2Climit_1%2Fformat%2Cf_jpg%2Fquality%2Cq_80)

页码-设置页码格式，改为“起始页码”为“1”，确定

![Word如何设置第一页不显示页码](https://exp-picture.cdn.bcebos.com/890dfb4a2f27e7efd83b5ab619dd3340b7f3f594.jpg?x-bce-process=image%2Fresize%2Cm_lfit%2Cw_500%2Climit_1%2Fformat%2Cf_jpg%2Fquality%2Cq_80)

![Word如何设置第一页不显示页码](https://exp-picture.cdn.bcebos.com/e40b3127e7ef28069a3ca36ab840b6f39087f294.jpg?x-bce-process=image%2Fresize%2Cm_lfit%2Cw_500%2Climit_1%2Fformat%2Cf_jpg%2Fquality%2Cq_80)

然后就开始插入页码

![Word如何设置第一页不显示页码](https://exp-picture.cdn.bcebos.com/2e66f9ef28066b0160e002f73df39187021cf394.jpg?x-bce-process=image%2Fresize%2Cm_lfit%2Cw_500%2Climit_1%2Fformat%2Cf_jpg%2Fquality%2Cq_80)

插入成功，从第二页开始显示1，第一页不显示

![Word如何设置第一页不显示页码](https://exp-picture.cdn.bcebos.com/e6ae36066b0192ddc07d87441a87031c98c0f094.jpg?x-bce-process=image%2Fresize%2Cm_lfit%2Cw_500%2Climit_1%2Fformat%2Cf_jpg%2Fquality%2Cq_80)

END





# ==好用的工具加教程==

**https://www.zhihu.com/question/388789219/answer/1955501175**



- 思维导图，流程图：画图软件 —— iodraw

  https://blog.csdn.net/qq_37541097/article/details/116024091



- cmd + Cmder 命令行 安装及使用教程技巧 
  主要参考：https://blog.csdn.net/sunsineq/article/details/122818453

  安装流程清晰：https://blog.csdn.net/dangerous317/article/details/122552643

  解释了cmd和cmder:https://blog.csdn.net/vanarrow/article/details/108025977

  



- 视频下载工具：you-get使用命令
  https://blog.csdn.net/qq_41251963/article/details/112920411

  https://blog.csdn.net/dreamer0823/article/details/89438512



# 清理电脑

- 清除缓存：win+r ,再输入 %temp%
  - **shift+del【不通过回收站删除文件】**



- 怎么删除右键出现的Open Folder as Intellij IDEA Project

  https://blog.csdn.net/qq_45266900/article/details/118972037

  https://blog.csdn.net/hOWtOdOthIs/article/details/90576965

# 简历制作

> https://www.bilibili.com/video/BV19L411j7K8?spm_id_from=333.337.search-card.all.click
>
> 在控制台使用`document.designMode='on'`,改变原版的内容
>
> ![image-20220508151809141](C:\Users\051129\AppData\Roaming\Typora\typora-user-images\image-20220508151809141.png)



```
腾讯：

* 熟练运用 HTML5、CSS3、ES6+
* 熟悉移动端Web/Hybrid开发
* 理解Web标准和兼容性
* 熟练运用至少一款主流的JS框架
* 具有良好的代码风格、接口设计与程序架构能力
* 掌握至少一门服务器端编程语言
* 思路清晰，具备良好的沟通能力和团队协作精神
```



```
职位职责:

1、负责前端技术选型和开发工作;

2、优化前端功能设计，解决各种浏览器和终端设备的兼容性问题;

3、通过技术手段，提升用户体验并满足高性能要求;

4、通用组件、类库编写，提升开发效率和质量。

职位要求:

1、本科及以上学历，2022年及以后毕业的在校同学，计算机相关专业;

2、精通HTML、CSS、JavaScript，熟悉页面架构和布局，熟悉HTML5/CSS3等常用技术;

3、熟悉常用UI框架（如antd、element-ui等);

4、精通JavaScript、ES6+或了解TypeScript等技术;

5、了解Node.js框架express 或 koa，熟练使用Webpack等构建工具;

6、具备MVVM框架开发经验，如React、Vue.js等;

7、具备良好的沟通和团队协作能力，热爱技术，责任心强,能推动技术框架的落地使用。
```

