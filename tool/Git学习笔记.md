# Git学习笔记

```c++
>>> 描述：
    代码托管平台;
>>> 网址：
    // 菜鸟教程 Git
    https://www.runoob.com/git/git-tutorial.html
```



## Git配置

```c++
>>>
```



### Git编辑器

```c++
>>> 描述：
    更改git默认的编辑器
    
>>> 操作：
    git config --global core.editor "vim"
```



### Git ssh配置

```c++
ssh-keygen -t rsa -C 'xxx@xxx.com' 然后一路回车(-C 参数是你的邮箱地址)
cd ~/.ssh
// then, add the key to gitlab sshkeys
```

```shell
#公钥：
	openssl genrsa -out rsa_private_key.pem 1024
#私钥：
	openssl rsa -in rsa_private_key.pem -pubout -out rsa_public_key.pem
```



####  SSH安装

```c++
>>> 系统：
    Ubuntu-14.04
    Ubuntu 系统默认安装了SSH客户端
    如果希望本地主机可以被其他主机通过SSH访问，则需要安装SSH服务端
>>> 依赖项：
    
>>> 安装包：
    // 安装SSH客户端
    sudo apt-get install openssh-client
    // 安装SSH服务端
	sudo apt-get install openssh-server 
>>> 参考网址：
    // SSH简介及两种远程登录的方法
    https://blog.csdn.net/li528405176/article/details/82810342
```







## Git命令

```c++
必须要说明的是，一般一个仓库中的内容代表一个项目。
```



### git add

-   **描述：**

    文件加入Git跟踪管理、将工作区文件添加到暂存区

-   **使用：**

    格式：git add [ options ] / <args>

    | 选项           | 描述                                                  |
    | -------------- | ----------------------------------------------------- |
    | git add <file> | 将指定文件添加到Git跟踪管理、将工作区文件添加到暂存区 |

    

------



### git branch

-   **描述：**

    操作分支

-   **使用**

    格式：git branch [ options ] / <args>

    | 选项                          | 说明                                         |
    | ----------------------------- | -------------------------------------------- |
    | git branch                    | 显示本地已缓存分支                           |
    | git branch < name >           | 新建分支，命名为 < name >                    |
    | git branch -a                 | 列出所有分支                                 |
    | git branch -d < branch >      | 删除< branch >所示分支                       |
    | git branch -m < old > < new > | 更改分支的名字(分支在本地，还未推送到远程)   |
    | git branch -v                 | 显示本地已缓存分支和其分支的最后一笔提交记录 |
    | git branch --merged           | 显示 与当前分支 已合并的 本地已缓存分支      |
    | git branch --no-merged        | 显示 与当前分支 未合并的 本地已缓存分支      |
    
-   **参考：**

    -   CSDN -《【Git】如何修改分支名》：https://blog.csdn.net/weixin_38629529/article/details/125359597


------



### git checkout

-   **描述：**

    切换分支，撤销修改

-   **使用：**

    格式：git checkout [ options ] / <args>

    | 选项                         | 说明                                           |
    | ---------------------------- | ---------------------------------------------- |
    | git checkout <branch>        | 切换到指定分支                                 |
    | git checkout <file>          | 撤销对文件的修改，将文件还原到上一次提交的状态 |
    | git checkout -b <new-branch> | 新建分支并切换到该分支                         |

    

------



### git clone

-   **描述：**

    建立仓库，将远程仓库克隆到本地，从而建立本地仓库

-   **使用：**

    格式：git clone [ options ] / <args>

    | 选项            | 说明                        |
    | --------------- | --------------------------- |
    | git clone <URL> | 克隆<URL>所示远程仓库到本地 |

    



### git commit

-   **描述：**

    将暂存区内容提交到本地仓库

-   **使用：**

    格式：git commit [ options ] / <args>

    | 选项                   | 描述                                         |
    | ---------------------- | -------------------------------------------- |
    | git commit             | 将暂存区内容提交到本地仓库，会打开文本编辑器 |
    | git commit -a          | 将暂存区和工作区内容都提交到本地仓库         |
    | git commit -m < info > | 以< info >所示内容为 提交 的备注信息         |
    | git commit -v          | 将在文本编辑器中显示更加详细的提交信息       |
    | git commit --amend     | 修改提交信息，可以重新编辑提交信息           |

    

------



### git config

-   **描述：**

    Git配置管理工具

-   **使用：**

    格式：git config [ options ] / <args>

    | 选项                                     | 描述                                                      |
    | ---------------------------------------- | --------------------------------------------------------- |
    | git config --system < key > < value >    | 作用于整个系统，修改 /etc/gitconfig                       |
    | git config --global < key > < value >    | 作用于当前用户，修改 ~/.gitconfig 或 ~/.config/git/config |
    | git config --local < key > < value >     | 作用于当前项目，修改 .git/config                          |
    | git config --list --show-origin          | 显示所有Git配置信息                                       |
    | git config --global user.name  <name>    | 配置用户名                                                |
    | git config --global user.email  <mail>   | 配置用户邮件                                              |
    | git config --global core.editor <editor> | 配置文本编辑器                                            |

    

------



### git diff

-   **描述：**

    比较文件差异，显示文件修改内容

-   **使用：**

    格式：git diff [ options ] / <args>

    | 选项                     | 描述                                     |
    | ------------------------ | ---------------------------------------- |
    | git diff                 | 显示工作区所有修改内容                   |
    | git diff <file-name>     | 显示指定文件在工作区的修改内容           |
    | git diff --staged        | 显示暂存区与上一次提交之间的修改内容     |
    | git diff --staged <file> | 显示暂存区文件与上一次提交之间的修改内容 |
    | git diff --cached        | 同 git diff --staged                     |
    | git diff --cached <file> | 同 git diff --staged <file>              |

-   **注意：**

    1.  请注意，git diff 本身只显示工作区中尚未暂存的改动，而不是自上次提交以来所做的所有改动。所以有时候你一下子暂
        存了所有更新过的文件，运行 git diff 后却什么也没有，就是这个原因。  



------



### git fetch

-   **描述：**

    仓库同步，拉取远程仓库数据到本地仓库。

-   **使用：**

    格式：git fetch [ options ] / <args>

    | 选项               | 说明                 |
    | ------------------ | -------------------- |
    | git fetch          | 同步当前所在仓库     |
    | git fetch < name > | 同步< name >所示仓库 |

-   **说明：**

    1.  这个命令会访问远程仓库，从中拉取所有你还没有的数据。执行完成后，你将会拥有那个远程仓库中所有分支的引用，可以随时合并或查看。  
    2.  必须注意 fetch 命令只会将数据下载到你的本地仓库——它并不会自动合并或修改你当前的工作。 当准备好时你必须手动将其合并入你的工作。  

------



### git log

-   **描述：**

    查看提交记录

-   **使用：**

    格式：git merge [ options ] / < args >

    | 选项                                 | 格式                                                         |
    | ------------------------------------ | ------------------------------------------------------------ |
    | git log                              | 按时间先后顺序列出所有 提交记录                              |
    | git log -p                           | 显示每次 提交 的改动                                         |
    | git log -p < commit-code >           | 提交记录 显示从< commit-code >所示提交开始，每次 提交 的改动。 |
    | git log -< num >                     | 显示近期的 < num > 条 提交                                   |
    | git log --patch                      | 同 git log -p                                                |
    | git log --pretty=format:"< format >" | 让 提交记录 按指定格式显示                                   |
    | git log --prett=full                 |                                                              |
    | git log --prett=fuller               |                                                              |
    | git log --pretty=oneline             | 将每次 提交 的信息在一行显示                                 |
    | git log --pretty=short               | 简短格式显示 提交记录                                        |
    | git log --stat                       | 显示每次 提交 的简略统计信息                                 |

-   **关于format格式：**

    | 选项 | 说明                                          |
    | ---- | --------------------------------------------- |
    | %H   | 提交的完整哈希值                              |
    | %h   | 提交的简写哈希值                              |
    | %T   | 树的完整哈希值                                |
    | %t   | 树的简写哈希值                                |
    | %P   | 父提交的完整哈希值                            |
    | %p   | 父提交的简写哈希值                            |
    | %an  | 作者名字                                      |
    | %ae  | 作者的电子邮件地址                            |
    | %ad  | 作者修订日期（可以用 --date=选项 来定制格式） |
    | %ar  | 作者修订日期，按多久以前的方式显示            |
    | %cn  | 提交者的名字                                  |
    | %ce  | 提交者的电子邮件地址                          |
    | %cd  | 提交日期                                      |
    | %cr  | 提交日期（距今多长时间）                      |
    | %s   | 提交说明                                      |

-   注意：

    1.  作者指的是实际作出修改的人，提交者指的是最后将此工作成果提交到仓库的人。  
    2.  提交：每一笔 commit；提交记录：提交历史，每笔 commit 集合。



------



### git merge

-   **描述：**

    分支合并

-   **使用：**

    格式：git merge [ options ] / < args >

    | 命令                     | 描述                                     |
    | ------------------------ | ---------------------------------------- |
    | git merge < obj-branch > | 将< obj-branch >分支与当前所在分支合并   |
    | git merget --abort       | 中断合并，将所在分支回退到合并之前的状态 |





------



### git mv

-   **描述：**

    移动或重命名文件

-   **使用：**

    格式：git mv [ options ] / <args>

    | 命令                     | 描述       |
    | ------------------------ | ---------- |
    | git mv <file> <new-name> | 重命名文件 |

    

------



### git pull

-   **描述：**

    将 远程仓库 与 本地仓库 同步。

-   **使用：**

    格式：git pull [ options ] / <args>

    | 选项     | 说明                                                   |
    | -------- | ------------------------------------------------------ |
    | git pull | 远程同步到本地，将当前所在本地分支与远程同名分支合并。 |

    



------



### git push

-   **描述：**

    将 本地仓库 与 远程仓库 同步

-   **使用：**

    格式：git push [ options ] / <args>

    | 选项        | 说明                                                   |
    | ----------- | ------------------------------------------------------ |
    | git push    | 本地同步到远程，将当前所在本地分支与远程同名分支同步。 |
    | git push -f | 强制同步                                               |

    

```c++
git push --set-upstream origin llh-0114
```





------



### git reset

-   **描述：**

    回退到指定的commit

-   **使用：**

    格式：git reset[ options ] / <args>
    
    | 选项                             | 说明                                           |
    | -------------------------------- | ---------------------------------------------- |
    | git reset HEAD < file >          | 将< file >所示文件从暂存区移至工作区，取消暂存 |
    | git reset --hard < commit-code > | 回退到< commit-code >所示提交                  |
    
    

------



### git rm

-   **描述：**

    移除文件

-   **使用：**

    格式：git rm[ options ] / <args>

    | 选项                    | 说明                                                         |
    | ----------------------- | ------------------------------------------------------------ |
    | git rm <file>           | 将文件从Git跟踪列表中移除，Git不再对文件进行管理，同时从磁盘删除 |
    | git rm -f <file>        | 强制删除，将删除已在暂存区或已修改的文件                     |
    | git rm --cached  <file> | 将文件从Git跟踪列表或缓存区移除，但不从磁盘删除              |

    

------



### git remote

-   **描述：**

    查看远程仓库服务器

-   **使用：**

    格式：git rmote[ options ] / <args>

    | 选项                                     | 说明                                                |
    | ---------------------------------------- | --------------------------------------------------- |
    | git remote                               | 显示远程仓库服务器名称简写                          |
    | git remote -v                            | 列出仓库服务器名称与URL                             |
    | git remote add < name > < URL >          | 添加 < URL > 所示远程仓库到本地，并命名为指定的名字 |
    | git remote remove < remote >             |                                                     |
    | git remote rename < remote > < new-name> | 将 < remote > 所示仓库 重命名为 < new-name >        |
    | git remote rm                            | 同 git remote remove < remote >                     |
    | git remote show                          | 显示当前所在仓库名                                  |
    | git remote show < remote >               | 显示 < remote > 所示仓库详细信息。                  |

-   **说明：**

    1.  如果你使用 clone 命令克隆了一个仓库，会自动将其同步到本地，成为本地仓库。而其远程仓库所在的服务器，会被默认命名为“origin”。  而 remote 命令可以让你指定仓库名。
    2.  尽管是同一个项目，但也可以放到不同的仓库服务器。就像是备份。这时候你就需要维护不同仓库服务器中的相同项目。

------

### git revert

-   **描述：**
    -   



------

### git status

-   **描述：**

    显示本地仓库状态信息

-   **使用：**

    格式：git status [ options ] / <args>

    | 选项          | 描述                       |
    | ------------- | -------------------------- |
    | git status    | 显示本地仓库状态信息       |
    | git status -s | 简洁模式显示文件的状态信息 |

-   **关于简洁模式标签：**

    1.  标签？：表示文件是新文件，Git未跟踪
    2.  标签A：表示文件是新加入到暂存区的文件
    3.  标签M：表示文件经过修改
    4.  暂存区状态栏：位于左侧
    5.  工作区状态栏：位于右侧



------



### git tag

-   **描述：**

    打标签

-   **使用：**

    格式：git tag [ options ] / <args>

    | 选项    | 说明     |
    | ------- | -------- |
    | git tag | 列出标签 |



------



## Git问题

-   **参考：**
    -   http://www.manongjc.com/detail/28-cabqggnjscbwnly.html
