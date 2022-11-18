# springcloud(一)：大话Spring Cloud

研究了一段时间Spring Boot了准备向Spring Cloud进发，公司架构和项目也全面拥抱了Spring Cloud。在使用了一段时间后发现Spring Cloud从技术架构上降低了对大型系统构建的要求，使我们以非常低的成本（技术或者硬件）搭建一套高效、分布式、容错的平台，但Spring Cloud也不是没有缺点，小型独立的项目不适合使用。

## Spring Cloud是什么鬼？

Spring Cloud是一系列框架的有序集合。它利用Spring Boot的开发便利性巧妙地简化了分布式系统基础设施的开发，如服务发现注册、配置中心、消息总线、负载均衡、断路器、数据监控等，都可以用Spring Boot的开发风格做到一键启动和部署。Spring并没有重复制造轮子，它只是将目前各家公司开发的比较成熟、经得起实际考验的服务框架组合起来，通过Spring Boot风格进行再封装屏蔽掉了复杂的配置和实现原理，最终给开发者留出了一套简单易懂、易部署和易维护的分布式系统开发工具包。

微服务是可以独立部署、水平扩展、独立访问（或者有独立的数据库）的服务单元，springcloud就是这些微服务的大管家，采用了微服务这种架构之后，项目的数量会非常多，springcloud做为大管家需要管理好这些微服务，自然需要很多小弟来帮忙。

主要的小弟有：Spring Cloud Config、Spring Cloud Netflix（Eureka、Hystrix、Zuul、Archaius…）、Spring Cloud Bus、Spring Cloud for Cloud Foundry、Spring Cloud Cluster、Spring Cloud Consul、Spring Cloud Security、Spring Cloud Sleuth、Spring Cloud Data Flow、Spring Cloud Stream、Spring Cloud Task、Spring Cloud Zookeeper、Spring Cloud Connectors、Spring Cloud Starters、Spring Cloud CLI，每个小弟身怀独门绝技武功高强下面来做一一介绍。

## 核心成员

### Spring Cloud Netflix

这可是个大boss，地位仅次于老大，老大各项服务依赖与它，与各种Netflix OSS组件集成，组成微服务的核心，它的小弟主要有Eureka, Hystrix, Zuul, Archaius… 太多了

**Netflix Eureka**

服务中心，云端服务发现，一个基于 REST 的服务，用于定位服务，以实现云端中间层服务发现和故障转移。这个可是springcloud最牛鼻的小弟，服务中心，任何小弟需要其它小弟支持什么都需要从这里来拿，同样的你有什么独门武功的都赶紧过报道，方便以后其它小弟来调用；它的好处是你不需要直接找各种什么小弟支持，只需要到服务中心来领取，也不需要知道提供支持的其它小弟在哪里，还是几个小弟来支持的，反正拿来用就行，服务中心来保证稳定性和质量。

**Netflix Hystrix**

熔断器，容错管理工具，旨在通过熔断机制控制服务和第三方库的节点,从而对延迟和故障提供更强大的容错能力。比如突然某个小弟生病了，但是你还需要它的支持，然后调用之后它半天没有响应，你却不知道，一直在等等这个响应；有可能别的小弟也正在调用你的武功绝技，那么当请求多之后，就会发生严重的阻塞影响老大的整体计划。这个时候Hystrix就派上用场了，当Hystrix发现某个小弟不在状态不稳定立马马上让它下线，让其它小弟来顶上来，或者给你说不用等了这个小弟今天肯定不行，该干嘛赶紧干嘛去别在这排队了。

**Netflix Zuul**

Zuul 是在云平台上提供动态路由,监控,弹性,安全等边缘服务的框架。Zuul 相当于是设备和 Netflix 流应用的 Web 网站后端所有请求的前门。当其它门派来找大哥办事的时候一定要先经过zuul,看下有没有带刀子什么的给拦截回去，或者是需要找那个小弟的直接给带过去。

**Netflix Archaius**

配置管理API，包含一系列配置管理API，提供动态类型化属性、线程安全配置操作、轮询框架、回调机制等功能。可以实现动态获取配置， 原理是每隔60s（默认，可配置）从配置源读取一次内容，这样修改了配置文件后不需要重启服务就可以使修改后的内容生效，前提使用archaius的API来读取。

### Spring Cloud Config

俗称的配置中心，配置管理工具包，让你可以把配置放到远程服务器，集中化管理集群配置，目前支持本地存储、Git以及Subversion。就是以后大家武器、枪火什么的东西都集中放到一起，别随便自己带，方便以后统一管理、升级装备。

### Spring Cloud Bus

事件、消息总线，用于在集群（例如，配置变化事件）中传播状态变化，可与Spring Cloud Config联合实现热部署。相当于水浒传中日行八百里的神行太保戴宗，确保各个小弟之间消息保持畅通。

### Spring Cloud for Cloud Foundry

Cloud Foundry是VMware推出的业界第一个开源PaaS云平台，它支持多种框架、语言、运行时环境、云平台及应用服务，使开发人员能够在几秒钟内进行应用程序的部署和扩展，无需担心任何基础架构的问题

其实就是与CloudFoundry进行集成的一套解决方案，抱了Cloud Foundry的大腿。

### Spring Cloud Cluster

Spring Cloud Cluster将取代Spring Integration。提供在分布式系统中的集群所需要的基础功能支持，如：选举、集群的状态一致性、全局锁、tokens等常见状态模式的抽象和实现。

如果把不同的帮派组织成统一的整体，Spring Cloud Cluster已经帮你提供了很多方便组织成统一的工具。

### Spring Cloud Consul

Consul 是一个支持多数据中心分布式高可用的服务发现和配置共享的服务软件,由 HashiCorp 公司用 Go 语言开发, 基于 Mozilla Public License 2.0 的协议进行开源. Consul 支持健康检查,并允许 HTTP 和 DNS 协议调用 API 存储键值对.

Spring Cloud Consul 封装了Consul操作，consul是一个服务发现与配置工具，与Docker容器可以无缝集成。

## 其它小弟

**Spring Cloud Security**

基于spring security的安全工具包，为你的应用程序添加安全控制。这个小弟很牛鼻专门负责整个帮派的安全问题，设置不同的门派访问特定的资源，不能把秘籍葵花宝典泄漏了。

**Spring Cloud Sleuth**

日志收集工具包，封装了Dapper和log-based追踪以及Zipkin和HTrace操作，为SpringCloud应用实现了一种分布式追踪解决方案。

**Spring Cloud Data Flow**

- Data flow 是一个用于开发和执行大范围数据处理其模式包括ETL，批量运算和持续运算的统一编程模型和托管服务。
- 对于在现代运行环境中可组合的微服务程序来说，Spring Cloud data flow是一个原生云可编配的服务。使用Spring Cloud data flow，开发者可以为像数据抽取，实时分析，和数据导入/导出这种常见用例创建和编配数据通道 （data pipelines）。
- Spring Cloud data flow 是基于原生云对 spring XD的重新设计，该项目目标是简化大数据应用的开发。Spring XD 的流处理和批处理模块的重构分别是基于 Spring Boot的stream 和 task/batch 的微服务程序。这些程序现在都是自动部署单元而且他们原生的支持像 Cloud Foundry、Apache YARN、Apache Mesos和Kubernetes 等现代运行环境。
- Spring Cloud data flow 为基于微服务的分布式流处理和批处理数据通道提供了一系列模型和最佳实践。

**Spring Cloud Stream**

Spring Cloud Stream是创建消息驱动微服务应用的框架。Spring Cloud Stream是基于Spring Boot创建，用来建立单独的／工业级spring应用，使用spring integration提供与消息代理之间的连接。数据流操作开发包，封装了与Redis,Rabbit、Kafka等发送接收消息。

一个业务会牵扯到多个任务，任务之间是通过事件触发的，这就是Spring Cloud stream要干的事了

**Spring Cloud Task**

Spring Cloud Task 主要解决短命微服务的任务管理，任务调度的工作，比如说某些定时任务晚上就跑一次，或者某项数据分析临时就跑几次。

**Spring Cloud Zookeeper**

ZooKeeper是一个分布式的，开放源码的分布式应用程序协调服务，是Google的Chubby一个开源的实现，是Hadoop和Hbase的重要组件。它是一个为分布式应用提供一致性服务的软件，提供的功能包括：配置维护、域名服务、分布式同步、组服务等。ZooKeeper的目标就是封装好复杂易出错的关键服务，将简单易用的接口和性能高效、功能稳定的系统提供给用户。

操作Zookeeper的工具包，用于使用zookeeper方式的服务发现和配置管理，抱了Zookeeper的大腿。

**Spring Cloud Connectors**

Spring Cloud Connectors 简化了连接到服务的过程和从云平台获取操作的过程，有很强的扩展性，可以利用Spring Cloud Connectors来构建你自己的云平台。

便于云端应用程序在各种PaaS平台连接到后端，如：数据库和消息代理服务。

**Spring Cloud Starters**

Spring Boot式的启动项目，为Spring Cloud提供开箱即用的依赖管理。

**Spring Cloud CLI**

基于 Spring Boot CLI，可以让你以命令行方式快速建立云组件。

## 和Spring Boot 是什么关系

Spring Boot 是 Spring 的一套快速配置脚手架，可以基于Spring Boot 快速开发单个微服务，Spring Cloud是一个基于Spring Boot实现的云应用开发工具；Spring Boot专注于快速、方便集成的单个个体，Spring Cloud是关注全局的服务治理框架；Spring Boot使用了默认大于配置的理念，很多集成方案已经帮你选择好了，能不配置就不配置，Spring Cloud很大的一部分是基于Spring Boot来实现,可以不基于Spring Boot吗？不可以。

Spring Boot可以离开Spring Cloud独立使用开发项目，但是Spring Cloud离不开Spring Boot，属于依赖的关系。

> spring -> spring boot > Spring Cloud 这样的关系。

## Spring Cloud的优势

微服务的框架那么多比如：dubbo、Kubernetes，为什么就要使用Spring Cloud的呢？

- 产出于spring大家族，spring在企业级开发框架中无人能敌，来头很大，可以保证后续的更新、完善。比如dubbo现在就差不多死了
- 有Spring Boot 这个独立干将可以省很多事，大大小小的活Spring Boot都搞的挺不错。
- 作为一个微服务治理的大家伙，考虑的很全面，几乎服务治理的方方面面都考虑到了，方便开发开箱即用。
- Spring Cloud 活跃度很高，教程很丰富，遇到问题很容易找到解决方案
- 轻轻松松几行代码就完成了熔断、均衡负载、服务中心的各种平台功能

Spring Cloud对于中小型互联网公司来说是一种福音，因为这类公司往往没有实力或者没有足够的资金投入去开发自己的分布式系统基础设施，使用Spring Cloud一站式解决方案能在从容应对业务发展的同时大大减少开发成本。同时，随着近几年微服务架构和Docker容器概念的火爆，也会让Spring Cloud在未来越来越“云”化的软件开发风格中立有一席之地，尤其是在目前五花八门的分布式解决方案中提供了标准化的、全站式的技术方案，意义可能会堪比当前Servlet规范的诞生，有效推进服务端软件系统技术水平的进步。

# springcloud(二)：注册中心Eureka

 2017/05/10

Eureka是Netflix开源的一款提供服务注册和发现的产品，它提供了完整的Service Registry和Service Discovery实现。也是springcloud体系中最重要最核心的组件之一。

## 背景介绍

### 服务中心

服务中心又称注册中心，管理各种服务功能包括服务的注册、发现、熔断、负载、降级等，比如dubbo admin后台的各种功能。

有了服务中心调用关系会有什么变化，画几个简图来帮忙理解

项目A调用项目B

正常调用项目A请求项目B

![img](assets/ab.jpg)

有了服务中心之后，任何一个服务都不能直接去掉用，都需要通过服务中心来调用

![img](assets/a2b.jpg)

项目A调用项目B，项目B在调用项目C

![img](assets/abc.jpg)

这时候调用的步骤就会为两步：第一步，项目A首先从服务中心请求项目B服务器，然后项目B在从服务中心请求项目C服务。

![img](assets/a2b2c.jpg)

上面的项目只是两三个相互之间的简单调用，但是如果项目超过20个30个呢，在15年底的时候我司分布式的项目就达到了二十几个，画一张图来描述几十个项目之间的相互调用关系全是线条，任何其中的一个项目改动，就会牵连好几个项目跟着重启，巨麻烦而且容易出错。通过服务中心来获取服务你不需要关注你调用的项目IP地址，由几台服务器组成，每次直接去服务中心获取可以使用的服务去调用既可。

由于各种服务都注册到了服务中心，就有了去做很多高级功能条件。比如几台服务提供相同服务来做均衡负载；监控服务器调用成功率来做熔断，移除服务列表中的故障点；监控服务调用时间来对不同的服务器设置不同的权重等等。

说Eureka之前我先八卦一下Netflix

### Netflix

以下介绍来自于百度百科：

> Netflix是一家美国公司，在美国、加拿大提供互联网随选流媒体播放，定制DVD、蓝光光碟在线出租业务。该公司成立于1997年，总部位于加利福尼亚州洛斯盖图，1999年开始订阅服务。2009年，该公司可提供多达10万部DVD电影，并有1千万的订户。2007年2月25日，Netflix宣布已经售出第10亿份DVD。HIS一份报告中表示，2011年Netflix网络电影销量占据美国用户在线电影总销量的45%。

我第一次看到这个单词的时候，是在各种美剧或者电影的开头，Netflix拍摄的代表性的美剧有《纸牌屋》、《毒枭》、《怪奇物语》。后来研究springcloud的时候发现了Netflix公司，就在想它们是不是同一家公司，经过核对github上面邮件后缀判定确实是同一家公司，其实springcloud的微服务就基于Netflix公司的开源产品来做的。

Netflix的开源框架组件已经在Netflix的大规模分布式微服务环境中经过多年的生产实战验证，正逐步被社区接受为构造微服务框架的标准组件。Spring Cloud开源产品，主要是基于对Netflix开源组件的进一步封装，方便Spring开发人员构建微服务基础框架。对于一些打算构建微服务框架体系的公司来说，充分利用或参考借鉴Netflix的开源微服务组件(或Spring Cloud)，在此基础上进行必要的企业定制，无疑是通向微服务架构的捷径。

### Eureka

按照官方介绍：

> Eureka is a REST (Representational State Transfer) based service that is primarily used in the AWS cloud for locating services for the purpose of load balancing and failover of middle-tier servers.
>
> Eureka 是一个基于 REST 的服务，主要在 AWS 云中使用, 定位服务来进行中间层服务器的负载均衡和故障转移。

Spring Cloud 封装了 Netflix 公司开发的 Eureka 模块来实现服务注册和发现。Eureka 采用了 C-S 的设计架构。Eureka Server 作为服务注册功能的服务器，它是服务注册中心。而系统中的其他微服务，使用 Eureka 的客户端连接到 Eureka Server，并维持心跳连接。这样系统的维护人员就可以通过 Eureka Server 来监控系统中各个微服务是否正常运行。Spring Cloud 的一些其他模块（比如Zuul）就可以通过 Eureka Server 来发现系统中的其他微服务，并执行相关的逻辑。

Eureka由两个组件组成：Eureka服务器和Eureka客户端。Eureka服务器用作服务注册服务器。Eureka客户端是一个java客户端，用来简化与服务器的交互、作为轮询负载均衡器，并提供服务的故障切换支持。Netflix在其生产环境中使用的是另外的.客户端，它提供基于流量、资源利用率以及出错状态的加权负载均衡。

用一张图来认识以下：

![img](assets/eureka-architecture-overview.png)

上图简要描述了Eureka的基本架构，由3个角色组成：

1、Eureka Server

- 提供服务注册和发现

2、Service Provider

- 服务提供方
- 将自身服务注册到Eureka，从而使服务消费方能够找到

3、Service Consumer

- 服务消费方
- 从Eureka获取注册服务列表，从而能够消费服务

## 案例实践

### Eureka Server

spring cloud已经帮我实现了服务注册中心，我们只需要很简单的几个步骤就可以完成。

1、pom中添加依赖

```
<dependencies>
	<dependency>
		<groupId>org.springframework.cloud</groupId>
		<artifactId>spring-cloud-starter</artifactId>
	</dependency>
	<dependency>
		<groupId>org.springframework.cloud</groupId>
		<artifactId>spring-cloud-starter-eureka-server</artifactId>
	</dependency>
	<dependency>
		<groupId>org.springframework.boot</groupId>
		<artifactId>spring-boot-starter-test</artifactId>
		<scope>test</scope>
	</dependency>
</dependencies>
```

2、添加启动代码中添加`@EnableEurekaServer`注解

```
@SpringBootApplication
@EnableEurekaServer
public class SpringCloudEurekaApplication {

	public static void main(String[] args) {
		SpringApplication.run(SpringCloudEurekaApplication.class, args);
	}
}
```

3、配置文件

在默认设置下，该服务注册中心也会将自己作为客户端来尝试注册它自己，所以我们需要禁用它的客户端注册行为，在`application.properties`添加以下配置：

```
spring.application.name=spring-cloud-eureka

server.port=8000
eureka.client.register-with-eureka=false
eureka.client.fetch-registry=false

eureka.client.serviceUrl.defaultZone=http://localhost:${server.port}/eureka/
```

- `eureka.client.register-with-eureka` ：表示是否将自己注册到Eureka Server，默认为true。
- `eureka.client.fetch-registry` ：表示是否从Eureka Server获取注册信息，默认为true。
- `eureka.client.serviceUrl.defaultZone` ：设置与Eureka Server交互的地址，查询服务和注册服务都需要依赖这个地址。默认是http://localhost:8761/eureka ；多个地址可使用 , 分隔。

启动工程后，访问：http://localhost:8000/，可以看到下面的页面，其中还没有发现任何服务

![img](assets/eureka_start.jpg)

## 集群

注册中心这么关键的服务，如果是单点话，遇到故障就是毁灭性的。在一个分布式系统中，服务注册中心是最重要的基础部分，理应随时处于可以提供服务的状态。为了维持其可用性，使用集群是很好的解决方案。Eureka通过互相注册的方式来实现高可用的部署，所以我们只需要将Eureke Server配置其他可用的serviceUrl就能实现高可用部署。

### 双节点注册中心

首次我们尝试一下双节点的注册中心的搭建。

1、创建application-peer1.properties，作为peer1服务中心的配置，并将serviceUrl指向peer2

```
spring.application.name=spring-cloud-eureka
server.port=8000
eureka.instance.hostname=peer1

eureka.client.serviceUrl.defaultZone=http://peer2:8001/eureka/
```

2、创建application-peer2.properties，作为peer2服务中心的配置，并将serviceUrl指向peer1

```
spring.application.name=spring-cloud-eureka
server.port=8001
eureka.instance.hostname=peer2

eureka.client.serviceUrl.defaultZone=http://peer1:8000/eureka/
```

3、host转换

在hosts文件中加入如下配置

```
127.0.0.1 peer1  
127.0.0.1 peer2  
```

4、打包启动

依次执行下面命令

```
#打包
mvn clean package
# 分别以peer1和peeer2 配置信息启动eureka
java -jar spring-cloud-eureka-0.0.1-SNAPSHOT.jar --spring.profiles.active=peer1
java -jar spring-cloud-eureka-0.0.1-SNAPSHOT.jar --spring.profiles.active=peer2
```

依次启动完成后，浏览器输入：`http://localhost:8000/` 效果图如下：

![img](assets/eureka-two.jpg)

根据图可以看出peer1的注册中心DS Replicas已经有了peer2的相关配置信息，并且出现在available-replicas中。我们手动停止peer2来观察，发现peer2就会移动到unavailable-replicas一栏中，表示peer2不可用。

到此双节点的配置已经完成。

### eureka集群使用

在生产中我们可能需要三台或者大于三台的注册中心来保证服务的稳定性，配置的原理其实都一样，将注册中心分别指向其它的注册中心。这里只介绍三台集群的配置情况，其实和双节点的注册中心类似，每台注册中心分别又指向其它两个节点即可，使用application.yml来配置。

application.yml配置详情如下：

```
---
spring:
  application:
    name: spring-cloud-eureka
  profiles: peer1
server:
  port: 8000
eureka:
  instance:
    hostname: peer1
  client:
    serviceUrl:
      defaultZone: http://peer2:8001/eureka/,http://peer3:8002/eureka/
---
spring:
  application:
    name: spring-cloud-eureka
  profiles: peer2
server:
  port: 8001
eureka:
  instance:
    hostname: peer2
  client:
    serviceUrl:
      defaultZone: http://peer1:8000/eureka/,http://peer3:8002/eureka/
---
spring:
  application:
    name: spring-cloud-eureka
  profiles: peer3
server:
  port: 8002
eureka:
  instance:
    hostname: peer3
  client:
    serviceUrl:
      defaultZone: http://peer1:8000/eureka/,http://peer2:8001/eureka/
```

分别以peer1、peer2、peer3的配置参数启动eureka注册中心。

```
java -jar spring-cloud-eureka-0.0.1-SNAPSHOT.jar --spring.profiles.active=peer1
java -jar spring-cloud-eureka-0.0.1-SNAPSHOT.jar --spring.profiles.active=peer2
java -jar spring-cloud-eureka-0.0.1-SNAPSHOT.jar --spring.profiles.active=peer3
```

依次启动完成后，浏览器输入：`http://localhost:8000/` 效果图如下：

![img](assets/eureka-cluster.jpg)

可以在peer1中看到了peer2、peer3的相关信息。至此eureka集群也已经完成了

# springcloud(三)：服务提供与调用

上一篇文章我们介绍了eureka服务注册中心的搭建，这篇文章介绍一下如何使用eureka服务注册中心，搭建一个简单的服务端注册服务，客户端去调用服务使用的案例。

案例中有三个角色：服务注册中心、服务提供者、服务消费者，其中服务注册中心就是我们上一篇的eureka单机版启动既可，流程是首先启动注册中心，服务提供者生产服务并注册到服务中心中，消费者从服务中心中获取服务并执行。

## 服务提供

我们假设服务提供者有一个hello方法，可以根据传入的参数，提供输出“hello xxx，this is first messge”的服务

### 1、pom包配置

创建一个springboot项目，pom.xml中添加如下配置：

```
<dependencies>
	<dependency>
		<groupId>org.springframework.cloud</groupId>
		<artifactId>spring-cloud-starter-eureka</artifactId>
	</dependency>
	<dependency>
		<groupId>org.springframework.boot</groupId>
		<artifactId>spring-boot-starter-test</artifactId>
		<scope>test</scope>
	</dependency>
</dependencies>
```

### 2、配置文件

application.properties配置如下：

```
spring.application.name=spring-cloud-producer
server.port=9000
eureka.client.serviceUrl.defaultZone=http://localhost:8000/eureka/
```

参数在上一篇都已经解释过，这里不多说。

### 3、启动类

启动类中添加`@EnableDiscoveryClient`注解

```
@SpringBootApplication
@EnableDiscoveryClient
public class ProducerApplication {

	public static void main(String[] args) {
		SpringApplication.run(ProducerApplication.class, args);
	}
}
```

### 4、controller

提供hello服务

```
@RestController
public class HelloController {
	
    @RequestMapping("/hello")
    public String index(@RequestParam String name) {
        return "hello "+name+"，this is first messge";
    }
}
```

添加`@EnableDiscoveryClient`注解后，项目就具有了服务注册的功能。启动工程后，就可以在注册中心的页面看到SPRING-CLOUD-PRODUCER服务。

![img](assets/eureka_server.png)

到此服务提供者配置就完成了。

## 服务调用

### 1、pom包配置

和服务提供者一致

```
<dependencies>
	<dependency>
		<groupId>org.springframework.cloud</groupId>
		<artifactId>spring-cloud-starter-eureka</artifactId>
	</dependency>
	<dependency>
		<groupId>org.springframework.boot</groupId>
		<artifactId>spring-boot-starter-test</artifactId>
		<scope>test</scope>
	</dependency>
</dependencies>
```

### 2、配置文件

application.properties配置如下：

```
spring.application.name=spring-cloud-consumer
server.port=9001
eureka.client.serviceUrl.defaultZone=http://localhost:8000/eureka/
```

### 3、启动类

启动类添加`@EnableDiscoveryClient`和`@EnableFeignClients`注解。

```
@SpringBootApplication
@EnableDiscoveryClient
@EnableFeignClients
public class ConsumerApplication {

	public static void main(String[] args) {
		SpringApplication.run(ConsumerApplication.class, args);
	}

}
```

- `@EnableDiscoveryClient` :启用服务注册与发现
- `@EnableFeignClients`：启用feign进行远程调用

> Feign是一个声明式Web Service客户端。使用Feign能让编写Web Service客户端更加简单, 它的使用方法是定义一个接口，然后在上面添加注解，同时也支持JAX-RS标准的注解。Feign也支持可拔插式的编码器和解码器。Spring Cloud对Feign进行了封装，使其支持了Spring MVC标准注解和HttpMessageConverters。Feign可以与Eureka和Ribbon组合使用以支持负载均衡。

### 4、feign调用实现

```
@FeignClient(name= "spring-cloud-producer")
public interface HelloRemote {
    @RequestMapping(value = "/hello")
    public String hello(@RequestParam(value = "name") String name);
}
```

- name:远程服务名，及spring.application.name配置的名称

此类中的方法和远程服务中contoller中的方法名和参数需保持一致。

### 5、web层调用远程服务

将HelloRemote注入到controller层，像普通方法一样去调用即可。

```
@RestController
public class ConsumerController {

    @Autowired
    HelloRemote HelloRemote;
	
    @RequestMapping("/hello/{name}")
    public String index(@PathVariable("name") String name) {
        return HelloRemote.hello(name);
    }

}
```

到此，最简单的一个服务注册与调用的例子就完成了。

## 测试

### 简单调用

依次启动spring-cloud-eureka、spring-cloud-producer、spring-cloud-consumer三个项目

先输入：`http://localhost:9000/hello?name=neo` 检查spring-cloud-producer服务是否正常

返回：`hello neo，this is first messge`

说明spring-cloud-producer正常启动，提供的服务也正常。

浏览器中输入：`http://localhost:9001/hello/neo`

返回：`hello neo，this is first messge`

说明客户端已经成功的通过feign调用了远程服务hello，并且将结果返回到了浏览器。

### 负载均衡

以上面spring-cloud-producer为例子修改，将其中的controller改动如下：

```
@RestController
public class HelloController {
	
    @RequestMapping("/hello")
    public String index(@RequestParam String name) {
        return "hello "+name+"，this is producer 2  send first messge";
    }
}
```

在配置文件中改动端口：

```
spring.application.name=spring-cloud-producer
server.port=9003
eureka.client.serviceUrl.defaultZone=http://localhost:8000/eureka/
```

打包启动后，在eureka就会发现两个服务提供者，如下图：

![img](assets/eureka_server2.png)

然后在浏览器再次输入：`http://localhost:9001/hello/neo` 进行测试：

第一次返回结果：`hello neo，this is first messge`

第二次返回结果：`hello neo，this is producer 2 send first messge`

不断的进行测试下去会发现两种结果交替出现，说明两个服务中心自动提供了服务均衡负载的功能。如果我们将服务提供者的数量在提高为N个，测试结果一样，请求会自动轮询到每个服务端来处理。

# springcloud(四)：熔断器Hystrix

说起springcloud熔断让我想起了去年股市中的熔断，多次痛的领悟，随意实施的熔断对整个系统的影响是灾难性的，好了接下来我们还是说正事。

## 熔断器

### 雪崩效应

在微服务架构中通常会有多个服务层调用，基础服务的故障可能会导致级联故障，进而造成整个系统不可用的情况，这种现象被称为服务雪崩效应。服务雪崩效应是一种因“服务提供者”的不可用导致“服务消费者”的不可用,并将不可用逐渐放大的过程。

如果下图所示：A作为服务提供者，B为A的服务消费者，C和D是B的服务消费者。A不可用引起了B的不可用，并将不可用像滚雪球一样放大到C和D时，雪崩效应就形成了。

![img](assets/hystrix-1.png)

### 熔断器（CircuitBreaker）

熔断器的原理很简单，如同电力过载保护器。它可以实现快速失败，如果它在一段时间内侦测到许多类似的错误，会强迫其以后的多个调用快速失败，不再访问远程服务器，从而防止应用程序不断地尝试执行可能会失败的操作，使得应用程序继续执行而不用等待修正错误，或者浪费CPU时间去等到长时间的超时产生。熔断器也可以使应用程序能够诊断错误是否已经修正，如果已经修正，应用程序会再次尝试调用操作。

熔断器模式就像是那些容易导致错误的操作的一种代理。这种代理能够记录最近调用发生错误的次数，然后决定使用允许操作继续，或者立即返回错误。 熔断器开关相互转换的逻辑如下图：

![img](assets/hystrix-2.png)

熔断器就是保护服务高可用的最后一道防线。

### Hystrix特性

**1.断路器机制**

断路器很好理解, 当Hystrix Command请求后端服务失败数量超过一定比例(默认50%), 断路器会切换到开路状态(Open). 这时所有请求会直接失败而不会发送到后端服务. 断路器保持在开路状态一段时间后(默认5秒), 自动切换到半开路状态(HALF-OPEN). 这时会判断下一次请求的返回情况, 如果请求成功, 断路器切回闭路状态(CLOSED), 否则重新切换到开路状态(OPEN). Hystrix的断路器就像我们家庭电路中的保险丝, 一旦后端服务不可用, 断路器会直接切断请求链, 避免发送大量无效请求影响系统吞吐量, 并且断路器有自我检测并恢复的能力.

**2.Fallback**

Fallback相当于是降级操作. 对于查询操作, 我们可以实现一个fallback方法, 当请求后端服务出现异常的时候, 可以使用fallback方法返回的值. fallback方法的返回值一般是设置的默认值或者来自缓存.

**3.资源隔离**

在Hystrix中, 主要通过线程池来实现资源隔离. 通常在使用的时候我们会根据调用的远程服务划分出多个线程池. 例如调用产品服务的Command放入A线程池, 调用账户服务的Command放入B线程池. 这样做的主要优点是运行环境被隔离开了. 这样就算调用服务的代码存在bug或者由于其他原因导致自己所在线程池被耗尽时, 不会对系统的其他服务造成影响. 但是带来的代价就是维护多个线程池会对系统带来额外的性能开销. 如果是对性能有严格要求而且确信自己调用服务的客户端代码不会出问题的话, 可以使用Hystrix的信号模式(Semaphores)来隔离资源.

## Feign Hystrix

因为熔断只是作用在服务调用这一端，因此我们根据上一篇的示例代码只需要改动spring-cloud-consumer项目相关代码就可以。因为，Feign中已经依赖了Hystrix所以在maven配置上不用做任何改动。

### 1、配置文件

application.properties添加这一条：

```
feign.hystrix.enabled=true
```

### 2、创建回调类

创建HelloRemoteHystrix类继承与HelloRemote实现回调的方法

```
@Component
public class HelloRemoteHystrix implements HelloRemote{

    @Override
    public String hello(@RequestParam(value = "name") String name) {
        return "hello" +name+", this messge send failed ";
    }
}
```

### 3、添加fallback属性

在`HelloRemote`类添加指定fallback类，在服务熔断的时候返回fallback类中的内容。

```
@FeignClient(name= "spring-cloud-producer",fallback = HelloRemoteHystrix.class)
public interface HelloRemote {

    @RequestMapping(value = "/hello")
    public String hello(@RequestParam(value = "name") String name);
}
```

改动点就这点，很简单吧。

### 4、测试

那我们就来测试一下看看效果吧。

依次启动spring-cloud-eureka、spring-cloud-producer、spring-cloud-consumer三个项目。

浏览器中输入：`http://localhost:9001/hello/neo`

返回：`hello neo，this is first messge`

说明加入熔断相关信息后，不影响正常的访问。接下来我们手动停止spring-cloud-producer项目再次测试：

浏览器中输入：`http://localhost:9001/hello/neo`

返回：`hello neo, this messge send failed`

根据返回结果说明熔断成功。

# springcloud(五)：熔断监控Hystrix Dashboard和Turbine

Hystrix-dashboard是一款针对Hystrix进行实时监控的工具，通过Hystrix Dashboard我们可以在直观地看到各Hystrix Command的请求响应时间, 请求成功率等数据。但是只使用Hystrix Dashboard的话, 你只能看到单个应用内的服务信息, 这明显不够. 我们需要一个工具能让我们汇总系统内多个服务的数据并显示到Hystrix Dashboard上, 这个工具就是Turbine.

## Hystrix Dashboard

我们在熔断示例项目spring-cloud-consumer-hystrix的基础上更改，重新命名为：spring-cloud-consumer-hystrix-dashboard。

### 1、添加依赖

```
<dependency>
	<groupId>org.springframework.cloud</groupId>
	<artifactId>spring-cloud-starter-hystrix</artifactId>
</dependency>
<dependency>
	<groupId>org.springframework.cloud</groupId>
	<artifactId>spring-cloud-starter-hystrix-dashboard</artifactId>
</dependency>
<dependency>
	<groupId>org.springframework.boot</groupId>
	<artifactId>spring-boot-starter-actuator</artifactId>
</dependency>
```

这三个包必须添加

### 2、启动类

启动类添加启用Hystrix Dashboard和熔断器

```
@SpringBootApplication
@EnableDiscoveryClient
@EnableFeignClients
@EnableHystrixDashboard
@EnableCircuitBreaker
public class ConsumerApplication {

	public static void main(String[] args) {
		SpringApplication.run(ConsumerApplication.class, args);
	}
}
```

### 3、测试

启动工程后访问 http://localhost:9001/hystrix，将会看到如下界面：

![img](assets/hystrix-dashboard-1.jpg)

图中会有一些提示：

> Cluster via Turbine (default cluster): http://turbine-hostname:port/turbine.stream
> Cluster via Turbine (custom cluster): http://turbine-hostname:port/turbine.stream?cluster=[clusterName]
> Single Hystrix App: http://hystrix-app:port/hystrix.stream

大概意思就是如果查看默认集群使用第一个url,查看指定集群使用第二个url,单个应用的监控使用最后一个，我们暂时只演示单个应用的所以在输入框中输入： http://localhost:9001/hystrix.stream ，输入之后点击 monitor，进入页面。

如果没有请求会先显示`Loading ...`，访问http://localhost:9001/hystrix.stream 也会不断的显示ping。

请求服务http://localhost:9001/hello/neo，就可以看到监控的效果了，首先访问http://localhost:9001/hystrix.stream，显示如下：

```
ping: 

data: {"type":...}

data: {"type":...}
```

说明已经返回了监控的各项结果

到监控页面就会显示如下图：

![img](assets/hystrix-dashboard-2.jpg)

其实就是http://localhost:9001/hystrix.stream返回结果的图形化显示，Hystrix Dashboard Wiki上详细说明了图上每个指标的含义，如下图：

![img](assets/hystrix-dashboard-3.png)

到此单个应用的熔断监控已经完成。

## Turbine

在复杂的分布式系统中，相同服务的节点经常需要部署上百甚至上千个，很多时候，运维人员希望能够把相同服务的节点状态以一个整体集群的形式展现出来，这样可以更好的把握整个系统的状态。 为此，Netflix提供了一个开源项目（Turbine）来提供把多个hystrix.stream的内容聚合为一个数据源供Dashboard展示。

### 1、添加依赖

```
<dependencies>
	<dependency>
		<groupId>org.springframework.cloud</groupId>
		<artifactId>spring-cloud-starter-turbine</artifactId>
	</dependency>
	<dependency>
		<groupId>org.springframework.cloud</groupId>
		<artifactId>spring-cloud-netflix-turbine</artifactId>
	</dependency>
	<dependency>
		<groupId>org.springframework.boot</groupId>
		<artifactId>spring-boot-starter-actuator</artifactId>
	</dependency>
	<dependency>
		<groupId>org.springframework.cloud</groupId>
		<artifactId>spring-cloud-starter-hystrix-dashboard</artifactId>
	</dependency>
</dependencies>
```

### 2、配置文件

```
spring.application.name=hystrix-dashboard-turbine
server.port=8001
turbine.appConfig=node01,node02
turbine.aggregator.clusterConfig= default
turbine.clusterNameExpression= new String("default")

eureka.client.serviceUrl.defaultZone=http://localhost:8000/eureka/
```

- `turbine.appConfig` ：配置Eureka中的serviceId列表，表明监控哪些服务
- `turbine.aggregator.clusterConfig` ：指定聚合哪些集群，多个使用”,”分割，默认为default。可使用`http://.../turbine.stream?cluster={clusterConfig之一}`访问
- `turbine.clusterNameExpression` ： 1. clusterNameExpression指定集群名称，默认表达式appName；此时：`turbine.aggregator.clusterConfig`需要配置想要监控的应用名称；2. 当clusterNameExpression: default时，`turbine.aggregator.clusterConfig`可以不写，因为默认就是default；3. 当clusterNameExpression: metadata[‘cluster’]时，假设想要监控的应用配置了`eureka.instance.metadata-map.cluster: ABC`，则需要配置，同时`turbine.aggregator.clusterConfig: ABC`

### 3、启动类

启动类添加`@EnableTurbine`，激活对Turbine的支持

```
@SpringBootApplication
@EnableHystrixDashboard
@EnableTurbine
public class DashboardApplication {

	public static void main(String[] args) {
		SpringApplication.run(DashboardApplication.class, args);
	}

}
```

到此Turbine（hystrix-dashboard-turbine）配置完成

### 4、测试

在示例项目spring-cloud-consumer-hystrix基础上修改为两个服务的调用者spring-cloud-consumer-node1和spring-cloud-consumer-node2

spring-cloud-consumer-node1项目改动如下： application.properties文件内容

```
spring.application.name=node01
server.port=9001
feign.hystrix.enabled=true

eureka.client.serviceUrl.defaultZone=http://localhost:8000/eureka/
```

spring-cloud-consumer-node2项目改动如下： application.properties文件内容

```
spring.application.name=node02
server.port=9002
feign.hystrix.enabled=true

eureka.client.serviceUrl.defaultZone=http://localhost:8000/eureka/
```

HelloRemote类修改：

```
@FeignClient(name= "spring-cloud-producer2", fallback = HelloRemoteHystrix.class)
public interface HelloRemote {

    @RequestMapping(value = "/hello")
    public String hello2(@RequestParam(value = "name") String name);

}
```

对应的`HelloRemoteHystrix`和`ConsumerController`类跟随修改，具体查看代码

修改完毕后，依次启动spring-cloud-eureka、spring-cloud-consumer-node1、spring-cloud-consumer-node1、hystrix-dashboard-turbine（Turbine）

打开eureka后台可以看到注册了三个服务：

![img](assets/turbine-01.jpg)

访问 http://localhost:8001/turbine.stream

返回：

```
: ping
data: {"reportingHostsLast10Seconds":1,"name":"meta","type":"meta","timestamp":1494921985839}
```

并且会不断刷新以获取实时的监控数据，说明和单个的监控类似，返回监控项目的信息。进行图形化监控查看，输入：http://localhost:8001/hystrix，返回酷酷的小熊界面，输入： http://localhost:8001/turbine.stream，然后点击 Monitor Stream ,可以看到出现了俩个监控列表

![img](assets/turbine-02.jpg)

# springcloud(六)：配置中心git示例

 2017/05/22

随着线上项目变的日益庞大，每个项目都散落着各种配置文件，如果采用分布式的开发模式，需要的配置文件随着服务增加而不断增多。某一个基础服务信息变更，都会引起一系列的更新和重启，运维苦不堪言也容易出错。配置中心便是解决此类问题的灵丹妙药。

市面上开源的配置中心有很多，BAT每家都出过，360的QConf、淘宝的diamond、百度的disconf都是解决这类问题。国外也有很多开源的配置中心Apache Commons Configuration、owner、cfg4j等等。这些开源的软件以及解决方案都很优秀，但是我最钟爱的却是Spring Cloud Config，因为它功能全面强大，可以无缝的和spring体系相结合，够方便够简单颜值高我喜欢。

## Spring Cloud Config

在我们了解spring cloud config之前，我可以想想一个配置中心提供的核心功能应该有什么

- 提供服务端和客户端支持
- 集中管理各环境的配置文件
- 配置文件修改之后，可以快速的生效
- 可以进行版本管理
- 支持大的并发查询
- 支持各种语言

Spring Cloud Config可以完美的支持以上所有的需求。

Spring Cloud Config项目是一个解决分布式系统的配置管理方案。它包含了Client和Server两个部分，server提供配置文件的存储、以接口的形式将配置文件的内容提供出去，client通过接口获取数据、并依据此数据初始化自己的应用。Spring cloud使用git或svn存放配置文件，默认情况下使用git，我们先以git为例做一套示例。

首先在github上面创建了一个文件夹config-repo用来存放配置文件，为了模拟生产环境，我们创建以下三个配置文件：

```
// 开发环境
neo-config-dev.properties
// 测试环境
neo-config-test.properties
// 生产环境
neo-config-pro.properties
```

每个配置文件中都写一个属性neo.hello,属性值分别是 hello im dev/test/pro 。下面我们开始配置server端

## server 端

### 1、添加依赖

```
<dependencies>
	<dependency>
		<groupId>org.springframework.cloud</groupId>
		<artifactId>spring-cloud-config-server</artifactId>
	</dependency>
</dependencies>
```

只需要加入spring-cloud-config-server包引用既可。

### 2、配置文件

```
server:
  port: 8001
spring:
  application:
    name: spring-cloud-config-server
  cloud:
    config:
      server:
        git:
          uri: https://github.com/ityouknow/spring-cloud-starter/     # 配置git仓库的地址
          search-paths: config-repo                             # git仓库地址下的相对地址，可以配置多个，用,分割。
          username:                                             # git仓库的账号
          password:                                             # git仓库的密码
```

Spring Cloud Config也提供本地存储配置的方式。我们只需要设置属性`spring.profiles.active=native`，Config Server会默认从应用的`src/main/resource`目录下检索配置文件。也可以通过`spring.cloud.config.server.native.searchLocations=file:E:/properties/`属性来指定配置文件的位置。虽然Spring Cloud Config提供了这样的功能，但是为了支持更好的管理内容和版本控制的功能，还是推荐使用git的方式。

### 3、启动类

启动类添加`@EnableConfigServer`，激活对配置中心的支持

```
@EnableConfigServer
@SpringBootApplication
public class ConfigServerApplication {

	public static void main(String[] args) {
		SpringApplication.run(ConfigServerApplication.class, args);
	}
}
```

到此server端相关配置已经完成

### 4、测试

首先我们先要测试server端是否可以读取到github上面的配置信息，直接访问：`http://localhost:8001/neo-config/dev`

返回信息如下：

```
{
    "name": "neo-config", 
    "profiles": [
        "dev"
    ], 
    "label": null, 
    "version": null, 
    "state": null, 
    "propertySources": [
        {
            "name": "https://github.com/ityouknow/spring-cloud-starter/config-repo/neo-config-dev.properties", 
            "source": {
                "neo.hello": "hello im dev"
            }
        }
    ]
}
```

上述的返回的信息包含了配置文件的位置、版本、配置文件的名称以及配置文件中的具体内容，说明server端已经成功获取了git仓库的配置信息。

如果直接查看配置文件中的配置信息可访问：`http://localhost:8001/neo-config-dev.properties`，返回：`neo.hello: hello im dev`

修改配置文件`neo-config-dev.properties`中配置信息为：`neo.hello=hello im dev update`,再次在浏览器访问`http://localhost:8001/neo-config-dev.properties`，返回：`neo.hello: hello im dev update`。说明server端会自动读取最新提交的内容

仓库中的配置文件会被转换成web接口，访问可以参照以下的规则：

- /{application}/{profile}[/{label}]
- /{application}-{profile}.yml
- /{label}/{application}-{profile}.yml
- /{application}-{profile}.properties
- /{label}/{application}-{profile}.properties

以neo-config-dev.properties为例子，它的application是neo-config，profile是dev。client会根据填写的参数来选择读取对应的配置。

## client 端

主要展示如何在业务项目中去获取server端的配置信息

### 1、添加依赖

```
<dependencies>
	<dependency>
		<groupId>org.springframework.cloud</groupId>
		<artifactId>spring-cloud-starter-config</artifactId>
	</dependency>
	<dependency>
		<groupId>org.springframework.boot</groupId>
		<artifactId>spring-boot-starter-web</artifactId>
	</dependency>
	<dependency>
		<groupId>org.springframework.boot</groupId>
		<artifactId>spring-boot-starter-test</artifactId>
		<scope>test</scope>
	</dependency>
</dependencies>
```

引入spring-boot-starter-web包方便web测试

### 2、配置文件

需要配置两个配置文件，application.properties和bootstrap.properties

application.properties如下：

```
spring.application.name=spring-cloud-config-client
server.port=8002
```

bootstrap.properties如下：

```
spring.cloud.config.name=neo-config
spring.cloud.config.profile=dev
spring.cloud.config.uri=http://localhost:8001/
spring.cloud.config.label=master
```

- spring.application.name：对应{application}部分
- spring.cloud.config.profile：对应{profile}部分
- spring.cloud.config.label：对应git的分支。如果配置中心使用的是本地存储，则该参数无用
- spring.cloud.config.uri：配置中心的具体地址
- spring.cloud.config.discovery.service-id：指定配置中心的service-id，便于扩展为高可用配置集群。

> 特别注意：上面这些与spring-cloud相关的属性必须配置在bootstrap.properties中，config部分内容才能被正确加载。因为config的相关配置会先于application.properties，而bootstrap.properties的加载也是先于application.properties。

### 3、启动类

启动类添加`@EnableConfigServer`，激活对配置中心的支持

```
@SpringBootApplication
public class ConfigClientApplication {

	public static void main(String[] args) {
		SpringApplication.run(ConfigClientApplication.class, args);
	}
}
```

启动类只需要`@SpringBootApplication`注解就可以

### 4、web测试

使用`@Value`注解来获取server端参数的值

```
@RestController
class HelloController {
    @Value("${neo.hello}")
    private String hello;

    @RequestMapping("/hello")
    public String from() {
        return this.hello;
    }
}
```

启动项目后访问：`http://localhost:8002/hello`，返回：`hello im dev update`说明已经正确的从server端获取到了参数。到此一个完整的服务端提供配置服务，客户端获取配置参数的例子就完成了。

我们在进行一些小实验，手动修改`neo-config-dev.properties`中配置信息为：`neo.hello=hello im dev update1`提交到github,再次在浏览器访问`http://localhost:8002/hello`，返回：`neo.hello: hello im dev update`，说明获取的信息还是旧的参数，这是为什么呢？因为springboot项目只有在启动的时候才会获取配置文件的值，修改github信息后，client端并没有在次去获取，所以导致这个问题。如何去解决这个问题呢？留到下一章我们在介绍。

# springcloud(七)：配置中心svn示例和refresh

上一篇[springcloud(六)：配置中心git示例](http://www.ityouknow.com/springcloud/2017/05/22/springcloud-config-git.html)留了一个小问题，当重新修改配置文件提交后，客户端获取的仍然是修改前的信息，这个问题我们先放下，待会再讲。国内很多公司都使用的svn来做代码的版本控制，我们先介绍以下如何使用svn+Spring Cloud Config来做配置中心。

## svn版本

同样先示例server端的代码，基本步骤一样。

### 1、添加依赖

```
<dependencies>
	<dependency>
		<groupId>org.springframework.cloud</groupId>
		<artifactId>spring-cloud-config-server</artifactId>
	</dependency>
	<dependency>
		<groupId>org.tmatesoft.svnkit</groupId>
		<artifactId>svnkit</artifactId>
	</dependency>
</dependencies>
```

需要多引入svnkitr包

### 2、配置文件

```
server:
  port: 8001

spring:
  cloud:
    config:
      server:
        svn:
          uri: http://192.168.0.6/svn/repo/config-repo
          username: username
          password: password
        default-label: trunk
  profiles:
    active: subversion
  application:
    name: spring-cloud-config-server
```

和git版本稍有区别，需要显示声明subversion.

### 3、启动类

启动类没有变化，添加`@EnableConfigServer`激活对配置中心的支持

```
@EnableConfigServer
@SpringBootApplication
public class ConfigServerApplication {

	public static void main(String[] args) {
		SpringApplication.run(ConfigServerApplication.class, args);
	}
}
```

### 4、测试

**服务端测试**

访问：`http://localhost:8001/neo-config-dev.properties`，返回：`neo.hello: hello im dev`，说明服务端可以正常读取到svn代码库中的配置信息。修改配置文件`neo-config-dev.properties`中配置信息为：`neo.hello=hello im dev update`,再次在浏览器访问`http://localhost:8001/neo-config-dev.properties`，返回：`neo.hello: hello im dev update`。说明server端会自动读取最新提交的内容

**客户端测试**

客户端直接使用上一篇示例项目`spring-cloud-config-client`来测试，配置基本不用变动。启动项目后访问：`http://localhost:8002/hello，返回：`hello im dev update`说明已经正确的从server端获取到了参数。同样修改svn配置并提交，再次访问``http://localhost:8002/hello```依然获取的是旧的信息，和git版本的问题一样。

## refresh

现在来解决上一篇的遗留问题，这个问题在svn版本中依然存在。Spring Cloud Config分服务端和客户端，服务端负责将git（svn）中存储的配置文件发布成REST接口，客户端可以从服务端REST接口获取配置。但客户端并不能主动感知到配置的变化，从而主动去获取新的配置。客户端如何去主动获取新的配置信息呢，springcloud已经给我们提供了解决方案，每个客户端通过POST方法触发各自的`/refresh`。

修改`spring-cloud-config-client`项目已到达可以refresh的功能。

### 1、添加依赖

```
<dependency>
  <groupId>org.springframework.boot</groupId>
  <artifactId>spring-boot-starter-actuator</artifactId>
</dependency>
```

增加了`spring-boot-starter-actuator`包，`spring-boot-starter-actuator`是一套监控的功能，可以监控程序在运行时状态，其中就包括`/refresh`的功能。

### 2、 开启更新机制

需要给加载变量的类上面加载`@RefreshScope`，在客户端执行`/refresh`的时候就会更新此类下面的变量值。

```
@RestController
@RefreshScope // 使用该注解的类，会在接到SpringCloud配置中心配置刷新的时候，自动将新的配置更新到该类对应的字段中。
class HelloController {

    @Value("${neo.hello}")
    private String hello;

    @RequestMapping("/hello")
    public String from() {
        return this.hello;
    }
}
```

### 3、测试

*springboot 1.5.X 以上默认开通了安全认证，所以需要在配置文件`application.properties`添加以下配置*

```
management.security.enabled=false
```

OK 这样就改造完了，以post请求的方式来访问`http://localhost:8002/refresh` 就会更新修改后的配置文件。

我们再次来测试，首先访问`http://localhost:8002/hello`，返回：`hello im dev`，我将库中的值修改为`hello im dev update`。在win上面打开cmd执行`curl -X POST http://localhost:8002/refresh`，返回`["neo.hello"]`说明已经更新了`neo.hello`的值。我们再次访问`http://localhost:8002/hello`，返回：`hello im dev update`,客户端已经得到了最新的值。

每次手动刷新客户端也很麻烦，有没有什么办法只要提交代码就自动调用客户端来更新呢，github的webhook是一个好的办法。

### 4、webhook

WebHook是当某个事件发生时，通过发送http post请求的方式来通知信息接收方。Webhook来监测你在Github.com上的各种事件，最常见的莫过于push事件。如果你设置了一个监测push事件的Webhook，那么每当你的这个项目有了任何提交，这个Webhook都会被触发，这时Github就会发送一个HTTP POST请求到你配置好的地址。

如此一来，你就可以通过这种方式去自动完成一些重复性工作，比如，你可以用Webhook来自动触发一些持续集成（CI）工具的运作，比如Travis CI；又或者是通过 Webhook 去部署你的线上服务器。下图就是github上面的webhook配置。

![img](assets/webhook.jpg)

- `Payload URL` ：触发后回调的URL
- `Content type` ：数据格式，两种一般使用json
- `Secret` ：用作给POST的body加密的字符串。采用HMAC算法
- `events` ：触发的事件列表。

| events事件类型 | 描述                       |
| :------------- | :------------------------- |
| push           | 仓库有push时触发。默认事件 |
| create         | 当有分支或标签被创建时触发 |
| delete         | 当有分支或标签被删除时触发 |

> svn也有类似的hook机制，每次提交后会触发post-commit脚本，我们可以在这里写一些post请求

这样我们就可以利用hook的机制去触发客户端的更新，但是当客户端越来越多的时候hook支持的已经不够优雅，另外每次增加客户端都需要改动hook也是不现实的。其实Spring Cloud给了我们更好解决方案，后面文章来介绍。

# springcloud(八)：配置中心服务化和高可用

在前两篇的介绍中，客户端都是直接调用配置中心的server端来获取配置文件信息。这样就存在了一个问题，客户端和服务端的耦合性太高，如果server端要做集群，客户端只能通过原始的方式来路由，server端改变IP地址的时候，客户端也需要修改配置，不符合springcloud服务治理的理念。springcloud提供了这样的解决方案，我们只需要将server端当做一个服务注册到eureka中，client端去eureka中去获取配置中心server端的服务既可。

这篇文章我们基于配置中心git版本的内容来改造

## server端改造

### 1、添加依赖

```
<dependencies>
	<dependency>
		<groupId>org.springframework.cloud</groupId>
		<artifactId>spring-cloud-config-server</artifactId>
	</dependency>
	<dependency>
		<groupId>org.springframework.cloud</groupId>
		<artifactId>spring-cloud-starter-eureka</artifactId>
	</dependency>
</dependencies>
```

需要多引入`spring-cloud-starter-eureka`包，来添加对eureka的支持。

### 2、配置文件

```
server:
server:
  port: 8001
spring:
  application:
    name: spring-cloud-config-server
  cloud:
    config:
      server:
        git:
          uri: https://github.com/ityouknow/spring-cloud-starter/     # 配置git仓库的地址
          search-paths: config-repo                             # git仓库地址下的相对地址，可以配置多个，用,分割。
          username: username                                        # git仓库的账号
          password: password                                    # git仓库的密码
eureka:
  client:
    serviceUrl:
      defaultZone: http://localhost:8000/eureka/   ## 注册中心eurka地址
```

增加了eureka注册中心的配置

### 3、启动类

启动类添加`@EnableDiscoveryClient`激活对注册中心的支持

```
@EnableDiscoveryClient
@EnableConfigServer
@SpringBootApplication
public class ConfigServerApplication {

	public static void main(String[] args) {
		SpringApplication.run(ConfigServerApplication.class, args);
	}
}
```

这样server端的改造就完成了。先启动eureka注册中心，在启动server端，在浏览器中访问：`http://localhost:8000/` 就会看到server端已经注册了到注册中心了。

![img](assets/eureka-config01.jpg)

按照上篇的测试步骤对server端进行测试服务正常。

## 客户端改造

### 1、添加依赖

```
<dependencies>
	<dependency>
		<groupId>org.springframework.cloud</groupId>
		<artifactId>spring-cloud-starter-config</artifactId>
	</dependency>
	<dependency>
		<groupId>org.springframework.boot</groupId>
		<artifactId>spring-boot-starter-web</artifactId>
	</dependency>
	<dependency>
		<groupId>org.springframework.cloud</groupId>
		<artifactId>spring-cloud-starter-eureka</artifactId>
	</dependency>
	<dependency>
		<groupId>org.springframework.boot</groupId>
		<artifactId>spring-boot-starter-test</artifactId>
		<scope>test</scope>
	</dependency>
</dependencies>
```

需要多引入`spring-cloud-starter-eureka`包，来添加对eureka的支持。

### 2、配置文件

```
spring.application.name=spring-cloud-config-client
server.port=8002

spring.cloud.config.name=neo-config
spring.cloud.config.profile=dev
spring.cloud.config.label=master
spring.cloud.config.discovery.enabled=true
spring.cloud.config.discovery.serviceId=spring-cloud-config-server

eureka.client.serviceUrl.defaultZone=http://localhost:8000/eureka/
```

主要是去掉了`spring.cloud.config.uri`直接指向server端地址的配置，增加了最后的三个配置：

- `spring.cloud.config.discovery.enabled` ：开启Config服务发现支持
- `spring.cloud.config.discovery.serviceId` ：指定server端的name,也就是server端`spring.application.name`的值
- `eureka.client.serviceUrl.defaultZone` ：指向注册中心的地址

这三个配置文件都需要放到`bootstrap.properties`的配置中

### 3、启动类

启动类添加`@EnableDiscoveryClient`激活对配置中心的支持

```
@EnableDiscoveryClient
@SpringBootApplication
public class ConfigClientApplication {

	public static void main(String[] args) {
		SpringApplication.run(ConfigClientApplication.class, args);
	}
}
```

启动client端，在浏览器中访问：`http://localhost:8000/` 就会看到server端和client端都已经注册了到注册中心了。

![img](assets/eureka-config02.jpg)

## 高可用

为了模拟生产集群环境，我们改动server端的端口为8003，再启动一个server端来做服务的负载，提供高可用的server端支持。

![img](assets/eureka-config03.jpg)

如上图就可发现会有两个server端同时提供配置中心的服务，防止某一台down掉之后影响整个系统的使用。

我们先单独测试服务端，分别访问：`http://localhost:8001/neo-config/dev`、`http://localhost:8003/neo-config/dev`返回信息：

```
{
    "name": "neo-config", 
    "profiles": [
        "dev"
    ], 
    "label": null, 
    "version": null, 
    "state": null, 
    "propertySources": [
        {
            "name": "https://github.com/ityouknow/spring-cloud-starter/config-repo/neo-config-dev.properties", 
            "source": {
                "neo.hello": "hello im dev"
            }
        }
    ]
}
```

说明两个server端都正常读取到了配置信息。

再次访问：`http://localhost:8002/hello`，返回：`hello im dev update`。说明客户端已经读取到了server端的内容，我们随机停掉一台server端的服务，再次访问`http://localhost:8002/hello`，返回：`hello im dev update`，说明达到了高可用的目的。

# springcloud(九)：配置中心和消息总线（配置中心终结版）

我们在[springcloud(七)：配置中心svn示例和refresh](http://www.ityouknow.com/springcloud/2017/05/23/springcloud-config-svn-refresh.html)中讲到，如果需要客户端获取到最新的配置信息需要执行`refresh`，我们可以利用webhook的机制每次提交代码发送请求来刷新客户端，当客户端越来越多的时候，需要每个客户端都执行一遍，这种方案就不太适合了。使用Spring Cloud Bus可以完美解决这一问题。

## Spring Cloud Bus

Spring cloud bus通过轻量消息代理连接各个分布的节点。这会用在广播状态的变化（例如配置变化）或者其他的消息指令。Spring bus的一个核心思想是通过分布式的启动器对spring boot应用进行扩展，也可以用来建立一个多个应用之间的通信频道。目前唯一实现的方式是用AMQP消息代理作为通道，同样特性的设置（有些取决于通道的设置）在更多通道的文档中。

Spring cloud bus被国内很多都翻译为消息总线，也挺形象的。大家可以将它理解为管理和传播所有分布式项目中的消息既可，其实本质是利用了MQ的广播机制在分布式的系统中传播消息，目前常用的有Kafka和RabbitMQ。利用bus的机制可以做很多的事情，其中配置中心客户端刷新就是典型的应用场景之一，我们用一张图来描述bus在配置中心使用的机制。

![img](assets/configbus1.jpg)

根据此图我们可以看出利用Spring Cloud Bus做配置更新的步骤:

- 1、提交代码触发post给客户端A发送bus/refresh
- 2、客户端A接收到请求从Server端更新配置并且发送给Spring Cloud Bus
- 3、Spring Cloud bus接到消息并通知给其它客户端
- 4、其它客户端接收到通知，请求Server端获取最新配置
- 5、全部客户端均获取到最新的配置

## 项目示例

我们选择上一篇文章[springcloud(八)：配置中心服务化和高可用](http://www.ityouknow.com/springcloud/2017/05/25/springcloud-config-eureka.html)版本的[示例代码](https://github.com/ityouknow/spring-cloud-starter/tree/master/spring-cloud-config-eureka)来改造,MQ我们使用RabbitMQ来做示例。

**客户端spring-cloud-config-client改造**

### 1、添加依赖

```
<dependency>
    <groupId>org.springframework.cloud</groupId>
    <artifactId>spring-cloud-starter-bus-amqp</artifactId>
</dependency>
```

需要多引入`spring-cloud-starter-bus-amqp`包，增加对消息总线的支持

### 2、配置文件

```
## 刷新时，关闭安全验证
management.security.enabled=false
## 开启消息跟踪
spring.cloud.bus.trace.enabled=true

spring.rabbitmq.host=192.168.9.89
spring.rabbitmq.port=5672
spring.rabbitmq.username=admin
spring.rabbitmq.password=123456
```

配置文件需要增加RebbitMq的相关配置，这样客户端代码就改造完成了。

### 3、测试

依次启动spring-cloud-eureka、spring-cloud-config-server、spring-cloud-config-client项目，在启动spring-cloud-config-client项目的时候我们会发现启动日志会输出这样的一条记录。

```
2017-05-26 17:05:38.568  INFO 21924 --- [           main] o.s.b.a.e.mvc.EndpointHandlerMapping     : Mapped "{[/bus/refresh],methods=[POST]}" onto public void org.springframework.cloud.bus.endpoint.RefreshBusEndpoint.refresh(java.lang.String)
```

说明客户端已经具备了消息总线通知的能力了，为了更好的模拟消息总线的效果，我们更改客户端spring-cloud-config-client项目的端口为8003、8004依次启动，这样测试环境就准备好了。启动后eureka后台效果图如下：

![img](assets/configbus3.jpg)

我们先分别测试一下服务端和客户端是否正确运行，访问：`http://localhost:8001/neo-config/dev`，返回信息：

```
{
    "name": "neo-config", 
    "profiles": [
        "dev"
    ], 
    "label": null, 
    "version": null, 
    "state": null, 
    "propertySources": [
        {
            "name": "https://github.com/ityouknow/spring-cloud-starter/config-repo/neo-config-dev.properties", 
            "source": {
                "neo.hello": "hello im dev"
            }
        }
    ]
}
```

说明server端都正常读取到了配置信息。

依次访问：`http://localhost:8002/hello`、`http://localhost:8003/hello`、`http://localhost:8004/hello`，返回：`hello im dev`。说明客户端都已经读取到了server端的内容。

现在我们更新`neo-config-dev.properties` 中`neo.hello`的值为`hello im dev update`并提交到代码库中，访问：`http://localhost:8002/hello` 依然返回`hello im dev`。我们对端口为8002的客户端发送一个`/bus/refresh`的post请求。在win下使用下面命令来模拟webhook.

```
curl -X POST http://localhost:8002/bus/refresh
```

执行完成后，依次访问：`http://localhost:8002/hello`、`http://localhost:8003/hello`、`http://localhost:8004/hello`，返回：`hello im dev update`。说明三个客户端均已经拿到了最新配置文件的信息，这样我们就实现了图一中的示例。

## 改进版本

在上面的流程中，我们已经到达了利用消息总线触发一个客户端`bus/refresh`,而刷新所有客户端的配置的目的。但这种方式并不优雅。原因如下：

- 打破了微服务的职责单一性。微服务本身是业务模块，它本不应该承担配置刷新的职责。
- 破坏了微服务各节点的对等性。
- 有一定的局限性。例如，微服务在迁移时，它的网络地址常常会发生变化，此时如果想要做到自动刷新，那就不得不修改WebHook的配置。

因此我们将上面的架构模式稍微改变一下

![img](assets/configbus2.jpg)

这时Spring Cloud Bus做配置更新步骤如下:

- 1、提交代码触发post请求给bus/refresh
- 2、server端接收到请求并发送给Spring Cloud Bus
- 3、Spring Cloud bus接到消息并通知给其它客户端
- 4、其它客户端接收到通知，请求Server端获取最新配置
- 5、全部客户端均获取到最新的配置

这样的话我们在server端的代码做一些改动，来支持`bus/refresh`

### 1、添加依赖

```
<dependencies>
	<dependency>
		<groupId>org.springframework.cloud</groupId>
		<artifactId>spring-cloud-config-server</artifactId>
	</dependency>
	<dependency>
		<groupId>org.springframework.cloud</groupId>
		<artifactId>spring-cloud-starter-bus-amqp</artifactId>
	</dependency>
	<dependency>
		<groupId>org.springframework.cloud</groupId>
		<artifactId>spring-cloud-starter-eureka</artifactId>
	</dependency>
</dependencies>
```

需要多引入`spring-cloud-starter-bus-amqp`包，增加对消息总线的支持

### 2、配置文件

```
server:
  port: 8001
spring:
  application:
    name: spring-cloud-config-server
  cloud:
    config:
      server:
        git:
          uri: https://github.com/ityouknow/spring-cloud-starter/     # 配置git仓库的地址
          search-paths: config-repo                             # git仓库地址下的相对地址，可以配置多个，用,分割。
          username: username                                        # git仓库的账号
          password: password                                    # git仓库的密码
  rabbitmq:
    host: 192.168.0.6
    port: 5672
    username: admin
    password: 123456

eureka:
  client:
    serviceUrl:
      defaultZone: http://localhost:8000/eureka/   ## 注册中心eurka地址


management:
  security:
     enabled: false
```

配置文件增加RebbitMq的相关配置，关闭安全验证。这样server端代码就改造完成了。

### 3、测试

依次启动spring-cloud-eureka、spring-cloud-config-server、spring-cloud-config-client项目，改动spring-cloud-config-client项目端口为8003、8004依次启动。测试环境准备完成。

按照上面的测试方式，访问server端和三个客户端测试均可以正确返回信息。同样修改`neo-config-dev.properties` 中`neo.hello`的值为`hello im dev update`并提交到代码库中。在win下使用下面命令来模拟webhook触发server端`bus/refresh`.

```
curl -X POST http://localhost:8001/bus/refresh
```

执行完成后，依次访问：`http://localhost:8002/hello`、`http://localhost:8003/hello`、`http://localhost:8004/hello`，返回：`hello im dev update`。说明三个客户端均已经拿到了最新配置文件的信息，这样我们就实现了上图中的示例。

## 其它

### 局部刷新

某些场景下（例如灰度发布），我们可能只想刷新部分微服务的配置，此时可通过`/bus/refresh`端点的destination参数来定位要刷新的应用程序。

例如：`/bus/refresh?destination=customers:8000`，这样消息总线上的微服务实例就会根据destination参数的值来判断是否需要要刷新。其中，`customers:8000`指的是各个微服务的ApplicationContext ID。

destination参数也可以用来定位特定的微服务。例如：`/bus/refresh?destination=customers:**`，这样就可以触发customers微服务所有实例的配置刷新。

### 跟踪总线事件

一些场景下，我们可能希望知道Spring Cloud Bus事件传播的细节。此时，我们可以跟踪总线事件（RemoteApplicationEvent的子类都是总线事件）。

跟踪总线事件非常简单，只需设置`spring.cloud.bus.trace.enabled=true`，这样在`/bus/refresh`端点被请求后，访问`/trace`端点就可获得类似如下的结果：

```
{
  "timestamp": 1495851419032,
  "info": {
    "signal": "spring.cloud.bus.ack",
    "type": "RefreshRemoteApplicationEvent",
    "id": "c4d374b7-58ea-4928-a312-31984def293b",
    "origin": "stores:8002",
    "destination": "*:**"
  }
  },
  {
  "timestamp": 1495851419033,
  "info": {
    "signal": "spring.cloud.bus.sent",
    "type": "RefreshRemoteApplicationEvent",
    "id": "c4d374b7-58ea-4928-a312-31984def293b",
    "origin": "spring-cloud-config-client:8001",
    "destination": "*:**"
  }
  },
  {
  "timestamp": 1495851422175,
  "info": {
    "signal": "spring.cloud.bus.ack",
    "type": "RefreshRemoteApplicationEvent",
    "id": "c4d374b7-58ea-4928-a312-31984def293b",
    "origin": "customers:8001",
    "destination": "*:**"
  }
}
```

这个日志显示了`customers:8001`发出了RefreshRemoteApplicationEvent事件，广播给所有的服务，被`customers:9000`和`stores:8081`接受到了。想要对接受到的消息自定义自己的处理方式的话，可以添加`@EventListener`注解的AckRemoteApplicationEvent和SentApplicationEvent类型到你自己的应用中。或者到TraceRepository类中，直接处理数据。

这样，我们就可清晰地知道事件的传播细节。

## `/bus/refresh` BUG

`/bus/refresh` 有一个很严重的BUG，一直没有解决：对客户端执行`/bus/refresh`之后，挂到总线的上的客户端都会从Eureka注册中心撤销登记；如果对server端执行`/bus/refresh`,server端也会从Eureka注册中心撤销登记。再用白话解释一下，就是本来人家在Eureka注册中心注册的好好的，只要你对着它执行一次`/bus/refresh`，立刻就会从Euraka中挂掉。

其实这个问题挺严重的，本来你利用`/bus/refresh`给所有的节点来更新配置信息呢，结果把服务从Euraka中给搞掉了，那么如果别人需要调用客户端的服务的时候就直接歇菜了。不知道国内有童鞋公司在生产中用到这个功能没有，用了不就很惨烈。在网上搜索了一下，国内网友和国外网友都遇到过很多次，但是一直没有解决，很幸运就是我在写这篇文章的**前三天**，Netflix修复了这个问题，使用Spring Cloud最新版本的包就可以解决这个问题。由此也可以发现Spring Cloud还在快速的发展中，最新的版本可能也会有一些不稳定性，可见路漫漫而修远兮。

在pom中使用Spring Cloud的版本，解决这个bug.

```
<properties>
	<project.build.sourceEncoding>UTF-8</project.build.sourceEncoding>
	<project.reporting.outputEncoding>UTF-8</project.reporting.outputEncoding>
	<java.version>1.8</java.version>
	<spring-cloud.version>Dalston.SR1</spring-cloud.version>
</properties>
```

主要是这句：`<spring-cloud.version>Dalston.SR1</spring-cloud.version>` ，详情可以参考本文示例中的代码

BUG的讨论和解决过程可以看github上面这两个issue:

- [/bus/refresh causes instances registered in Eureka Server disappeared #692](https://github.com/spring-cloud/spring-cloud-config/issues/692)
- [Making POST on ‘refresh’ permamently deregisters the service from Eureka #1857](https://github.com/spring-cloud/spring-cloud-netflix/issues/1857)

# springcloud(十)：服务网关zuul初级篇

 2017/06/01

前面的文章我们介绍了，Eureka用于服务的注册于发现，Feign支持服务的调用以及均衡负载，Hystrix处理服务的熔断防止故障扩散，Spring Cloud Config服务集群配置中心，似乎一个微服务框架已经完成了。

我们还是少考虑了一个问题，外部的应用如何来访问内部各种各样的微服务呢？在微服务架构中，后端服务往往不直接开放给调用端，而是通过一个API网关根据请求的url，路由到相应的服务。当添加API网关后，在第三方调用端和服务提供方之间就创建了一面墙，这面墙直接与调用方通信进行权限控制，后将请求均衡分发给后台服务端。

## 为什么需要API Gateway

1、简化客户端调用复杂度

在微服务架构模式下后端服务的实例数一般是动态的，对于客户端而言很难发现动态改变的服务实例的访问地址信息。因此在基于微服务的项目中为了简化前端的调用逻辑，通常会引入API Gateway作为轻量级网关，同时API Gateway中也会实现相关的认证逻辑从而简化内部服务之间相互调用的复杂度。

![img](assets/api_gateway.png)

2、数据裁剪以及聚合

通常而言不同的客户端对于显示时对于数据的需求是不一致的，比如手机端或者Web端又或者在低延迟的网络环境或者高延迟的网络环境。

因此为了优化客户端的使用体验，API Gateway可以对通用性的响应数据进行裁剪以适应不同客户端的使用需求。同时还可以将多个API调用逻辑进行聚合，从而减少客户端的请求数，优化客户端用户体验

3、多渠道支持

当然我们还可以针对不同的渠道和客户端提供不同的API Gateway,对于该模式的使用由另外一个大家熟知的方式叫Backend for front-end, 在Backend for front-end模式当中，我们可以针对不同的客户端分别创建其BFF，进一步了解BFF可以参考这篇文章：[Pattern: Backends For Frontends](http://samnewman.io/patterns/architectural/bff/)

![img](assets/bff.png)

4、遗留系统的微服务化改造

对于系统而言进行微服务改造通常是由于原有的系统存在或多或少的问题，比如技术债务，代码质量，可维护性，可扩展性等等。API Gateway的模式同样适用于这一类遗留系统的改造，通过微服务化的改造逐步实现对原有系统中的问题的修复，从而提升对于原有业务响应力的提升。通过引入抽象层，逐步使用新的实现替换旧的实现。

![img](assets/bff-process.png)

> 在Spring Cloud体系中， Spring Cloud Zuul就是提供负载均衡、反向代理、权限认证的一个API gateway。

## Spring Cloud Zuul

Spring Cloud Zuul路由是微服务架构的不可或缺的一部分，提供动态路由，监控，弹性，安全等的边缘服务。Zuul是Netflix出品的一个基于JVM路由和服务端的负载均衡器。

下面我们通过代码来了解Zuul是如何工作的

### 简单使用

1、添加依赖

```
<dependency>
	<groupId>org.springframework.cloud</groupId>
	<artifactId>spring-cloud-starter-zuul</artifactId>
</dependency>
```

引入`spring-cloud-starter-zuul`包

2、配置文件

```
spring.application.name=gateway-service-zuul
server.port=8888

#这里的配置表示，访问/it/** 直接重定向到http://www.ityouknow.com/**
zuul.routes.baidu.path=/it/**
zuul.routes.baidu.url=http://www.ityouknow.com/
```

3、启动类

```
@SpringBootApplication
@EnableZuulProxy
public class GatewayServiceZuulApplication {

	public static void main(String[] args) {
		SpringApplication.run(GatewayServiceZuulApplication.class, args);
	}
}
```

启动类添加`@EnableZuulProxy`，支持网关路由。

史上最简单的zuul案例就配置完了

4、测试

启动`gateway-service-zuul-simple`项目，在浏览器中访问：`http://localhost:8888/it/spring-cloud`，看到页面返回了：`http://www.ityouknow.com/spring-cloud` 页面的信息，如下：

![img](assets/zuul-01.jpg)

我们以前面文章的示例代码`spring-cloud-producer`为例来测试请求的重定向，在配置文件中添加：

```
zuul.routes.hello.path=/hello/**
zuul.routes.hello.url=http://localhost:9000/
```

启动`spring-cloud-producer`，重新启动`gateway-service-zuul-simple`，访问：`http://localhost:8888/hello/hello?name=%E5%B0%8F%E6%98%8E`，返回：`hello 小明，this is first messge`

说明访问`gateway-service-zuul-simple`的请求自动转发到了`spring-cloud-producer`，并且将结果返回。

### 服务化

通过url映射的方式来实现zull的转发有局限性，比如每增加一个服务就需要配置一条内容，另外后端的服务如果是动态来提供，就不能采用这种方案来配置了。实际上在实现微服务架构时，服务名与服务实例地址的关系在eureka server中已经存在了，所以只需要将Zuul注册到eureka server上去发现其他服务，就可以实现对serviceId的映射。

我们结合示例来说明，在上面示例项目`gateway-service-zuul-simple`的基础上来改造。

1、添加依赖

```
<dependency>
    <groupId>org.springframework.cloud</groupId>
    <artifactId>spring-cloud-starter-eureka</artifactId>
</dependency>
```

增加`spring-cloud-starter-eureka`包，添加对eureka的支持。

2、配置文件

配置修改为：

```
spring.application.name=gateway-service-zuul
server.port=8888

zuul.routes.api-a.path=/producer/**
zuul.routes.api-a.serviceId=spring-cloud-producer

eureka.client.serviceUrl.defaultZone=http://localhost:8000/eureka/
```

3、测试

依次启动 `spring-cloud-eureka`、 `spring-cloud-producer`、`gateway-service-zuul-eureka`，访问：`http://localhost:8888/producer/hello?name=%E5%B0%8F%E6%98%8E`，返回：`hello 小明，this is first messge`

说明访问`gateway-service-zuul-eureka`的请求自动转发到了`spring-cloud-producer`，并且将结果返回。

为了更好的模拟服务集群，我们复制`spring-cloud-producer`项目改为`spring-cloud-producer-2`，修改`spring-cloud-producer-2`项目端口为9001，controller代码修改如下：

```
@RestController
public class HelloController {
	
    @RequestMapping("/hello")
    public String index(@RequestParam String name) {
        return "hello "+name+"，this is two messge";
    }
}
```

修改完成后启动`spring-cloud-producer-2`，重启`gateway-service-zuul-eureka`。测试多次访问`http://localhost:8888/producer/hello?name=%E5%B0%8F%E6%98%8E`，依次返回：

```
hello 小明，this is first messge
hello 小明，this is two messge
hello 小明，this is first messge
hello 小明，this is two messge
...
```

说明通过zuul成功调用了producer服务并且做了均衡负载。

**网关的默认路由规则**

但是如果后端服务多达十几个的时候，每一个都这样配置也挺麻烦的，spring cloud zuul已经帮我们做了默认配置。默认情况下，Zuul会代理所有注册到Eureka Server的微服务，并且Zuul的路由规则如下：`http://ZUUL_HOST:ZUUL_PORT/微服务在Eureka上的serviceId/**`会被转发到serviceId对应的微服务。

我们注销掉`gateway-service-zuul-eureka`项目中关于路由的配置：

```
#zuul.routes.api-a.path=/producer/**
#zuul.routes.api-a.serviceId=spring-cloud-producer
```

重新启动后，访问`http://localhost:8888/spring-cloud-producer/hello?name=%E5%B0%8F%E6%98%8E`，测试返回结果和上述示例相同，说明Spring cloud zuul默认已经提供了转发功能。到此zuul的基本使用我们就介绍完了。关于zuul更高级使用，我们下篇再来介绍。

# Spring Cloud在国内中小型公司能用起来吗？

 2017/09/11

今天吃完饭休息的时候瞎逛知乎，突然看到这个一个问题[Spring Cloud在国内中小型公司能用起来吗？](https://www.zhihu.com/question/61403505)，吸引了我的注意。仔细的看了题主的问题，发现这是一个好问题，题主经过了一番思考，并且用图形全面的将自己的疑问表达了出来，作为一个研究并使用Spring Boot和Spring Cloud近两年的程序员，看的我手痒痒不答不快呀。

## 好问题

好问题必须配认真的回答，仔细的看了题主的问题，发现这个问题非常具有代表性，可能是广大网友想使用Spring Cloud却又对Spring Cloud不太了解的共同想法，题主对Spring Cloud使用的方方面面都进行过了思考，包括市场，学习、前后端、测试、配置、部署、开发以及运维，下面就是题主原本的问题：

**想在公司推广Spring Cloud，但我对这项技术还缺乏了解,画了一张脑图，总结了种种问题。**

![img](assets/springcloud-question.png)

**微服务是这样一个结构吗?**

```
前端或二方 - > ng集群 -> zuul集群 -> eureka-server集群 -> service provider集群
```

> （二方指其他业务部门）

想要明白这个问题，首先需要知道什么是Spring Boot，什么是Spring Cloud，以及两者之间有什么关系？

## 什么是Spring Boot

Spring Boot简化了基于Spring的应用开发，通过少量的代码就能创建一个独立的、产品级别的Spring应用。 Spring Boot为Spring平台及第三方库提供开箱即用的设置，这样你就可以有条不紊地开始。多数Spring Boot应用只需要很少的Spring配置。

Spring Boot是由Pivotal团队提供的全新框架，其设计目的是用来简化新Spring应用的初始搭建以及开发过程。该框架使用了特定的方式来进行配置，从而使开发人员不再需要定义样板化的配置。用我的话来理解，就是Spring Boot其实不是什么新的框架，它默认配置了很多框架的使用方式，就像maven整合了所有的jar包，Spring Boot整合了所有的框架（不知道这样比喻是否合适）。

Spring Boot的核心思想就是约定大于配置，一切自动完成。采用Spring Boot可以大大的简化你的开发模式，所有你想集成的常用框架，它都有对应的组件支持。如果你对Spring Boot完全不了解，可以参考我的这篇文章：[Springboot(一)：入门篇](http://www.ityouknow.com/springboot/2016/01/06/springboot(一)-入门篇.html)

## 什么是Spring Cloud

Spring Cloud是一系列框架的有序集合。它利用Spring Boot的开发便利性巧妙地简化了分布式系统基础设施的开发，如服务发现注册、配置中心、消息总线、负载均衡、断路器、数据监控等，都可以用Spring Boot的开发风格做到一键启动和部署。Spring并没有重复制造轮子，它只是将目前各家公司开发的比较成熟、经得起实际考验的服务框架组合起来，通过Spring Boot风格进行再封装屏蔽掉了复杂的配置和实现原理，最终给开发者留出了一套简单易懂、易部署和易维护的分布式系统开发工具包。

微服务是可以独立部署、水平扩展、独立访问（或者有独立的数据库）的服务单元，Spring Cloud就是这些微服务的大管家，采用了微服务这种架构之后，项目的数量会非常多，Spring Cloud做为大管家就需要提供各种方案来维护整个生态。

Spring Cloud就是一套分布式服务治理的框架，既然它是一套服务治理的框架，那么它本身不会提供具体功能性的操作，更专注于服务之间的通讯、熔断、监控等。因此就需要很多的组件来支持一套功能，如果你对Spring Cloud组件不是特别了解的话，可以参考我的这篇文章：[springcloud(一)：大话Spring Cloud](http://www.ityouknow.com/springcloud/2017/05/01/simple-springcloud.html)

## Spring Boot和Spring Cloud的关系

Spring Boot 是 Spring 的一套快速配置脚手架，可以基于Spring Boot 快速开发单个微服务，Spring Cloud是一个基于Spring Boot实现的云应用开发工具；Spring Boot专注于快速、方便集成的单个微服务个体，Spring Cloud关注全局的服务治理框架；Spring Boot使用了默认大于配置的理念，很多集成方案已经帮你选择好了，能不配置就不配置，Spring Cloud很大的一部分是基于Spring Boot来实现，可以不基于Spring Boot吗？不可以。

Spring Boot可以离开Spring Cloud独立使用开发项目，但是Spring Cloud离不开Spring Boot，属于依赖的关系。

> Spring -> Spring Boot > Spring Cloud 这样的关系。

## 回答

> 以下为我在知乎的回答。

首先楼主问的这些问题都挺好的，算是经过了自己的一番思考，我恰好经历了你所说的中小公司，且都使用Spring Cloud并且已经投产上线。第一家公司技术开发人员15人左右，项目实例 30多，第二家公司开发人员100人左右，项目实例达160多。

实话说Spring Boot、Spring Cloud仍在高速发展，技术生态不断的完善和扩张，不免也会有一些小的bug，但对于中小公司的使用来将，完全可以忽略，基本都可以找到解决方案，接下来回到你的问题。

1、市场

据我所知有很多知名互联网公司都已经使用了Spring Cloud，比如阿里、美团但都是小规模，没有像我经历的这俩家公司，业务线全部拥抱Spring Cloud；另外Spring Cloud并不是一套高深的技术，普通的Java程序员经过一到俩个月完全就可以上手，但前期需要一个比较精通人的来带队。

> 后记，找阿里的小马哥确认了下，阿里也在大规模使用。

2、学习

有很多种方式，现在Spring Cloud越来越火的情况下，各种资源也越来越丰富，查看官方文档和示例，现在很多优秀的博客在写Spring cloud的相关教程，我这里收集了一些Spring Boot和Spring Cloud的相关资源可以参考，找到博客也就找到人和组织了。

- [Spring Boot学习资料汇总](http://www.ityouknow.com/springboot/2015/12/30/springboot-collect.html)：
- [Spring Cloud学习资料汇总](http://www.ityouknow.com/springcloud/2016/12/30/springcloud-collect.html) ：

3、前后职责划分

其实这个问题是每个系统架构都应该考虑的问题，Spring Cloud只是后端服务治理的一套框架，唯一和前端有关系的是thymeleaf，Spring推荐使用它做模板引擎。一般情况下，前端app或者网页通过zuul来调用后端的服务，如果包含静态资源也可以使用nginx做一下代理转发。

4、测试

Spring-boot-starter-test支持项目中各层方法的测试，也支持controller层的各种属性。所以一般测试的步奏是这样，首先开发人员覆盖自己的所有方法，然后测试微服务内所有对外接口保证微服务内的正确性，再进行微服务之间集成测试，最后交付测试。

5、配置

session共享有很多种方式，比如使用tomcat sesion共享机制，但我比较推荐使用redis缓存来做session共享。完全可以分批引入，我在上一家公司就是分批过渡上线，新旧项目通过zuul进行交互，分批引入的时候，最好是新业务线先使用Spring Cloud，老业务做过渡，当完全掌握之后在全部替换。如果只是请求转发，zuul的性能不一定比nginx低，但是如果涉及到静态资源，还是建议在前端使用nginx做一下代理。另外Spring Cloud有配置中心，可以非常灵活的做所有配置的事情。

6、部署

多环境不同配置，Spring Boot最擅长做这个事情了，使用不同的配置文件来配置不同环境的参数，在服务启动的时候指明某个配置文件即可，例如：`java -jar app.jar --spring.profiles.active=dev`就是启动测试环境的配置文件；Spring Cloud 没有提供发布平台，因为jenkins已经足够完善了，推荐使用jenkins来部署Spring Boot项目，会省非常多的事情；灰度暂时不支持，可能需要自己来做，如果有多个实例，可以一个一个来更新；支持混合部署，一台机子部署多个是常见的事情。

7、开发

你说的包含html接口就是前端页面吧，Spring Boot可以支持，但其实也是Spring Mvc在做这个事情，Spring Cloud只做服务治理，其它具体的功能都是集成了各种框架来解决而已；excel报表可以，其实除过swing项目外，其它Java项目都可以想象；Spring Cloud和老项目可以混合使用，通过zuul来支持。是否支持callback，可以通过MQ来实现，还是强调Spring Cloud只是服务治理。

8、运维

Turbine、zipkin可以用来做熔断和性能监控；动态上下线某个节点可以通过jenkins来实现；provider下线后，会有其它相同的实例来提供服务，Eureka会间隔一段时间来检测服务的可用性；不同节点配置不同的流量权值目前还不支持。注册中心必须做高可用集群，注册中心挂掉之后，服务实例会全部停止。

总结，中小企业是否能用的起来Spring Cloud，完全取决于自己公司的环境，如果是一个技术活跃型的团队就大胆的去尝试吧，目前Spring Cloud是所有微服务治理中最优秀的方案，也是一个趋势，未来一两年可能就会像Spring一样流行，早接触早学习岂不更好。

希望能解答了你的疑问。

## Spring Cloud 架构

我们从整体来看一下Spring Cloud主要的组件，以及它的访问流程

![img](assets/spring-cloud-architecture.png)

- 1、外部或者内部的非Spring Cloud项目都统一通过API网关（Zuul）来访问内部服务.
- 2、网关接收到请求后，从注册中心（Eureka）获取可用服务
- 3、由Ribbon进行均衡负载后，分发到后端的具体实例
- 4、微服务之间通过Feign进行通信处理业务
- 5、Hystrix负责处理服务超时熔断
- 6、Turbine监控服务间的调用和熔断相关指标

图中没有画出配置中心，配置中心管理各微服务不同环境下的配置文件。

以上就是一个完整的Spring Cloud生态图。

最后送一个完整示例的Spring Cloud开源项目等你去[spring-cloud-examples](https://github.com/ityouknow/spring-cloud-examples)

# 中小型互联网公司微服务实践-经验和教训

 2017/10/19

上次写了一篇文章叫[Spring Cloud在国内中小型公司能用起来吗?](https://mp.weixin.qq.com/s/vnWXpH5pv-FAzLZfbgTGvg)介绍了Spring Cloud是否能在中小公司使用起来，这篇文章是它的姊妹篇。其实我们在这条路上已经走了一年多，从16年初到现在。在使用Spring Cloud之前我们对微服务实践是没有太多的体会和经验的。从最初的开源软件[云收藏](https://github.com/cloudfavorites/favorites-web)来熟悉Spring Boot，到项目中的慢慢使用，再到最后全面拥抱Spring Cloud。这篇文章就给大家介绍一下我们使用Spring Boot/Cloud一年多的经验。

在开始之前我们先介绍一下几个概念，什么是微服务，它的特点是什么? Spring Boot/Cloud都做了那些事情？他们三者之间又有什么联系？

## 技术背景

### 什么是微服务

微服务的概念源于2014年3月Martin Fowler所写的一篇文章“[Microservices](http://martinfowler.com/articles/microservices.html)”。

微服务架构是一种架构模式，它提倡将单一应用程序划分成一组小的服务，服务之间互相协调、互相配合，为用户提供最终价值。每个服务运行在其独立的进程中，服务与服务间采用轻量级的通信机制互相沟通（通常是基于HTTP的RESTful API）。每个服务都围绕着具体业务进行构建，并且能够被独立地部署到生产环境、类生产环境等。另外，应尽量避免统一的、集中式的服务管理机制，对具体的一个服务而言，应根据业务上下文，选择合适的语言、工具对其进行构建。

微服务是一种架构风格，一个大型复杂软件应用由一个或多个微服务组成。系统中的各个微服务可被独立部署，各个微服务之间是松耦合的。每个微服务仅关注于完成一件任务并很好地完成该任务。在所有情况下，每个任务代表着一个小的业务能力。

### 微服务架构优势

**复杂度可控**：在将应用分解的同时，规避了原本复杂度无止境的积累。每一个微服务专注于单一功能，并通过定义良好的接口清晰表述服务边界。由于体积小、复杂度低，每个微服务可由一个小规模开发团队完全掌控，易于保持高可维护性和开发效率。

**独立部署**：由于微服务具备独立的运行进程，所以每个微服务也可以独立部署。当某个微服务发生变更时无需编译、部署整个应用。由微服务组成的应用相当于具备一系列可并行的发布流程，使得发布更加高效，同时降低对生产环境所造成的风险，最终缩短应用交付周期。

**技术选型灵活**：微服务架构下，技术选型是去中心化的。每个团队可以根据自身服务的需求和行业发展的现状，自由选择最适合的技术栈。由于每个微服务相对简单，故需要对技术栈进行升级时所面临的风险就较低，甚至完全重构一个微服务也是可行的。

**容错**：当某一组件发生故障时，在单一进程的传统架构下，故障很有可能在进程内扩散，形成应用全局性的不可用。在微服务架构下，故障会被隔离在单个服务中。若设计良好，其他服务可通过重试、平稳退化等机制实现应用层面的容错。

**扩展**：单块架构应用也可以实现横向扩展，就是将整个应用完整的复制到不同的节点。当应用的不同组件在扩展需求上存在差异时，微服务架构便体现出其灵活性，因为每个服务可以根据实际需求独立进行扩展。

### 什么是Spring Boot

Spring Boot是由Pivotal团队提供的全新框架，其设计目的是用来简化新Spring应用的初始搭建以及开发过程。该框架使用了特定的方式来进行配置，从而使开发人员不再需要定义样板化的配置。用我的话来理解，就是Spring Boot其实不是什么新的框架，它默认配置了很多框架的使用方式，就像maven整合了所有的jar包，Spring Boot整合了所有的框架（不知道这样比喻是否合适）。

Spring Boot简化了基于Spring的应用开发，通过少量的代码就能创建一个独立的、产品级别的Spring应用。 Spring Boot为Spring平台及第三方库提供开箱即用的设置，这样你就可以有条不紊地开始。Spring Boot的核心思想就是约定大于配置，多数Spring Boot应用只需要很少的Spring配置。采用Spring Boot可以大大的简化你的开发模式，所有你想集成的常用框架，它都有对应的组件支持。

### Spring Cloud都做了哪些事

Spring Cloud是一系列框架的有序集合。它利用Spring Boot的开发便利性巧妙地简化了分布式系统基础设施的开发，如服务发现注册、配置中心、消息总线、负载均衡、断路器、数据监控等，都可以用Spring Boot的开发风格做到一键启动和部署。Spring并没有重复制造轮子，它只是将目前各家公司开发的比较成熟、经得起实际考验的服务框架组合起来，通过Spring Boot风格进行再封装屏蔽掉了复杂的配置和实现原理，最终给开发者留出了一套简单易懂、易部署和易维护的分布式系统开发工具包

以下为Spring Cloud的核心功能：

- 分布式/版本化配置
- 服务注册和发现
- 路由
- 服务和服务之间的调用
- 负载均衡
- 断路器
- 分布式消息传递

我们再来看一张图：

![img](assets/spring-cloud-architecture-1668656704405-61.png)

通过这张图，我们来了解一下各组件配置使用运行流程：

- 1、请求统一通过API网关（Zuul）来访问内部服务.
- 2、网关接收到请求后，从注册中心（Eureka）获取可用服务
- 3、由Ribbon进行均衡负载后，分发到后端具体实例
- 4、微服务之间通过Feign进行通信处理业务
- 5、Hystrix负责处理服务超时熔断
- 6、Turbine监控服务间的调用和熔断相关指标

### Spring Cloud体系介绍

上图只是Spring Cloud体系的一部分，Spring Cloud共集成了19个子项目，里面都包含一个或者多个第三方的组件或者框架！

Spring Cloud 工具框架

1、Spring Cloud Config 配置中心，利用git集中管理程序的配置。
2、Spring Cloud Netflix 集成众多Netflix的开源软件
3、Spring Cloud Bus 消息总线，利用分布式消息将服务和服务实例连接在一起，用于在一个集群中传播状态的变化
4、Spring Cloud for Cloud Foundry 利用Pivotal Cloudfoundry集成你的应用程序
5、Spring Cloud Cloud Foundry Service Broker 为建立管理云托管服务的服务代理提供了一个起点。
6、Spring Cloud Cluster 基于Zookeeper, Redis, Hazelcast, Consul实现的领导选举和平民状态模式的抽象和实现。
7、Spring Cloud Consul 基于Hashicorp Consul实现的服务发现和配置管理。
8、Spring Cloud Security 在Zuul代理中为OAuth2 rest客户端和认证头转发提供负载均衡
9、Spring Cloud Sleuth SpringCloud应用的分布式追踪系统，和Zipkin，HTrace，ELK兼容。
10、Spring Cloud Data Flow 一个云本地程序和操作模型，组成数据微服务在一个结构化的平台上。
11、Spring Cloud Stream 基于Redis,Rabbit,Kafka实现的消息微服务，简单声明模型用以在Spring Cloud应用中收发消息。
12、Spring Cloud Stream App Starters 基于Spring Boot为外部系统提供spring的集成
13、Spring Cloud Task 短生命周期的微服务，为SpringBooot应用简单声明添加功能和非功能特性。
14、Spring Cloud Task App Starters
15、Spring Cloud Zookeeper 服务发现和配置管理基于Apache Zookeeper。
16、Spring Cloud for Amazon Web Services 快速和亚马逊网络服务集成。
17、Spring Cloud Connectors 便于PaaS应用在各种平台上连接到后端像数据库和消息经纪服务。
18、Spring Cloud Starters （项目已经终止并且在Angel.SR2后的版本和其他项目合并）
19、Spring Cloud CLI 插件用Groovy快速的创建Spring Cloud组件应用。

> 当然这个数量还在一直增加…

### 三者之间的关系

微服务是一种架构的理念，提出了微服务的设计原则，从理论为具体的技术落地提供了指导思想。Spring Boot是一套快速配置脚手架，可以基于Spring Boot快速开发单个微服务；Spring Cloud是一个基于Spring Boot实现的服务治理工具包；Spring Boot专注于快速、方便集成的单个微服务个体，Spring Cloud关注全局的服务治理框架。

**Spring Boot/Cloud是微服务实践的最佳落地方案。**

## 实战经历

### 遇到问题，寻找方案

2015年初的时候，因为公司业务的大量发展，我们开始对原有的业务进行拆分，新上的业务线也全部使用独立的项目来开发，项目和项目之间通过http接口进行访问。15年的业务发展非常迅速，项目数量也就相应急剧扩大，到了15底的时候项目达60多个，当项目数达到30几个的时候，其实我们就遇到了问题，经常某个项目因为扩展增加了新的IP地址，我们就需要被动的更新好几个相关的项目。服务越来越多，服务之间的调用关系也越来越复杂，有时候想画一张图来表示项目和项目之间的依赖关系，线条密密麻麻无法看清。网上有一张图可以表达我们的心情。

![img](assets/calling_relation.png)

这个时候我们就想找一种方案，可以将我们这么多分布式的服务给管理起来，到网上进行了技术调研。我们发现有两款开源软件比较适合我们，一个是Dubbo，一个是Spring Cloud。

其实刚开始我们是走了一些弯路的。这两款框架我们当时都不熟悉，当时国内使用Spring Cloud进行开发的企业非常的少，我在网上也几乎没找到太多应用的案例。但是Dubbo当时在国内的使用还是挺普遍的，相关的资料各方面都比较完善。因此在公司扩展新业务线众筹平台的时候，技术选型就先定了Dubbo，因为也是全新的业务没有什么负担，这个项目我们大概开发了六个月投产，上线之初也遇到了一些问题，但最终还比较顺利。

在新业务线选型使用Dubbo的同时，我们也没有完全放弃Spring Cloud，我们抽出了一两名开发人员学习Spring Boot我也参与其中，为了验证Spring Boot是否可以到达实战的标准，我们在业余的时间使用Spring Boot开发了一款开源软件[云收藏](http://favorites.ren/)，经过这个项目的实战验证我们对Spring Boot就有了信心。最重要的是大家体会到使用Spring Boot的各种便利之后，就再也不想使用传统的方式来进行开发了。

但是还有一个问题，在选择了Spring Boot进行新业务开发的同时，并没有解决我们上面的那个问题，服务于服务直接调用仍然比较复杂和传统，这时候我们就开始研究Spring Cloud。因为大家在前期对Spring Boot有了足够的了解，因此学习Sprig Cloud就显得顺风顺水了。所以在使用Dubbo半年之后，我们又全面开始拥抱Spring Cloud。

### 为什么选择使用Spring Cloud而放弃了Dubbo

可能大家会问，为什么选择了使用Dubbo之后，而又选择全面使用Spring Cloud呢？其中有几个原因：

1）从两个公司的背景来谈：Dubbo，是阿里巴巴服务化治理的核心框架，并被广泛应用于中国各互联网公司；Spring Cloud是大名鼎鼎的Spring家族的产品。阿里巴巴是一个商业公司，虽然也开源了很多的顶级的项目，但从整体战略上来讲，仍然是服务于自身的业务为主。Spring专注于企业级开源框架的研发，不论是在中国还是在世界上使用都非常广泛，开发出通用、开源、稳健的开源框架就是他们的主业。

2）从社区活跃度这个角度来对比，Dubbo虽然也是一个非常优秀的服务治理框架，并且在服务治理、灰度发布、流量分发这方面做的比Spring Cloud还好，除过当当网在基础上增加了rest支持外，已有两年多的时间几乎都没有任何更新了。在使用过程中出现问题，提交到github的Issue也少有回复。

相反Spring Cloud自从发展到现在，仍然在不断的高速发展，从github上提交代码的频度和发布版本的时间间隔就可以看出，现在Spring Cloud即将发布2.0版本，到了后期会更加完善和稳定。

\3) 从整个大的平台架构来讲，dubbo框架只是专注于服务之间的治理，如果我们需要使用配置中心、分布式跟踪这些内容都需要自己去集成，这样无形中使用dubbo的难度就会增加。Spring Cloud几乎考虑了服务治理的方方面面，更有Spring Boot这个大将的支持，开发起来非常的便利和简单。

4）从技术发展的角度来讲，Dubbo刚出来的那会技术理念还是非常先进，解决了各大互联网公司服务治理的问题，中国的各中小公司也从中受益不少。经过了这么多年的发展，互联网行业也是涌现了更多先进的技术和理念，Dubbo一直停滞不前，自然有些掉队，有时候我个人也会感到有点可惜，如果Dubbo一直沿着当初的那个路线发展，并且延伸到周边，今天可能又是另一番景象了。

Spring 推出Spring Boot/Cloud也是因为自身的很多原因。Spring最初推崇的轻量级框架，随着不断的发展也越来越庞大，随着集成项目越来越多，配置文件也越来越混乱，慢慢的背离最初的理念。随着这么多年的发展，微服务、分布式链路跟踪等更多新的技术理念的出现，Spring急需一款框架来改善以前的开发模式，因此才会出现Spring Boot/Cloud项目，我们现在访问Spring官网，会发现Spring Boot和Spring Cloud已经放到首页最重点突出的三个项目中的前两个，可见Spring对这两个框架的重视程度。

**总结一下，dubbo曾经确实很牛逼，但是Spring Cloud是站在近些年技术发展之上进行开发，因此更具技术代表性。**

### 如何进行微服务架构演进

当我们将所有的新业务都使用Spring Cloud这套架构之后，就会出现这样一个现象，公司的系统被分成了两部分，一部分是传统架构的项目，一部分是微服务架构的项目，如何让这两套配合起来使用就成为了关键，这时候Spring Cloud里面的一个关键组件解决了我们的问题，就是Zuul。在Spring Cloud架构体系内的所有微服务都通过Zuul来对外提供统一的访问入口，所有需要和微服务架构内部服务进行通讯的请求都走统一网关。如下图：

![img](assets/framework4.jpg)

从上图可以看出我们对服务进行了分类，有四种：基础服务、业务服务、组合服务、前置服务。不同服务迁移的优先级不同

- **基础服务**，是一些基础组件，与具体的业务无关。比如：短信服务、邮件服务。这里的服务最容易摘出来做微服务，也是我们第一优先级分离出来的服务。
- **业务服务**，是一些垂直的业务系统，只处理单一的业务类型，比如：风控系统、积分系统、合同系统。这类服务职责比较单一，根据业务情况来选择是否迁移，比如：如果突然有需求对积分系统进行大优化，我们就趁机将积分系统进行改造，是我们的第二优先级分离出来的服务。
- **前置服务**，前置服务一般为服务的接入或者输出服务，比如网站的前端服务、app的服务接口这类，这是我们第三优先级分离出来的服务。
- **组合服务**，组合服务就是涉及到了具体的业务，比如买标过程，需要调用很多垂直的业务服务，这类的服务我们一般放到最后再进行微服务化架构来改造，因为这类服务最为复杂，除非涉及到大的业务逻辑变更，我们是不会轻易进行迁移。

在这四类服务之外，新上线的业务全部使用Sprng Boot/Cloud这套技术栈。就这样，我们从开源项目[云收藏](https://github.com/cloudfavorites/favorites-web)开始，上线几个Spring Boot项目，到现在公司绝大部分的项目都是在Spring Cloud这个架构体系中。

## 经验和教训

### 架构演化的步骤

- 在确定使用Spring Boot/Cloud这套技术栈进行微服务改造之前，先梳理平台的服务，对不同的服务进行分类，以确认演化的节奏。
- 先让团队熟悉Spring Boot技术，并且优先在基础服务上进行技术改造，推动改动后的项目投产上线
- 当团队熟悉Spring Boot之后，再推进使用Spring Cloud对原有的项目进行改造。
- 在进行微服务改造过程中，优先应用于新业务系统，前期可以只是少量的项目进行了微服务化改造，随着大家对技术的熟悉度增加，可以加快加大微服务改造的范围
- 传统项目和微服务项目共存是一个很常见的情况，除非公司业务有大的变化，不建议直接迁移核心项目。

### 服务拆分原则

服务拆分有以下几个原则和大家分享

**横向拆分**。按照不同的业务域进行拆分，例如订单、营销、风控、积分资源等。形成独立的业务领域微服务集群。

**纵向拆分**。把一个业务功能里的不同模块或者组件进行拆分。例如把公共组件拆分成独立的原子服务，下沉到底层，形成相对独立的原子服务层。这样一纵一横，就可以实现业务的服务化拆分。

要做好微服务的分层：梳理和抽取核心应用、公共应用，作为独立的服务下沉到核心和公共能力层，逐渐形成稳定的服务中心，使前端应用能更快速的响应多变的市场需求

服务拆分是越小越好吗？微服务的大与小是相对的。比如在初期，我们把交易拆分为一个微服务，但是随着业务量的增大，可能一个交易系统已经慢慢变得很大，并且并发流量也不小，为了支撑更多的交易量，我会把交易系统，拆分为订单服务、投标服务、转让服务等。因此微服务的拆分力度需与具体业务相结合，总的原则是**服务内部高内聚，服务之间低耦合。**

### 微服务vs传统开发

使用微服务有一段时间了，这种开发模式和传统的开发模式对比，有很大的不同。

- 分工不同，以前我们可能是一个一个模块，现在可能是一人一个系统。
- 架构不同，服务的拆分是一个技术含量很高的问题，拆分是否合理对以后发展影响巨大。
- 部署方式不同，如果还像以前一样部署估计累死了，自动化运维不可不上。
- 容灾不同，好的微服务可以隔离故障避免服务整体down掉，坏的微服务设计仍然可以因为一个子服务出现问题导致连锁反应。

### 给数据库带来的挑战

每个微服务都有自己独立的数据库，那么后台管理的联合查询怎么处理？这应该是大家会普遍遇到的一个问题，有三种处理方案。

1）严格按照微服务的划分来做，微服务相互独立，各微服务数据库也独立，后台需要展示数据时，调用各微服务的接口来获取对应的数据，再进行数据处理后展示出来，这是标准的用法，也是最麻烦的用法。

\2) 将业务高度相关的表放到一个库中，将业务关系不是很紧密的表严格按照微服务模式来拆分，这样既可以使用微服务，也避免了数据库分散导致后台系统统计功能难以实现，是一个折中的方案。

3）数据库严格按照微服务的要求来切分，以满足业务高并发，实时或者准实时将各微服务数据库数据同步到NoSQL数据库中，在同步的过程中进行数据清洗，用来满足后台业务系统的使用，推荐使用MongoDB、HBase等。

三种方案在不同的公司我都使用过，第一种方案适合业务较为简单的小公司；第二种方案，适合在原有系统之上，慢慢演化为微服务架构的公司；第三种适合大型高并发的互联网公司。

### 微服务的经验和建议

1、建议尽量不要使用Jsp，页面开发推荐使用Thymeleaf。Web项目建议独立部署Tomcat，不要使用内嵌的Tomcat，内嵌Tomcat部署Jsp项目会偶现龟速访问的情况。

2、服务编排是个好东西，主要的作用是减少项目中的相互依赖。比如现在有项目a调用项目b，项目b调用项目c…一直到h，是一个调用链，那么项目上线的时候需要先更新最底层的h再更新g…更新c更新b最后是更新项目a。这只是这一个调用链，在复杂的业务中有非常多的调用，如果要记住每一个调用链对开发运维人员来说就是灾难。

有这样一个好办法可以尽量的减少项目的相互依赖，就是服务编排，一个核心的业务处理项目，负责和各个微服务打交道。比如之前是a调用b，b掉用c，c调用d，现在统一在一个核心项目W中来处理，W服务使用a的时候去调用b，使用b的时候W去调用c，举个例子：在第三方支付业务中，有一个核心支付项目是服务编排，负责处理支付的业务逻辑，W项目使用商户信息的时候就去调用“商户系统”，需要校验设备的时候就去调用“终端系统”，需要风控的时候就调用“风控系统”，各个项目需要的依赖参数都由W来做主控。以后项目部署的时候，只需要最后启动服务编排项目即可。

3、不要为了追求技术而追求技术，确定进行微服务架构改造之前，需要考虑以下几方面的因素：
1）团队的技术人员是否已经具备相关技术基础。
2）公司业务是否适合进行微服务化改造，并不是所有的平台都适合进行微服务化改造，比如：传统行业有很多复杂垂直的业务系统。
3）Spring Cloud生态的技术有很多，并不是每一种技术方案都需要用上，适合自己的才是最好的。

## 总结

**Spring Cloud对于中小型互联网公司来说是一种福音**，因为这类公司往往没有实力或者没有足够的资金投入去开发自己的分布式系统基础设施，使用Spring Cloud一站式解决方案能在从容应对业务发展的同时大大减少开发成本。同时，随着近几年微服务架构和Docker容器概念的火爆，也会让Spring Cloud在未来越来越“云”化的软件开发风格中立有一席之地，尤其是在目前五花八门的分布式解决方案中提供了标准化的、全站式的技术方案，意义可能会堪比当前Servlet规范的诞生，有效推进服务端软件系统技术水平的进步。

# 从架构演进的角度聊聊Spring Cloud都做了些什么？

 2017/11/02

Spring Cloud作为一套微服务治理的框架，几乎考虑到了微服务治理的方方面面，之前也写过一些关于Spring Cloud文章，主要偏重各组件的使用，本次分享主要解答这两个问题：Spring Cloud在微服务的架构中都做了哪些事情？Spring Cloud提供的这些功能对微服务的架构提供了怎样的便利？

这也是我写Spring Cloud三部曲的最后一篇文章，前两面篇内容如下：

- [中小型互联网公司微服务实践-经验和教训](http://mp.weixin.qq.com/s/bciSlKearaVFQg1QWOSn_g)
- [Spring Cloud在国内中小型公司能用起来吗？](https://mp.weixin.qq.com/s/vnWXpH5pv-FAzLZfbgTGvg)

我们先来简单回顾一下，我们以往互联网架构的发展情况：

## 传统架构发展史

### 单体架构

单体架构在小微企业比较常见，典型代表就是一个应用、一个数据库、一个web容器就可以跑起来，比如我们开发的开源软件[云收藏](https://github.com/cloudfavorites/favorites-web)，就是标准的单体架构。

在两种情况下可能会选择单体架构：一是在企业发展的初期，为了保证快速上线，采用此种方案较为简单灵活；二是传统企业中垂直度较高，访问压力较小的业务。在这种模式下对技术要求较低，方便各层次开发人员接手，也能满足客户需求。

下面是单体架构的架构图：

![img](assets/single_structure.jpg)

在单体架构中，技术选型非常灵活，优先满足快速上线的要求，也便于快速跟进市场。

### 垂直架构

在单体架构发展一段时间后，公司的业务模式得到了认可，交易量也慢慢的大起来，这时候有些企业为了应对更大的流量，就会对原有的业务进行拆分，比如说：后台系统、前端系统、交易系统等。

在这一阶段往往会将系统分为不同的层级，每个层级有对应的职责，UI层负责和用户进行交互、业务逻辑层负责具体的业务功能、数据库层负责和上层进行数据交换和存储。

下面是垂直架构的架构图：

![img](assets/vertical__structure.jpg)

在这个阶段SSH（struts+spring+hibernate）是项目的关键技术，Struts负责web层逻辑控制、Spring负责业务层管理Bean、Hibernate负责数据库操作进行封装，持久化数据。

### 服务化架构

如果公司进一步的做大，垂直子系统会变的越来越多，系统和系统之间的调用关系呈指数上升的趋势。在这样的背景下，很多公司都会考虑服务的SOA化。SOA代表面向服务的架构，将应用程序根据不同的职责划分为不同的模块，不同的模块直接通过特定的协议和接口进行交互。这样使整个系统切分成很多单个组件服务来完成请求，当流量过大时通过水平扩展相应的组件来支撑，所有的组件通过交互来满足整体的业务需求。

SOA服务化的优点是，它可以根据需求通过网络对松散耦合的粗粒度应用组件进行分布式部署、组合和使用。服务层是SOA的基础，可以直接被应用调用，从而有效控制系统中与软件代理交互的人为依赖性。

服务化架构是一套松耦合的架构，服务的拆分原则是服务内部高内聚，服务之间低耦合。

下面是服务化架构图：

![img](assets/soa__structure.jpg)

在这个阶段可以使用WebService或者dubbo来服务治理。

我们发现从单体架构到服务化架构，应用数量都在不断的增加，慢慢的下沉的就成了基础组建，上浮的就成为业务系统。从上述也可以看出架构的本质就是不断的拆分重构：分的过程是把系统拆分为各个子系统/模块/组件，拆的时候，首先要解决每个组件的定位问题，然后才能划分彼此的边界，实现合理的拆分。合就是根据最终要求，把各个分离的组件有机整合在一起。拆分的结果使开发人员能够做到业务聚焦、技能聚焦，实现开发敏捷，合的结果是系统变得柔性，可以因需而变，实现业务敏捷。

## SOA和微服务架构

### SOA和微服务的区别

其实服务化架构已经可以解决大部分企业的需求了，那么我们为什么要研究微服务呢？先说说它们的区别；

- 微服务架构强调业务系统需要彻底的组件化和服务化，一个组件就是一个产品，可以独立对外提供服务
- 微服务不再强调传统SOA架构里面比较重的ESB企业服务总线
- 微服务强调每个微服务都有自己独立的运行空间，包括数据库资源。
- 微服务架构本身来源于互联网的思路，因此组件对外发布的服务强调了采用HTTP Rest API的方式来进行
- 微服务的切分粒度会更小

> 总结:微服务架构是 SOA 架构思想的一种扩展，更加强调服务个体的独立性、拆分粒度更小。

### 为什么考虑Spring Cloud

- Spring Cloud来源于Spring，质量、稳定性、持续性都可以得到保证
- Spring Cloud天然支持Spring Boot，更加便于业务落地。
- Spring Cloud发展非常的快，从16年开始接触的时候相关组件版本为1.x，到现在将要发布2.x系列
- Spring Cloud是Java领域最适合做微服务的框架。
- 相比于其它框架,Spring Cloud对微服务周边环境的支持力度最大。
- 对于中小企业来讲，使用门槛较低。

> Spring Cloud　是微服务架构的最佳落地方案

### 它的特性

以下为Spring Cloud的核心特性：

- 分布式/版本化配置
- 服务注册和发现
- 路由
- 服务和服务之间的调用
- 负载均衡
- 断路器
- 分布式消息传递

这些特性都是由不同的组件来完成，在架构的演进过程中扮演着重要的角色，接下来我们一起看看。

## 微服务架构

Spring Cloud解决的第一个问题就是：服务与服务之间的解耦。很多公司在业务高速发展的时候，服务组件也会相应的不断增加。服务和服务之间有着复杂的相互调用关系，经常有服务A调用服务B，服务B调用服务C和服务D …，随着服务化组件的不断增多，服务之间的调用关系成指数级别的增长，极端情况下就如下图所示：

![img](assets/calling_relation-1668656718296-71.png)

这样最容易导致的情况就是牵一发而动全身。经常出现由于某个服务更新而没有通知到其它服务，导致上线后惨案频发。这时候就应该进行服务治理，将服务之间的直接依赖转化为服务对服务中心的依赖。Spring Cloud 核心组件Eureka就是解决这类问题。

### Eureka

Eureka是Netflix开源的一款提供服务注册和发现的产品，它提供了完整的Service Registry和Service Discovery实现。也是Spring Cloud体系中最重要最核心的组件之一。

用大白话讲，Eureka就是一个服务中心，将所有的可以提供的服务都注册到它这里来管理，其它各调用者需要的时候去注册中心获取，然后再进行调用，避免了服务之间的直接调用，方便后续的水平扩展、故障转移等。如下图：

![img](assets/eureka.jpg)

当然服务中心这么重要的组件一但挂掉将会影响全部服务，因此需要搭建Eureka集群来保持高可用性，生产中建议最少两台。随着系统的流量不断增加，需要根据情况来扩展某个服务，Eureka内部已经提供均衡负载的功能，只需要增加相应的服务端实例既可。那么在系统的运行期间某个实例挂了怎么办？Eureka内容有一个心跳检测机制，如果某个实例在规定的时间内没有进行通讯则会自动被剔除掉，避免了某个实例挂掉而影响服务。

因此使用了Eureka就自动具有了注册中心、负载均衡、故障转移的功能。如果想对Eureka进一步了解可以参考这篇文章：[注册中心Eureka](http://www.ityouknow.com/springcloud/2017/05/10/springcloud-eureka.html)

### Hystrix

在微服务架构中通常会有多个服务层调用，基础服务的故障可能会导致级联故障，进而造成整个系统不可用的情况，这种现象被称为服务雪崩效应。服务雪崩效应是一种因“服务提供者”的不可用导致“服务消费者”的不可用,并将不可用逐渐放大的过程。

如下图所示：A作为服务提供者，B为A的服务消费者，C和D是B的服务消费者。A不可用引起了B的不可用，并将不可用像滚雪球一样放大到C和D时，雪崩效应就形成了。

![img](assets/hystrix-1-1668656718296-74.png)

在这种情况下就需要整个服务机构具有故障隔离的功能，避免某一个服务挂掉影响全局。在Spring Cloud 中Hystrix组件就扮演这个角色。

Hystrix会在某个服务连续调用N次不响应的情况下，立即通知调用端调用失败，避免调用端持续等待而影响了整体服务。Hystrix间隔时间会再次检查此服务，如果服务恢复将继续提供服务。

继续了解Hystrix可以参考：[熔断器Hystrix](http://www.ityouknow.com/springcloud/2017/05/10/springcloud-eureka.html)

### Hystrix Dashboard和Turbine

当熔断发生的时候需要迅速的响应来解决问题，避免故障进一步扩散，那么对熔断的监控就变得非常重要。熔断的监控现在有两款工具：Hystrix-dashboard和Turbine

Hystrix-dashboard是一款针对Hystrix进行实时监控的工具，通过Hystrix Dashboard我们可以直观地看到各Hystrix Command的请求响应时间, 请求成功率等数据。但是只使用Hystrix Dashboard的话, 你只能看到单个应用内的服务信息, 这明显不够. 我们需要一个工具能让我们汇总系统内多个服务的数据并显示到Hystrix Dashboard上, 这个工具就是Turbine. 监控的效果图如下：

![img](assets/turbine-02-1668656718296-76.jpg)

想了解具体都监控了哪些指标，以及如何监控可以参考这篇文章：[熔断监控Hystrix Dashboard和Turbine](http://www.ityouknow.com/springcloud/2017/05/18/hystrix-dashboard-turbine.html)

### 配置中心

随着微服务不断的增多，每个微服务都有自己对应的配置文件。在研发过程中有测试环境、UAT环境、生产环境，因此每个微服务又对应至少三个不同环境的配置文件。这么多的配置文件，如果需要修改某个公共服务的配置信息，如：缓存、数据库等，难免会产生混乱，这个时候就需要引入Spring Cloud另外一个组件：Spring Cloud Config。

#### Spring Cloud Config

Spring Cloud Config是一个解决分布式系统的配置管理方案。它包含了Client和Server两个部分，Server提供配置文件的存储、以接口的形式将配置文件的内容提供出去，Client通过接口获取数据、并依据此数据初始化自己的应用。

其实就是Server端将所有的配置文件服务化，需要配置文件的服务实例去Config Server获取对应的数据。将所有的配置文件统一整理，避免了配置文件碎片化。配置中心git实例参考：[配置中心git示例](http://www.ityouknow.com/springcloud/2017/05/22/springcloud-config-git.html)；

如果服务运行期间改变配置文件，服务是不会得到最新的配置信息，需要解决这个问题就需要引入Refresh。可以在服务的运行期间重新加载配置文件，具体可以参考这篇文章：[配置中心svn示例和refresh](http://www.ityouknow.com/springcloud/2017/05/23/springcloud-config-svn-refresh.html)

当所有的配置文件都存储在配置中心的时候，配置中心就成为了一个非常重要的组件。如果配置中心出现问题将会导致灾难性的后果，因此在生产中建议对配置中心做集群，来支持配置中心高可用性。具体参考：[配置中心服务化和高可用](http://www.ityouknow.com/springcloud/2017/05/25/springcloud-config-eureka.html)

#### Spring Cloud Bus

上面的Refresh方案虽然可以解决单个微服务运行期间重载配置信息的问题，但是在真正的实践生产中，可能会有N多的服务需要更新配置，如果每次依靠手动Refresh将是一个巨大的工作量，这时候Spring Cloud提出了另外一个解决方案：Spring Cloud Bus

Spring Cloud Bus通过轻量消息代理连接各个分布的节点。这会用在广播状态的变化（例如配置变化）或者其它的消息指令中。Spring Cloud Bus的一个核心思想是通过分布式的启动器对Spring Boot应用进行扩展，也可以用来建立一个或多个应用之间的通信频道。目前唯一实现的方式是用AMQP消息代理作为通道。

Spring Cloud Bus是轻量级的通讯组件，也可以用在其它类似的场景中。有了Spring Cloud Bus之后，当我们改变配置文件提交到版本库中时，会自动的触发对应实例的Refresh，具体的工作流程如下：

![img](assets/configbus2-1668656718296-78.jpg)

也可以参考这篇文章来了解：[配置中心和消息总线](http://www.ityouknow.com/springcloud/2017/05/26/springcloud-config-eureka-bus.html)

### 服务网关

在微服务架构模式下，后端服务的实例数一般是动态的，对于客户端而言很难发现动态改变的服务实例的访问地址信息。因此在基于微服务的项目中为了简化前端的调用逻辑，通常会引入API Gateway作为轻量级网关，同时API Gateway中也会实现相关的认证逻辑从而简化内部服务之间相互调用的复杂度。

![img](assets/api_gateway-1668656718296-80.png)

Spring Cloud体系中支持API Gateway落地的技术就是Zuul。Spring Cloud Zuul路由是微服务架构中不可或缺的一部分，提供动态路由，监控，弹性，安全等的边缘服务。Zuul是Netflix出品的一个基于JVM路由和服务端的负载均衡器。

它的具体作用就是服务转发，接收并转发所有内外部的客户端调用。使用Zuul可以作为资源的统一访问入口，同时也可以在网关做一些权限校验等类似的功能。

具体使用参考这篇文章：[服务网关zuul](http://www.ityouknow.com/springcloud/2017/06/01/gateway-service-zuul.html)

### 链路跟踪

随着服务的越来越多，对调用链的分析会越来越复杂，如服务之间的调用关系、某个请求对应的调用链、调用之间消费的时间等，对这些信息进行监控就成为一个问题。在实际的使用中我们需要监控服务和服务之间通讯的各项指标，这些数据将是我们改进系统架构的主要依据。因此分布式的链路跟踪就变的非常重要，Spring Cloud也给出了具体的解决方案：Spring Cloud Sleuth和Zipkin

![img](assets/dyl.png)

Spring Cloud Sleuth为服务之间调用提供链路追踪。通过Sleuth可以很清楚的了解到一个服务请求经过了哪些服务，每个服务处理花费了多长时间。从而让我们可以很方便的理清各微服务间的调用关系。

Zipkin是Twitter的一个开源项目，允许开发者收集 Twitter 各个服务上的监控数据，并提供查询接口

分布式链路跟踪需要Sleuth+Zipkin结合来实现，具体操作参考这篇文章：[分布式链路跟踪(Sleuth)](http://www.jianshu.com/p/c3d191663279)

### 总结

我们从整体上来看一下Spring Cloud各个组件如何来配套使用：

![img](assets/spring_cloud_structure.png)

从上图可以看出Spring Cloud各个组件相互配合，合作支持了一套完整的微服务架构。

- 其中Eureka负责服务的注册与发现，很好将各服务连接起来
- Hystrix 负责监控服务之间的调用情况，连续多次失败进行熔断保护。
- Hystrix dashboard,Turbine 负责监控 Hystrix的熔断情况，并给予图形化的展示
- Spring Cloud Config 提供了统一的配置中心服务
- 当配置文件发生变化的时候，Spring Cloud Bus 负责通知各服务去获取最新的配置信息
- 所有对外的请求和服务，我们都通过Zuul来进行转发，起到API网关的作用
- 最后我们使用Sleuth+Zipkin将所有的请求数据记录下来，方便我们进行后续分析

Spring Cloud从设计之初就考虑了绝大多数互联网公司架构演化所需的功能，如服务发现注册、配置中心、消息总线、负载均衡、断路器、数据监控等。这些功能都是以插拔的形式提供出来，方便我们系统架构演进的过程中，可以合理的选择需要的组件进行集成，从而在架构演进的过程中会更加平滑、顺利。

微服务架构是一种趋势，Spring Cloud提供了标准化的、全站式的技术方案，意义可能会堪比当前Servlet规范的诞生，有效推进服务端软件系统技术水平的进步。

# 阿里Dubbo疯狂更新，关Spring Cloud什么事？

 2017/11/20

最近，开源社区发生了一件大事，那个全国 Java 开发者使用最广的开源服务框架 Dubbo 低调重启维护，并且 3 个月连续发布了 4 个维护版本。

我上次在写[放弃Dubbo，选择最流行的Spring Cloud微服务架构实践与经验总结](http://mp.weixin.qq.com/s/bciSlKearaVFQg1QWOSn_g)这篇文章的时候，就有很多的网友给我留言说，Dubbo 又开始更新了。我当然是清楚的，我也一直在关注着 Dubbo 的走向，在几个月前技术圈里面就有一个消息说是 Dubbo 又开始更新了，大家议论纷纷不知真伪。我还专门跑到 GitHub 上面进行了留言询问，最后在 Dubbo 的 gitter 聊天室里面找到了确信的答案，说是正在组建团队。虽然稍稍有所期待，但也不知道阿里这次拿出了多少的诚意来做这件事，于是我昨天又到 GitHub 逛了一下，发现从 9 月开始，阿里三个月连着发布了四个版本，还是非常有诚意的，值得关注。

## Dubbo简介

Dubbo 是阿里巴巴公司一个开源的高性能服务框架，致力于提供高性能和透明化的 RPC 远程服务调用方案，以及 SOA 服务治理方案，使得应用可通过高性能 RPC 实现服务的输出、输入功能和 Spring 框架无缝集成。Dubbo 包含远程通讯、集群容错和自动发现三个核心部分。

它提供透明化的远程方法调用，实现像调用本地方法一样调用远程方法，只需简单配置，没有任何 API 侵入。同时它具备软负载均衡及容错机制，可在内网替代 F5 等硬件负载均衡器，降低成本，减少单点。它可以实现服务自动注册与发现，不再需要写死服务提供方地址，注册中心基于接口名查询服务提供者的 IP 地址，并且能够平滑添加或删除服务提供者。

2011 年末，阿里巴巴在 GitHub 上开源了基于 Java 的分布式服务治理框架 Dubbo，之后它成为了国内该类开源项目的佼佼者，许多开发者对其表示青睐。同时，先后有不少公司在实践中基于 Dubbo 进行分布式系统架构。目前在 GitHub 上，它的 fork、star 数均已破万。

**Dubbo核心功能**:

- 远程通讯，提供对多种基于长连接的 NIO 框架抽象封装，包括多种线程模型，序列化，以及“请求-响应”模式的信息交换方式。
- 集群容错，提供基于接口方法的透明远程过程调用，包括多协议支持，以及软负载均衡，失败容错，地址路由，动态配置等集群支持。
- 自动发现，基于注册中心目录服务，使服务消费方能动态的查找服务提供方，使地址透明，使服务提供方可以平滑增加或减少机器。

![img](assets/dubbo-architecture.png)

## Dubbo发展史

**发展到开源**

2008 年底在阿里内部开始规划调用，2009 年初开发 1.0 版本；2010 年 04 月在 1.0 的版本之上进行了重构，发布了 2.0 版本；2011 年 10 月阿里宣布将 Dubbo 开源，开源的第一个版本为版本 **dubbo-2.0.7**。

**开源成长**

Dubbo 开源之后，框架发展比较迅速，几乎两三个月会发布一个版本，于 2012 年 3 月 14 号发布版本 dubbo-2.1.0。随后又进入另一个快速发展期，版本发布频繁，几乎每一个月会发布好几次。直到 2013 年 3 月 17 号发布了 dubbo-2.4.10，版本陷入停滞；2014 年 10 月 30 号发布版本 dubbo-2.4.11，修复了一个小 Bug，版本又陷入漫长的停滞到现在。

**阿里之外的发展**

2014 年的 10 月 20 号，当当网 Fork 了阿里的一个 Dubbo 版本开始维护，并命名为 dubbox-2.8.0。值得注意的是，当当网扩展 Dubbo 服务框架支持 REST 风格远程调用，并且跟随着 ZooKeepe 和 Spring 升级了对应的版本。之后 Dubbox 一直在小版本维护，2015 年 3 月 31 号发布了最后一个版本 **dubbox-2.8.4**。

![img](http://favorites.ren/assets/images/2017/architecture/dubbox_rest.jpg)

## Dubbo团队这三个月都做了什么

目前 Dubbo 的主力开发以阿里巴巴中间件团队为主，同时在阿里内部也招募了一些对 Dubbo 感兴趣的同事。大家要知道，Dubbo 距离今年开始维护的上一个版本是什么时间发布的吗？是 2014 年 10 月 30 号，差了整整将近 3 年，Dubbo 所依赖的 Jdk、Spring、Zookeeper、Zkclient 等等不知道都更新了多少个版本。因此阿里恢复更新的第一步就是适配所依赖的各组件版本，让 Dubbo 所依赖的基础环境不要太落伍，另外也 Fixed 掉了一些严重的 Bug。

**dubbo-2.5.4/5版本**

2017 年 9 月，阿里发布了 dubbo-2.5.4/5 版本，更新内容如下：

**依赖升级**

| 依赖            | 当前版本       | 目标版本       | 影响点                       |
| :-------------- | :------------- | :------------- | :--------------------------- |
| spring          | 3.2.16.RELEASE | 4.3.10.RELEASE | schema配置解析；Http RPC协议 |
| zookeeper       | 3.3.3          | 3.4.9          | 常用注册中心                 |
| zkclient        | 0.1 0.10       | zookeeper      | 客户端工具                   |
| curator         | 1.1.16         | 2.12.0         | zookeeper客户端工具          |
| commons-logging | 1.1.1          | 1.2            | 日志实现集成                 |
| hessian         | 4.0.6          | 4.0.38         | hessian RPC协议              |
| jedis           | 2.1.0          | 2.9.0          | redis注册中心；缓存RPC       |
| httpclient      | 4.1.2          | 4.5.3          | hessian等用http连接池        |
| validator       | 1.0.0          | 1.1.0.Final    | java validation规范          |
| cxf             | 2.6.1          | 3.0.14         | webservice                   |
| jcache          | 0.4            | 1.0.0          | jcache规范                   |

这版在升级相关依赖版本的同时，以问题反馈频率和影响面排定优先级，优先解决了几个反馈最多、影响较大的一些缺陷，包括优雅停机、异步调用、动态配置、MonitorFilter 监控统计等问题。

**dubbo-2.5.6版本**

2017 年 10 月，阿里发布了 dubbo-2.5.6 版本，又 Fixed 掉了一大批严重的 Bug。

**发布内容**

- 泛化调用PojoUtils工具类不能正确处理枚举类型、私有字段等问题
- provider业务线程池满后，拒绝请求的异常无法通知到consumer端
- 业务返回值payload超阈值时，payload被重复发送回consumer
- slf4jLogger正确输出log调用实际所在行号
- 延迟(delay)暴露存在潜在并发问题，导致不同服务占用多个端口
- 无provider时，consumer端mock逻辑不能生效
- 一些小优化：OverrideListener监听逻辑、provider端关闭心跳请求、Main启动类停机逻辑等
- 一些小bug修复：动态配置不能删除、telnet支持泛型json调用、monitor统计错误等

**dubbo-2.5.7版本**

2017 年 11 月，也就是 12 天前，阿里发布了 dubbo-2.5.7。这次不但修复了一批主要的 Bug，还做了一处小功能的完善。

**发布内容**

- 完善注解配置方式，修复社区反馈的旧版注解bug
- 支持启动时从环境变量读取注册ip port、绑定ip port，支持社区反馈的容器化部署场景等
- 调整、开放一些不完善的xml配置项，如dump.directory等
- 解决启动阶段zk无法连接导致应用无限阻塞的问题
- 解决zk无法连接时，MonitorService初次访问会导致rpc请求阻塞问题 #672
- 内部json实现标记deprecate，转为依赖开源fastjson实现
- RMI协议支持传递attachments
- Hessian支持EnumSet类型序列化
- 社区反馈的一些小bug修复及优化

这次版本发布内容较多，因此还给出了升级建议。

**升级请注意**

- 此次升级存在以下不兼容或需要注意点，但对核心功能均无影响，且只需添加依赖或遵守配置规则即可避免。这里只是把潜在的注意点列出来，如果你没用到这些功能无需额外关注。
- AccesslogFilter、telnet、mock等部分功能依赖了老版JSON实现，如开启以上功能，升级后请添加fastjson作为第三方依赖。
- 此次升级完善了注解配置方式，同时保留了老的注解配置代码，如工程从之前的老版本注解配置转到2.5.7版本，请确保删除老的注解扫描配置，使用新的配置形式。
- 在工程启动阶段，如遇到zk不可达，当前版本的行为是使用注册中心缓存继续启动（具体由check参数决定。 MonitorService初次调用，如遇zk不可达，当前版本会忽略monitor数据上传，以避免阻塞rpc主流程。

**重点**

在 2.5.7 版本更新的同时还给出了下一步的预告，近期即将提供 dubbo-spring-boot-starter 启动配置模块。

这个提示说明了两个事情：

- Dubbo 还会继续完善，后续会开发很多的新的功能，所以希望大家关注。
- 说明 Spring Boot 的影响力也越来越大，各种牛逼的开源软件纷纷给出了支持，现在也将包括 Dubbo。

## Dubbo 下一步会做什么？

**根据阿里技术的信息，最近三个版本会做的事情如下：**

- 优先解决社区使用过程中的问题和框架的缺陷，吸收社区贡献的新特性，解决文档访问和不全面的问题。
- 提供服务延迟暴乱、优雅停机 API 接口支持 RESTFULE 风格服务调用，提供 netty http 的支持，集成高性能序列化协议。
- 路由功能优化、消费端异步功能优化、提供端异步调用支持注册中心推送通知异步、合并处理改造等。

**未来计划**：

重构动态配置模块，动态配置和注册中心分离，集成流行的开源分布式配置管理框架，服务元数据注册与注册中心分离，丰富元数据内容，适配流行的 consul etcd 等注册中心方案。考虑提供 opentrace、oauth2、metrics、health、gateway 等部分服务化基础组件的支持，服务治理平台 OPS 重做，除代码、UI 重构外，期望能提供更强的服务测试、健康检查、服务动态治理等特性。Dubbo 模块化，各个模块可单独打包、单独依赖，集群熔断和自动故障检测能力。

继续在 Dubbo 框架现代化、国际化这两个大的方向上进行探索。现代化方面主要是考虑到目前微服务架构以及容器化日渐流行的大趋势，Dubbo 作为 RPC 框架如何很好地融入其中，成为其生态体系中不可或缺的一个组件。**强调的是 Dubbo 未来的定位并不是要成为一个微服务的全面解决方案，而是专注在 RPC 领域，成为微服务生态体系中的一个重要组件。**至于大家关注的微服务化衍生出的服务治理需求， Dubbo 将积极适配开源解决方案，甚至启动独立的开源项目予以支持。

## Dubbo和Spring Cloud有何不同？

首先做一个简单的功能对比：

|              | Dubbo         | Spring Cloud                 |
| :----------- | :------------ | :--------------------------- |
| 服务注册中心 | Zookeeper     | Spring Cloud Netflix Eureka  |
| 服务调用方式 | RPC           | REST API                     |
| 服务监控     | Dubbo-monitor | Spring Boot Admin            |
| 断路器       | 不完善        | Spring Cloud Netflix Hystrix |
| 服务网关     | 无            | Spring Cloud Netflix Zuul    |
| 分布式配置   | 无            | Spring Cloud Config          |
| 服务跟踪     | 无            | Spring Cloud Sleuth          |
| 消息总线     | 无            | Spring Cloud Bus             |
| 数据流       | 无            | Spring Cloud Stream          |
| 批量任务     | 无            | Spring Cloud Task            |
| ……           | ……            | ……                           |

**从上图可以看出其实Dubbo的功能只是Spring Cloud体系的一部分。**

这样对比是不够公平的，首先 Dubbo 是 SOA 时代的产物，它的关注点主要在于服务的调用，流量分发、流量监控和熔断。而 Spring Cloud 诞生于微服务架构时代，考虑的是微服务治理的方方面面，另外由于依托了 Spring、Spring Boot 的优势之上，两个框架在开始目标就不一致，Dubbo 定位服务治理、Spring Cloud 是一个生态。

**如果仅仅关注于服务治理的这个层面，Dubbo其实还优于Spring Cloud很多：**

- Dubbo 支持更多的协议，如：rmi、hessian、http、webservice、thrift、memcached、redis 等。
- Dubbo 使用 RPC 协议效率更高，在极端压力测试下，Dubbo 的效率会高于 Spring Cloud 效率一倍多。
- Dubbo 有更强大的后台管理，Dubbo 提供的后台管理 Dubbo Admin 功能强大，提供了路由规则、动态配置、访问控制、权重调节、均衡负载等诸多强大的功能。
- 可以限制某个 IP 流量的访问权限，设置不同服务器分发不同的流量权重，并且支持多种算法，利用这些功能我们可以在线上做灰度发布、故障转移等，Spring Cloud 到现在还不支持灰度发布、流量权重等功能。

![img](http://favorites.ren/assets/images/2017/architecture/dubbo_admin.png)

**所以Dubbo专注于服务治理；Spring Cloud关注于微服务架构生态。**

## Dubbo发布对Spring Cloud有影响吗？

国内技术人喜欢拿 Dubbo 和 Spring Cloud 进行对比，是因为两者都是服务治理非常优秀的开源框架。但它们两者的出发点是不一样的，Dubbo 关注于服务治理这块并且以后也会继续往这个方向去发展。Spring Cloud 关注的是微服务治理的生态。因为微服务治理的方方面面都是它所关注的内容，服务治理也只是微服务生态的一部分而已。因此可以大胆的断定，Dubbo 未来会在服务治理方面更为出色，而 Spring Cloud 在微服务治理上面无人能敌。

同时根据 Dubbo 最新的更新技术来看，Dubbo 也会积极的拥抱开源，拥抱新技术。Dubbo 接下来的版本将会很快的支持 Spring Boot，方便我们享受高效开发的同时，也可以支持高效的服务调用。Dubbo 被广泛应用于中国各互联网公司，如今阿里又重新重视起来并且发布了新版本和一系列的计划，对于正在使用 Dubbo 的公司来说是一个喜讯，对于中国广大的开发者来说更是一件非常喜悦的事情。我们非常乐于看到中国有一款非常优秀的开源框架，让我们有更多的选择，有更好的支持。

**两者其实不一定有竞争关系，如果使用得当甚至可以互补；另外两个关注的领域也不一致，因此对 Spring Cloud 的影响甚微。**

## 如何选择？

可能很多人正在犹豫，在服务治理的时候应该选择那个框架呢？如果公司对效率有极高的要求建议使用 Dubbo，相对比 RPC 的效率会比 HTTP 高很多；如果团队不想对技术架构做大的改造建议使用 Dubbo，Dubbo 仅仅需要少量的修改就可以融入到内部系统的架构中。但如果技术团队喜欢挑战新技术，建议选择 Spring Cloud，Spring Cloud 架构体系有有趣很酷的技术。如果公司选择微服务架构去重构整个技术体系，那么 Spring Cloud 是当仁不让之选，它可以说是目前最好的微服务框架没有之一。

最后，技术选型是一个综合的问题，需要考虑团队的情况、业务的发展以及公司的产品特征。最炫最酷的技术并不一定是最好的，选择适合自己团队、符合公司业务的框架才是最佳方案。技术的发展永远没有尽头，因此我们对技术也要保持空杯、保持饥饿、保持敬畏！

# springcloud(十一)：服务网关Zuul高级篇

时间过的很快，写[springcloud(十)：服务网关zuul初级篇](http://www.ityouknow.com/springcloud/2017/06/01/gateway-service-zuul.html)还在半年前，现在已经是2018年了，我们继续探讨Zuul更高级的使用方式。

上篇文章主要介绍了Zuul网关使用模式，以及自动转发机制，但其实Zuul还有更多的应用场景，比如：鉴权、流量转发、请求统计等等，这些功能都可以使用Zuul来实现。

## Zuul的核心

Filter是Zuul的核心，用来实现对外服务的控制。Filter的生命周期有4个，分别是“PRE”、“ROUTING”、“POST”、“ERROR”，整个生命周期可以用下图来表示。

![img](assets/zuul-core.png)

Zuul大部分功能都是通过过滤器来实现的，这些过滤器类型对应于请求的典型生命周期。

- **PRE：** 这种过滤器在请求被路由之前调用。我们可利用这种过滤器实现身份验证、在集群中选择请求的微服务、记录调试信息等。
- **ROUTING：**这种过滤器将请求路由到微服务。这种过滤器用于构建发送给微服务的请求，并使用Apache HttpClient或Netfilx Ribbon请求微服务。
- **POST：**这种过滤器在路由到微服务以后执行。这种过滤器可用来为响应添加标准的HTTP Header、收集统计信息和指标、将响应从微服务发送给客户端等。
- **ERROR：**在其他阶段发生错误时执行该过滤器。 除了默认的过滤器类型，Zuul还允许我们创建自定义的过滤器类型。例如，我们可以定制一种STATIC类型的过滤器，直接在Zuul中生成响应，而不将请求转发到后端的微服务。

### Zuul中默认实现的Filter

| 类型  | 顺序 | 过滤器                  | 功能                       |
| :---- | :--- | :---------------------- | :------------------------- |
| pre   | -3   | ServletDetectionFilter  | 标记处理Servlet的类型      |
| pre   | -2   | Servlet30WrapperFilter  | 包装HttpServletRequest请求 |
| pre   | -1   | FormBodyWrapperFilter   | 包装请求体                 |
| route | 1    | DebugFilter             | 标记调试标志               |
| route | 5    | PreDecorationFilter     | 处理请求上下文供后续使用   |
| route | 10   | RibbonRoutingFilter     | serviceId请求转发          |
| route | 100  | SimpleHostRoutingFilter | url请求转发                |
| route | 500  | SendForwardFilter       | forward请求转发            |
| post  | 0    | SendErrorFilter         | 处理有错误的请求响应       |
| post  | 1000 | SendResponseFilter      | 处理正常的请求响应         |

**禁用指定的Filter**

可以在application.yml中配置需要禁用的filter，格式：

```
zuul:
	FormBodyWrapperFilter:
		pre:
			disable: true
```

## 自定义Filter

实现自定义Filter，需要继承ZuulFilter的类，并覆盖其中的4个方法。

```
public class MyFilter extends ZuulFilter {
    @Override
    String filterType() {
        return "pre"; //定义filter的类型，有pre、route、post、error四种
    }

    @Override
    int filterOrder() {
        return 10; //定义filter的顺序，数字越小表示顺序越高，越先执行
    }

    @Override
    boolean shouldFilter() {
        return true; //表示是否需要执行该filter，true表示执行，false表示不执行
    }

    @Override
    Object run() {
        return null; //filter需要执行的具体操作
    }
}
```

## 自定义Filter示例

我们假设有这样一个场景，因为服务网关应对的是外部的所有请求，为了避免产生安全隐患，我们需要对请求做一定的限制，比如请求中含有Token便让请求继续往下走，如果请求不带Token就直接返回并给出提示。

首先自定义一个Filter，在run()方法中验证参数是否含有Token。

```
public class TokenFilter extends ZuulFilter {

    private final Logger logger = LoggerFactory.getLogger(TokenFilter.class);

    @Override
    public String filterType() {
        return "pre"; // 可以在请求被路由之前调用
    }

    @Override
    public int filterOrder() {
        return 0; // filter执行顺序，通过数字指定 ,优先级为0，数字越大，优先级越低
    }

    @Override
    public boolean shouldFilter() {
        return true;// 是否执行该过滤器，此处为true，说明需要过滤
    }

    @Override
    public Object run() {
        RequestContext ctx = RequestContext.getCurrentContext();
        HttpServletRequest request = ctx.getRequest();

        logger.info("--->>> TokenFilter {},{}", request.getMethod(), request.getRequestURL().toString());

        String token = request.getParameter("token");// 获取请求的参数

        if (StringUtils.isNotBlank(token)) {
            ctx.setSendZuulResponse(true); //对请求进行路由
            ctx.setResponseStatusCode(200);
            ctx.set("isSuccess", true);
            return null;
        } else {
            ctx.setSendZuulResponse(false); //不对其进行路由
            ctx.setResponseStatusCode(400);
            ctx.setResponseBody("token is empty");
            ctx.set("isSuccess", false);
            return null;
        }
    }

}
```

将TokenFilter加入到请求拦截队列，在启动类中添加以下代码：

```
@Bean
public TokenFilter tokenFilter() {
	return new TokenFilter();
}
```

这样就将我们自定义好的Filter加入到了请求拦截中。

**测试**

我们依次启动示例项目：`spring-cloud-eureka`、`spring-cloud-producer`、`spring-cloud-zuul`，这个三个项目均为上一篇示例项目，`spring-cloud-zuul`稍微进行改造。

访问地址：`http://localhost:8888/spring-cloud-producer/hello?name=neo`，返回：token is empty ，请求被拦截返回。
访问地址：`http://localhost:8888/spring-cloud-producer/hello?name=neo&token=xx`，返回：hello neo，this is first messge，说明请求正常响应。

通过上面这例子我们可以看出，我们可以使用“PRE”类型的Filter做很多的验证工作，在实际使用中我们可以结合shiro、oauth2.0等技术去做鉴权、验证。

## 路由熔断

当我们的后端服务出现异常的时候，我们不希望将异常抛出给最外层，期望服务可以自动进行一降级。Zuul给我们提供了这样的支持。当某个服务出现异常时，直接返回我们预设的信息。

我们通过自定义的fallback方法，并且将其指定给某个route来实现该route访问出问题的熔断处理。主要继承ZuulFallbackProvider接口来实现，ZuulFallbackProvider默认有两个方法，一个用来指明熔断拦截哪个服务，一个定制返回内容。

```
public interface ZuulFallbackProvider {
   /**
	 * The route this fallback will be used for.
	 * @return The route the fallback will be used for.
	 */
	public String getRoute();

	/**
	 * Provides a fallback response.
	 * @return The fallback response.
	 */
	public ClientHttpResponse fallbackResponse();
}
```

实现类通过实现getRoute方法，告诉Zuul它是负责哪个route定义的熔断。而fallbackResponse方法则是告诉 Zuul 断路出现时，它会提供一个什么返回值来处理请求。

后来Spring又扩展了此类，丰富了返回方式，在返回的内容中添加了异常信息，因此最新版本建议直接继承类`FallbackProvider` 。

我们以上面的spring-cloud-producer服务为例，定制它的熔断返回内容。

```
@Component
public class ProducerFallback implements FallbackProvider {
    private final Logger logger = LoggerFactory.getLogger(FallbackProvider.class);

    //指定要处理的 service。
    @Override
    public String getRoute() {
        return "spring-cloud-producer";
    }

    public ClientHttpResponse fallbackResponse() {
        return new ClientHttpResponse() {
            @Override
            public HttpStatus getStatusCode() throws IOException {
                return HttpStatus.OK;
            }

            @Override
            public int getRawStatusCode() throws IOException {
                return 200;
            }

            @Override
            public String getStatusText() throws IOException {
                return "OK";
            }

            @Override
            public void close() {

            }

            @Override
            public InputStream getBody() throws IOException {
                return new ByteArrayInputStream("The service is unavailable.".getBytes());
            }

            @Override
            public HttpHeaders getHeaders() {
                HttpHeaders headers = new HttpHeaders();
                headers.setContentType(MediaType.APPLICATION_JSON);
                return headers;
            }
        };
    }

    @Override
    public ClientHttpResponse fallbackResponse(Throwable cause) {
        if (cause != null && cause.getCause() != null) {
            String reason = cause.getCause().getMessage();
            logger.info("Excption {}",reason);
        }
        return fallbackResponse();
    }
}
```

当服务出现异常时，打印相关异常信息，并返回”The service is unavailable.”。

启动项目spring-cloud-producer-2，这时候服务中心会有两个spring-cloud-producer项目，我们重启Zuul项目。再手动关闭spring-cloud-producer-2项目，多次访问地址：`http://localhost:8888/spring-cloud-producer/hello?name=neo&token=xx`，会交替返回：

```
hello neo，this is first messge
The service is unavailable.
...
```

根据返回结果可以看出：spring-cloud-producer-2项目已经启用了熔断，返回:`The service is unavailable.`

> Zuul 目前只支持服务级别的熔断，不支持具体到某个URL进行熔断。

## 路由重试

有时候因为网络或者其它原因，服务可能会暂时的不可用，这个时候我们希望可以再次对服务进行重试，Zuul也帮我们实现了此功能，需要结合Spring Retry 一起来实现。下面我们以上面的项目为例做演示。

**添加Spring Retry依赖**

首先在spring-cloud-zuul项目中添加Spring Retry依赖。

```
<dependency>
	<groupId>org.springframework.retry</groupId>
	<artifactId>spring-retry</artifactId>
</dependency>
```

**开启Zuul Retry**

再配置文件中配置启用Zuul Retry

```
#是否开启重试功能
zuul.retryable=true
#对当前服务的重试次数
ribbon.MaxAutoRetries=2
#切换相同Server的次数
ribbon.MaxAutoRetriesNextServer=0
```

这样我们就开启了Zuul的重试功能。

**测试**

我们对spring-cloud-producer-2进行改造，在hello方法中添加定时，并且在请求的一开始打印参数。

```
@RequestMapping("/hello")
public String index(@RequestParam String name) {
    logger.info("request two name is "+name);
    try{
        Thread.sleep(1000000);
    }catch ( Exception e){
        logger.error(" hello two error",e);
    }
    return "hello "+name+"，this is two messge";
}
```

重启 spring-cloud-producer-2和spring-cloud-zuul项目。

访问地址：`http://localhost:8888/spring-cloud-producer/hello?name=neo&token=xx`，当页面返回：`The service is unavailable.`时查看项目spring-cloud-producer-2后台日志如下：

```
2018-01-22 19:50:32.401  INFO 19488 --- [io-9001-exec-14] o.s.c.n.z.f.route.FallbackProvider       : request two name is neo
2018-01-22 19:50:33.402  INFO 19488 --- [io-9001-exec-15] o.s.c.n.z.f.route.FallbackProvider       : request two name is neo
2018-01-22 19:50:34.404  INFO 19488 --- [io-9001-exec-16] o.s.c.n.z.f.route.FallbackProvider       : request two name is neo
```

说明进行了三次的请求，也就是进行了两次的重试。这样也就验证了我们的配置信息，完成了Zuul的重试功能。

**注意**

开启重试在某些情况下是有问题的，比如当压力过大，一个实例停止响应时，路由将流量转到另一个实例，很有可能导致最终所有的实例全被压垮。说到底，断路器的其中一个作用就是防止故障或者压力扩散。用了retry，断路器就只有在该服务的所有实例都无法运作的情况下才能起作用。这种时候，断路器的形式更像是提供一种友好的错误信息，或者假装服务正常运行的假象给使用者。

不用retry，仅使用负载均衡和熔断，就必须考虑到是否能够接受单个服务实例关闭和eureka刷新服务列表之间带来的短时间的熔断。如果可以接受，就无需使用retry。

## Zuul高可用

![img](assets/zuul-case.png)

我们实际使用Zuul的方式如上图，不同的客户端使用不同的负载将请求分发到后端的Zuul，Zuul在通过Eureka调用后端服务，最后对外输出。因此为了保证Zuul的高可用性，前端可以同时启动多个Zuul实例进行负载，在Zuul的前端使用Nginx或者F5进行负载转发以达到高可用性。

# springcloud(十二)：使用Spring Cloud Sleuth和Zipkin进行分布式链路跟踪

随着业务发展，系统拆分导致系统调用链路愈发复杂一个前端请求可能最终需要调用很多次后端服务才能完成，当整个请求变慢或不可用时，我们是无法得知该请求是由某个或某些后端服务引起的，这时就需要解决如何快读定位服务故障点，以对症下药。于是就有了分布式系统调用跟踪的诞生。

现今业界分布式服务跟踪的理论基础主要来自于 Google 的一篇论文[《Dapper, a Large-Scale Distributed Systems Tracing Infrastructure》](https://research.google.com/pubs/pub36356.html)，使用最为广泛的开源实现是 Twitter 的 Zipkin，为了实现平台无关、厂商无关的分布式服务跟踪，CNCF 发布了布式服务跟踪标准 Open Tracing。国内，淘宝的“鹰眼”、京东的“Hydra”、大众点评的“CAT”、新浪的“Watchman”、唯品会的“Microscope”、窝窝网的“Tracing”都是这样的系统。

## Spring Cloud Sleuth

一般的，一个分布式服务跟踪系统，主要有三部分：数据收集、数据存储和数据展示。根据系统大小不同，每一部分的结构又有一定变化。譬如，对于大规模分布式系统，数据存储可分为实时数据和全量数据两部分，实时数据用于故障排查（troubleshooting），全量数据用于系统优化；数据收集除了支持平台无关和开发语言无关系统的数据收集，还包括异步数据收集（需要跟踪队列中的消息，保证调用的连贯性），以及确保更小的侵入性；数据展示又涉及到数据挖掘和分析。虽然每一部分都可能变得很复杂，但基本原理都类似。

![img](assets/tracing1.png)

服务追踪的追踪单元是从客户发起请求（request）抵达被追踪系统的边界开始，到被追踪系统向客户返回响应（response）为止的过程，称为一个“trace”。每个 trace 中会调用若干个服务，为了记录调用了哪些服务，以及每次调用的消耗时间等信息，在每次调用服务时，埋入一个调用记录，称为一个“span”。这样，若干个有序的 span 就组成了一个 trace。在系统向外界提供服务的过程中，会不断地有请求和响应发生，也就会不断生成 trace，把这些带有span 的 trace 记录下来，就可以描绘出一幅系统的服务拓扑图。附带上 span 中的响应时间，以及请求成功与否等信息，就可以在发生问题的时候，找到异常的服务；根据历史数据，还可以从系统整体层面分析出哪里性能差，定位性能优化的目标。

Spring Cloud Sleuth为服务之间调用提供链路追踪。通过Sleuth可以很清楚的了解到一个服务请求经过了哪些服务，每个服务处理花费了多长。从而让我们可以很方便的理清各微服务间的调用关系。此外Sleuth可以帮助我们：

- 耗时分析: 通过Sleuth可以很方便的了解到每个采样请求的耗时，从而分析出哪些服务调用比较耗时;
- 可视化错误: 对于程序未捕捉的异常，可以通过集成Zipkin服务界面上看到;
- 链路优化: 对于调用比较频繁的服务，可以针对这些服务实施一些优化措施。

spring cloud sleuth可以结合zipkin，将信息发送到zipkin，利用zipkin的存储来存储信息，利用zipkin ui来展示数据。

这是Spring Cloud Sleuth的概念图：

![img](assets/tracing2.png)

## ZipKin

Zipkin 是一个开放源代码分布式的跟踪系统，由Twitter公司开源，它致力于收集服务的定时数据，以解决微服务架构中的延迟问题，包括数据的收集、存储、查找和展现。

每个服务向zipkin报告计时数据，zipkin会根据调用关系通过Zipkin UI生成依赖关系图，显示了多少跟踪请求通过每个服务，该系统让开发者可通过一个 Web 前端轻松的收集和分析数据，例如用户每次请求服务的处理时间等，可方便的监测系统中存在的瓶颈。

Zipkin提供了可插拔数据存储方式：In-Memory、MySql、Cassandra以及Elasticsearch。接下来的测试为方便直接采用In-Memory方式进行存储，生产推荐Elasticsearch。

## 快速上手

### 创建zipkin-server项目

**项目依赖**

```
<dependencies>
    <dependency>
        <groupId>org.springframework.cloud</groupId>
        <artifactId>spring-cloud-starter-eureka</artifactId>
    </dependency>
    <dependency>
        <groupId>io.zipkin.java</groupId>
        <artifactId>zipkin-server</artifactId>
    </dependency>
    <dependency>
        <groupId>io.zipkin.java</groupId>
        <artifactId>zipkin-autoconfigure-ui</artifactId>
    </dependency>
</dependencies>
```

**启动类**

```
@SpringBootApplication
@EnableEurekaClient
@EnableZipkinServer
public class ZipkinApplication {

    public static void main(String[] args) {
        SpringApplication.run(ZipkinApplication.class, args);
    }

}
```

使用了`@EnableZipkinServer`注解，启用Zipkin服务。

**配置文件**

```
eureka:
  client:
    serviceUrl:
      defaultZone: http://localhost:8761/eureka/
server:
  port: 9000
spring:
  application:
    name: zipkin-server
```

配置完成后依次启动示例项目：`spring-cloud-eureka`、`zipkin-server`项目。刚问地址:`http://localhost:9000/zipkin/`可以看到Zipkin后台页面

![img](assets/tracing3.png)

### 项目添加zipkin支持

在项目`spring-cloud-producer`和`spring-cloud-zuul`中添加zipkin的支持。

```
<dependency>
    <groupId>org.springframework.cloud</groupId>
    <artifactId>spring-cloud-starter-zipkin</artifactId>
</dependency>
```

Spring应用在监测到Java依赖包中有sleuth和zipkin后，会自动在RestTemplate的调用过程中向HTTP请求注入追踪信息，并向Zipkin Server发送这些信息。

同时配置文件中添加如下代码：

```
spring:
  zipkin:
    base-url: http://localhost:9000
  sleuth:
    sampler:
      percentage: 1.0
```

spring.zipkin.base-url指定了Zipkin服务器的地址，spring.sleuth.sampler.percentage将采样比例设置为1.0，也就是全部都需要。

Spring Cloud Sleuth有一个Sampler策略，可以通过这个实现类来控制采样算法。采样器不会阻碍span相关id的产生，但是会对导出以及附加事件标签的相关操作造成影响。 Sleuth默认采样算法的实现是Reservoir sampling，具体的实现类是PercentageBasedSampler，默认的采样比例为: 0.1(即10%)。不过我们可以通过spring.sleuth.sampler.percentage来设置，所设置的值介于0.0到1.0之间，1.0则表示全部采集。

这两个项目添加zipkin之后，依次进行启动。

### 进行验证

这样我们就模拟了这样一个场景，通过外部请求访问Zuul网关，Zuul网关去调用`spring-cloud-producer`对外提供的服务。

四个项目均启动后，在浏览器中访问地址：`http://localhost:8888/producer/hello?name=neo` 两次，然后再打开地址： `http://localhost:9000/zipkin/`点击对应按钮进行查看。

点击查找看到有两条记录

![img](assets/zipkin1.png)

点击记录进去页面，可以看到每一个服务所耗费的时间和顺序

![img](assets/zipkin2.png)

点击依赖分析，可以看到项目之间的调用关系

![img](assets/zipkin3.png)

# springcloud(十三)：注册中心 Consul 使用详解

 2018/07/20

在上个月我们知道 Eureka 2.X 遇到困难停止开发了，但其实对国内的用户影响甚小，一方面国内大都使用的是 Eureka 1.X 系列，另一方面 Spring Cloud 支持很多服务发现的软件，Eureka 只是其中之一，下面是 Spring Cloud 支持的服务发现软件以及特性对比：

| Feature              | euerka                       | Consul                 | zookeeper             | etcd              |
| :------------------- | :--------------------------- | :--------------------- | :-------------------- | :---------------- |
| 服务健康检查         | 可配支持                     | 服务状态，内存，硬盘等 | (弱)长连接，keepalive | 连接心跳          |
| 多数据中心           | —                            | 支持                   | —                     | —                 |
| kv 存储服务          | —                            | 支持                   | 支持                  | 支持              |
| 一致性               | —                            | raft                   | paxos                 | raft              |
| cap                  | ap                           | cp                     | cp                    | cp                |
| 使用接口(多语言能力) | http（sidecar）              | 支持 http 和 dns       | 客户端                | http/grpc         |
| watch 支持           | 支持 long polling/大部分增量 | 全量/支持long polling  | 支持                  | 支持 long polling |
| 自身监控             | metrics                      | metrics                | —                     | metrics           |
| 安全                 | —                            | acl /https             | acl                   | https 支持（弱）  |
| spring cloud 集成    | 已支持                       | 已支持                 | 已支持                | 已支持            |

在以上服务发现的软件中，Euerka 和 Consul 使用最为广泛。如果大家对注册中心的概念和 Euerka 不太了解的话， 可以参考我前期的文章：[springcloud(二)：注册中心Eureka ](http://www.ityouknow.com/springcloud/2017/05/10/springcloud-eureka.html)，本篇文章主要给大家介绍 Spring Cloud Consul 的使用。

## Consul 介绍

Consul 是 HashiCorp 公司推出的开源工具，用于实现分布式系统的服务发现与配置。与其它分布式服务注册与发现的方案，Consul 的方案更“一站式”，内置了服务注册与发现框 架、分布一致性协议实现、健康检查、Key/Value 存储、多数据中心方案，不再需要依赖其它工具（比如 ZooKeeper 等）。使用起来也较 为简单。Consul 使用 Go 语言编写，因此具有天然可移植性(支持Linux、windows和Mac OS X)；安装包仅包含一个可执行文件，方便部署，与 Docker 等轻量级容器可无缝配合。

**Consul 的优势：**

- 使用 Raft 算法来保证一致性, 比复杂的 Paxos 算法更直接. 相比较而言, zookeeper 采用的是 Paxos, 而 etcd 使用的则是 Raft。
- 支持多数据中心，内外网的服务采用不同的端口进行监听。 多数据中心集群可以避免单数据中心的单点故障,而其部署则需要考虑网络延迟, 分片等情况等。 zookeeper 和 etcd 均不提供多数据中心功能的支持。
- 支持健康检查。 etcd 不提供此功能。
- 支持 http 和 dns 协议接口。 zookeeper 的集成较为复杂, etcd 只支持 http 协议。
- 官方提供 web 管理界面, etcd 无此功能。
- 综合比较, Consul 作为服务注册和配置管理的新星, 比较值得关注和研究。

**特性：**

- 服务发现
- 健康检查
- Key/Value 存储
- 多数据中心

**Consul 角色**

- client: 客户端, 无状态, 将 HTTP 和 DNS 接口请求转发给局域网内的服务端集群。
- server: 服务端, 保存配置信息, 高可用集群, 在局域网内与本地客户端通讯, 通过广域网与其它数据中心通讯。 每个数据中心的 server 数量推荐为 3 个或是 5 个。

Consul 客户端、服务端还支持夸中心的使用，更加提高了它的高可用性。

![img](assets/consul-server-client.png)

**Consul 工作原理：**

![img](assets/consol_service.png)

- 1、当 Producer 启动的时候，会向 Consul 发送一个 post 请求，告诉 Consul 自己的 IP 和 Port
- 2、Consul 接收到 Producer 的注册后，每隔10s（默认）会向 Producer 发送一个健康检查的请求，检验Producer是否健康
- 3、当 Consumer 发送 GET 方式请求 /api/address 到 Producer 时，会先从 Consul 中拿到一个存储服务 IP 和 Port 的临时表，从表中拿到 Producer 的 IP 和 Port 后再发送 GET 方式请求 /api/address
- 4、该临时表每隔10s会更新，只包含有通过了健康检查的 Producer

Spring Cloud Consul 项目是针对 Consul 的服务治理实现。Consul 是一个分布式高可用的系统，它包含多个组件，但是作为一个整体，在微服务架构中为我们的基础设施提供服务发现和服务配置的工具。

## Consul VS Eureka

Eureka 是一个服务发现工具。该体系结构主要是客户端/服务器，每个数据中心有一组 Eureka 服务器，通常每个可用区域一个。通常 Eureka 的客户使用嵌入式 SDK 来注册和发现服务。对于非本地集成的客户，官方提供的 Eureka 一些 REST 操作 API，其它语言可以使用这些 API 来实现对 Eureka Server 的操作从而实现一个非 jvm 语言的 Eureka Client。

Eureka 提供了一个弱一致的服务视图，尽可能的提供服务可用性。当客户端向服务器注册时，该服务器将尝试复制到其它服务器，但不提供保证复制完成。服务注册的生存时间（TTL）较短，要求客户端对服务器心跳检测。不健康的服务或节点停止心跳，导致它们超时并从注册表中删除。服务发现可以路由到注册的任何服务，由于心跳检测机制有时间间隔，可能会导致部分服务不可用。这个简化的模型允许简单的群集管理和高可扩展性。

Consul 提供了一些列特性，包括更丰富的健康检查，键值对存储以及多数据中心。Consul 需要每个数据中心都有一套服务，以及每个客户端的 agent，类似于使用像 Ribbon 这样的服务。Consul agent 允许大多数应用程序成为 Consul 不知情者，通过配置文件执行服务注册并通过 DNS 或负载平衡器 sidecars 发现。

Consul 提供强大的一致性保证，因为服务器使用 Raft 协议复制状态 。Consul 支持丰富的健康检查，包括 TCP，HTTP，Nagios / Sensu 兼容脚本或基于 Eureka 的 TTL。客户端节点参与基于 Gossip 协议的健康检查，该检查分发健康检查工作，而不像集中式心跳检测那样成为可扩展性挑战。发现请求被路由到选举出来的 leader，这使他们默认情况下强一致性。允许客户端过时读取取使任何服务器处理他们的请求，从而实现像 Eureka 这样的线性可伸缩性。

Consul 强烈的一致性意味着它可以作为领导选举和集群协调的锁定服务。Eureka 不提供类似的保证，并且通常需要为需要执行协调或具有更强一致性需求的服务运行 ZooKeeper。

Consul 提供了支持面向服务的体系结构所需的一系列功能。这包括服务发现，还包括丰富的运行状况检查，锁定，密钥/值，多数据中心联合，事件系统和 ACL。Consul 和 consul-template 和 envconsul 等工具生态系统都试图尽量减少集成所需的应用程序更改，以避免需要通过 SDK 进行本地集成。Eureka 是一个更大的 Netflix OSS 套件的一部分，该套件预计应用程序相对均匀且紧密集成。因此 Eureka 只解决了一小部分问题，可以和 ZooKeeper 等其它工具可以一起使用。

Consul 强一致性(C)带来的是：

服务注册相比 Eureka 会稍慢一些。因为 Consul 的 raft 协议要求必须过半数的节点都写入成功才认为注册成功 Leader 挂掉时，重新选举期间整个 Consul 不可用。保证了强一致性但牺牲了可用性。

Eureka 保证高可用(A)和最终一致性：

服务注册相对要快，因为不需要等注册信息 replicate 到其它节点，也不保证注册信息是否 replicate 成功 当数据出现不一致时，虽然 A, B 上的注册信息不完全相同，但每个 Eureka 节点依然能够正常对外提供服务，这会出现查询服务信息时如果请求 A 查不到，但请求 B 就能查到。如此保证了可用性但牺牲了一致性。

其它方面，eureka 就是个 servlet 程序，跑在 servlet 容器中; Consul 则是 go 编写而成。

## Consul 安装

Consul 不同于 Eureka 需要单独安装，访问[Consul 官网](https://www.consul.io/downloads.html)下载 Consul 的最新版本，我这里是 consul_1.2.1。

根据不同的系统类型选择不同的安装包，从下图也可以看出 Consul 支持所有主流系统。

![img](assets/consul_insall.png)

我这里以 Windows 为例，下载下来是一个 consul_1.2.1_windows_amd64.zip 的压缩包，解压是是一个 consul.exe 的执行文件。

![img](assets/consul_win.png)

cd 到对应的目录下，使用 cmd 启动 Consul

```
cd D:\Common Files\consul
#cmd启动：
consul agent -dev        # -dev表示开发模式运行，另外还有-server表示服务模式运行
```

为了方便期间，可以在同级目录下创建一个 run.bat 脚本来启动，脚本内容如下：

```
consul agent -dev
pause
```

启动结果如下：

![img](assets/consol_cmd.png)

启动成功之后访问：`http://localhost:8500`，可以看到 Consul 的管理界面

![img](assets/consol_manage.png)

这样就意味着我们的 Consul 服务启动成功了。

## Consul 服务端

接下来我们开发 Consul 的服务端，我们创建一个 spring-cloud-consul-producer 项目

### 添加依赖包

依赖包如下：

```
<dependencies>
	<dependency>
		<groupId>org.springframework.boot</groupId>
		<artifactId>spring-boot-starter-actuator</artifactId>
	</dependency>
	<dependency>
		<groupId>org.springframework.cloud</groupId>
		<artifactId>spring-cloud-starter-consul-discovery</artifactId>
	</dependency>
	<dependency>
		<groupId>org.springframework.boot</groupId>
		<artifactId>spring-boot-starter-web</artifactId>
	</dependency>
	<dependency>
		<groupId>org.springframework.boot</groupId>
		<artifactId>spring-boot-starter-test</artifactId>
		<scope>test</scope>
	</dependency>
</dependencies>
```

- `spring-boot-starter-actuator` 健康检查依赖于此包。
- `spring-cloud-starter-consul-discovery` Spring Cloud Consul 的支持。

Spring Boot 版本使用的是 2.0.3.RELEASE，Spring Cloud 最新版本是 Finchley.RELEASE 依赖于 Spring Boot 2.x.

```
<parent>
	<groupId>org.springframework.boot</groupId>
	<artifactId>spring-boot-starter-parent</artifactId>
	<version>2.0.3.RELEASE</version>
	<relativePath/> <!-- lookup parent from repository -->
</parent>

<dependencyManagement>
	<dependencies>
		<dependency>
			<groupId>org.springframework.cloud</groupId>
			<artifactId>spring-cloud-dependencies</artifactId>
			<version>${spring-cloud.version}</version>
			<type>pom</type>
			<scope>import</scope>
		</dependency>
	</dependencies>
</dependencyManagement>
```

完整的 pom.xml 文件大家可以参考示例源码。

### 配置文件

配置文件内容如下

```
spring.application.name=spring-cloud-consul-producer
server.port=8501
spring.cloud.consul.host=localhost
spring.cloud.consul.port=8500
#注册到consul的服务名称
spring.cloud.consul.discovery.serviceName=service-producer
```

Consul 的地址和端口号默认是 localhost:8500 ，如果不是这个地址可以自行配置。 `spring.cloud.consul.discovery.serviceName` 是指注册到 Consul 的服务名称，后期客户端会根据这个名称来进行服务调用。

### 启动类

```
@SpringBootApplication
@EnableDiscoveryClient
public class ConsulProducerApplication {

	public static void main(String[] args) {
		SpringApplication.run(ConsulProducerApplication.class, args);
	}
}
```

添加了 `@EnableDiscoveryClient` 注解表示支持服务发现。

### 提供服务

我们在创建一个 Controller，推文提供 hello 的服务。

```
@RestController
public class HelloController {

    @RequestMapping("/hello")
    public String hello() {
        return "hello consul";
    }
}
```

为了模拟注册均衡负载复制一份上面的项目重命名为 spring-cloud-consul-producer-2 ,修改对应的端口为 8502，修改 hello 方法的返回值为：”hello consul two”，修改完成后依次启动两个项目。

这时候我们再次在浏览器访问地址：http://localhost:8500，显示如下：

![img](assets/consol_producer.png)

我们发现页面多了 service-producer 服务，点击进去后页面显示有两个服务提供者：

![img](assets/consol_producer-2.png)

这样服务提供者就准备好了。

## Consul 消费端

我们创建一个 spring-cloud-consul-consumer 项目，pom 文件和上面示例保持一致。

### 配置文件

配置文件内容如下

```
spring.application.name=spring-cloud-consul-consumer
server.port=8503
spring.cloud.consul.host=127.0.0.1
spring.cloud.consul.port=8500
#设置不需要注册到 consul 中
spring.cloud.consul.discovery.register=false
```

客户端可以设置注册到 Consul 中，也可以不注册到 Consul 注册中心中，根据我们的业务来选择，只需要在使用服务时通过 Consul 对外提供的接口获取服务信息即可。

### 启动类

```
@SpringBootApplication
public class ConsulConsumerApplication {

	public static void main(String[] args) {
		SpringApplication.run(ConsulConsumerApplication.class, args);
	}
}
```

### 进行测试

我们先来创建一个 ServiceController ,试试如果去获取 Consul 中的服务。

```
@RestController
public class ServiceController {

    @Autowired
    private LoadBalancerClient loadBalancer;
    @Autowired
    private DiscoveryClient discoveryClient;

   /**
     * 获取所有服务
     */
    @RequestMapping("/services")
    public Object services() {
        return discoveryClient.getInstances("service-producer");
    }

    /**
     * 从所有服务中选择一个服务（轮询）
     */
    @RequestMapping("/discover")
    public Object discover() {
        return loadBalancer.choose("service-producer").getUri().toString();
    }
}
```

Controller 中有俩个方法，一个是获取所有服务名为`service-producer`的服务信息并返回到页面，一个是随机从服务名为`service-producer`的服务中获取一个并返回到页面。

添加完 ServiceController 之后我们启动项目，访问地址：`http://localhost:8503/services`，返回：

```
[{"serviceId":"service-producer","host":"windows10.microdone.cn","port":8501,"secure":false,"metadata":{"secure":"false"},"uri":"http://windows10.microdone.cn:8501","scheme":null},{"serviceId":"service-producer","host":"windows10.microdone.cn","port":8502,"secure":false,"metadata":{"secure":"false"},"uri":"http://windows10.microdone.cn:8502","scheme":null}]
```

发现我们刚才创建的端口为 8501 和 8502 的两个服务端都存在。

多次访问地址：`http://localhost:8503/discover`，页面会交替返回下面信息：

```
http://windows10.microdone.cn:8501
http://windows10.microdone.cn:8502
...
```

说明 8501 和 8502 的两个服务会交替出现，从而实现了获取服务端地址的均衡负载。

大多数情况下我们希望使用均衡负载的形式去获取服务端提供的服务，因此使用第二种方法来模拟调用服务端提供的 hello 方法。

创建 CallHelloController ：

```
@RestController
public class CallHelloController {

    @Autowired
    private LoadBalancerClient loadBalancer;

    @RequestMapping("/call")
    public String call() {
        ServiceInstance serviceInstance = loadBalancer.choose("service-producer");
        System.out.println("服务地址：" + serviceInstance.getUri());
        System.out.println("服务名称：" + serviceInstance.getServiceId());

        String callServiceResult = new RestTemplate().getForObject(serviceInstance.getUri().toString() + "/hello", String.class);
        System.out.println(callServiceResult);
        return callServiceResult;
    }

}
```

使用 RestTemplate 进行远程调用。添加完之后重启 spring-cloud-consul-consumer 项目。在浏览器中访问地址：`http://localhost:8503/call`，依次返回结果如下：

```
hello consul
hello consul two
...
```

说明我们已经成功的调用了 Consul 服务端提供的服务，并且实现了服务端的均衡负载功能。通过今天的实践我们发现 Consul 提供的服务发现易用、强大。

# springcloud(十四)：Spring Cloud 开源软件都有哪些？

 2018/08/06

学习一门新的技术如果有优秀的开源项目，对初学者的学习将会是事半功倍，通过研究和学习优秀的开源项目，可以快速的了解此技术的相关应用场景和应用示例，参考优秀开源项目会降低将此技术引入到项目中的成本。为此抽了一些时间为大家寻找了一些非常优秀的 Spring Cloud 开源软件供大家学习参考。

上次写了一篇文章[Spring Boot 2 (三)：Spring Boot 开源软件都有哪些](http://www.ityouknow.com/springboot/2018/03/05/spring-boot-open-source.html) 给大家介绍优秀的 Spring Boot 开源项目，本篇文章给介绍 Spring Cloud 的优秀开源项目。Spring Cloud 开源项目主要集中在 Github/码云 ，本文所有项目地址也均来自于这两个网站。

## 1、 [awesome-spring-cloud](https://github.com/ityouknow/awesome-spring-cloud)

首先给大家介绍的就是 Spring Cloud 中文索引，这是一个专门收集 Spring Cloud 相关资料的开源项目，也有对应的导航页面。

**产品主页**

http://springcloud.fun/

**项目主页**

https://github.com/ityouknow/awesome-spring-cloud

**产品截图**

![img](assets/awesome-spring-cloud.png)

## 2、 [PiggyMetrics](https://github.com/sqshq/PiggyMetrics)

一个简单的个人财务系统，基于 Spring Boot，Spring Cloud 和 Docker 简单演示了微服务的架构模式，整个项目几乎包含了 Spring Cloud 的所有特性包括 配置中心、Gateway zuul API 网关、Eureka 服务发现、Hystrix、Turbine仪 表盘应用健康监控等等。

PiggyMetrics 被分解为三个核心微服务。这些服务都是围绕某些业务能力组织的可独立部署的应用程序。

![img](assets/PiggyMetrics_sercive.png)

PiggyMetrics 的项目架构图

![img](http://favorites.ren/assets/images/2018/springcloud/PInfrastructure.png)

**项目主页**

https://github.com/sqshq/PiggyMetrics

**产品截图**

![img](assets/piggyMetrics.png)

## 3、 [spaascloud-master](https://github.com/paascloud/paascloud-master)

spring cloud + vue 全家桶实战，模拟商城，完整的购物流程、后端运营平台，可以实现快速搭建企业级微服务项目。

功能点： 模拟商城，完整的购物流程、后端运营平台对前端业务的支撑，和对项目的运维，有各项的监控指标和运维指标。

技术点： 核心技术为springcloud+vue两个全家桶实现，采取了取自开源用于开源的目标，所以能用开源绝不用收费框架，整体技术栈只有 阿里云短信服务是收费的，都是目前java前瞻性的框架，可以为中小企业解决微服务架构难题，可以帮助企业快速建站。由于服务 器成本较高，尽量降低开发成本的原则，本项目由10个后端项目和3个前端项目共同组成。真正实现了基于RBAC、jwt和oauth2的 无状态统一权限认证的解决方案，实现了异常和日志的统一管理，实现了MQ落地保证100%到达的解决方案。

**产品主页**

http://mall.paascloud.net/index

**项目主页**

https://github.com/paascloud/paascloud-master

**产品截图**

![img](http://favorites.ren/assets/images/2018/springcloud/paascloud.png)

## 4、 [Cloud-Admin](https://gitee.com/minull/ace-security)

Cloud-Admin是国内首个基于Spring Cloud微服务化开发平台，核心技术采用Spring Boot2以及Spring Cloud Gateway相关核心组件，前端采用vue-element-admin组件。具有统一授权、认证后台管理系统，其中包含具备用户管理、资源权限管理、网关API管理等多个模块，支持多业务系统并行开发，可以作为后端服务的开发脚手架。代码简洁，架构清晰，适合学习和直接项目中使用。

**项目主页**

https://gitee.com/minull/ace-security

**项目架构**

![img](http://favorites.ren/assets/images/2018/springcloud/ace-security.png)

## 5、 [spring-cloud-rest-tcc](https://github.com/prontera/spring-cloud-rest-tcc)

基于Spring Cloud Netflix的TCC柔性事务和EDA事件驱动示例，结合Spring Cloud Sleuth进行会话追踪和Spring Boot Admin的健康监控，并辅以Hystrix Dashboard提供近实时的熔断监控.

**项目主页**

https://github.com/prontera/spring-cloud-rest-tcc

**项目架构**

![img](http://favorites.ren/assets/images/2018/springcloud/spring-cloud-rest-tcc.png)

## 6、 [pig](https://gitee.com/log4j/pig)

基于Spring Cloud、oAuth2.0开发，基于Vue前后分离的开发平台，支持账号、短信、SSO等多种登录

**产品主页**

https://www.pig4cloud.com/

**项目主页**

https://gitee.com/log4j/pig

**产品截图**

![img](http://favorites.ren/assets/images/2018/springcloud/ping.png)

## 7、 [xxpay-master](https://gitee.com/jmdhappy/xxpay-master)

XxPay聚合支付使用Java开发，包括spring-cloud、dubbo、spring-boot三个架构版本，已接入微信、支付宝等主流支付渠道，可直接用于生产环境。

**产品主页**

http://www.xxpay.org/

**项目主页**

https://gitee.com/jmdhappy/xxpay-master

**产品截图**

![img](http://favorites.ren/assets/images/2018/springcloud/xxpay.png)

## 8、 [spring-boot-cloud](https://github.com/zhangxd1989/spring-boot-cloud)

基于 Spring Boot、Spring Cloud、Spring Oauth2 和 Spring Cloud Netflix 等框架构建的微服务项目

**项目主页**

https://github.com/zhangxd1989/spring-boot-cloud

**项目架构**

![img](http://favorites.ren/assets/images/2018/springcloud/spring-boot-cloud.jpg)

## 9、 [FCat](https://gitee.com/xfdm/FCat)

FCat项目基于 Angular 4 + Spring Cloud 的企业级基础功能框架。

**项目主页**

https://gitee.com/xfdm/FCat

**项目架构**

![img](http://favorites.ren/assets/images/2018/springcloud/FCat.png)

## 10、 [spring-cloud-examples](https://github.com/ityouknow/spring-cloud-examples)

Spring Cloud 技术栈示例代码，快速简单上手教程，一个帮助大家学习 Spring Cloud 的开源示例项目，每个 Spring Cloud 组件都有独立的示例供大家参考学习。

**项目主页**

https://github.com/ityouknow/spring-cloud-examples

**项目截图**

![img](http://favorites.ren/assets/images/2018/springcloud/spring-cloud-examples.png)

> 应该还有更多优秀的 Spring Cloud 开源项目，目前仅发现这些，也希望大家多反馈一些优秀的 Spring Cloud 开源项目，统一将这些项目收集到 awesome-spring-cloud 中，方便后续大家学习查找。

# springcloud(十五)：服务网关 Spring Cloud GateWay 入门

 2018/12/12

Spring 官方最终还是按捺不住推出了自己的网关组件：Spring Cloud Gateway ，相比之前我们使用的 Zuul（1.x） 它有哪些优势呢？Zuul（1.x） 基于 Servlet，使用阻塞 API，它不支持任何长连接，如 WebSockets，Spring Cloud Gateway 使用非阻塞 API，支持 WebSockets，支持限流等新特性。

## Spring Cloud Gateway

Spring Cloud Gateway 是 Spring Cloud 的一个全新项目，该项目是基于 Spring 5.0，Spring Boot 2.0 和 Project Reactor 等技术开发的网关，它旨在为微服务架构提供一种简单有效的统一的 API 路由管理方式。

Spring Cloud Gateway 作为 Spring Cloud 生态系统中的网关，目标是替代 Netflix Zuul，其不仅提供统一的路由方式，并且基于 Filter 链的方式提供了网关基本的功能，例如：安全，监控/指标，和限流。

**相关概念:**

- Route（路由）：这是网关的基本构建块。它由一个 ID，一个目标 URI，一组断言和一组过滤器定义。如果断言为真，则路由匹配。
- Predicate（断言）：这是一个 Java 8 的 Predicate。输入类型是一个 ServerWebExchange。我们可以使用它来匹配来自 HTTP 请求的任何内容，例如 headers 或参数。
- Filter（过滤器）：这是`org.springframework.cloud.gateway.filter.GatewayFilter`的实例，我们可以使用它修改请求和响应。

**工作流程：**

![img](assets/spring-cloud-gateway.png)

客户端向 Spring Cloud Gateway 发出请求。如果 Gateway Handler Mapping 中找到与请求相匹配的路由，将其发送到 Gateway Web Handler。Handler 再通过指定的过滤器链来将请求发送到我们实际的服务执行业务逻辑，然后返回。 过滤器之间用虚线分开是因为过滤器可能会在发送代理请求之前（“pre”）或之后（“post”）执行业务逻辑。

Spring Cloud Gateway 的特征：

- 基于 Spring Framework 5，Project Reactor 和 Spring Boot 2.0
- 动态路由
- Predicates 和 Filters 作用于特定路由
- 集成 Hystrix 断路器
- 集成 Spring Cloud DiscoveryClient
- 易于编写的 Predicates 和 Filters
- 限流
- 路径重写

## 快速上手

Spring Cloud Gateway 网关路由有两种配置方式：

- 在配置文件 yml 中配置
- 通过`@Bean`自定义 RouteLocator，在启动主类 Application 中配置

这两种方式是等价的，建议使用 yml 方式进配置。

使用 Spring Cloud Finchley 版本，Finchley 版本依赖于 Spring Boot 2.0.6.RELEASE。

```
<parent>
	<groupId>org.springframework.boot</groupId>
	<artifactId>spring-boot-starter-parent</artifactId>
	<version>2.0.6.RELEASE</version>
	<relativePath/> <!-- lookup parent from repository -->
</parent>

<dependencyManagement>
	<dependencies>
		<dependency>
			<groupId>org.springframework.cloud</groupId>
			<artifactId>spring-cloud-dependencies</artifactId>
			<version>Finchley.SR2</version>
			<type>pom</type>
			<scope>import</scope>
		</dependency>
	</dependencies>
</dependencyManagement>
```

> 经测试 Finchley.RELEASE 有 bug 多次请求会报空指针异常，SR2 是 Spring Cloud 的最新版本。

添加项目需要使用的依赖包

```
<dependency>
	<groupId>org.springframework.cloud</groupId>
	<artifactId>spring-cloud-starter-gateway</artifactId>
</dependency>
```

Spring Cloud Gateway 是使用 netty+webflux 实现因此不需要再引入 web 模块。

我们先来测试一个最简单的请求转发。

```
server:
  port: 8080
spring:
  cloud:
    gateway:
      routes:
      - id: neo_route
        uri: http://www.ityouknow.com
        predicates:
        - Path=/spring-cloud
```

各字段含义如下：

- id：我们自定义的路由 ID，保持唯一
- uri：目标服务地址
- predicates：路由条件，Predicate 接受一个输入参数，返回一个布尔值结果。该接口包含多种默认方法来将 Predicate 组合成其他复杂的逻辑（比如：与，或，非）。
- filters：过滤规则，本示例暂时没用。

上面这段配置的意思是，配置了一个 id 为 neo_route 的路由规则，当访问地址 `http://localhost:8080/spring-cloud`时会自动转发到地址：`http://www.ityouknow.com/spring-cloud`。配置完成启动项目即可在浏览器访问进行测试，当我们访问地址`http://localhost:8080/spring-cloud` 时会展示页面展示如下：

![img](http://favorites.ren/assets/images/2018/springcloud/spring-cloud-gateway1.png)

证明页面转发成功。

转发功能同样可以通过代码来实现，我们可以在启动类 GateWayApplication 中添加方法 `customRouteLocator()` 来定制转发规则。

```
@SpringBootApplication
public class GateWayApplication {

	public static void main(String[] args) {
		SpringApplication.run(GateWayApplication.class, args);
	}

	@Bean
	public RouteLocator customRouteLocator(RouteLocatorBuilder builder) {
		return builder.routes()
				.route("path_route", r -> r.path("/about")
						.uri("http://ityouknow.com"))
				.build();
	}

}
```

上面配置了一个 id 为 path_route 的路由，当访问地址`http://localhost:8080/about`时会自动转发到地址：`http://www.ityouknow.com/about`和上面的转发效果一样，只是这里转发的是以`项目地址/about`格式的请求地址。

上面两个示例中 uri 都是指向了我的个人网站，在实际项目使用中可以将 uri 指向对外提供服务的项目地址，统一对外输出接口。

以上便是 Spring Cloud Gateway 最简单的两个请求示例，Spring Cloud Gateway 还有更多实用的功能接下来我们一一介绍。

## 路由规则

Spring Cloud Gateway 的功能很强大，我们仅仅通过 Predicates 的设计就可以看出来，前面我们只是使用了 predicates 进行了简单的条件匹配，其实 Spring Cloud Gataway 帮我们内置了很多 Predicates 功能。

Spring Cloud Gateway 是通过 Spring WebFlux 的 `HandlerMapping` 做为底层支持来匹配到转发路由，Spring Cloud Gateway 内置了很多 Predicates 工厂，这些 Predicates 工厂通过不同的 HTTP 请求参数来匹配，多个 Predicates 工厂可以组合使用。

### Predicate 介绍

Predicate 来源于 Java 8，是 Java 8 中引入的一个函数，Predicate 接受一个输入参数，返回一个布尔值结果。该接口包含多种默认方法来将 Predicate 组合成其他复杂的逻辑（比如：与，或，非）。可以用于接口请求参数校验、判断新老数据是否有变化需要进行更新操作。

在 Spring Cloud Gateway 中 Spring 利用 Predicate 的特性实现了各种路由匹配规则，有通过 Header、请求参数等不同的条件来进行作为条件匹配到对应的路由。网上有一张图总结了 Spring Cloud 内置的几种 Predicate 的实现。

![img](http://favorites.ren/assets/images/2018/springcloud/spring-cloud-gateway3.png)

说白了 Predicate 就是为了实现一组匹配规则，方便让请求过来找到对应的 Route 进行处理，接下来我们接下 Spring Cloud GateWay 内置几种 Predicate 的使用。

### 通过时间匹配

Predicate 支持设置一个时间，在请求进行转发的时候，可以通过判断在这个时间之前或者之后进行转发。比如我们现在设置只有在2019年1月1日才会转发到我的网站，在这之前不进行转发，我就可以这样配置：

```
spring:
  cloud:
    gateway:
      routes:
       - id: time_route
        uri: http://ityouknow.com
        predicates:
         - After=2018-01-20T06:06:06+08:00[Asia/Shanghai]
```

Spring 是通过 ZonedDateTime 来对时间进行的对比，ZonedDateTime 是 Java 8 中日期时间功能里，用于表示带时区的日期与时间信息的类，ZonedDateTime 支持通过时区来设置时间，中国的时区是：`Asia/Shanghai`。

After Route Predicate 是指在这个时间之后的请求都转发到目标地址。上面的示例是指，请求时间在 2018年1月20日6点6分6秒之后的所有请求都转发到地址`http://ityouknow.com`。`+08:00`是指时间和UTC时间相差八个小时，时间地区为`Asia/Shanghai`。

添加完路由规则之后，访问地址`http://localhost:8080`会自动转发到`http://ityouknow.com`。

Before Route Predicate 刚好相反，在某个时间之前的请求的请求都进行转发。我们把上面路由规则中的 After 改为 Before，如下：

```
spring:
  cloud:
    gateway:
      routes:
       - id: after_route
        uri: http://ityouknow.com
        predicates:
         - Before=2018-01-20T06:06:06+08:00[Asia/Shanghai]
```

就表示在这个时间之前可以进行路由，在这时间之后停止路由，修改完之后重启项目再次访问地址`http://localhost:8080`，页面会报 404 没有找到地址。

除过在时间之前或者之后外，Gateway 还支持限制路由请求在某一个时间段范围内，可以使用 Between Route Predicate 来实现。

```
spring:
  cloud:
    gateway:
      routes:
       - id: after_route
        uri: http://ityouknow.com
        predicates:
         - Between=2018-01-20T06:06:06+08:00[Asia/Shanghai], 2019-01-20T06:06:06+08:00[Asia/Shanghai]
```

这样设置就意味着在这个时间段内可以匹配到此路由，超过这个时间段范围则不会进行匹配。通过时间匹配路由的功能很酷，可以用在限时抢购的一些场景中。

### 通过 Cookie 匹配

Cookie Route Predicate 可以接收两个参数，一个是 Cookie name ,一个是正则表达式，路由规则会通过获取对应的 Cookie name 值和正则表达式去匹配，如果匹配上就会执行路由，如果没有匹配上则不执行。

```
spring:
  cloud:
    gateway:
      routes:
       - id: cookie_route
         uri: http://ityouknow.com
         predicates:
         - Cookie=ityouknow, kee.e
```

使用 curl 测试，命令行输入:

```
curl http://localhost:8080 --cookie "ityouknow=kee.e"
```

则会返回页面代码，如果去掉`--cookie "ityouknow=kee.e"`，后台汇报 404 错误。

### 通过 Header 属性匹配

Header Route Predicate 和 Cookie Route Predicate 一样，也是接收 2 个参数，一个 header 中属性名称和一个正则表达式，这个属性值和正则表达式匹配则执行。

```
spring:
  cloud:
    gateway:
      routes:
      - id: header_route
        uri: http://ityouknow.com
        predicates:
        - Header=X-Request-Id, \d+
```

使用 curl 测试，命令行输入:

```
curl http://localhost:8080  -H "X-Request-Id:666666" 
```

则返回页面代码证明匹配成功。将参数`-H "X-Request-Id:666666"`改为`-H "X-Request-Id:neo"`再次执行时返回404证明没有匹配。

### 通过 Host 匹配

Host Route Predicate 接收一组参数，一组匹配的域名列表，这个模板是一个 ant 分隔的模板，用`.`号作为分隔符。它通过参数中的主机地址作为匹配规则。

```
spring:
  cloud:
    gateway:
      routes:
      - id: host_route
        uri: http://ityouknow.com
        predicates:
        - Host=**.ityouknow.com
```

使用 curl 测试，命令行输入:

```
curl http://localhost:8080  -H "Host: www.ityouknow.com" 
curl http://localhost:8080  -H "Host: md.ityouknow.com" 
```

经测试以上两种 host 均可匹配到 host_route 路由，去掉 host 参数则会报 404 错误。

### 通过请求方式匹配

可以通过是 POST、GET、PUT、DELETE 等不同的请求方式来进行路由。

```
spring:
  cloud:
    gateway:
      routes:
      - id: method_route
        uri: http://ityouknow.com
        predicates:
        - Method=GET
```

使用 curl 测试，命令行输入:

```
# curl 默认是以 GET 的方式去请求
curl http://localhost:8080
```

测试返回页面代码，证明匹配到路由，我们再以 POST 的方式请求测试。

```
# curl 默认是以 GET 的方式去请求
curl -X POST http://localhost:8080
```

返回 404 没有找到，证明没有匹配上路由

### 通过请求路径匹配

Path Route Predicate 接收一个匹配路径的参数来判断是否走路由。

```
spring:
  cloud:
    gateway:
      routes:
      - id: host_route
        uri: http://ityouknow.com
        predicates:
        - Path=/foo/{segment}
```

如果请求路径符合要求，则此路由将匹配，例如：/foo/1 或者 /foo/bar。

使用 curl 测试，命令行输入:

```
curl http://localhost:8080/foo/1
curl http://localhost:8080/foo/xx
curl http://localhost:8080/boo/xx
```

经过测试第一和第二条命令可以正常获取到页面返回值，最后一个命令报404，证明路由是通过指定路由来匹配。

### 通过请求参数匹配

Query Route Predicate 支持传入两个参数，一个是属性名一个为属性值，属性值可以是正则表达式。

```
spring:
  cloud:
    gateway:
      routes:
      - id: query_route
        uri: http://ityouknow.com
        predicates:
        - Query=smile
```

这样配置，只要请求中包含 smile 属性的参数即可匹配路由。

使用 curl 测试，命令行输入:

```
curl localhost:8080?smile=x&id=2
```

经过测试发现只要请求汇总带有 smile 参数即会匹配路由，不带 smile 参数则不会匹配。

还可以将 Query 的值以键值对的方式进行配置，这样在请求过来时会对属性值和正则进行匹配，匹配上才会走路由。

```
spring:
  cloud:
    gateway:
      routes:
      - id: query_route
        uri: http://ityouknow.com
        predicates:
        - Query=keep, pu.
```

这样只要当请求中包含 keep 属性并且参数值是以 pu 开头的长度为三位的字符串才会进行匹配和路由。

使用 curl 测试，命令行输入:

```
curl localhost:8080?keep=pub
```

测试可以返回页面代码，将 keep 的属性值改为 pubx 再次访问就会报 404,证明路由需要匹配正则表达式才会进行路由。

### 通过请求 ip 地址进行匹配

Predicate 也支持通过设置某个 ip 区间号段的请求才会路由，RemoteAddr Route Predicate 接受 cidr 符号(IPv4 或 IPv6 )字符串的列表(最小大小为1)，例如 192.168.0.1/16 (其中 192.168.0.1 是 IP 地址，16 是子网掩码)。

```
spring:
  cloud:
    gateway:
      routes:
      - id: remoteaddr_route
        uri: http://ityouknow.com
        predicates:
        - RemoteAddr=192.168.1.1/24
```

可以将此地址设置为本机的 ip 地址进行测试。

```
curl localhost:8080
```

果请求的远程地址是 192.168.1.10，则此路由将匹配。

### 组合使用

上面为了演示各个 Predicate 的使用，我们是单个单个进行配置测试，其实可以将各种 Predicate 组合起来一起使用。

例如：

```
spring:
  cloud:
    gateway:
      routes:
       - id: host_foo_path_headers_to_httpbin
        uri: http://ityouknow.com
        predicates:
        - Host=**.foo.org
        - Path=/headers
        - Method=GET
        - Header=X-Request-Id, \d+
        - Query=foo, ba.
        - Query=baz
        - Cookie=chocolate, ch.p
        - After=2018-01-20T06:06:06+08:00[Asia/Shanghai]
```

各种 Predicates 同时存在于同一个路由时，请求必须同时满足所有的条件才被这个路由匹配。

> 一个请求满足多个路由的谓词条件时，请求只会被首个成功匹配的路由转发

## 总结

通过今天的学习发现 Spring Cloud Gateway 使用非常的灵活，可以根据不同的情况来进行路由分发，在实际项目中可以自由组合使用。同时 Spring Cloud Gateway 还有更多很酷的功能，比如 Filter 、熔断和限流等，下次我们继续学习 Spring Cloud Gateway 的高级功能。

# springcloud(十六)：服务网关 Spring Cloud GateWay 服务化和过滤器

上一篇文章[服务网关 Spring Cloud GateWay 初级篇](http://www.ityouknow.com/springcloud/2018/12/12/spring-cloud-gateway-start.html)，介绍了 Spring Cloud Gateway 的相关术语、技术原理，以及如何快速使用 Spring Cloud Gateway。这篇文章我们继续学习 Spring Cloud Gateway 的高级使用方式，比如如何配置服务中心来使用，如何使用熔断、限流等高级功能。

## 注册中心

上篇主要讲解了网关代理单个服务的使用语法，在实际的工作中，服务的相互调用都是依赖于服务中心提供的入口来使用，服务中心往往注册了很多服务，如果每个服务都需要单独配置的话，这将是一份很枯燥的工作。Spring Cloud Gateway 提供了一种默认转发的能力，只要将 Spring Cloud Gateway 注册到服务中心，Spring Cloud Gateway 默认就会代理服务中心的所有服务，下面用代码演示。

### 准备服务和注册中心

在介绍[服务网关 zuul 的使用](http://www.ityouknow.com/springcloud/2017/06/01/gateway-service-zuul.html)时，提供了 spring-cloud-eureka 、spring-cloud-producer 项目示例，本次演示我们将两个项目版本升级到 `Finchley.SR2` 后继续演示使用。

spring-cloud-eureka(Eureka Server) 的 pom 文件更改，其它依赖包不变。

升级前：

```
<dependency>
    <groupId>org.springframework.cloud</groupId>
    <artifactId>spring-cloud-starter-eureka-server</artifactId>
</dependency>
```

升级后：

```
<dependency>
    <groupId>org.springframework.cloud</groupId>
    <artifactId>spring-cloud-starter-netflix-eureka-server</artifactId>
</dependency>
```

spring-cloud-producer(Eureka Client)的 pom 文件更改。因为配置中心需要作为服务注册到注册中心，所以需要升级 Eureka Client，其他依赖没有变动。

升级前：

```
<dependency>
    <groupId>org.springframework.cloud</groupId>
    <artifactId>spring-cloud-starter-eureka</artifactId>
</dependency>
```

升级后：

```
<dependency>
    <groupId>org.springframework.cloud</groupId>
    <artifactId>spring-cloud-starter-netflix-eureka-client</artifactId>
</dependency>
```

两个项目升级完依赖包后依次重启，访问注册中心地址 `http://localhost:8000/` 即可看到名为 `SPRING-CLOUD-PRODUCER`的服务。

### 服务网关注册到注册中心

复制上一节的示例项目 [cloud-gateway](http://www.ityouknow.com/springcloud/2018/12/12/spring-cloud-gateway-start.html) 重新命名为 cloud-gateway-eureka，添加 eureka 的客户端依赖包。

```
<dependency>
    <groupId>org.springframework.cloud</groupId>
    <artifactId>spring-cloud-starter-netflix-eureka-client</artifactId>
</dependency>
```

修改 application.yml 配置文件内容如下

```
server:
  port: 8888
spring:
  application:
    name: cloud-gateway-eureka
  cloud:
    gateway:
     discovery:
        locator:
         enabled: true
eureka:
  client:
    service-url:
      defaultZone: http://localhost:8000/eureka/
logging:
  level:
    org.springframework.cloud.gateway: debug
```

配置说明：

- `spring.cloud.gateway.discovery.locator.enabled`：是否与服务注册于发现组件进行结合，通过 serviceId 转发到具体的服务实例。默认为 false，设为 true 便开启通过服务中心的自动根据 serviceId 创建路由的功能。
- `eureka.client.service-url.defaultZone`指定注册中心的地址，以便使用服务发现功能
- `logging.level.org.springframework.cloud.gateway` 调整相 gateway 包的 log 级别，以便排查问题

修改完成后启动 cloud-gateway-eureka 项目，访问注册中心地址 `http://localhost:8000/` 即可看到名为 `CLOUD-GATEWAY-EUREKA`的服务。

### 测试

将 Spring Cloud Gateway 注册到服务中心之后，网关会自动代理所有的在注册中心的服务，访问这些服务的语法为：

```
http://网关地址：端口/服务中心注册 serviceId/具体的url
```

比如我们的 spring-cloud-producer 项目有一个 `/hello` 的服务，访问此服务的时候会返回：hello world。

比如访问地址：`http://localhost:9000/hello`，页面返回：hello world!

按照上面的语法我们通过网关来访问，浏览器输入：`http://localhost:8888/SPRING-CLOUD-PRODUCER/hello` 同样返回：hello world!证明服务网关转发成功。

我们将项目 spring-cloud-producer 复制一份为 spring-cloud-producer-1，将`/hello`服务的返回值修改为 hello world smile !，修改端口号为 9001 ，修完完成后重启，这时候访问注册中心后台会发现有两个名为 `SPRING-CLOUD-PRODUCER`的服务。

在浏览器多次访问地址：`http://localhost:8888/SPRING-CLOUD-PRODUCER/hello`，页面交替返回以下信息：

```
hello world!
hello world smile!
```

说明后端服务自动进行了均衡负载。

## 基于 Filter(过滤器) 实现的高级功能

在[服务网关Zuul高级篇](http://www.ityouknow.com/springcloud/2018/01/20/spring-cloud-zuul.html)中大概介绍过 Filter 的概念。

Spring Cloud Gateway 的 Filter 的生命周期不像 Zuul 的那么丰富，它只有两个：“pre” 和 “post”。

- **PRE**： 这种过滤器在请求被路由之前调用。我们可利用这种过滤器实现身份验证、在集群中选择请求的微服务、记录调试信息等。
- **POST**：这种过滤器在路由到微服务以后执行。这种过滤器可用来为响应添加标准的 HTTP Header、收集统计信息和指标、将响应从微服务发送给客户端等。

Spring Cloud Gateway 的 Filter 分为两种：GatewayFilter 与 GlobalFilter。GlobalFilter 会应用到所有的路由上，而 GatewayFilter 将应用到单个路由或者一个分组的路由上。

Spring Cloud Gateway 内置了9种 GlobalFilter，比如 Netty Routing Filter、LoadBalancerClient Filter、Websocket Routing Filter 等，根据名字即可猜测出这些 Filter 的作者，具体大家可以参考官网内容：[Global Filters](http://cloud.spring.io/spring-cloud-gateway/single/spring-cloud-gateway.html#_global_filters)

利用 GatewayFilter 可以修改请求的 Http 的请求或者响应，或者根据请求或者响应做一些特殊的限制。 更多时候我们会利用 GatewayFilter 做一些具体的路由配置，下面我们做一些简单的介绍。

### 快速上手 Filter 使用

我们以 AddRequestParameter GatewayFilter 来演示一下，如何在项目中使用 GatewayFilter，AddRequestParameter GatewayFilter 可以在请求中添加指定参数。

**application.yml配置示例**

```
spring:
  cloud:
    gateway:
      routes:
      - id: add_request_parameter_route
        uri: http://example.org
        filters:
        - AddRequestParameter=foo, bar
```

这样就会给匹配的每个请求添加上`foo=bar`的参数和值。

我们将以上配置融入到 cloud-gateway-eureka 项目中，完整的 `application.yml` 文件配置信息如下：

```
server:
  port: 8888
spring:
  application:
    name: cloud-gateway-eureka
  cloud:
    gateway:
     discovery:
        locator:
         enabled: true
     routes:
     - id: add_request_parameter_route
       uri: http://localhost:9000
       filters:
       - AddRequestParameter=foo, bar
       predicates:
         - Method=GET
eureka:
  client:
    service-url:
      defaultZone: http://localhost:8000/eureka/
logging:
  level:
    org.springframework.cloud.gateway: debug
```

这里的 routes 手动指定了服务的转发地址，设置所有的 GET 方法都会自动添加`foo=bar`，`http://localhost:9000` 是 spring-cloud-producer 项目，我们在此项目中添加一个 foo() 方法，用来接收转发中添加的参数 foo。

```
@RequestMapping("/foo")
public String foo(String foo) {
    return "hello "+foo+"!";
}
```

修改完成后重启 cloud-gateway-eureka、spring-cloud-producer 项目。访问地址`http://localhost:9000/foo`页面返回：hello null!，说明并没有接受到参数 foo；通过网关来调用此服务，浏览器访问地址`http://localhost:8888/foo`页面返回：hello bar!，说明成功接收到参数 foo 参数的值 bar ,证明网关在转发的过程中已经通过 filter 添加了设置的参数和值。

### 服务化路由转发

上面我们使用 uri 指定了一个服务转发地址，单个服务这样使用问题不大，但是我们在注册中心往往会使用多个服务来共同支撑整个服务的使用，这个时候我们就期望可以将 Filter 作用到每个应用的实例上，spring cloud gateway 工了这样的功能，只需要简单配置即可。

为了测试两个服务提供者是否都被调用，我们在 spring-cloud-producer-1 项目中也同样添加 foo() 方法。

```
@RequestMapping("/foo")
public String foo(String foo) {
    return "hello "+foo+"!!";
}
```

为了和 spring-cloud-producer 中 foo() 方法有所区别，这里使用了两个感叹号。同时将 cloud-gateway-eureka 项目配置文件中的 uri 内容修改如下：

```
#格式为：lb://应用注册服务名
uri: lb://spring-cloud-producer
```

修改完之后，重新启动项目 cloud-gateway-eureka、spring-cloud-producer-1，浏览器访问地址:`http://localhost:8888/foo`页面交替出现：

```
hello bar!
hello bar!!
```

证明请求依据均匀转发到后端服务，并且后端服务均接收到了 filter 增加的参数 foo 值。

这里其实默认使用了全局过滤器 LoadBalancerClient ，当路由配置中 uri 所用的协议为 lb 时（以uri: lb://spring-cloud-producer为例），gateway 将使用 LoadBalancerClient 把 spring-cloud-producer 通过 eureka 解析为实际的主机和端口，并进行负载均衡。

下篇再给大家介绍集中比较常用的 Filter 功能。

# springcloud(十七)：服务网关 Spring Cloud GateWay 熔断、限流、重试

 2019/01/26

上篇文章介绍了 Gataway 和注册中心的使用，以及 Gataway 中 Filter 的基本使用，这篇文章我们将继续介绍 Filter 的一些常用功能。

## 修改请求路径的过滤器

**StripPrefix Filter**

StripPrefix Filter 是一个请求路径截取的功能，我们可以利用这个功能来做特殊业务的转发。

application.yml 配置如下：

```
spring:
  cloud:
    gateway:
      routes:
      - id: nameRoot
        uri: http://nameservice
        predicates:
        - Path=/name/**
        filters:
        - StripPrefix=2
```

上面这个配置的例子表示，当请求路径匹配到`/name/**`会将包含name和后边的字符串接去掉转发， `StripPrefix=2`就代表截取路径的个数，这样配置后当请求`/name/bar/foo`后端匹配到的请求路径就会变成`http://nameservice/foo`。

我们还是在 cloud-gateway-eureka 项目中进行测试，修改 application.yml 如下：

```
spring:
  cloud:
     routes:
     - id: nameRoot
       uri: lb://spring-cloud-producer
       predicates:
       - Path=/name/**
       filters:
       - StripPrefix=2
```

配置完后重启 cloud-gateway-eureka 项目，访问地址：`http://localhost:8888/name/foo/hello`页面会交替显示：

```
hello world!
hello world smile!
```

和直接访问地址 `http://localhost:8888/hello`展示的效果一致，说明请求路径中的 `name/foo/` 已经被截取。

**PrefixPath Filter**

PrefixPath Filter 的作用和 StripPrefix 正相反，是在 URL 路径前面添加一部分的前缀

```
spring:
  cloud:
    gateway:
      routes:
      - id: prefixpath_route
        uri: http://example.org
        filters:
        - PrefixPath=/mypath
```

大家可以下来去测试，这里不在演示。

## 限速路由器

限速在高并发场景中比较常用的手段之一，可以有效的保障服务的整体稳定性，Spring Cloud Gateway 提供了基于 Redis 的限流方案。所以我们首先需要添加对应的依赖包`spring-boot-starter-data-redis-reactive`

```
<dependency>
  <groupId>org.springframework.cloud</groupId>
  <artifactId>spring-boot-starter-data-redis-reactive</artifactId>
</dependency>
```

配置文件中需要添加 Redis 地址和限流的相关配置

```
spring:
  application:
    name: cloud-gateway-eureka
  redis:
    host: localhost
    password:
    port: 6379
  cloud:
    gateway:
     discovery:
        locator:
         enabled: true
     routes:
     - id: requestratelimiter_route
       uri: http://example.org
       filters:
       - name: RequestRateLimiter
         args:
           redis-rate-limiter.replenishRate: 10
           redis-rate-limiter.burstCapacity: 20
           key-resolver: "#{@userKeyResolver}"
       predicates:
         - Method=GET
```

- filter 名称必须是 RequestRateLimiter
- redis-rate-limiter.replenishRate：允许用户每秒处理多少个请求
- redis-rate-limiter.burstCapacity：令牌桶的容量，允许在一秒钟内完成的最大请求数
- key-resolver：使用 SpEL 按名称引用 bean

项目中设置限流的策略，创建 Config 类。

```
public class Config {

    @Bean
    KeyResolver userKeyResolver() {
        return exchange -> Mono.just(exchange.getRequest().getQueryParams().getFirst("user"));
    }
}
```

根据请求参数中的 user 字段来限流，也可以设置根据请求 IP 地址来限流，设置如下:

```
@Bean
public KeyResolver ipKeyResolver() {
    return exchange -> Mono.just(exchange.getRequest().getRemoteAddress().getHostName());
}
```

这样网关就可以根据不同策略来对请求进行限流了。

## 熔断路由器

在之前的 Spring Cloud 系列文章中，大家对熔断应该有了一定的了解，如过不了解可以先读这篇文章：[熔断器 Hystrix](http://www.ityouknow.com/springcloud/2017/05/16/springcloud-hystrix.html)

Spring Cloud Gateway 也可以利用 Hystrix 的熔断特性，在流量过大时进行服务降级，同样我们还是首先给项目添加上依赖。

```
<dependency>
  <groupId>org.springframework.cloud</groupId>
  <artifactId>spring-cloud-starter-netflix-hystrix</artifactId>
</dependency>
```

配置示例

```
spring:
  cloud:
    gateway:
      routes:
      - id: hystrix_route
        uri: http://example.org
        filters:
        - Hystrix=myCommandName
```

配置后，gateway 将使用 myCommandName 作为名称生成 HystrixCommand 对象来进行熔断管理。如果想添加熔断后的回调内容，需要在添加一些配置。

```
spring:
  cloud:
    gateway:
      routes:
      - id: hystrix_route
        uri: lb://spring-cloud-producer
        predicates:
        - Path=/consumingserviceendpoint
        filters:
        - name: Hystrix
          args:
            name: fallbackcmd
            fallbackUri: forward:/incaseoffailureusethis
```

`fallbackUri: forward:/incaseoffailureusethis`配置了 fallback 时要会调的路径，当调用 Hystrix 的 fallback 被调用时，请求将转发到`/incaseoffailureuset`这个 URI。

## 重试路由器

RetryGatewayFilter 是 Spring Cloud Gateway 对请求重试提供的一个 GatewayFilter Factory

配置示例：

```
spring:
  cloud:
    gateway:
      routes:
      - id: retry_test
        uri: lb://spring-cloud-producer
        predicates:
        - Path=/retry
        filters:
        - name: Retry
          args:
            retries: 3
            statuses: BAD_GATEWAY
```

Retry GatewayFilter 通过这四个参数来控制重试机制： retries, statuses, methods, 和 series。

- retries：重试次数，默认值是 3 次
- statuses：HTTP 的状态返回码，取值请参考：`org.springframework.http.HttpStatus`
- methods：指定哪些方法的请求需要进行重试逻辑，默认值是 GET 方法，取值参考：`org.springframework.http.HttpMethod`
- series：一些列的状态码配置，取值参考：`org.springframework.http.HttpStatus.Series`。符合的某段状态码才会进行重试逻辑，默认值是 SERVER_ERROR，值是 5，也就是 5XX(5 开头的状态码)，共有5 个值。

以上便是项目中常用的一些网关操作，更多关于 Spring Cloud GateWay 的使用请参考官网。