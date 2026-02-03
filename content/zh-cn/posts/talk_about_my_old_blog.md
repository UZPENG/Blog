---
title: "漫谈博客来时路"
date: 2026-01-25T07:47:20+08:00
draft: false
weight: 20
sticky: true
---

## 前言

在重启博客之际，回顾自己7年前的老博客，不由心生感慨：“撒老师，我没白活！”

在这7年间，软件开发的技术迭代日新月异，如今我们已经步进了Vibe Coding的时代，
大模型重塑了软件开发的范式。这一变化让很多东西变得没有意义，也让很多东西变得更有意义。

我标题的“漫谈”是广度上的“漫谈”，也就是把我曾经写的博客都谈谈，而并非组织形式上的随便谈谈的“漫谈”。

因此，我先说一下我的组织形式。回顾我的博客，我大致将博文分为了以下几类：**编程武器**、**web架构**、**爬虫** 这三大类。

每一类，我都会解构一些重要的知识点，重新用新时代的方式表达一次；同时，对于一些淘汰落后的内容，我也会给出新时代下的替代。简单的内容就直接写在这篇博客了，复杂的内容再考虑另开博客。话不多说，我们开始吧。

## 编程武器类

[<u>git怎样使用</u>](/posts/git)、[<u>软件的集锦</u>](/posts/software)、[<u>Linux的命令</u>](/posts/linux-command)、[<u>个人域名的邮箱</u>](/posts/mail)

### 关于git

版本控制在程序开发甚至内容管理上面至关重要，`git` 就是其中的佼佼者，在 `vibe coding`的时代，`git` 依然这么重要，甚至更上一层楼。

毕竟当AI 生成搞坏你的代码的时候，如何恢复特别重要。而 `git` 能够很好的解决这个问题。

首先，**在大模型时代，我认为学习一个知识，学习宏观层面的设计尤为重要，至于细枝末节，问大模型+manual勘查即可**。

因此，我们先总结下`git`的宏观设计:

**逻辑区域的划分和状态转移**

{{< mermaid >}}
stateDiagram-v2
    [*] --> RemoteRepo: 初始化

    state "Remote Repository</br>(远端仓库)" as RemoteRepo
    state "Working Directory</br>(工作区)" as WorkSpace
    state "Staging Area</br>(暂存区)" as Stage
    state "Local Repository</br>(本地仓库)" as LocalRepo
    state "Stash Stack</br>(储藏栈)" as Stash

    RemoteRepo --> WorkSpace: git clone (克隆仓库)

    WorkSpace --> Stage: git add (添加到暂存区)
    Stage --> WorkSpace: git reset HEAD (撤销暂存)

    Stage --> LocalRepo: git commit (提交)

    LocalRepo --> WorkSpace: git checkout (检出/切换分支)
    LocalRepo --> WorkSpace: git checkout -- file (丢弃修改)

    LocalRepo --> RemoteRepo: git push (推送更新)
    RemoteRepo --> LocalRepo: git fetch (获取更新)

    RemoteRepo --> WorkSpace: git pull (拉取并合并)

    %% Git Stash 相关
    WorkSpace --> Stash: git stash (储藏当前修改)
    Stash --> WorkSpace: git stash pop (恢复并删除储藏)

    %% Git Revert 相关
    LocalRepo --> LocalRepo: git revert (撤销提交并生成新提交)
{{< /mermaid >}}


> git reset HEAD 中的 HEAD 是提交记录的引用，在此不再赘述，可通过AI检索更多引用的方式

**本地仓库管理**

以下是关于 Git 本地仓库管理中常用指令的说明表格：

| 指令 | 核心作用 | 命令参考 |
| :--- | :--- | :--- |
| **Branch** | 创建独立的开发线路，实现并行开发。 | `git branch` (查看), `git checkout -b` (创建并切换) |
| **Merge** | 将分支历史合并，保留完整提交记录（会有分叉）。 | `git merge <branch-name>` |
| **Rebase** | 变基，将提交移植到目标分支顶端，使历史线性化。 | `git rebase <branch-name>` |
| **Cherry-pick** | 拣选，将指定的某个提交单独应用到当前分支。 | `git cherry-pick <commit-id>` |
| **Reflog** | 引用日志，记录 HEAD 移动历史，用于找回误删数据。 | `git reflog` |
| **Tag** | 标记特定的发布版本节点（如 v1.0），通常不随代码变动。 | `git tag <name>`, `git push origin <tag>` |
| **Remote** | 管理远程仓库的连接别名（如 origin），实现本地与远端交互。 | `git remote -v` (查看), `git remote add` (添加) |

> 详细的用法不再赘述，使用AI问答结合实际项目多尝试即可体会其中的用处


**其他** 

还有以下这些常用内容，仅作索引，详情可使用 **大模型检索+manual勘误**：

* 在提交历史抹除指定内容(比如误提交了账号密码，需要在历史中抹除掉)
* 配置`git`(用户名、邮箱、alias、proxy、统一换行符、LFS等)
* `git hook`，Hook 就是可以在git的一些操作前后定义自己的逻辑，如：提交前自动格式化、合并时设置门禁检查等 
* `log` 查看历史；`diff` 对比不同commit的差异；`blame` 找到指定代码是谁最后改的；`merge`的冲突解决；以上这些都使用GUI的工具即可，`VSCode` 和 `IDEA全家桶`都有较好的支持


### 软件的集锦

这个没啥好说的，典型的大模型秒杀场景，现在直接根据使用场景问大模型即可，免费、开源、付费的都有

结合我们的思路，在Agentic时代，包管理工具也有广阔的空间，Windows现在也有 `choco` 了

不过话说回来，虽然包管理好用，但是有些时候我们还是需要自己编译的，所以掌握开源软件的编译也很重要

### Linux的命令

这个也是大模型秒杀的场景，最佳实践：**问大模型+manual勘误+自己多尝试**

### 个人域名的邮箱

这个现在也不用自己搞这么麻烦了，找云厂商注册域名，备案域名，绑定一些三方邮箱即可

**云厂商是个很好的练兵场，花小钱可以学习和体验各种技术，新人还是有必要的，一定要花这笔费用**

### 锐评

1. 一定要学会用命令行，多敲敲git的命令，从根本上掌握的git的设计
2. 最高效的方式就是命令行+GUI结合。命令行适合自动化，Agentic 时代更加重要；GUI适合人工介入，对人为操作更友好
3. **在大模型时代，我认为学习一个知识，学习宏观层面的设计尤为重要，至于细枝末节，问大模型+manual勘误即可**

## web架构

[<u>Java并发编程入门</u>](/posts/concurrent)、[<u>Ngnix+Tomcat+MySQL项目部署</u>](/posts/deploy-doc)、[<u>Linux-IO多路复用-SELECT/POLL/EPOLL</u>](/posts/io-multiplexing)

### 高性能

1. 首先IO多路复用时至今日，仍然是重要的技术，**批量+主动提醒是其核心的优势**。
   另外这些函数都是系统调用，也就是说如果你使用的语言比较高级，你得查查对应的IO API的底层是什么模式。
2. 并发编程旧博文理论太多了。用当前的眼光看：Java并发编程去学习`Akka`，学习什么是 `Actor 模式`; 去学习并发编程包的API，多使用现代的并发抽象源语
   另外Golang的`CSP 模式`也值得学习，那句 **不要通过共享内存来通信，而要通过通信来共享内存**颇具哲学意味。

### 部署模式

1. 独立Tomcat容器早已淘汰，拥抱`Spring Boot`吧
2. Nginx基于IO多路复用，依旧是Web的核心组件
3. 裸机部署已过时，现在是成熟的容器化时代，docker+k8s是主流。伴随k8s生态的还有：CI/CD（持续集成，持续发布）、日志监控（ELK+grafana）、告警（Prometheus）、自动扩缩容、健康检查
4. 关于docker和k8s又是长篇大论，就不在这里展开了，学习的时候，记得遵循**先学习宏观层面的设计，至于细枝末节，问大模型+manual勘误即可**
  
### 锐评

1. 多实践，多尝试，拒绝只看理论。AI大模型时代，生成代码触手可及，带着自己的想法在vibe coding 中学习，比干巴巴的理论有趣多了呢
2. 架构变化的核心思想还是KISS（Keep It Stupid Simple），人能理解的内容是有限的，所以我们要**自动化、可重复、可观测、可追踪**

## 爬虫

[<u>爬虫实践--淘数据网站的数据爬取和存储</u>](/posts/crawl)、[<u>scrapy+selenium+headless-chrome</u>](/posts/scrapy)

### HTTP协议

1. 爬虫本质上就是构造对应的网络请求去获取对应的网络相应内容。至于如何构造，那就是对应协议的细节了，因此HTTP协议的设计是需要掌握的
2. HTTP协议关键概念：URL的组成和含义、请求方法、HTTP版本、请求HEADER、请求体、响应码、响应HEADER、响应体
3. 相关知识有：REST API设计、常用HEADER及其的含义
4. HTTP版本有1.0、1.1、2.0、3.0，相关细节查对应RFC即可
5. **抽象的概念特别重要，编程大多数的时候都是现有抽象的设计，然后再编码来建模，如果你不懂抽象的概念，也就不会理解相应的API设计**
6. 你问协议为啥是这样设计的？所谓协议就是彼此协商好的通信规则。特别是浏览器，就个是按web规范实现的客户端，所以当你按照web规范实现接口时，浏览器就能进行解析和渲染。

### web前端

1. 毕竟很多内容都是通过web浏览器承载的，所以学习一些浏览器知识也很有帮助的。
2. 比如：cookie / localstorage / session / xpath / css selector / DOM / HTML 
3. 浏览器自动化目前使用 `playwright`，API简洁且有方便的等待机制，比 `selenium` 写起来舒服多了


### scrapy 

1. 这个也不深入讲了，涉及到比较多Python的知识，核心流程就是：请求、响应、数据处理、入库

### 锐评

1. 感慨时光易逝呀，以前的淘数据网站现在都已经404了
2. 反爬和反反爬内容也很多，也不再赘述，给点关键词吧：浏览器自动化、JS加解密、cloudfare金盾等等
3. **爬虫还是挺有意思的，能够激发新人学习的兴趣，配上浏览器自动化，享受vibe coding吧**


## 结语

在这里，旧博客的复盘就结束了。

很显然，内容不多，也比较简单，细节的内容大模型基本都能够很好地替代。

不过在这个过程中，还是有几个新的体会值得参考的：

1. **在大模型时代，我认为学习一个知识，学习宏观层面的设计尤为重要，至于细枝末节，问大模型+manual勘误即可**
2. **抽象的概念特别重要，编程大多数的时候都是现有抽象的设计，然后再编码来建模，如果你不懂抽象的概念，也就不会理解相应的API设计**
3. **AI大模型时代，生成代码触手可及，带着自己的想法在vibe coding 中学习，比干巴巴的理论有趣多了呢**
4. **KISS（Keep It Stupid Simple），人能理解的内容是有限的，所以我们要自动化、可重复、可观测、可追踪**

共勉




