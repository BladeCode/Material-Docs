# Git 学习笔记
2016-01-19 19:59:08

Git属于分布式版本控制管理系统。在这类系统中，像 Git、Mercurial、Bazaar 以及 Darcs 等，客户端并不只提取最新版本的文件快照，而是把代码仓库完整地镜像下来。 这么一来，任何一处协同工作用的服务器发生故障，事后都可以用任何一个镜像出来的本地仓库恢复。 因为每一次的克隆操作，实际上都是一次对代码仓库的完整备份。

#### Git特点
1. 直接记录快照，而非差异比较，Git只关心文件数据的整体是否发生变化，而不会关心文件内容的具体差异。
2. 近乎所有操作都是本地执行，在 Git 中的绝大多数操作都只需要访问本地文件和资源，不用连网
3. 时刻保持数据完整性，在保存到 Git 之前，所有数据都要进行内容的校验和（checksum）计算，并将此结果作为数据的唯一标识和索引
4. 多数操作仅添加数据，常用的 Git 操作大多仅仅是把数据添加到数据库

#### Git工作流程
![git-workflow](../assets/images/gitpages-git-workflow.png)
名词解释：

1. Workspace：工作区
2. Index / Stage：暂存区
3. Repository：仓库区（或本地仓库）
4. Remote：远程仓库

#### Git安装配置
1. Git下载官网：[地址](https://git-scm.com/downloads)
2. Git用户配置：
    * Git用户级别：system(系统全局) < global(当前用户) < local(当前仓库)
    ``` git
    git config --global user.name "xxxxx"
    git config --global user.email xxx@xxxx.com
    ```
    * Git查看配置：
    ``` git
    #git查看全局配置信息
    git config --list
    ```
    * Git获取帮助：
    ``` git
    #git查看帮助文档html格式
    git config --help
    #git查看帮助
    git help 或者 git --help
    ```

#### Git项目仓库
1. 在现存的目录下，通过导入所有文件来创建新的Git仓库
```git
#要对现有的某个项目开始用Git管理，只需到此项目所在的目录，执行：
git init
```
2. 从已有的Git仓库克隆出一个新的镜像仓库来
```git
git clone [url地址]
```