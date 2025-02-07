## Git常用命令汇总

### 远程仓库相关命令

| Name         | CMD                                       |
| ------------ | ----------------------------------------- |
| 检出仓库     | git clone git://github.com/xxxx/xxxx.git  |
| 查看远程仓库 | git remote -v                             |
| 添加远程仓库 | git remote add [name] [url]               |
| 删除远程仓库 | git remote rm [name]                      |
| 修改远程仓库 | git remote set-url --push [name] [newUrl] |
| 拉取远程仓库 | git pull [remoteName] [localBranchName]   |
| 推送远程仓库 | git push [remoteName] [localBranchName]   |
|              |                                           |

### 分支(branch)操作相关命令

| Name                                                         | CMD                           |
| ------------------------------------------------------------ | ----------------------------- |
| 查看本地分支                                                 | git branch                    |
| 查看远程分支                                                 | git branch -r                 |
| 创建本地分支（注意新分支创建后不会自动切换为当前分支）       | git branch [name]             |
| 切换分支                                                     | git checkout [name]           |
| 创建新分支并立即切换到新分支                                 | git checkout -b [name]        |
| 删除分支（-d选项只能删除已经参与了合并的分支，对于未有合并的分支是无法删除的。如果想强制删除一个分支，可以使用-D选项） | git branch -d [name]          |
| 合并分支（将名称为[name]的分支与当前分支合并）               | git merge [name]              |
| 创建远程分支(本地分支push到远程)                             | git push origin [name]        |
| 删除远程分支                                                 | git push origin :heads/[name] |

```
Ps :  我从master分支创建了一个issue5560分支，做了一些修改后，使用git push origin master提交，但是显示的结果却是'Everything up-to-date'，发生问题的原因是git push origin master 在没有track远程分支的本地分支中默认提交的master分支，因为master分支默认指向了origin master 分支，这里要使用git push origin issue5560：master 就可以把issue5560推送到远程的master分支了。

$ git push origin test:master         	// 提交本地test分支作为远程的master分支 //好像只写这一句，远程的github就会自动创建一个test分支
$ git push origin test:test              	// 提交本地test分支作为远程的test分支

如果想删除远程的分支呢？类似于上面，如果:左边的分支为空，那么将删除:右边的远程的分支。

$ git push origin :test              		  // 刚提交到远程的test将被删除，但是本地还会保存的，不用担心
```

### 版本(tag)操作相关命令

| Name                             | CMD                               |
| -------------------------------- | --------------------------------- |
| 查看版本                         | git tag                           |
| 创建版本                         | git tag [name]                    |
| 删除版本                         | git tag -d [name]                 |
| 查看远程版本                     | git tag -r                        |
| 创建远程版本(本地版本push到远程) | git push origin [name]            |
| 删除远程版本                     | git push origin :refs/tags/[name] |
|                                  |                                   |

### 子模块(submodule)相关操作命令

```
添加子模块：	**$ git submodule add [url] [path]**
如：$ git submodule add git://github.com/soberh/ui-libs.git src/main/webapp/ui-libs
初始化子模块：**$ git submodule init** ----只在首次检出仓库时运行一次就行
更新子模块：	**$ git submodule update** ----每次更新或切换分支后都需要运行一下
删除子模块：（分4步走哦）
1)$ git rm --cached [path]
2) 编辑“.gitmodules”文件，将子模块的相关配置节点删除掉
3) 编辑“.git/config”文件，将子模块的相关配置节点删除掉
4) 手动删除子模块残留的目录

5）忽略一些文件、文件夹不提交
在仓库根目录下创建名称为“.gitignore”的文件，写入不需要的文件夹名或文件，每个元素占一行即可，如
target
bin
*.db
```





## Linux调试问题汇总

### libncurses.so.5

问题：arm-none-eabi-gdb: error while loading shared libraries: libncurses.so.5: cannot open shared object file: No such file or directory

解决：

1.sudo apt install apt-file 

2.sudo apt-file update

3.sudo apt-file find libncurses.so.5

4.sudo apt install libncurses5





## GDB调试问题汇总

### gdb无法下载调试

问题：远程linux可连接本地gdb server，但是一旦load elf文件就会卡死，如下图：

![1585459602666](C:\Users\AngusChan\AppData\Roaming\Typora\typora-user-images\1585459602666.png)

解决：

待解决