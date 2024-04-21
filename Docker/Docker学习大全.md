# 1 Docker简介

## 1.1 是什么？

### 1.1.1 问题：为什么会有docker出现？

假定您在开发一个尚硅谷的谷粒商城，您使用的是一台笔记本电脑而且您的开发环境具有特定的配置。其他开发人员身处的环境配置也各有不同。您正在开发的应用依赖于您当前的配置且还要依赖于某些配置文件。此外，您的企业还拥有标准化的测试和生产环境，且具有自身的配置和一系列支持文件。您希望尽可能多在本地模拟这些环境而不产生重新创建服务器环境的开销。请问？

您要如何确保应用能够在这些环境中运行和通过质量检测？并且在部署过程中不出现令人头疼的版本、配置问题，也无需重新编写代码和进行故障修复？

答案就是使用容器。Docker之所以发展如此迅速，也是因为它对此给出了一个标准化的解决方案-----系统平滑移植，容器虚拟化技术。

环境配置相当麻烦，换一台机器，就要重来一次，费力费时。很多人想到，能不能从根本上解决问题，软件可以带环境安装？也就是说，安装的时候，把原始环境一模一样地复制过来。开发人员利用 Docker 可以消除协作编码时“在我的机器上可正常工作”的问题。

![image-20240407211546001](C:\Users\JB.Lee\AppData\Roaming\Typora\typora-user-images\image-20240407211546001.png)

之前在服务器配置一个应用的运行环境，要安装各种软件，就拿尚硅谷电商项目的环境来说，Java/RabbitMQ/MySQL/JDBC驱动包等。安装和配置这些东西有多麻烦就不说了，它还不能跨平台。假如我们是在 Windows 上安装的这些环境，到了 Linux 又得重新装。况且就算不跨操作系统，换另一台同样操作系统的服务器，要移植应用也是非常麻烦的。

传统上认为，软件编码开发/测试结束后，所产出的成果即是程序或是能够编译执行的二进制字节码等(java为例)。而为了让这些程序可以顺利执行，开发团队也得准备完整的部署文件，让维运团队得以部署应用程式，开发需要清楚的告诉运维部署团队，用的全部配置文件+所有软件环境。不过，即便如此，仍然常常发生部署失败的状况。Docker的出现使得Docker得以打破过去「程序即应用」的观念。透过镜像(images)将作业系统核心除外，运作应用程式所需要的系统环境，由下而上打包，达到应用程式跨平台间的无缝接轨运作。

### 1.1.2 Docker理念

Docker是基于Go语言实现的云开源项目。

Docker的主要目标是“Build，Ship and Run Any App,Anywhere”，也就是通过对应用组件的封装、分发、部署、运行等生命周期的管理，使用户的APP（可以是一个WEB应用或数据库应用等等）及其运行环境能够做到“一次镜像，处处运行”。



![image-20240407212632130](C:\Users\JB.Lee\AppData\Roaming\Typora\typora-user-images\image-20240407212632130.png)

![image-20240407213303108](C:\Users\JB.Lee\AppData\Roaming\Typora\typora-user-images\image-20240407213303108.png)

### 1.1.3 一句话

解决了运行环境和配置问题的软件容器，方便做持续集成并有助于整体发布的容器虚拟化技术。

## 1.2 容器与虚拟机比较

### 1.2.1 容器发展简史

![image-20240407213848468](C:\Users\JB.Lee\AppData\Roaming\Typora\typora-user-images\image-20240407213848468.png)

### 1.2.2 传统虚拟机技术

虚拟机（virtual machine）就是带环境安装的一种解决方案。

它可以在一种操作系统里面运行另一种操作系统，比如在Windows10系统里面运行Linux系统CentOS7。应用程序对此毫无感知，因为虚拟机看上去跟真实系统一模一样，而对于底层系统来说，虚拟机就是一个普通文件，不需要了就删掉，对其他部分毫无影响。这类虚拟机完美的运行了另一套系统，能够使应用程序，操作系统和硬件三者之间的逻辑不变。  

![image-20240407214218866](C:\Users\JB.Lee\AppData\Roaming\Typora\typora-user-images\image-20240407214218866.png)

虚拟机的缺点：

1    资源占用多               2    冗余步骤多                 3    启动慢

### 1.2.3 容器虚拟化技术

由于前面虚拟机存在某些缺点，Linux发展出了另一种虚拟化技术：

Linux容器(Linux Containers，缩写为 LXC)

Linux容器是与系统其他部分隔离开的一系列进程，从另一个镜像运行，并由该镜像提供支持进程所需的全部文件。容器提供的镜像包含了应用的所有依赖项，因而在从开发到测试再到生产的整个过程中，它都具有可移植性和一致性。

Linux 容器不是模拟一个完整的操作系统而是对进程进行隔离。有了容器，就可以将软件运行所需的所有资源打包到一个隔离的容器中。容器与虚拟机不同，不需要捆绑一整套操作系统，只需要软件工作所需的库资源和设置。系统因此而变得高效轻量并保证部署在任何环境中的软件都能始终如一地运行。

![image-20240407214854720](C:\Users\JB.Lee\AppData\Roaming\Typora\typora-user-images\image-20240407214854720.png)

### 1.2.4 对比

![img](https://cdn.nlark.com/yuque/0/2022/png/27791237/1657880996734-690ddcbe-c837-416f-824f-ad393c62d5c3.png)

 比较了 Docker 和传统虚拟化方式的不同之处：

*传统虚拟机技术是虚拟出一套硬件后，在其上运行一个完整操作系统，在该系统上再运行所需应用进程；

*容器内的应用进程直接运行于宿主的内核，容器内没有自己的内核且也没有进行硬件虚拟。因此容器要比传统虚拟机更为轻便。

\* 每个容器之间互相隔离，每个容器有自己的文件系统 ，容器之间进程不会相互影响，能区分计算资源。

## 1.3 能干嘛

### 1.3.1 技术职级变化

coder -> programmer -> software engineer -> DevOps engineer

### 1.3.2 开发/运维（DevOps）新一代开发工程师

#### 1.3.2.1 一次构建、随处运行

**更快速的应用交付和部署**

传统的应用开发完成后，需要提供一堆安装程序和配置说明文档，安装部署后需根据配置文档进行繁杂的配置才能正常运行。Docker化之后只需要交付少量容器镜像文件，在正式生产环境加载镜像并运行即可，应用安装配置在镜像里已经内置好，大大节省部署配置和测试验证时间。

**更便捷的升级和扩缩容**

随着微服务架构和Docker的发展，大量的应用会通过微服务方式架构，应用的开发构建将变成搭乐高积木一样，每个Docker容器将变成一块“积木”，应用的升级将变得非常容易。当现有的容器不足以支撑业务处理时，可通过镜像运行新的容器进行快速扩容，使应用系统的扩容从原先的天级变成分钟级甚至秒级。

**更简单的系统运维**

应用容器化运行后，生产环境运行的应用可与开发、测试环境的应用高度一致，容器会将应用程序相关的环境和状态完全封装起来，不会因为底层基础架构和操作系统的不一致性给应用带来影响，产生新的BUG。当出现程序异常时，也可以通过测试环境的相同容器进行快速定位和修复。

**更高效的计算资源利用**

Docker是内核级虚拟化，其不像传统的虚拟化技术一样需要额外的Hypervisor支持，所以在一台物理机上可以运行很多个容器实例，可大大提升物理服务器的CPU和内存的利用率。

#### 1.3.2.2 Docker应用场景

![img](https://cdn.nlark.com/yuque/0/2022/png/27791237/1657881290040-78a22fd8-751e-4086-b6dc-2639014968d6.png)

### 1.3.3 哪些企业在使用

**新浪**

![img](https://cdn.nlark.com/yuque/0/2022/png/27791237/1657881441251-509ebbd9-ade6-4f60-9636-9c2080ed3af0.png)

![img](https://cdn.nlark.com/yuque/0/2022/png/27791237/1657881445543-04310f31-a5cf-45e9-9f75-499a75b5c46b.png)

![img](https://cdn.nlark.com/yuque/0/2022/png/27791237/1657881450387-3ac29e28-516f-4b8a-8c62-3c11e9e4fcfd.png)

![img](https://cdn.nlark.com/yuque/0/2022/png/27791237/1657881454056-681bbe5f-7a38-417c-ae6b-e3f5f2527d3c.png)

**美团**

![img](https://cdn.nlark.com/yuque/0/2022/png/27791237/1657881467654-27e45b82-cd64-44e0-a25a-8d250097633c.png)

![img](https://cdn.nlark.com/yuque/0/2022/png/27791237/1657881471736-2541e62f-fea1-441b-a4c9-58f55cb82ea3.png)

**蘑菇街**

![img](https://cdn.nlark.com/yuque/0/2022/png/27791237/1657881498336-1e4ec7a9-a263-410c-820d-79f99232596a.png)

![img](https://cdn.nlark.com/yuque/0/2022/png/27791237/1657881504105-0f0998a9-6f71-49e4-8a39-d4d32a1263de.png)

## 1.4 去哪下

### 1.4.1 官网

docker官网：http://www.docker.com

### 1.4.2 仓库

Docker Hub官网: https://hub.docker.com/

# 2 Docker安装

## 2.1 前提说明

CentOS Docker 安装

![img](https://cdn.nlark.com/yuque/0/2022/png/27791237/1658125998124-ae2d8764-3a68-4259-b7df-a945e02505e3.png)

前提条件

目前，CentOS 仅发行版本中的内核支持 Docker。Docker 运行在CentOS 7 (64-bit)上，

要求系统为64位、Linux系统内核版本为 3.8以上，这里选用Centos7.x

查看自己的内核

uname命令用于打印当前系统相关信息（内核版本号、硬件架构、主机名称和操作系统类型等）。

![img](https://cdn.nlark.com/yuque/0/2022/png/27791237/1658126004570-975d10a1-54ff-444b-9ae6-6f2f6252221b.png)

## 2.2 Docker的基本组成

![img](https://cdn.nlark.com/yuque/0/2022/png/27791237/1658126239499-f71db64a-4246-4167-bd7c-eb71b2b606be.png)

入门：

Docker是一个Client-Server结构的系统，Docker守护进程运行在主机上， 然后通过Socket连接从客户端访问，守护进程从客户端接受命令并管理运行在主机上的容器。 容器，是一个运行时环境，就是我们前面说到的集装箱。可以对比mysql演示对比讲解

![img](https://cdn.nlark.com/yuque/0/2022/png/27791237/1658126258223-a333c821-0360-4ab7-a9f8-3d77f0f39b0d.png)

### 2.2.1 镜像(image)

![image-20240407230730565](C:\Users\JB.Lee\AppData\Roaming\Typora\typora-user-images\image-20240407230730565.png)

Docker 镜像（Image）就是一个只读的模板。镜像可以用来创建 Docker 容器，一个镜像可以创建很多容器。

它也相当于是一个root文件系统。比如官方镜像 centos:7 就包含了完整的一套 centos:7 最小系统的 root 文件系统。

相当于容器的“源代码”，docker镜像文件类似于Java的类模板，而docker容器实例类似于java中new出来的实例对象。

![img](https://cdn.nlark.com/yuque/0/2022/png/27791237/1658126091673-3fabd0d4-7dd4-4575-8d38-184787b9d236.png)

---------

java的类模板类似于docker的镜像吗 分别举例说明：

是的，Java的类模板与Docker镜像在概念上确实存在相似之处。它们都是用来定义某种标准或蓝图，并可以根据这些模板创建出具体的实例。下面分别对Java的类模板和Docker镜像进行举例说明，并阐述它们之间的类比关系。

**Java的类模板（类定义）**

在Java编程中，类是一种抽象的概念，它定义了一组属性（变量）和行为（方法）。类相当于一个模板或蓝图，用于描述一类具有相同特性和行为的对象。当你定义一个类时，你是在定义一种数据类型和一套操作该类型数据的规则。例如：

```java
public class Person {
    private String name;
    private int age;

    public Person(String name, int age) {
        this.name = name;
        this.age = age;
    }

    public void introduce() {
        System.out.println("Hello, my name is " + name + " and I am " + age + " years old.");
    }
}
```

在这个例子中，`Person` 类是一个模板，它定义了一个对象应有的属性（姓名 `name` 和年龄 `age`）以及行为（介绍自己 `introduce()`）。基于这个模板，你可以创建多个`Person`对象（即类的实例），每个实例有自己的具体属性值：

```java
Person alice = new Person("Alice", 30);
Person bob = new Person("Bob", 35);

alice.introduce(); // 输出: Hello, my name is Alice and I am 30 years old.
bob.introduce();   // 输出: Hello, my name is Bob and I am 35 years old.
```

**Docker镜像**

Docker镜像则是一个轻量级、可执行的软件包，包含运行某个应用程序及其依赖的所有内容，如代码、运行时环境、库、配置等。镜像是一个只读模板，它可以被用来创建Docker容器。镜像由多层文件系统组成，每一层代表一个指令集的执行结果，这些指令通常记录在`Dockerfile`中。例如：

```Dockerfile
FROM openjdk:8-jdk-alpine

WORKDIR /app

COPY target/my-java-app.jar app.jar

EXPOSE 8080

ENTRYPOINT ["java", "-jar", "/app/app.jar"]
```

这个`Dockerfile`定义了一个基于`openjdk:8-jdk-alpine`镜像的新的Docker镜像，其中包含了以下步骤：

1. 从基础镜像 `openjdk:8-jdk-alpine` 开始，它提供了Java 8运行环境。
2. 设置工作目录为 `/app`。
3. 将编译好的应用程序 `my-java-app.jar` 拷贝到容器内的 `/app` 目录。
4. 声明容器将监听的端口为 `8080`。
5. 设置容器启动时执行的命令为 `java -jar /app/app.jar`，即运行JAR包中的应用程序。

基于这个Dockerfile构建的镜像，可以创建任意数量的Docker容器实例，每个容器都将包含相同的环境和应用程序，但它们各自独立运行，拥有各自的进程空间、网络配置、存储卷等资源：

```bash
docker build -t my-java-app .
docker run -p 8080:8080 my-java-app
```

**类比关系**

- **模板/蓝图**：
  - Java类模板定义了对象的数据结构和行为规则。
  - Docker镜像定义了容器的文件系统结构、运行环境、启动命令等规范。

- **实例化**：
  - 根据Java类模板使用 `new` 关键字创建具体的对象实例。
  - 根据Docker镜像使用 `docker run` 命令创建运行中的容器实例。

- **不变性**：
  - Java类模板本身是不可变的，修改类的行为需重新编译。
  - Docker镜像是只读的，修改镜像内容需重新构建新的镜像。

- **复用性**：
  - 同一Java类可以创建多个对象，共享相同的结构和行为定义。
  - 同一Docker镜像可以启动多个容器，共享相同的软件环境和配置。

综上所述，Java的类模板和Docker镜像均作为创建实例的依据，它们分别在编程领域和容器化技术中提供了一种标准化、可复制的创建实体的方式，确保了实例的一致性和高效复用。

---------------



### 2.2.2 容器(container)

**1 从面向对象角度**

Docker 利用容器（Container）独立运行的一个或一组应用，应用程序或服务运行在容器里面，容器就类似于一个虚拟化的运行环境，**容器是用镜像创建的运行实例**。就像是Java中的类和实例对象一样，镜像是静态的定义，容器是镜像运行时的实体。容器为镜像提供了一个标准的和隔离的运行环境，它可以被启动、开始、停止、删除。每个容器都是相互隔离的、保证安全的平台

**2 从镜像容器角度**

可以把容器看做是一个简易版的 Linux 环境（包括root用户权限、进程空间、用户空间和网络空间等）和运行在其中的应用程序。

----------

java的实例对象类似于docker的容器吗？分别举例说明

是的，Java的实例对象与Docker容器在概念上具有很强的对应关系。两者都是基于模板创建的具体、独立且可运行的实体，分别在软件对象层次和操作系统资源层次上实现了隔离与复用。下面分别对Java的实例对象和Docker容器进行举例说明：

**Java的实例对象**

在Java编程中，当你基于一个类模板（即类定义）使用 `new` 关键字创建一个对象时，就得到了该类的一个实例。每个实例对象都有自己独立的内存空间来存储属性值，并且可以独立调用类中定义的方法。实例对象是类的具象化表现，它们各自维持自己的状态并执行特定的操作。例如：

```java
public class Counter {
    private int count;

    public Counter(int initialCount) {
        this.count = initialCount;
    }

    public void increment() {
        count++;
    }

    public int getCount() {
        return count;
    }
}

// 创建两个Counter实例
Counter counter1 = new Counter(0);
Counter counter2 = new Counter(100);

// 对每个实例独立操作
counter1.increment();
counter2.increment();

System.out.println(counter1.getCount()); // 输出: 1
System.out.println(counter2.getCount()); // 输出: 101
```

在这个例子中，`Counter` 类是一个模板，我们基于它创建了两个实例对象 `counter1` 和 `counter2`。每个实例都有独立的 `count` 属性值，它们各自进行 `increment()` 操作时互不影响，保持了状态的隔离。

**Docker容器**

Docker容器则是基于Docker镜像创建的运行时环境，每个容器封装了应用程序及其所有依赖，并提供了隔离的计算资源（如CPU、内存、网络、文件系统等）。容器内部看起来就像一个独立的、最小化的虚拟机，但实际上它们共享宿主机的内核，从而实现轻量化和高效的资源利用。容器之间互不影响，即使运行相同的镜像，每个容器也保持着各自的进程、网络配置、存储状态等。例如：

```bash
# 假设已有 my-web-app 镜像
docker run -d --name webapp1 -p 8081:80 my-web-app
docker run -d --name webapp2 -p 8082:80 my-web-app
```

上述命令基于 `my-web-app` 镜像创建了两个Docker容器：`webapp1` 和 `webapp2`。虽然它们都基于同一镜像，但：

- 每个容器运行在独立的进程中，拥有各自的PID（进程ID）。
- 容器间的网络通信通过端口映射 (`-p`) 实现隔离，`webapp1` 使用 `8081` 端口对外提供服务，`webapp2` 使用 `8082` 端口。
- 如果应用程序在容器内部保存状态，那么每个容器的状态将是独立且互不影响的。

**类比关系**

- **实例化**：
  - 根据Java类模板使用 `new` 关键字创建具体的对象实例。
  - 根据Docker镜像使用 `docker run` 命令创建运行中的容器实例。

- **独立性**：
  - Java实例对象在内存中拥有独立的空间，存储各自的属性值，执行方法时互不影响。
  - Docker容器在操作系统层面实现资源隔离，包括独立的进程、网络、文件系统等，确保容器间互不影响。

- **状态**：
  - Java实例对象维护自己的状态，通过属性值和方法调用体现。
  - Docker容器内部的应用程序和相关资源构成其运行状态，可通过容器内部操作或API查询。

- **复用与一致性**：
  - 多个Java实例对象可以共享相同的类定义，确保行为一致，但各自维持独立状态。
  - 多个Docker容器基于同一镜像创建，保证软件环境和配置一致性，但各自独立运行并维持独立的资源状态。

总结来说，Java的实例对象和Docker容器都是基于模板创建的独立运行实体，它们分别在编程对象级别和操作系统级别实现了隔离、状态管理和复用，确保了系统的模块化、可扩展性和稳定性。

-----------



### 2.2.3 仓库(repository)

仓库（Repository）是集中存放镜像文件的场所。

类似于

Maven仓库，存放各种jar包的地方；

github仓库，存放各种git项目的地方；

Docker公司提供的官方registry被称为Docker Hub，存放各种镜像模板的地方。

仓库分为公开仓库（Public）和私有仓库（Private）两种形式。

最大的公开仓库是 Docker Hub(https://hub.docker.com/)，

存放了数量庞大的镜像供用户下载。国内的公开仓库包括阿里云 、网易云等。

### 2.2.4 小总结

需要正确的理解仓库/镜像/容器这几个概念:

Docker 本身是一个容器运行载体或称之为管理引擎。我们把应用程序和配置依赖打包好形成一个可交付的运行环境，这个打包好的运行环境就是image镜像文件。只有通过这个镜像文件才能生成Docker容器实例(类似Java中new出来一个对象)。

image文件可以看作是容器的模板。Docker 根据 image 文件生成容器的实例。同一个 image 文件，可以生成多个同时运行的容器实例。

镜像文件

\*  image 文件生成的容器实例，本身也是一个文件，称为镜像文件。

容器实例

\*  一个容器运行一种服务，当我们需要的时候，就可以通过docker客户端创建一个对应的运行实例，也就是我们的容器

仓库

\* 就是放一堆镜像的地方，我们可以把镜像发布到仓库中，需要的时候再从仓库中拉下来就可以了。

## 2.3 Docker平台架构图解(架构版)

Docker 是一个 C/S 模式的架构，后端是一个松耦合架构，众多模块各司其职。 

![img](https://cdn.nlark.com/yuque/0/2022/png/27791237/1658126295227-b2ddb2e3-292d-4b30-8c5d-f357e888f842.png)

![img](https://cdn.nlark.com/yuque/0/2022/png/27791237/1658126301842-ffbb9b01-b708-4fde-b2b4-66649f00ff27.png)

## 2.4 安装步骤

CentOS7安装Docker：https://docs.docker.com/engine/install/centos/

### 2.4.1 确定你是CentOS7及以上版本 

```
cat /etc/redhat-release
```

###  2.4.2 卸载旧版本

https://docs.docker.com/engine/install/centos/

![img](https://cdn.nlark.com/yuque/0/2022/png/27791237/1658126844192-45e71ac5-a5bf-46ca-8942-b668436b372a.png)

### 2.4.3 yum安装gcc相关

CentOS7能上外网

```
yum -y install gcc
yum -y install gcc-c++
```

### 2.4.4 安装需要的软件包

官网要求

![img](https://cdn.nlark.com/yuque/0/2022/png/27791237/1658126862915-d8d43523-c57c-466a-ba96-ee1a91932a13.png)

执行命令

```
yum install -y yum-utils
```

### 2.4.5 设置stable镜像仓库

❌

```
yum-config-manager --add-repo https://download.docker.com/linux/centos/docker-ce.repo
```

![img](https://cdn.nlark.com/yuque/0/2022/png/27791237/1658126979708-37e95321-1241-4470-9052-7af819b752cd.png)

报错：

1   [Errno 14] curl#35 - TCP connection reset by peer

2   [Errno 12] curl#35 - Timeout

✔️

```
yum-config-manager --add-repo http://mirrors.aliyun.com/docker-ce/linux/centos/docker-ce.repo
```

![img](https://cdn.nlark.com/yuque/0/2022/png/27791237/1658127043948-db9cd0a7-402b-49d4-aab9-96048a5b9c19.png)

### 2.4.6 更新yum软件包索引

```
yum makecache fast
```

### 2.4.7 安装DOCKER CE

```
yum -y install docker-ce docker-ce-cli containerd.io
```

官网要求

![img](https://cdn.nlark.com/yuque/0/2022/png/27791237/1658127068915-03fe61b8-f818-41cc-bea6-ac90c9a39704.png)

执行结果

![img](https://cdn.nlark.com/yuque/0/2022/png/27791237/1658127075536-0f42eb08-adec-4617-880e-5e3291fd103a.png)

![img](https://cdn.nlark.com/yuque/0/2022/png/27791237/1658127081500-41d8c813-86fa-4894-86f7-0a3e5fbcbcc5.png)

### 2.4.8 启动docker

```
systemctl start docker
```

### 2.4.9 测试

```
docker version
```

![img](https://cdn.nlark.com/yuque/0/2022/png/27791237/1658127110699-6b35fe5b-40dd-4b00-aa5a-edf410a551c9.png)

```
docker run hello-world
```

![img](https://cdn.nlark.com/yuque/0/2022/png/27791237/1658127121361-38f89b48-1f6b-41db-a4e4-b5daa2033cd8.png)

###  2.4.10 卸载

```
systemctl stop docker 
yum remove docker-ce docker-ce-cli containerd.io
rm -rf /var/lib/docker
rm -rf /var/lib/containerd
```

## 2.5 阿里云镜像加速

1. 是什么

https://promotion.aliyun.com/ntms/act/kubernetes.html

1. 注册一个属于自己的阿里云账户(可复用淘宝账号)
2. 获得加速器地址连接

1. 登陆阿里云开发者平台

![img](https://cdn.nlark.com/yuque/0/2022/png/27791237/1658127431916-8d79fe8c-71ce-4bc4-89a4-9ca421cc6806.png)

1. 点击控制台	
2. 选择容器镜像服务

![img](https://cdn.nlark.com/yuque/0/2022/png/27791237/1658127461505-e6f718dd-b5f3-423d-b893-b381a253efb0.png)

1. 获取加速器地址

![img](https://cdn.nlark.com/yuque/0/2022/png/27791237/1658127474673-4b4b8945-91f7-49b9-ad66-aec303c5e6c5.png)

1. 粘贴脚本直接执行

1. 直接粘

![img](https://cdn.nlark.com/yuque/0/2022/png/27791237/1658127498966-c1bd9a06-2d45-4589-b3b1-de5bb4ee2df1.png)

[root@JaBen docker]# cat /etc/docker/daemon.json
{
  "registry-mirrors": ["https://elsjyyuc.mirror.aliyuncs.com"]
}

1. 或者分步骤都行

```
mkdir -p /etc/docker
vim  /etc/docker/daemon.json
```

1. 重启服务器

```
systemctl daemon-reload
systemctl restart docker
```

## 2.6 永远的HelloWorld

启动Docker后台容器(测试运行 hello-world)

```
docker run hello-world
```

![img](https://cdn.nlark.com/yuque/0/2022/png/27791237/1658127597827-3f44d88b-495b-4203-b88a-df12a5077bec.png)

输出这段提示以后，hello world就会停止运行，容器自动终止。

run干了什么？

![img](https://cdn.nlark.com/yuque/0/2022/png/27791237/1658127613575-33c2ea48-6218-48dc-936d-66b4c45d8165.png)

## 2.7 底层原理

为什么Docker会比VM虚拟机快

**(1)docker有着比虚拟机更少的抽象层**

   由于docker不需要Hypervisor(虚拟机)实现硬件资源虚拟化,运行在docker容器上的程序直接使用的都是实际物理机的硬件资源。因此在CPU、内存利用率上docker将会在效率上有明显优势。

**(2)docker利用的是宿主机的内核,而不需要加载操作系统OS内核**

   当新建一个容器时,docker不需要和虚拟机一样重新加载一个操作系统内核。进而避免引寻、加载操作系统内核返回等比较费时费资源的过程,当新建一个虚拟机时,虚拟机软件需要加载OS,返回新建过程是分钟级别的。而docker由于直接利用宿主机的操作系统,则省略了返回过程,因此新建一个docker容器只需要几秒钟。

![img](https://cdn.nlark.com/yuque/0/2022/png/27791237/1658127650958-09fa7db3-82a6-4422-82f2-1f199c5587e3.png)

![img](https://cdn.nlark.com/yuque/0/2022/png/27791237/1658127674217-cece7c8f-55e1-404d-80b8-4ef145cab176.png)

# 3 Docker常用命令

## 3.1 帮助启动类命令

- 启动docker： `systemctl start docker`
- 停止docker： `systemctl stop docker`
- 重启docker： `systemctl restart docker`
- 查看docker状态： `systemctl status docker`
- 开机启动： `systemctl enable docker`
- 查看docker概要信息： `docker info`
- 查看docker总体帮助文档： `docker --help`
- 查看docker命令帮助文档：` docker 具体命令 --help`

## 3.2 镜像命令

### 3.2.1`docker images`

列出本地主机上的镜像

![img](https://cdn.nlark.com/yuque/0/2022/png/27791237/1658128356068-5e3ff7a4-7f38-4a11-90e0-12bf83456dae.png)

各个选项说明:

REPOSITORY：表示镜像的仓库源

TAG：镜像的标签版本号

IMAGE ID：镜像ID

CREATED：镜像创建时间

SIZE：镜像大小

 同一仓库源可以有多个 TAG版本，代表这个仓库源的不同个版本，我们使用 REPOSITORY:TAG 来定义不同的镜像。

如果你不指定一个镜像的版本标签，例如你只使用 ubuntu，docker 将默认使用 ubuntu:latest 镜像

OPTIONS说明：

 -a :列出本地所有的镜像（含历史映像层）

-q :只显示镜像ID。

### 3.2.2`docker search 某个XXX镜像名字`

网站：https://hub.docker.com

命令：`docker search [OPTIONS] 镜像名字`

![img](https://cdn.nlark.com/yuque/0/2022/png/27791237/1658128663501-7a2ed748-1710-4a5b-a807-6d2f5904224e.png)

![img](https://cdn.nlark.com/yuque/0/2022/png/27791237/1658128646788-0a2bb440-6da9-42de-ad89-9c7d8e758397.png)

OPTIONS说明：

--limit : 只列出N个镜像，默认25个

docker search --limit 5 redis

### 3.2.3`docker pull 某个XXX镜像名字`

下载镜像

```
docker pull 镜像名字[:TAG]
docker pull 镜像名字
```

没有TAG就是最新版

等价于

```
docker pull 镜像名字:latest
docker pull ubuntu
```

![img](https://cdn.nlark.com/yuque/0/2022/png/27791237/1658128687848-01ba57aa-4730-4b81-88f0-62e356717c87.png)

### 3.2.4`docker system df `

查看镜像/容器/数据卷所占的空间

![img](https://cdn.nlark.com/yuque/0/2022/png/27791237/1658128697120-12812d85-0d3d-419f-ac6f-767d8c470316.png)

### 3.2.5`docker rmi 某个XXX镜像名字ID`

删除镜像

删除单个

```
docker rmi -f 镜像ID
```

删除多个

```
docker rmi -f 镜像名1:TAG 镜像名2:TAG 
```

删除全部

```
docker rmi -f $(docker images -qa)
```

### 3.2.6 面试题：谈谈docker虚悬镜像是什么？

是什么？

仓库名、标签都是<none>的镜像，俗称虚悬镜像dangling image

长什么样？

![img](https://cdn.nlark.com/yuque/0/2022/png/27791237/1658128731936-a1972083-d868-493b-b199-818efc071b0f.png)

## 3.3 容器命令

### 3.3.1 有镜像才能创建容器， 这是根本前提(下载一个CentOS或者ubuntu镜像演示)

![img](https://cdn.nlark.com/yuque/0/2022/png/27791237/1658129060820-e3bbad90-56b9-44d7-971b-305557ab2ed9.png)

```
docker pull centos
docker pull ubuntu
```

![img](https://cdn.nlark.com/yuque/0/2022/png/27791237/1658129093993-0b483619-b517-46b5-a248-887a445e78eb.png)

### 3.3.2 新建+启动容器

```
docker run [OPTIONS] IMAGE [COMMAND] [ARG...]
```

OPTIONS说明

 OPTIONS说明（常用）：有些是一个减号，有些是两个减号

--name="容器新名字"       为容器指定一个名称；

-d: 后台运行容器并返回容器ID，也即启动守护式容器(后台运行)；

-i：以交互模式运行容器，通常与 -t 同时使用；

-t：为容器重新分配一个伪输入终端，通常与 -i 同时使用；

也即启动交互式容器(前台有伪终端，等待交互)；

-P: 随机端口映射，大写P

-p: 指定端口映射，小写p

![img](https://cdn.nlark.com/yuque/0/2022/png/27791237/1658129219778-97778de9-d0a0-4824-93f7-14f42b329784.png)

启动交互式容器(前台命令行)

![img](https://cdn.nlark.com/yuque/0/2022/png/27791237/1658129248609-498afeab-bed1-4ff1-b3f4-4c6b55ef6aea.png)

\#使用镜像centos:latest以交互模式启动一个容器,在容器内执行/bin/bash命令。

```
docker run -it centos /bin/bash 
```

参数说明：

-i: 交互式操作。

-t: 终端。

centos : centos 镜像。

/bin/bash：放在镜像名后的是命令，这里我们希望有个交互式 Shell，因此用的是 /bin/bash。

要退出终端，直接输入 exit:

### 3.3.3 列出当前所有正在运行的容器

```
docker ps [OPTIONS]
```

OPTIONS说明（常用）：

-a :列出当前所有正在运行的容器+历史上运行过的

-l :显示最近创建的容器。

-n：显示最近n个创建的容器。

-q :静默模式，只显示容器编号。

### 3.3.4 退出容器

两种退出方式

```
exit
```

run进去容器，exit退出，容器停止

```
ctrl+p+q
```

run进去容器，ctrl+p+q退出，容器不停止

### 3.3.5 启动已停止运行的容器

```
docker start 容器ID或者容器名
```

### 3.3.6 重启容器

```
docker restart 容器ID或者容器名
```

### 3.3.7 停止容器

```
docker stop 容器ID或者容器名
```

### 3.3.8 强制停止容器

```
docker kill 容器ID或容器名
```

### 3.3.9 删除已停止的容器

```
docker rm 容器ID
```

一次性删除多个容器实例

```
docker rm -f $(docker ps -a -q)
docker ps -a -q | xargs docker rm
```

### 3.3.10 重要

1. **有镜像才能创建容器，这是根本前提(下载一个Redis6.0.8镜像演示)**
2. **启动守护式容器(后台服务器)**

在大部分的场景下，我们希望 docker 的服务是在后台运行的， 我们可以过 -d 指定容器的后台运行模式。

```
docker run -d 容器名
```

\#使用镜像centos:latest以后台模式启动一个容器

```
docker run -d centos
```

问题：然后docker ps -a 进行查看, 会发现容器已经退出

很重要的要说明的一点: Docker容器后台运行,就必须有一个前台进程。

容器运行的命令如果不是那些一直挂起的命令（比如运行top，tail），就是会自动退出的。

这个是docker的机制问题,比如你的web容器,我们以nginx为例，正常情况下,我们配置启动服务只需要启动响应的service即可。例如service nginx start。但是,这样做,nginx为后台进程模式运行,就导致docker前台没有运行的应用，这样的容器后台启动后，会立即自杀因为他觉得他没事可做了。所以，最佳的解决方案是将你要运行的程序以前台进程的形式运行，常见就是命令行模式，表示我还有交互操作，别中断。

redis 前后台启动演示case

前台交互式启动

```
docker run -it redis:6.0.8
```

后台守护式启动

```
docker run -d redis:6.0.8
```

1. **查看容器日志**

```
docker logs 容器ID
```

1. **查看容器内运行的进程**

```
docker top 容器ID
```

1. **查看容器内部细节**

```
docker inspect 容器ID
```

1. **进入正在运行的容器并以命令行交互**

```
docker exec -it 容器ID bashShell
```

![img](https://cdn.nlark.com/yuque/0/2022/png/27791237/1658129562647-19bbffb5-a7ca-4d2f-a8ca-b01397829662.png)

![img](https://cdn.nlark.com/yuque/0/2022/png/27791237/1658129567142-bc7d765d-1b49-4fd0-b3d9-244c8b10ced9.png)

重新进入`docker attach 容器ID`

上述两个区别？

attach 直接进入容器启动命令的终端，不会启动新的进程 用exit退出，会导致容器的停止。

![img](https://cdn.nlark.com/yuque/0/2022/png/27791237/1658129646053-362cd580-f5d7-44f6-bc46-5ea6f147c32f.png)

exec 是在容器中打开新的终端，并且可以启动新的进程 用exit退出，不会导致容器的停止。

![img](https://cdn.nlark.com/yuque/0/2022/png/27791237/1658129692386-311936c6-f387-4624-bdad-10036137c934.png)

推荐大家使用 docker exec 命令，因为退出容器终端，不会导致容器的停止。

用之前的redis容器实例进入试试

进入redis服务

```
docker exec -it 容器ID /bin/bash
docker exec -it 容器ID redis-cli
```

一般用-d后台启动的程序，再用exec进入对应容器实例

1. **从容器内拷贝文件到主机上**

容器→主机

```
docker cp 容器ID:容器内路径 目的主机路径
```

![img](https://cdn.nlark.com/yuque/0/2022/png/27791237/1658129765070-038e032d-52d3-496a-b3a6-5e0cc96f9cfa.png)

1. **导入和导出容器**

`export `导出容器的内容留作为一个tar归档文件[对应import命令]

`import `从tar包中的内容创建一个新的文件系统再导入为镜像[对应export]

案例

```
docker export 容器ID > 文件名.tar
```

![img](https://cdn.nlark.com/yuque/0/2022/png/27791237/1658129809181-66670b9e-4977-40ab-8111-f18db9ef6da6.png)

```
cat 文件名.tar | docker import - 镜像用户/镜像名:镜像版本号
```

![img](https://cdn.nlark.com/yuque/0/2022/png/27791237/1658129845413-9942d9fa-3481-4211-b348-fdd0d4369dbf.png)

## 3.4 小总结

![img](https://cdn.nlark.com/yuque/0/2022/png/27791237/1658128808416-bc53f29a-c6b0-4b5f-966c-b6cb83a9e66b.png)

attach    Attach to a running container                 # 当前 shell 下 attach 连接指定运行镜像

build     Build an image from a Dockerfile              # 通过 Dockerfile 定制镜像

commit    Create a new image from a container changes   # 提交当前容器为新的镜像

cp        Copy files/folders from the containers filesystem to the host path   #从容器中拷贝指定文件或者目录到宿主机中

create    Create a new container                        # 创建一个新的容器，同 run，但不启动容器

diff      Inspect changes on a container's filesystem   # 查看 docker 容器变化

events    Get real time events from the server          # 从 docker 服务获取容器实时事件

exec      Run a command in an existing container        # 在已存在的容器上运行命令

export    Stream the contents of a container as a tar archive   # 导出容器的内容流作为一个 tar 归档文件[对应 import ]

history   Show the history of an image                  # 展示一个镜像形成历史

images    List images                                   # 列出系统当前镜像

import    Create a new filesystem image from the contents of a tarball # 从tar包中的内容创建一个新的文件系统映像[对应export]

info      Display system-wide information               # 显示系统相关信息

inspect   Return low-level information on a container   # 查看容器详细信息

kill      Kill a running container                      # kill 指定 docker 容器

load      Load an image from a tar archive              # 从一个 tar 包中加载一个镜像[对应 save]

login     Register or Login to the docker registry server    # 注册或者登陆一个 docker 源服务器

logout    Log out from a Docker registry server          # 从当前 Docker registry 退出

logs      Fetch the logs of a container                 # 输出当前容器日志信息

port      Lookup the public-facing port which is NAT-ed to PRIVATE_PORT    # 查看映射端口对应的容器内部源端口

pause     Pause all processes within a container        # 暂停容器

ps        List containers                               # 列出容器列表

pull      Pull an image or a repository from the docker registry server   # 从docker镜像源服务器拉取指定镜像或者库镜像

push      Push an image or a repository to the docker registry server    # 推送指定镜像或者库镜像至docker源服务器

restart   Restart a running container                   # 重启运行的容器

rm        Remove one or more containers                 # 移除一个或者多个容器

rmi       Remove one or more images       # 移除一个或多个镜像[无容器使用该镜像才可删除，否则需删除相关容器才可继续或 -f 强制删除]

run       Run a command in a new container              # 创建一个新的容器并运行一个命令

save      Save an image to a tar archive                # 保存一个镜像为一个 tar 包[对应 load]

search    Search for an image on the Docker Hub         # 在 docker hub 中搜索镜像

start     Start a stopped containers                    # 启动容器

stop      Stop a running containers                     # 停止容器

tag       Tag an image into a repository                # 给源中镜像打标签

top       Lookup the running processes of a container   # 查看容器中运行的进程信息

unpause   Unpause a paused container                    # 取消暂停容器

version   Show the docker version information           # 查看 docker 版本号

wait      Block until a container stops, then print its exit code   # 截取容器停止时的退出状态值





![image-20240412195435573](C:\Users\JB.Lee\AppData\Roaming\Typora\typora-user-images\image-20240412195435573.png)



# 4 Docker镜像

### 4.1 是什么

是一种轻量级、可执行的独立软件包，它包含运行某个软件所需的所有内容，我们把应用程序和配置依赖打包好形成一个可交付的运行环境(包括代码、运行时需要的库、环境变量和配置文件等)，这个打包好的运行环境就是image镜像文件。

只有通过这个镜像文件才能生成Docker容器实例(类似Java中new出来一个对象)。

#### 4.1.1 分层的镜像

以我们的pull为例，在下载的过程中我们可以看到docker的镜像好像是在一层一层的在下载

![img](https://cdn.nlark.com/yuque/0/2022/png/27791237/1658139351043-7a36850b-bd26-491a-9597-76535f2b0a1f.png)

#### 4.1.2 UnionFS（联合文件系统）

UnionFS（联合文件系统）：Union文件系统（UnionFS）是一种分层、轻量级并且高性能的文件系统，它支持对文件系统的修改作为一次提交来一层层的叠加，同时可以将不同目录挂载到同一个虚拟文件系统下(unite several directories into a single virtual filesystem)。Union 文件系统是 Docker 镜像的基础。镜像可以通过分层来进行继承，基于基础镜像（没有父镜像），可以制作各种具体的应用镜像。

 ![img](https://cdn.nlark.com/yuque/0/2022/png/27791237/1658139366360-eee5b96b-2f64-4a11-a3ae-5aa027fc7d33.png)

特性：一次同时加载多个文件系统，但从外面看起来，只能看到一个文件系统，联合加载会把各层文件系统叠加起来，这样最终的文件系统会包含所有底层的文件和目录

####  4.1.3 Docker镜像加载原理

docker的镜像实际上由一层一层的文件系统组成，这种层级的文件系统UnionFS。

bootfs(boot file system)主要包含bootloader和kernel, bootloader主要是引导加载kernel, Linux刚启动时会加载bootfs文件系统，在Docker镜像的最底层是引导文件系统bootfs。这一层与我们典型的Linux/Unix系统是一样的，包含boot加载器和内核。当boot加载完成之后整个内核就都在内存中了，此时内存的使用权已由bootfs转交给内核，此时系统也会卸载bootfs。

rootfs (root file system) ，在bootfs之上。包含的就是典型 Linux 系统中的 /dev, /proc, /bin, /etc 等标准目录和文件。rootfs就是各种不同的操作系统发行版，比如Ubuntu，Centos等等。 

![img](https://cdn.nlark.com/yuque/0/2022/png/27791237/1658139389739-dedef184-d920-4cb8-b046-6d74cd73a390.png)

 平时我们安装进虚拟机的CentOS都是好几个G，为什么docker这里才200M？？

![img](https://cdn.nlark.com/yuque/0/2022/png/27791237/1658139396091-72001717-33f4-4790-afbe-9d4e8198447a.png)

对于一个精简的OS，rootfs可以很小，只需要包括最基本的命令、工具和程序库就可以了，因为底层直接用Host的kernel，自己只需要提供 rootfs 就行了。由此可见对于不同的linux发行版, bootfs基本是一致的, rootfs会有差别, 因此不同的发行版可以公用bootfs。

#### 4.1.4 为什么 Docker 镜像要采用这种分层结构呢

镜像分层最大的一个好处就是共享资源，方便复制迁移，就是为了复用。

比如说有多个镜像都从相同的 base 镜像构建而来，那么 Docker Host 只需在磁盘上保存一份 base 镜像；

同时内存中也只需加载一份 base 镜像，就可以为所有容器服务了。而且镜像的每一层都可以被共享。

### 4.2 重点理解

Docker镜像层都是只读的，容器层是可写的。当容器启动时，一个新的可写层被加载到镜像的顶部。 这一层通常被称作“容器层”，“容器层”之下的都叫“镜像层”。

所有对容器的改动 - 无论添加、删除、还是修改文件都只会发生在容器层中。只有容器层是可写的，容器层下面的所有镜像层都是只读的。

![img](https://cdn.nlark.com/yuque/0/2022/png/27791237/1658139462778-98182b2f-6e3d-4e23-96ca-04107d94efe9.png)

### 4.3 Docker镜像commit操作案例

docker commit 提交容器副本使之成为一个新的镜像

```
docker commit -m="提交的描述信息" -a="作者" 容器ID 要创建的目标镜像名:[标签名]
```

#### 4.3.1 案例演示ubuntu安装vim

1. **从Hub上下载ubuntu镜像到本地并成功运行**
2. **原始的默认Ubuntu镜像是不带着vim命令的**

![img](https://cdn.nlark.com/yuque/0/2022/png/27791237/1658139528237-90855992-8e34-4d7b-bfb5-ce29b0ac411f.png)

1. **外网连通的情况下，安装vim**

![img](https://cdn.nlark.com/yuque/0/2022/png/27791237/1658139546512-e54ea2c6-cf8e-4782-915a-b0c59fb0c5dc.png)

docker容器内执行上述两条命令：

```
apt-get update
apt-get -y install vim
```

![img](https://cdn.nlark.com/yuque/0/2022/png/27791237/1658139552106-4c75c757-2789-4b36-9162-d435e5278456.png)

![img](https://cdn.nlark.com/yuque/0/2022/png/27791237/1658139557574-59af7f26-86c4-4af9-bba7-650897d6ff82.png)

1. **安装完成后，commit我们自己的新镜像**

![img](https://cdn.nlark.com/yuque/0/2022/png/27791237/1658139596868-4312899d-c9dd-4a45-9b34-8a075d61116c.png)

![img](https://cdn.nlark.com/yuque/0/2022/png/27791237/1658139602000-6bb1bb7f-a2f8-4bad-8d03-ff1f147da555.png)

1. **启动我们的新镜像并和原来的对比**

![img](https://cdn.nlark.com/yuque/0/2022/png/27791237/1658139612305-4d9e9f72-1e44-4988-8ef3-255090cd1b82.png)

1. 官网是默认下载的Ubuntu没有vim命令
2. 我们自己commit构建的镜像，新增加了vim功能，可以成功使用。

#### 4.3.2 小总结

Docker中的镜像分层，支持通过扩展现有镜像，创建新的镜像。类似Java继承于一个Base基础类，自己再按需扩展。

新镜像是从 base 镜像一层一层叠加生成的。每安装一个软件，就在现有镜像的基础上增加一层

![img](https://cdn.nlark.com/yuque/0/2022/png/27791237/1658139701434-5322591f-b716-4232-8f3c-9420ba706072.png)

# 5 本地镜像发布到阿里云

## 5.1 本地镜像发布到阿里云流程

![img](https://cdn.nlark.com/yuque/0/2022/png/27791237/1658139786698-1f881901-f53d-482d-8198-5c71a779db6f.png)

## 5.2 镜像的生成方法

基于当前容器创建一个新的镜像，新功能增强 `docker commit [OPTIONS] 容器ID [REPOSITORY[:TAG]]`

OPTIONS说明：

-a :提交的镜像作者；

-m :提交时的说明文字；

![img](https://cdn.nlark.com/yuque/0/2022/png/27791237/1658139828870-7f14de5e-85a2-4409-b30d-1d833b6e014a.png)

![img](https://cdn.nlark.com/yuque/0/2022/png/27791237/1658139835046-ce1ff5bb-96dc-46a8-92ac-9cc522f730ab.png)

## 5.3 将本地镜像推送到阿里云

本地镜像素材原型

![img](https://cdn.nlark.com/yuque/0/2022/png/27791237/1658139862888-96cc93ff-c7a6-4f73-9268-c9a9fd06dad3.png)

![img](https://cdn.nlark.com/yuque/0/2022/png/27791237/1658139867564-59ac7072-d068-4d74-b012-de24e64f65b0.png)

阿里云开发者平台

https://promotion.aliyun.com/ntms/act/kubernetes.html

![img](https://cdn.nlark.com/yuque/0/2022/png/27791237/1658139877321-2fee875d-2343-460f-93ba-5eadd35c479b.png)

### 5.3.1 创建仓库镜像

1. **选择控制台，进入容器镜像服务**

![img](https://cdn.nlark.com/yuque/0/2022/png/27791237/1658139928853-ccc16d88-bb05-4f73-82f3-429a883e6754.png)

1. **选择个人实例**

![img](https://cdn.nlark.com/yuque/0/2022/png/27791237/1658139936677-14362c3e-3c89-4af3-8ebf-233b303e59ce.png)

1. **命名空间**

![img](https://cdn.nlark.com/yuque/0/2022/png/27791237/1658139942874-f2e3db26-3f56-46d1-b353-da6c80b4064e.png)

![img](https://cdn.nlark.com/yuque/0/2022/png/27791237/1658139948785-659bd67e-b21f-46ef-9b9c-4cff763f0c30.png)

1. **仓库名称**

![img](https://cdn.nlark.com/yuque/0/2022/png/27791237/1658139954429-530f3efa-c1cf-41ab-8ee3-4d0ed47a5423.png)

![img](https://cdn.nlark.com/yuque/0/2022/png/27791237/1658139962035-85aaed76-b131-4997-8ba6-aeafc9e45a45.png)

![img](https://cdn.nlark.com/yuque/0/2022/png/27791237/1658139971022-400de815-a008-4fbd-8ac3-16d2337d68a3.png)

1. **进入管理界面获得脚本**

![img](https://cdn.nlark.com/yuque/0/2022/png/27791237/1658139979398-d997e648-e878-44bf-97a9-99a9b4cc182b.png)

### 5.3.2 将镜像推送到阿里云

1. **管理界面脚本**

![img](https://cdn.nlark.com/yuque/0/2022/png/27791237/1658140037335-a8e58945-9160-4db5-82d7-51bdce65a98f.png)

1. **脚本实例**

```
docker login --username=zzyybuy registry.cn-hangzhou.aliyuncs.com
docker tag cea1bb40441c registry.cn-hangzhou.aliyuncs.com/atguiguwh/myubuntu:1.1
docker push registry.cn-hangzhou.aliyuncs.com/atguiguwh/myubuntu:1.1
```

上面命令是阳哥自己本地的，你自己酌情处理，不要粘贴我的。

![img](https://cdn.nlark.com/yuque/0/2022/png/27791237/1658140061637-73ca4162-693e-4e3a-8431-b7b3f969d791.png)

## 5.4 将阿里云上的镜像下载到本地

![img](https://cdn.nlark.com/yuque/0/2022/png/27791237/1658140107483-05a4996e-cc38-4cc9-8ede-6b137c76d182.png)

```
docker pull registry.cn-hangzhou.aliyuncs.com/atguiguwh/myubuntu:1.1
```

# 6 本地镜像发布到私有库

![img](https://cdn.nlark.com/yuque/0/2022/png/27791237/1658140528137-0139f39f-85e8-4b9c-8b90-176cf342f638.png)

## 6.1 是什么

1 官方Docker Hub地址：https://hub.docker.com/，中国大陆访问太慢了且准备被阿里云取代的趋势，不太主流。

2 Dockerhub、阿里云这样的公共镜像仓库可能不太方便，涉及机密的公司不可能提供镜像给公网，所以需要创建一个本地私人仓库供给团队使用，基于公司内部项目构建镜像。

Docker Registry是官方提供的工具，可以用于构建私有镜像仓库

## 6.2 将本地镜像推送到私有库

### 6.2.1 下载镜像Docker Registry

```
docker pull registry 
```

![img](https://cdn.nlark.com/yuque/0/2022/png/27791237/1658140613549-4ae195ec-d23f-4bfa-8081-8010a0951a84.png)

![img](https://cdn.nlark.com/yuque/0/2022/png/27791237/1658140617335-e8afc163-f22c-425e-a57f-fb4c0fa2db65.png)

### 6.2.2 运行私有库Registry，相当于本地有个私有Docker hub

```
docker run -d -p 5000:5000  -v /zzyyuse/myregistry/:/tmp/registry --privileged=true registry
```

默认情况，仓库被创建在容器的/var/lib/registry目录下，建议自行用容器卷映射，方便于宿主机联调

![img](https://cdn.nlark.com/yuque/0/2022/png/27791237/1658140662023-ea9286a4-9a1a-4f1e-8e69-c9bcfa9f4123.png)

### 6.2.3 案例演示创建一个新镜像，ubuntu安装ifconfig命令

1. **从Hub上下载ubuntu镜像到本地并成功运行**
2. **原始的Ubuntu镜像是不带着ifconfig命令的**

![img](https://cdn.nlark.com/yuque/0/2022/png/27791237/1658140729301-8d261790-2b2a-4ef2-b647-5c1dfdaf11a2.png)

1. **外网连通的情况下，安装ifconfig命令并测试通过**

docker容器内执行上述两条命令：

```
apt-get update
apt-get install net-tools
```

![img](https://cdn.nlark.com/yuque/0/2022/png/27791237/1658140754797-30955eea-85ca-45ad-9eed-4d6e8bc85bcf.png)

![img](https://cdn.nlark.com/yuque/0/2022/png/27791237/1658140766303-cab53637-5e99-4582-895e-8c6b25b87b9f.png)

1. **安装完成后，commit我们自己的新镜像**

公式：

```
docker commit -m="提交的描述信息" -a="作者" 容器ID 要创建的目标镜像名:[标签名]
```

命令：在容器外执行，记得

```
docker commit -m="ifconfig cmd add" -a="zzyy" a69d7c825c4f zzyyubuntu:1.2
```

![img](https://cdn.nlark.com/yuque/0/2022/png/27791237/1658140814745-9a6cf515-820d-4691-9476-851c5d33824f.png)

1. **启动我们的新镜像并和原来的对比**

1. 官网是默认下载的Ubuntu没有ifconfig命令。
2. 我们自己commit构建的新镜像，新增加了ifconfig功能，可以成功使用。

![img](https://cdn.nlark.com/yuque/0/2022/png/27791237/1658140903228-f2f55e73-53bd-49e7-be3e-4d550b27cce1.png)

### 6.2.4 curl验证私服库上有什么镜像

```
curl -XGET http://192.168.111.162:5000/v2/_catalog
```

可以看到，目前私服库没有任何镜像上传过。

![img](https://cdn.nlark.com/yuque/0/2022/png/27791237/1658141032605-48d1e492-bfbf-46fd-81e1-cad973215f2a.png)

### 6.2.5 将新镜像zzyyubuntu:1.2修改符合私服规范的Tag

按照公式： `docker   tag   镜像:Tag   Host:Port/Repository:Tag`

自己host主机IP地址，填写同学你们自己的，不要粘贴错误。

使用命令 docker tag 将zzyyubuntu:1.2 这个镜像修改为192.168.111.162:5000/zzyyubuntu:1.2

```
docker tag  zzyyubuntu:1.2  192.168.111.162:5000/zzyyubuntu:1.2
```

![img](https://cdn.nlark.com/yuque/0/2022/png/27791237/1658141064520-1a2b1710-ec76-4ad0-a8b5-33c4594d258a.png)

### 6.2.6 修改配置文件使之支持http

![img](https://cdn.nlark.com/yuque/0/2022/png/27791237/1658141072463-038196d4-b032-471a-bd38-29c9ac5f53a5.png)

别无脑照着复制，registry-mirrors 配置的是国内阿里提供的镜像加速地址，不用加速的话访问官网的会很慢。

2个配置中间有个逗号 ','别漏了，这个配置是json格式的。

vim命令新增如下红色内容：`vim /etc/docker/daemon.json`

{

  "registry-mirrors": ["https://aa25jngu.mirror.aliyuncs.com"],

  "insecure-registries": ["192.168.111.162:5000"]

}

上述理由：docker默认不允许http方式推送镜像，通过配置选项来取消这个限制。====> 修改完后如果不生效，建议重启docker。

### 6.2.7 push推送到私服库

```
docker push 192.168.111.162:5000/zzyyubuntu:1.2
```

![img](https://cdn.nlark.com/yuque/0/2022/png/27791237/1658141185869-6653bf41-3f41-413a-8805-1a9427b163ed.png)

### 6.2.8 curl验证私服库上有什么镜像2

```
curl -XGET http://192.168.111.162:5000/v2/_catalog
```

![img](https://cdn.nlark.com/yuque/0/2022/png/27791237/1658141198749-a2fb2ce6-a874-447a-8a97-5007707b570b.png)

### 6.2.9 pull到本地并运行

```
docker pull 192.168.111.162:5000/zzyyubuntu:1.2
```

![img](https://cdn.nlark.com/yuque/0/2022/png/27791237/1658141231233-35349bc8-96f8-45dc-a59e-ce0e543ec32b.png)

```
docker run -it 镜像ID /bin/bash
```

![img](https://cdn.nlark.com/yuque/0/2022/png/27791237/1658141235833-b15f4d66-7533-445e-9681-820eea024934.png)

# 7 Docker容器数据卷

## 7.1 坑：容器卷记得加入

```
--privileged=true
```

 Docker挂载主机目录访问如果出现cannot open directory .: Permission denied

**解决办法：在挂载目录后多加一个--privileged=true参数即可**

如果是CentOS7安全模块会比之前系统版本加强，不安全的会先禁止，所以目录挂载的情况被默认为不安全的行为，在SELinux里面挂载目录被禁止掉了，如果要开启，我们一般使用--privileged=true命令，扩大容器的权限解决挂载目录没有权限的问题，也即使用该参数，container内的root拥有真正的root权限，否则，container内的root只是外部的一个普通用户权限。

![image-20240413101657973](C:\Users\JB.Lee\AppData\Roaming\Typora\typora-user-images\image-20240413101657973.png)



## 7.2 回顾下上一讲的知识点，参数V

![img](https://cdn.nlark.com/yuque/0/2022/png/27791237/1658193898005-66ac7a6e-7f2f-4f7b-899d-5114a1215fa0.png)

## 7.3 是什么

卷就是目录或文件，存在于一个或多个容器中，由docker挂载到容器，但不属于联合文件系统，因此能够绕过Union File System提供一些用于持续存储或共享数据的特性：卷的设计目的就是数据的持久化，完全独立于容器的生存周期，因此Docker不会在容器删除时删除其挂载的数据卷。

**一句话：有点类似我们Redis里面的rdb和aof文件。**

将docker容器内的数据保存进宿主机的磁盘中，运行一个带有容器卷存储功能的容器实例。

```
 docker run -it --privileged=true -v /宿主机绝对路径目录:/容器内目录      镜像名
```

## 7.4 能干嘛

将运用与运行的环境打包镜像，run后形成容器实例运行 ，但是我们对数据的要求希望是持久化的。

Docker容器产生的数据，如果不备份，那么当容器实例删除后，容器内的数据自然也就没有了。为了能保存数据在docker中我们使用卷。

 特点：

1. **数据卷可在容器之间共享或重用数据**
2. **卷中的更改可以直接实时生效，爽**
3. **数据卷中的更改不会包含在镜像的更新中**
4. **数据卷的生命周期一直持续到没有容器使用它为止**

## 7.5 数据卷案例

### 7.5.1 宿主vs容器之间映射添加容器卷

1. `直接命令添加`

```
docker run -it --privileged=true -v /宿主机绝对路径目录:/容器内目录 镜像名
```

公式：`docker run -it -v /宿主机目录:/容器内目录 ubuntu /bin/bash`

```
docker run -it --name myu3 --privileged=true -v /tmp/myHostData:/tmp/myDockerData ubuntu /bin/bash
```

 ![img](https://cdn.nlark.com/yuque/0/2022/png/27791237/1658226408944-61a9764d-b3db-42f6-b8e6-10ed888287d9.png)

1. **查看数据卷是否挂载成功**

```
docker inspect 容器ID
```

![img](https://cdn.nlark.com/yuque/0/2022/png/27791237/1658226437704-b3a2cbb1-9110-4a67-b6d8-fcf33c3fae29.png)

1. **容器和宿主机之间数据共享**

1. docker修改，主机同步获得 。
2. 主机修改，docker同步获得。
3. docker容器stop，主机修改，docker容器重启看数据是否同步。

![img](https://cdn.nlark.com/yuque/0/2022/png/27791237/1658226473979-b13500a4-0605-49d3-aa07-7e405342dd92.png)

### 7.5.2 读写规则映射添加说明

读写(默认)

```
docker run -it --privileged=true -v /宿主机绝对路径目录:/容器内目录:rw 镜像名
```

默认同上案例，默认就是rw

![img](https://cdn.nlark.com/yuque/0/2022/png/27791237/1658226514729-c2112eaf-6ec8-47ee-94a0-35f8ea7c9beb.png)

 rw = read + write

![img](https://cdn.nlark.com/yuque/0/2022/png/27791237/1658226520150-41d79186-a2ef-460f-80b6-dcb0bbee1ecb.png)

只读

容器实例内部被限制，只能读取不能写

![img](https://cdn.nlark.com/yuque/0/2022/png/27791237/1658226536605-315fd061-8879-4685-a4cd-345ff3fcd1d7.png)

 /容器目录:ro 镜像名               就能完成功能，此时容器自己只能读取不能写  

ro = read only

此时如果宿主机写入内容，可以同步给容器内，容器可以读取到。

```
docker run -it --privileged=true -v /宿主机绝对路径目录:/容器内目录:ro 镜像名
```

### 7.5.3 卷的继承和共享

容器1完成和宿主机的映射

```
docker run -it  --privileged=true -v /mydocker/u:/tmp --name u1 ubuntu
```

![img](https://cdn.nlark.com/yuque/0/2022/png/27791237/1658226567377-ed27036f-cba3-4e16-9d6a-b18e249e0464.png)

![img](https://cdn.nlark.com/yuque/0/2022/png/27791237/1658226571771-a1484811-0dae-4ddb-bf4b-e3c69b001269.png)

容器2继承容器1的卷规则

```
docker run -it  --privileged=true --volumes-from 父类  --name u2 ubuntu
```

![img](https://cdn.nlark.com/yuque/0/2022/png/27791237/1658226594280-b1d73980-163b-4bbb-bc46-823b22e432dd.png)



# 8 Docker常规安装简介

## 8.1 总体步骤

1.搜索镜像

2.拉取镜像

3.查看镜像

4.启动镜像-p服务端口映射

5.停止容器

6.移除容器

## 8.2 安装tomcat

1. **docker hub上面查找tomcat镜像**

```
docker search tomcat
```

![img](https://cdn.nlark.com/yuque/0/2022/png/27791237/1658227019564-3256fed5-8d29-4b9b-b63c-f9db6688647f.png)

1. **从docker hub上拉取tomcat镜像到本地**

```
docker pull tomcat
```

![img](https://cdn.nlark.com/yuque/0/2022/png/27791237/1658227032736-fd32aed9-dbe6-4fdf-8323-37a9f764528a.png)

![img](https://cdn.nlark.com/yuque/0/2022/png/27791237/1658227037231-8c821604-210e-432f-a311-552c51918845.png)

1. **docker images查看是否有拉取到的tomcat**

![img](https://cdn.nlark.com/yuque/0/2022/png/27791237/1658227047824-ae101631-a620-4703-9dac-8af6d9b80fdc.png)

1. **使用tomcat镜像创建容器实例(也叫运行镜像)**

```
docker run -it -p 8080:8080 tomcat
```

-p 小写，主机端口:docker容器端口

-P 大写，随机分配端口

-i 交互

-t 终端

-d 后台

![img](https://cdn.nlark.com/yuque/0/2022/png/27791237/1658227076652-dccf1356-5133-4dfd-ad51-31bdc8d905d5.png)

1. **访问猫首页**

问题

![img](https://cdn.nlark.com/yuque/0/2022/png/27791237/1658227151748-3f6e8cf0-c183-4a32-aec3-c17011ce7929.png)

解决

1. 可能没有映射端口或者没有关闭防火墙
2. 把webapps.dist目录换成webapps

先成功启动tomcat

![img](https://cdn.nlark.com/yuque/0/2022/png/27791237/1658227198315-f76f4e96-a574-4027-ab56-e8ec70855676.png)

查看webapps 文件夹查看为空

![img](https://cdn.nlark.com/yuque/0/2022/png/27791237/1658227241415-7b7a562e-b601-45e1-982f-5cdaf482e1f9.png)

1. **免修改版说明**

```
docker pull billygoo/tomcat8-jdk8
docker run -d -p 8080:8080 --name mytomcat8 billygoo/tomcat8-jdk8
```

![img](https://cdn.nlark.com/yuque/0/2022/png/27791237/1658227293652-4c38aded-e9e1-48bb-a40f-7642928172f4.png)

## 8.3 安装mysql

## 8.3 安装mysql

### 8.3.1 docker hub上面查找mysql镜像

![img](https://cdn.nlark.com/yuque/0/2022/png/27791237/1658385582810-fcaff7bf-61c8-41b5-bf2f-ae0cf7a29e84.png)

### 8.3.2 从docker hub上(阿里云加速器)拉取mysql镜像到本地标签为5.7

![img](https://cdn.nlark.com/yuque/0/2022/png/27791237/1658385588787-239d33e3-87ef-465a-9513-841f703dd972.png)

### 8.3.3 使用mysql5.7镜像创建容器(也叫运行镜像)

#### 8.3.3.1 命令出处，哪里来的？

![img](https://cdn.nlark.com/yuque/0/2022/png/27791237/1658385610694-1b65bab9-3a5a-4cb6-a995-d715004a0c00.png)

#### 8.3.3.2 简单版

使用mysql镜像

docker run -p 3306:3306 -e MYSQL_ROOT_PASSWORD=3011625ljb -d mysql:5.7

```
docker ps
docker exec -it 容器ID /bin/bash
mysql -uroot -p
```

![img](https://cdn.nlark.com/yuque/0/2022/png/27791237/1658385723966-fa2bc241-6f24-4faf-96a2-3098a16d1706.png)

建库建表插入数据

mysql> show databases;
+--------------------+
| Database           |
+--------------------+
| information_schema |
| mysql              |
| performance_schema |
| sys                |
+--------------------+
4 rows in set (0.00 sec)

mysql> create database db_01;
Query OK, 1 row affected (0.00 sec)

mysql> use db_01;
Database changed
mysql> create table user01(id int,name varchar(10));
Query OK, 0 rows affected (0.05 sec)

mysql> insert into user01 values (1,'zhangsan'),(2,'lisi');
Query OK, 2 rows affected (0.02 sec)
Records: 2  Duplicates: 0  Warnings: 0

mysql> select * from user01;
+------+----------+
| id   | name     |
+------+----------+
|    1 | zhangsan |
|    2 | lisi     |
+------+----------+
2 rows in set (0.00 sec)

mysql>

外部Win10也来连接运行在dokcer上的mysql容器实例服务

![img](https://cdn.nlark.com/yuque/0/2022/png/27791237/1658385770994-f0843127-92ef-4299-94b6-3b641109d2cc.png)

问题

插入中文数据试试

![img](https://cdn.nlark.com/yuque/0/2022/png/27791237/1658385783102-bdbbdfe5-30f1-493c-bdc3-79c35c2bf8f5.png)

为什么报错?

docker上默认字符集编码隐患,docker里面的mysql容器实例查看，内容如下：

```
SHOW VARIABLES LIKE 'character%'
```

![img](https://cdn.nlark.com/yuque/0/2022/png/27791237/1658385796114-e5691a9b-d302-4058-9467-90bd86a26944.png)

删除容器后，里面的mysql数据怎么办？

####  8.3.3.3 实战版 

新建mysql容器实例

docker run -d -p 3308:3306 --privileged=true -v /zzyyuse/mysql/log:/var/log/mysql -v /zzyyuse/mysql/data:/var/lib/mysql -v /zzyyuse/mysql/conf:/etc/mysql/conf.d -eMYSQL_ROOT_PASSWORD=3011625ljb --name mysql mysql:5.7

新建my.cnf，通过容器卷同步给mysql容器实例

```shell
[client]
default_character_set=utf8
[mysqld]
collation_server = utf8_general_ci
character_set_server = utf8
```

![img](https://cdn.nlark.com/yuque/0/2022/png/27791237/1658385982627-5fe54dbd-eb94-4d5d-a7ea-354e1be76f35.png)

重新启动mysql容器实例再重新进入并查看字符编码



![img](https://cdn.nlark.com/yuque/0/2022/png/27791237/1658386018656-712d254c-d270-4f17-aa62-cf93b98577d3.png)

![img](https://cdn.nlark.com/yuque/0/2022/png/27791237/1658386026933-dee09e82-39a2-4699-bb63-3930d3e8ba6e.png)

再新建库新建表再插入中文测试

![img](https://cdn.nlark.com/yuque/0/2022/png/27791237/1658386040814-18b11add-9638-4461-ab79-81799679f00c.png)

![img](https://cdn.nlark.com/yuque/0/2022/png/27791237/1658386045922-c04af725-cacb-4b76-a885-4cdbb82b2cc7.png)

结论

之前的DB  无效，修改字符集操作+重启mysql容器实例

之后的DB  有效，需要新建

结论：docker安装完MySQL并run出容器后，建议请先修改完字符集编码后再新建mysql库-表-插数据

![img](https://cdn.nlark.com/yuque/0/2022/png/27791237/1658386205878-9ade8aa5-cc6e-455a-b6d1-5b70344c05d9.png)

##  8.4 安装redis 

**1**从docker hub上(阿里云加速器)拉取redis镜像到本地标签为6.0.8

![image.png](https://cdn.nlark.com/yuque/0/2022/png/27791237/1658386269314-4f582385-baa4-478e-8dbe-d8e3cea4b808.png?x-oss-process=image%2Fformat%2Cwebp)



**2**入门命令

R RUN-D -P 6379:6379 REDIS:6.0.8

[ ROOT@ZZYY DOCKER]#DOCKER RUN -

IF216C38EA035FCEFB5D54245956F9F29750AE2EDD423450A0C59D12B448724F9

[ROOT@ZZYY DOCKER]#

ROOT@ZZYY DOCKER]# DOCKER PS

STATUS

CONTAINER ID

PORTS

CREATED

COMMAND

IMAGE

NAMES

"DOCKER-ENTRYPOINT.S..."

UP 4 SECONDS

F216C38EA035

REDIS:6.0.8

0.0.0.0:6379->6379/TCP,:::::6379->6379

SECONDS AGO

/TCP

AGITATED_PASCAL

4  DOCKER]#

ROOT@ZZYY D

RY DOCKER]# DOCKER EXEC -IT F216C38EAO35 /BIN/BASH

ROOT@ZZYY O

ROOT@F216C38EA035://DATA#REDIS-CLI

127.0.0.1:6379> SET K1 V1

OK

127.0.0.1:6379> GET K1

"V1"

127.0.0.1:6379> PING

PONG

127.0.0.1:6379>

![image.png](https://cdn.nlark.com/yuque/0/2022/png/27791237/1658386283541-4dd83134-4c11-46e9-b6ca-de55f10d25ec.png?x-oss-process=image%2Fformat%2Cwebp)



**3**命令提醒：容器卷记得加入--privileged=true

Docker挂载主机目录Docker访问出现cannot open directory .: Permission denied

解决办法：在挂载目录后多加一个--privileged=true参数即可

**4**在CentOS宿主机下新建目录/app/redis

mkdir -p /app/redis

ROOT@ZZYY

[Y ~]#MKDIR-P /APP/REDIS/

ROOT@ZZYY~]# CD /APP

ROOT@ZZYY APP]# CD REDIS

ROOT@ZZYY R

REDIS]# PWD

/APP/REDIS

[ROOT@ZZYY REDIS]#

![image.png](https://cdn.nlark.com/yuque/0/2022/png/27791237/1658386476816-44e3daec-8880-48c2-9412-4997a1b0cd86.png?x-oss-process=image%2Fformat%2Cwebp)



**5**将一个redis.conf文件模板拷贝进/app/redis目录下

MKDIR-P /APP/REDIS

ROOT@ZZYY /]#

ROOT@ZZYY /]#

P/MYREDIS/REDIS.CONF

ROOT@ZZYY /]#

/APP/REDIS/

/]#

ROOT@ZZYY

ROOT@ZZYY /1# CD /APP/REDIS/

[ROOT@ZZYY REDIS]#

[ROOT@ZZYY REDIS]# LS - L

总用量84

-RW-R--R--. 1 ROOT ROOT 84672 5月

REDIS.CONF

16:21

16

[ROOT@ZZYY REDIS]#

![image.png](https://cdn.nlark.com/yuque/0/2022/png/27791237/1658386499130-3dfd0b28-9053-4a8a-8089-d02cfac2eabc.png?x-oss-process=image%2Fformat%2Cwebp)



将准备好的redis.conf文件放进/app/redis目录下

**6**/app/redis目录下修改redis.conf文件

默认出厂的原始redis.conf



**7**使用redis6.0.8镜像创建容器(也叫运行镜像)



[ROATREDIS REDIS/# DOCKER RUN - D  8373;  RANE  MYY3 -- PRIVILEG8D;TRUE -V /V / /EDIS CONF// REDIS, C

IV/APP/REDIS/DATA:/DATA -D REDIS:6.0.8 REDIS-SERVERVER /ETC/REDIS/REDIS.CONF

LBFF87DOED459FF0A8F34E7E141AEF476121425C77F084611AF60693665F8652C

[ROOT@ZZYY REDIS]#DOCKER PS

CREATED

COMMAND

CONTAINER ID

PORTS

STATUS

IMAGE

NAMES

"DOCKER-ENTRYPOINT..."

2 SECONDS AGO

UP 1 SECOND

REDIS:6.0.8

0.0.0.0:6379->637

BFF F87DOED459

9/TCPMYR3

[ ROOT@ZZYY REDIS]#

![image.png](https://cdn.nlark.com/yuque/0/2022/png/27791237/1658386630490-14317133-6f0e-44b1-a15a-21966767b766.png?x-oss-process=image%2Fformat%2Cwebp)



**8**测试redis-cli连接上来

IV /APP/REDIS/DATA:/DATA -D REDIS:6.0.8 REDIS-SERVER /ETC/REDIS/REDIS.CONF

LD673B7FE3BC8877D9CA36BAA67EOF2091455389BA8EF00E94B6C51FLAFECELA

[ ROOT@ZZYY REDIS]# DOCKER PS

CONTAINER ID

COMMAND

CREATED

PORTS

IMAGE

STATUS

NAMES

"DOCKER-ENTRYPOINT..."

2 SECONDS AGO

0.0.0.0:6379->637

D673B7FE3BC8

UP

1 SECOND

REDIS:6.0.8

9/TCPMYR3

[ ROOT@ZZYY REDIS]# DOCKER EXEC - IT MVR3 /BIN/BASH

ROOT@D673B7FE3BC8://DATA#REDIS-CLI

127.0.0.1:6379>

SET K1 V1

OK

127.0.0.1:6379>

GET K1

"V1"

127.0.0.1:6379>

![image.png](https://cdn.nlark.com/yuque/0/2022/png/27791237/1658386639463-b2b6c0a5-2dcb-49f8-9751-208fa735fd0f.png?x-oss-process=image%2Fformat%2Cwebp)



docker exec -it 运行着Rediis服务的容器ID redis-cli

**9**请证明docker启动使用了我们自己指定的配置文件

修改前

[ROOT@ZZYY REDIS]# DOCKER EXEC - IT MYR3 /BIN/BASH

LROOT@D673B7FE3BC8://DATA# REDIS-CLI

127.0.0.1:6379> SET K1 V1

OK

GET K1

127.0.0.1:6379>

127.0.0.1:6379> SELECT 15

OK

127.0.0.1:6379[15]> EXIT

 EXIT

ROOT@D673B7FE3BC8://DATA#E

EXIT

[ROOT@ZZYY REDIS]#

![image.png](https://cdn.nlark.com/yuque/0/2022/png/27791237/1658386662346-efff690c-15ef-4246-af15-3ceef75e82c1.png?x-oss-process=image%2Fformat%2Cwebp)



我们用的配置文件，数据库默认是16个

修改后

ROOT@ZZYY:/APP/REDIS

文件(F) 编辑(E) 查看(V) 搜索(S) 搜索(S) 帮助(H)

262 # TO ENABLE LOGGING TO THE SYSTEM LOGGER, JUST

JUST

TO YES,

SET

SYSLOG-ENABLED'

TO SUIT

263 # AND OPTIONALLY UPDATE THE OTHER SYSLOG FE

YOUR NEEDS.

SLOG PARAMETERS

264 # SYSLOG-ENABLED NO

265

266 # SPECIFY THE SYSLOG IDENTITY.

7 # SYSLOG- IDENT REDIS

267

268

269 # SPECIFY THE SYSLOG FACILITY. MUST BE USER OR BETWEEN LOCALO-LOCAL7.

269#

\# SYSLOG- FACILITY LOCALO

270

271

272 # SET THE NUMBER OF UAT

F DATABASES. THE DEFAULT DATABASE IS DB O, YOU CAN SELECT

S USING SELECT <DBID> WHERE

3 # A DIFFERENT ONE ON A PER-CONNECTION BASIS USING

273# A

274 # DBID IS A NUMBER BETWEEN O AND ' DATABASES'-1

275

DATABASES 10

276

![image.png](https://cdn.nlark.com/yuque/0/2022/png/27791237/1658386674971-89bd06ec-8496-40c8-835a-81019dbec40b.png?x-oss-process=image%2Fformat%2Cwebp)



宿主机的修改会同步给docker容器里面的配置。记得重启服务

**10**测试redis-cli连接上来第2次

[ROOT@ZZYY REDIS]#

DOCKER PS

CONTAINER ID

COMMAND

STATUS

PORTS

CREATED

IMAGE

NAMES

5 MINUTES AGO

REDIS:6.0.8

"DOCKER-ENTRYPOINT...."

D673B7FE3BC8

0.0.0.0:6379->637

UP 5 MINUTES

9/TCPMYR3

[ROOT@ZZYY REDIS]# DOCKER RESTART MYR3

MYR3

DOCKER EXEC-IT MYR3 /BIN/BASH

[ ROOT@ZZYY REDIS]#

DATA# REDIS-CLI

ROOT@D673B7FE3BC8:

127.0.0.1:6379> SELECT 11

(ERROR) ERR DB INDEX IS OUT OF RANGE

127.0.0.1:6379>SELECT 9

OK

127.0.0.1:6379[9]>SELECT 10

(ERROR) ERR DB INDEX IS OUT OF RANGE

127.0.0.1:6379[9]> SELECT 15

(ERROR) ERR DB INDEX IS OUT OF RANGE

127.0.0.1:6379[9]

![image.png](https://cdn.nlark.com/yuque/0/2022/png/27791237/1658386695258-47156844-dae4-4919-9e77-fb9b215dff21.png?x-oss-process=image%2Fformat%2Cwebp)



##  8.5 安装Nginx 

见高级篇Portaine



在Docker环境下安装Nginx，可以按照以下步骤进行：

#### 1-安装Docker

确保你的系统上已安装Docker。如果你还没有安装，可以从[Docker官方网站](https://www.docker.com/)下载适用于你操作系统的Docker安装包，并按照官方文档的指示进行安装。

#### 2-拉取Nginx镜像

打开终端或命令提示符，输入以下命令来从Docker Hub下载最新版本的Nginx镜像：

```bash
docker pull nginx
```

如果你想拉取特定版本的Nginx，可以在`nginx`后加上版本标签，例如：

```bash
docker pull nginx:1.19
```

#### 3-查看下载的镜像

确认Nginx镜像是否成功下载：

```bash
docker images
```

#### 4-启动Nginx容器

使用以下命令启动Nginx容器，其中：

- `--name nginx` 指定容器的名称为`nginx`。
- `-p 80:80` 将宿主机的80端口映射到容器的80端口，以便外部可以访问Nginx服务。
- `-d` 表示以后台模式运行容器。
- 最后的`nginx`是指使用刚刚拉取的Nginx镜像。

```bash
docker run --name nginx -p 80:80 -d nginx
```

#### 5-验证Nginx是否启动成功

可以通过访问`http://localhost`（如果你是在本地宿主机上操作）来验证Nginx是否正确启动并对外提供服务。另外，可以使用以下命令检查容器状态：

```bash
docker ps
```

#### 6-（可选）自定义Nginx配置

如果你需要修改Nginx的配置或部署项目到Nginx，可以采取以下步骤：

- **进入容器**：使用`docker exec -it nginx /bin/bash`命令进入运行中的Nginx容器。
- **修改配置文件**：在容器内，Nginx的配置文件通常位于`/etc/nginx/nginx.conf`，你可以使用文本编辑器如`vi`或`nano`来修改它。
- **复制项目文件**：将你的项目文件复制到Nginx的默认网站根目录，通常是`/usr/share/nginx/html`。
- **重新加载配置**：修改配置后，执行`nginx -s reload`命令以重新加载Nginx配置，使更改生效。如果修改了配置文件路径或有其他重大更改，可能需要使用`nginx -t`测试配置文件，无误后再重启Nginx。

#### 7-（可选）持久化配置和数据

为了使你的Nginx配置和数据在容器重启后仍然存在，你可以通过映射卷的方式在启动容器时挂载宿主机的目录。例如，挂载配置文件和数据目录：

```bash
docker run --name nginx -p 80:80  --privileged=true -v /path/to/nginx/conf:/etc/nginx/conf.d -v /path/to/nginx/html:/usr/share/nginx/html -d nginx
```

这里，`/path/to/nginx/conf`和`/path/to/nginx/html`是你宿主机上存放Nginx配置文件和网页文件的目录。

按照以上步骤，你就能在Docker环境中成功安装并运行Nginx了。