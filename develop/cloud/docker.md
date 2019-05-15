# Docker

**Docker由下面几样东西组成，先简单认识一下吧**

* **Docker Client** : Docker提供给用户的客户端。Docker Client提供给用户一个终端，用户输入Docker提供的命令来管理本地或者远程的服务器。
* **Docker Daemon** : Docker服务的守护进程。每台服务器（物理机或虚机）上只要安装了Docker的环境，基本上就跑了一个后台程序Docker Daemon，Docker Daemon会接收Docker Client发过来的指令,并对服务器的进行具体操作。
* **Docker Images** : 俗称Docker的镜像，这个可难懂了。你暂时可以认为这个就像我们要给电脑装系统用的系统CD盘，里面有操作系统的程序，并且还有一些CD盘在系统的基础上安装了必要的软件，做成的一张 **“只读”** 的CD。
* **Docker Registry** : 这个可认为是Docker Images的仓库，就像git的仓库一样，用来管理Docker镜像的，提供了Docker镜像的上传、下载和浏览等功能，并且提供安全的账号管理可以管理只有自己可见的私人image。就像git的仓库一样，docker也提供了官方的Registry，叫做Dock Hub\([http://hub.Docker.com\)](https://yq.aliyun.com/articles/63035?utm_campaign=wenzhang&utm_medium=article&utm_source=QQ-qun&utm_content=m_7538)
* **Docker Container** : 俗称Docker的容器，这个是最关键的东西了。Docker Container是真正跑项目程序、消耗机器资源、提供服务的地方，Docker Container通过Docker Images启动，在Docker Images的基础上运行你需要的代码。 **你可以认为Docker Container提供了系统硬件环境，然后使用了Docker Images这些制作好的系统盘，再加上你的项目代码，跑起来就可以提供服务了。** 听到这里，可能你会觉得是不是有点像一个VM利用保存的备份或者快照跑起来环境一样，其实是挺像的，但是实际上是有本质的区别，后面我会细说。

![](../../.gitbook/assets/image%20%2819%29.png)



{% embed url="https://yq.aliyun.com/articles/63035?utm\_campaign=wenzhang&utm\_medium=article&utm\_source=QQ-qun&utm\_content=m\_7538" %}

{% embed url="http://www.ruanyifeng.com/blog/2018/02/docker-tutorial.html" %}

{% embed url="https://docs.docker.com/get-started/" %}

MicroServices即我们同时启动多个Docker container来实现一个应用。

{% embed url="http://www.ruanyifeng.com/blog/2018/02/docker-wordpress-tutorial.html" %}

