###  1.简述什么是Kubernetes？

- Kubernetes是一个全新的基于容器技术的分布式系统支撑平台。是Google开源的容器集群管理系统（谷歌内部:Borg）。在Docker技术的基础上，为容器化的应用提供部署运行、资源调度、服务发现和动态伸缩等一系列完整功能，提高了大规模容器集群管理的便捷性。并且具有完备的集群管理能力，多层次的安全防护和准入机制、多租户应用支撑能力、透明的服务注册和发现机制、內建智能负载均衡器、强大的故障发现和自我修复能力、服务滚动升级和在线扩容能力、可扩展的资源自动调度机制以及多粒度的资源配额管理能力。

Kubernetes（简称K8s）是一种用来管理容器化应用程序的工具，就像是一支能够自动化管理大量容器的舞台导演。想象一下，你有很多表演者（容器）在舞台上表演不同的节目（应用程序），Kubernetes就像是一个智能的导演，负责确保每个表演者都在正确的时间出场，舞台布景恰到好处，以及在演出过程中自动解决各种问题，确保表演顺利进行。这样，你就可以轻松地管理和部署你的应用程序，而不必担心复杂的细节。

容器化应用程序种类繁多，包括但不限于：

1. Web 服务器和应用程序：例如，使用容器化的Nginx、Apache或Node.js来托管网站和Web应用程序。
2. 数据库：例如，容器化的MySQL、PostgreSQL或MongoDB用于存储和管理数据。
3. 消息队列和中间件：例如，使用容器化的RabbitMQ、Kafka或Redis来处理消息传递和数据缓存。
4. 大数据处理应用程序：例如，容器化的Apache Spark、Hadoop或Flink用于大规模数据分析和处理。
5. 微服务应用程序：例如，将整个应用程序拆分为小型、独立的服务单元，每个服务单元都可以容器化部署，如容器化的Spring Boot应用。
6. 容器化的开发工具：例如，Docker本身就是一个用于容器化应用程序的工具，也可以容器化开发环境，如容器化的IDE或代码编辑器。

这些只是一小部分容器化应用程序的例子，实际上，几乎任何类型的应用程序都可以通过容器化来简化部署、提高可移植性和灵活性。

### 2.简述Kubernetes和Docker的关系？

Kubernetes和Docker是两个不同但相关的概念，它们通常被一起使用来构建和管理容器化应用程序的整个生命周期。

1. Docker是一种容器化技术，它允许开发人员将应用程序及其所有依赖项打包到一个称为容器的独立单元中。Docker提供了一种标准的打包格式和工具集，使应用程序在不同的环境中可以一致地运行。因此，Docker负责创建、管理和运行容器。

2. Kubernetes是一个容器编排平台，它用于自动化容器化应用程序的部署、扩展和管理。Kubernetes可以管理多个Docker容器，自动调度它们在集群中的运行位置，并提供弹性、高可用性和自我修复的能力。简而言之，Kubernetes负责管理整个容器化应用程序的生命周期。

因此，可以说，Docker提供了容器化技术，而Kubernetes提供了容器化应用程序的管理和编排能力。它们通常一起使用，使开发人员能够更轻松地构建、部署和管理复杂的分布式应用程序。

### 3.简述Kubernetes如何实现集群管理？

- 在集群管理方面，Kubernetes将集群中的机器划分为一个Master节点和一群工作节点Node。其中，在Master节点运行着集群管理相关的一组进程kube-apiserver、kube-controller-manager和kube-scheduler，这些进程实现了整个集群的资源管理、Pod调度、弹性伸缩、安全控制、系统监控和纠错等管理能力，并且都是全自动完成的。

Kubernetes实现集群管理的关键在于其架构和组件的设计。以下是Kubernetes如何实现集群管理的主要步骤：

1. **Master节点**：Kubernetes集群通常由多个节点组成，其中包括至少一个Master节点和多个Worker节点。Master节点是整个集群的控制中心，负责管理和协调集群中的所有工作。（管理）

2. **API服务器**：Kubernetes集群的Master节点上运行着一个API服务器，它充当着集群管理的主要接口。所有的管理命令和操作都通过API服务器来执行。

3. **控制器管理器**：控制器管理器是Kubernetes集群中的一个核心组件，负责监视集群状态，并根据用户定义的期望状态来进行调整。比如，它会确保所需的副本数量处于正确的状态，当发现状态不符合预期时，会主动进行调整。

4. **调度器**：调度器负责将新创建的Pod（容器集合）调度到集群中的合适节点上。它会考虑诸多因素，如资源利用率、节点负载、亲和性和反亲和性规则等，以确保最佳的运行效率和负载均衡。

5. **etcd**：etcd是一个分布式键值存储系统，用于保存集群的状态信息、配置数据以及所有关于集群的重要信息。Kubernetes中的所有组件都会使用etcd来存储和检索数据，以确保集群的一致性和可靠性。

6. **Worker节点**：Worker节点是运行容器的主机，它们负责实际运行容器化的应用程序。每个Worker节点上运行着一个称为kubelet的代理程序，它负责接收来自Master节点的指令，并根据指令来创建、启动、停止或删除容器。（干活）

通过这些组件的协作，Kubernetes实现了集群管理的各项功能，包括调度容器、自动扩展、负载均衡、故障恢复等。这使得用户能够轻松地部署和管理容器化应用程序，并确保它们能够以高效、稳定和可靠的方式运行在集群中。

### 4.kubernetes组件谈谈理解

一个kubernetes集群主要是由**控制节点(master)**、**工作节点(node)**构成，每个节点上都会安装不同的组件。

**master：集群的控制平面，负责集群的决策 ( 管理 )**

> **ApiServer** : 资源操作的唯一入口，接收用户输入的命令，提供认证、授权、API注册和发现等机制
>
> **Scheduler** : 负责集群资源调度，按照预定的调度策略将Pod调度到相应的node节点上
>
> **ControllerManager** : 负责维护集群的状态，比如程序部署安排、故障检测、自动扩展、滚动更新等
>
> **Etcd** ：负责存储集群中各种资源对象的信息

**node：集群的数据平面，负责为容器提供运行环境 ( 干活 )**

> **Kubelet** : 负责维护容器的生命周期，即通过控制docker，来创建、更新、销毁容器
>
> **KubeProxy** : 负责提供集群内部的服务发现和负载均衡
>
> **Docker** : 负责节点上容器的各种操作

![image-20200406184656917](https://gitee.com/yooome/golang/raw/main/21-k8s%E8%AF%A6%E7%BB%86%E6%95%99%E7%A8%8B/images/image-20200406184656917.png)

下面，以部署一个nginx服务来说明kubernetes系统各个组件调用关系：

1. 首先要明确，一旦kubernetes环境启动之后，master和node都会将自身的信息存储到etcd数据库中

2. 一个nginx服务的安装请求会首先被发送到master节点的apiServer组件

3. apiServer组件会调用scheduler组件来决定到底应该把这个服务安装到哪个node节点上

   在此时，它会从etcd中读取各个node节点的信息，然后按照一定的算法进行选择，并将结果告知apiServer

4. apiServer调用controller-manager去调度Node节点安装nginx服务

5. kubelet接收到指令后，会通知docker，然后由docker来启动一个nginx的pod

   pod是kubernetes的最小操作单元，容器必须跑在pod中至此，

6. 一个nginx服务就运行了，如果需要访问nginx，就需要通过kube-proxy来对pod产生访问的代理

这样，外界用户就可以访问集群中的nginx服务了

### 5.kubernetes概念

**Master**：集群控制节点，每个集群需要至少一个master节点负责集群的管控

**Node**：工作负载节点，由master分配容器到这些node工作节点上，然后node节点上的docker负责容器的运行

**Pod**：kubernetes的最小控制单元，容器都是运行在pod中的，一个pod中可以有1个或者多个容器

**Controller**：控制器，通过它来实现对pod的管理，比如启动pod、停止pod、伸缩pod的数量等等

**Service**：pod对外服务的统一入口，下面可以维护者同一类的多个pod

**Label**：标签，用于对pod进行分类，同一类pod会拥有相同的标签

**NameSpace**：命名空间，用来隔离pod的运行环境

------

当涉及Kubernetes时，有几个基础概念非常重要。以下是其中一些：

1. **Pod（容器组）**：Pod是Kubernetes的最小部署单位，它可以包含一个或多个容器。这些容器共享网络和存储，并在同一个节点上运行。Pod是部署、扩展和管理的基本单位。

2. **服务（Service）**：服务是一种抽象，用于定义一组Pod的访问方式。它通过标签选择器将一组Pod组合成一个服务，并为其提供一个稳定的访问点，使其他应用程序可以通过服务名访问这些Pod，而无需关心底层Pod的具体位置。

3. **控制器（Controller）**：控制器是Kubernetes中用于管理Pod副本数量和状态的抽象。常见的控制器包括Deployment、ReplicaSet、StatefulSet等，它们负责确保所管理的Pod在集群中按照用户期望的状态运行。

4. **部署（Deployment）**：部署是一种控制器类型，用于管理Pod的部署和更新。它允许用户指定所需的Pod副本数量，并提供滚动更新、回滚和自动修复等功能。

5. **命名空间（Namespace）**：命名空间是Kubernetes中用于将集群资源划分为多个虚拟集群的一种方式。它允许用户在同一集群中创建多个逻辑分区，并将资源进行隔离和管理。

6. **节点（Node）**：节点是Kubernetes集群中的工作节点，它是运行Pod的实际主机。每个节点都有一个kubelet代理程序运行，负责与Master节点通信，并执行Pod的创建、管理和监控。

7. **容器（Container）**：容器是一种轻量级、独立的软件打包形式，其中包含应用程序及其所有依赖项。在Kubernetes中，容器通常是通过Docker等容器引擎创建的。

这些是Kubernetes的一些基础概念，理解它们对于有效地使用和管理Kubernetes集群至关重要。

### 6.简述kube-proxy作用？

kube-proxy是Kubernetes集群中的一个关键组件，其主要作用是实现服务的网络代理和负载均衡。具体来说，kube-proxy有以下几个主要功能：

1. **服务代理**：kube-proxy负责监视Kubernetes集群中的服务和端口映射的变化，并为这些服务创建网络代理。当有新的服务被创建时，kube-proxy会动态地更新代理规则，以确保可以通过服务名访问到后端Pod。

2. **负载均衡**：在服务代理的基础上，kube-proxy还负责实现服务的负载均衡。当服务有多个后端Pod时，kube-proxy会根据负载均衡策略将请求分发给这些Pod，以实现请求的均衡分配。

3. **服务发现**：通过为服务创建代理规则，kube-proxy允许其他Pod或外部用户通过服务名来访问服务，而无需了解服务后端Pod的具体IP地址和端口。这为服务发现提供了便利，使得应用程序可以更轻松地与其他服务通信。

总的来说，kube-proxy是Kubernetes中的一项重要组件，负责实现服务的网络代理、负载均衡和服务发现等功能，从而为集群中的应用程序提供稳定、可靠的网络访问。

### 7.简述Kubernetes常见的部署方式？

- kubeadm：也是推荐的一种部署方式

以下是使用 `kubeadm` 部署 Kubernetes 集群的一般步骤：

1. **准备环境**：
   - 确保所有节点满足 Kubernetes 的最低要求，如操作系统版本、内存和CPU要求等。
   - 确保节点之间能够相互通信，包括网络连通性和DNS解析。

2. **安装 Docker 或其他容器运行时**：
   - Kubernetes需要一个容器运行时来运行应用程序。通常情况下，会选择Docker或者Containerd。

3. **安装 kubeadm、kubelet 和 kubectl**：
   - 在所有节点上安装 Kubernetes 组件，可以使用包管理器或者直接下载二进制文件。

4. **初始化控制平面节点**：
   - 在其中一个节点上运行 `kubeadm init` 命令，这会初始化 Kubernetes 控制平面。你可以通过参数设置一些选项，比如指定 Pod 网络的插件。

5. **配置kubectl**：
   - 配置 `kubectl` 来连接到 Kubernetes 集群，`kubeadm init` 命令会输出相应的配置信息。

6. **部署网络插件**：
   - 部署网络插件，以便 Kubernetes 集群中的 Pod 可以相互通信。常用的网络插件包括 Calico、Flannel 和 Cilium。

7. **加入其他节点**：
   - 使用 `kubeadm join` 命令将其他节点加入到集群中。这个命令是在初始化控制平面节点时生成的。

8. **可选：配置容器运行时**：
   - 根据需要，配置容器运行时的参数，比如Cgroup驱动程序、镜像存储等。

9. **验证集群**：
   - 使用 `kubectl` 命令验证集群的状态，确保所有节点已成功加入，并且 Pod 能够正常运行。

10. **可选：添加负载均衡**：
   - 如果需要，可以添加负载均衡来分配流量到 Kubernetes 集群中的各个节点，以提高可用性和性能。

这些步骤提供了一个基本的部署流程，但具体的步骤和配置可能会因环境和需求而有所不同。在执行部署过程时，建议查阅 Kubernetes 官方文档以获取最新的指导和最佳实践。

- 二进制包部署：

以下是使用 Kubernetes 二进制包手动部署 Kubernetes 集群的一般步骤：

1. **准备环境**：
   - 确保所有节点满足 Kubernetes 的最低要求，包括操作系统版本、内存和CPU要求等。
   - 确保节点之间能够相互通信，包括网络连通性和DNS解析。

2. **安装和配置 Docker 或其他容器运行时**：
   - Kubernetes需要一个容器运行时来运行应用程序。通常情况下，你可以选择安装 Docker 或者其他容器运行时，如 Containerd。

3. **下载 Kubernetes 二进制文件**：
   - 下载所需版本的 Kubernetes 二进制文件，包括 kube-apiserver、kube-controller-manager、kube-scheduler、kubelet 和 kube-proxy 等组件。

4. **在所有节点上安装和配置 Kubernetes 组件**：
   - 将下载的 Kubernetes 二进制文件解压，并将它们放置在每个节点的合适目录中（例如 `/usr/local/bin/`）。
   - 配置每个组件的配置文件，通常位于 `/etc/kubernetes/` 目录下。这些配置文件包括 kube-apiserver、kube-controller-manager、kube-scheduler 和 kubelet 的配置。
   - 启动和配置 kubelet 服务。

5. **初始化控制平面节点**：
   - 在其中一个节点上运行 `kube-apiserver`、`kube-controller-manager` 和 `kube-scheduler`，并确保它们正确运行。
   - 运行 `kube-apiserver` 时，需要指定 API server 相关的参数，比如 `--service-cluster-ip-range`、`--etcd-servers` 等。
   - 运行 `kube-controller-manager` 时，需要指定 controller manager 相关的参数，比如 `--cluster-cidr` 等。
   - 运行 `kube-scheduler` 时，需要指定 scheduler 相关的参数，比如 `--address`、`--kubeconfig` 等。

6. **初始化工作节点**：
   - 在每个工作节点上运行 `kubelet` 和 `kube-proxy`。

7. **加入工作节点到集群**：
   - 在每个工作节点上运行 `kubelet` 和 `kube-proxy` 后，使用 `kubeadm join` 命令将其加入到 Kubernetes 集群中。该命令将在控制平面节点初始化时生成。

8. **部署网络插件**：
   - 部署网络插件，以便 Kubernetes 集群中的 Pod 可以相互通信。常用的网络插件包括 Calico、Flannel 和 Cilium。

9. **验证集群**：
   - 使用 `kubectl` 命令验证集群的状态，确保所有节点已成功加入，并且 Pod 能够正常运行。

这些步骤提供了手动部署 Kubernetes 集群的基本流程，但具体的步骤和配置可能会因环境和需求而有所不同。在执行部署过程时，建议查阅 Kubernetes 官方文档以获取最新的指导和最佳实践。

- minikube：在本地轻松运行一个单节点 Kubernetes 群集的工具。

Minikube 是一个用于在本地机器上运行单节点 Kubernetes 集群的工具，以下是使用 Minikube 部署 Kubernetes 集群的一般步骤：

1. **安装 Minikube**：
   - 根据你的操作系统，从 Minikube 的官方网站下载并安装 Minikube。通常你可以通过包管理器或者从二进制文件安装。

2. **安装 Hypervisor（可选）**：
   - 如果你打算在虚拟机中运行 Minikube，你需要在本地机器上安装一个支持的 Hypervisor，比如 VirtualBox、VMware Fusion、HyperKit 等。如果你使用 Docker Desktop，则无需安装额外的 Hypervisor。

3. **启动 Minikube**：
   - 在终端中运行 `minikube start` 命令来启动 Minikube 集群。根据你的配置和网络情况，Minikube 会下载和启动一个单节点 Kubernetes 集群。

4. **验证集群**：
   - 运行 `kubectl get nodes` 命令来验证 Minikube 集群是否已成功启动，并且节点处于 Ready 状态。

5. **管理 Minikube 集群**：
   - 你可以使用 `minikube stop`、`minikube delete` 等命令来停止或删除 Minikube 集群。另外，你还可以通过 `minikube dashboard` 命令启动 Kubernetes Dashboard 来管理集群中的资源。

6. **使用 Minikube**：
   - 一旦 Minikube 集群启动，你就可以使用 `kubectl` 命令或者 Kubernetes Dashboard 来部署和管理应用程序、服务和其他 Kubernetes 资源。你可以部署测试应用、调试容器等。

请注意，这些步骤提供了一个基本的部署流程。具体的步骤和配置可能会因环境和需求而有所不同。在执行部署过程时，建议查阅 Minikube 官方文档以获取最新的指导和最佳实践。