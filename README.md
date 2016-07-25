# docker学习笔记idoc(i-docker-book)

---

### docker的简介

  Docker是一个开源的引擎，可以轻松的为任何应用创建一个轻量级的、可移植的、自给自足的容器。简言之，docker就是用go开发的一种轻量级虚拟化容器。

  Docker 使用客户端-服务器 (C/S) 架构模式。Docker 客户端会与 Docker 守护进程进行通信。Docker 守护进程会处理复杂繁重的任务，例如建立、运行、发布你的 Docker 容器。Docker 客户端和守护进程可以运行在同一个系统上，当然你也可以使用 Docker 客户端去连接一个远程的 Docker 守护进程。Docker 客户端和守护进程之间通过 socket 或者 RESTful API 进行通信。

  Docker 守护进程运行在一台主机上。用户并不直接和守护进程进行交互，而是通过 Docker 客户端间接和其通信。Docker 客户端，实际上是 docker 的二进制程序，是主要的用户与 Docker 交互方式。它接收用户指令并且与背后的 Docker 守护进程通信，如此来回往复。


### docker的三大组件

* 镜像

  Docker 仓库用来保存镜像，可以理解为代码控制中的代码仓库。同样的，Docker 仓库也有公有和私有的概念。公有的 Docker 仓库名字是 Docker Hub。Docker Hub 提供了庞大的镜像集合供使用。这些镜像可以是自己创建，或者在别人的镜像基础上创建。Docker 仓库是 Docker 的分发部分。
  
* 仓库
  
  Docker 仓库用来保存镜像，可以理解为代码控制中的代码仓库。同样的，Docker 仓库也有公有和私有的概念。公有的 Docker 仓库名字是 Docker Hub。Docker Hub 提供了庞大的镜像集合供使用。这些镜像可以是自己创建，或者在别人的镜像基础上创建。Docker 仓库是 Docker 的分发部分。
  
* 容器

  Docker 容器和文件夹很类似，一个Docker容器包含了所有的某个应用运行所需要的环境。每一个 Docker 容器都是从 Docker 镜像创建的。Docker 容器可以运行、开始、停止、移动和删除。每一个 Docker 容器都是独立和安全的应用平台，Docker 容器是 Docker 的运行部分。
  
  
### 为什么要学习docker


### docker的优缺点

  1. 标准化应用发布，docker容器包含了运行环境和可执行程序，可以跨平台和主机使用；
  2. 快速部署和启动，VM启动一般是分钟级，docker容器启动是秒级，即启即用；
  3. 方便构建基于SOA架构或微服务架构的系统，通过服务编排，更好的松耦合；
  4. 轻量低成本，占有更少的磁盘空间，一台主机可以启动上千个容器；
  5. 方便持续集成，通过与代码进行关联使持续集成非常方便；
  6. 安全隔离的执行环境，每个运行的容器互不影响；
  7. 文件系统分离，每一个进程容器跑在完全分离的root权限的文件系统下
  资源分离，系统资源（像CPU、内存）能被指定的分配给每一个进程容器,使用cgroups
  网络分离，使用一个虚拟的接口和IP地址，每一个进程容器跑在它自己的网络命名空间
  丰富的镜像资源，用户可以方便的在此基础上构建自己的容器运行；

  #### Docker VS VM虚拟机: 优势那就是轻量和高性能和便捷性
  
  * 快 <br>
　　运行时的性能可以获取极大提升(经典的案例是提升97%) <br>
　　管理操作(启动，停止，开始，重启等等) 都是以秒或毫秒为单位的。 <br>

  * 敏捷 <br>
　　像虚拟机一样敏捷，而且会更便宜，在bare metal(裸机)上布署像点个按钮一样简单。<br>

  * 灵活 <br>
　　将应用和系统“容器化”，不添加额外的操作系统 <br>

  * 轻量 <br>
　　你会拥有足够的“操作系统”，仅需添加或减小镜像即可。在一台服务器上可以布署100~1000个Containers容器。<br>

  * 便宜 <br>
　　开源的，免费的，低成本的。由现代Linux内核支持并驱动。注* 轻量的Container必定可以在一个物理机上开启更多“容器”，注定比VMs要便宜。<br>

  * 生态系统 <br>
　　正在越来越受欢迎，只需要看一看Google的趋势就知道了， docker or LXC.  <br>
　　还有不计其数的社区和第三方应用。<br>

  * 云支持 <br>
　　不计其数的云服务提供创建和管理Linux容器框架。 <br>
　　有关Docker性能方面的优势，还可参考此IBM工程师对性能提升的评测，从各个方面比VMs(OS系统级别虚拟化)都有非常大的提升。 <br>
　　Performance Characteristics of VMs vs Docker Containers by Boden Russel (IBM) <br>
　　Performance characteristics of traditional v ms vs docker containers  <br>

  * 有争论的部分 <br>
　　任何项目都会有争论，就像Go，像NodeJS, 同样Docker也有一些。 <br>

  * 能否彻底隔离<br>
　　在超复杂的业务系统中，单OS到底能不能实现彻底隔离，一个程序的崩溃/内存溢出/高CPU占用到底会不会影响到其他容器或者整个系统?很多人对Docker能否在实际的多主机的生产环境中支持关键任务系统还有所怀疑。 注* 就像有人质疑Node.JS单线程快而不稳，无法在复杂场景中应用一样。 <br>
　　不过可喜的是，目前Linux内核已经针对Container做了很多改进，以支持更好的隔离。<br>

  * GO语言还没有完全成熟 <br>
　　Docker由Go语言开发，但GO语言对大多数开发者来说比较陌生，而且还在不断改进，距离成熟还有一段时间。此半git、半包管理的方式让一些人产生不适。 <br>

  * 被私有公司控制  <br>
　　Docker是一家叫Dotcloud的私有公司设计的，公司都是以营利为目的，比如你没有办法使用源代码编绎Docker项目，只能使用黑匣子编出的Docker二进制发行包，未来可能不是完全免费的。 目前Docker已经推出面向公司的企业级服务(咨询、支持和培训)。 <br>
  

### docker的应用场景


### docker的安装与使用

