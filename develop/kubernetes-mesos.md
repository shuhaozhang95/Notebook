# Kubernetes, mesos

OpenStack：公认的云计算IaaS平台，其管理的核心目标对象是机器（虚拟机或物理机），当然也可以管理存储和网络，但那些也大都是围绕着机器所提供的配套资源。近年来容器技术火了之后，OpenStack也开始通过各种方式增加对容器的支持，但目前OpenStack还不被视为管理容器的主流平台。

Docker：这里我假定你指的是Docker engine（也叫做Docker daemon，或最新的名字：Moby），它是一种容器运行时（container runtime）的实现，而且是最主流的实现，几乎就是容器业界的事实标准。Docker是用来创建和管理容器的，它和容器的关系就好比Hypervisor（比如：KVM）和虚拟机之间的关系。当然，Docker公司对Docker engine本身的定位和期望不仅仅在于在单机上管理容器，所以近年来一直在向Docker engine中加入各种各样的高级功能，比如：组建多节点的Docker集群、容器编排、服务发现，等等。

Kubernetes（K8s）：搭建容器集群和进行容器编排的主流开源项目（亲爹是Google），适合搭建PaaS平台。容器是Kubernetes管理的核心目标对象，它和容器的关系就好比OpenStack和虚拟机之间的关系，而它和Docker的关系就好比OpenStack和Hypervisor之间的关系。一般来说，Kubernetes是和Docker配合使用的，Kubernetes调用每个节点上的Docker去创建和管理容器，所以，你可以认为Kubernetes是大脑，而Docker是四肢。

Mesos：Mesos是一个通用资源管理平台，它所管理的核心目标对象既不是虚拟机/物理机，也不是容器，而是各种各样的计算资源（CPU、memory、disk、port、GPU等等）。Mesos会收集各个节点上的计算资源然后提供给运行在它之上的应用框架（比如：Spark、Marathon、甚至是Kubernetes）来使用，应用框架可以将收到的计算资源以自己喜欢的任何方式创建成计算任务来完成特定工作（比如：创建一个大数据任务计算个π什么的）。由于容器技术近年来的火热，Mesos也对容器进行非常深层次的支持，它内部完整地实现了一个容器运行时（类似于Docker），所以，上层的应用框架可以方便地把自己的计算任务以容器的方式在Mesos管理的计算集群中运行起来。使用Mesos的门槛相对较高（需要应用框架编写代码调用Mesos的API和其集成），但一旦用起来之后灵活性和可扩展性更高，因为Mesos并不限制应用框架如何使用计算资源（可以以容器的方式使用，也可以是其它方式，比如：传统的进程），主动权完全在应用框架自己手中。作为对比，Kubernetes只能管理容器，所有任务都必须以容器的方式来运行。为了解决门槛较高的问题（当然也是为了赚钱），Mesosphere（Mesos这个开源项目背后的商业公司）推出了DC/OS，其核心就是Mesos加一个内置的应用框架Marathon（可以用做容器编排），能够达到开箱即用的效果，安装好之后立刻就可以创建和管理容器和非容器类的任务了。

![](../.gitbook/assets/image%20%289%29.png)



* Docker 主要针对 **Paas** 平台，是以**应用**为中心。
* OpenStack 主要针对 **Iaas** 平台，以**资源**为中心，可以为上层的 PaaS 平台提供存储、网络、计算等资源。

我们也看到，OpenStack 社区和 Docker 的结合越来越紧密。然而正如其他回答所示，OpenStack 主要还是用来管理 VM（虚拟机）。  
  
另外两项技术，Kubernetes 是面向应用的 PaaS 层，Mesos 也偏向资源管理，但 Mesos 框架设计不错，基于它很容易构建 PaaS。

OpenStack 很庞大，底层资源管理能力很强。

Kubernetes 的强项在于容器编排，可以很好解决应用上云的问题。Kubernetes 可以运行在 OpenStack 上。  
  


