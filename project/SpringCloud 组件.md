> 谷粒商城
>
> SpringCloud 组件

# 一、SpringCloud Alibaba

## 1、SpringCloud Alibaba 简介

1.  **、简介**

> Spring Cloud Alibaba 致力于提供**微服务开发的一站式解决方案**。此项目包含开发分布式应用微服务的必需组件，方便开发者通过 Spring Cloud 编程模型轻松使用这些组件来开发分布式应用服务。
>
> 依托 Spring Cloud Alibaba，您只需要添加一些注解和少量配置，就可以将 Spring Cloud 应用接入阿里微服务解决方案，通过阿里中间件来迅速搭建分布式应用系统。
>
> [*https://github.com/alibaba/spring-cloud-alibaba*](https://github.com/alibaba/spring-cloud-alibaba)

2.  **、为什么使用**

![](https://raw.githubusercontent.com/xqy-power/images/main/202308101611516.jpeg)

![](https://raw.githubusercontent.com/xqy-power/images/main/202308101611517.jpeg)

#### SpringCloud 的几大痛点

> SpringCloud 部分组件停止维护和更新，给开发带来不便；
>
> SpringCloud 部分环境搭建复杂，没有完善的可视化界面，我们需要大量的二次开发和定制
>
> SpringCloud 配置复杂，难以上手，部分配置差别难以区分和合理应用

#### SpringCloud Alibaba 的优势：

> 阿里使用过的组件经历了考验，性能强悍，设计合理，现在开源出来大家用 成套的产品搭配完善的可视化界面给开发运维带来极大的便利
>
> 搭建简单，学习曲线低。

#### 结合 SpringCloud Alibaba 我们最终的技术搭配方案： SpringCloud Alibaba - Nacos：注册中心（服务发现/注册） SpringCloud Alibaba - Nacos：配置中心（动态配置管理） SpringCloud - Ribbon：负载均衡

> **SpringCloud - Feign：声明式 HTTP 客户端（调用远程服务） SpringCloud Alibaba - Sentinel：服务容错（限流、降级、熔断） SpringCloud - Gateway：API 网 关 （webflux 编 程 模 式 ） SpringCloud - Sleuth：调用链监控**
>
> **SpringCloud Alibaba - Seata：原 Fescar，即分布式事务解决方案**

3.  **、版本选择**

> 由于 Spring Boot 1 和 Spring Boot 2 在 Actuator 模块的接口和注解有很大的变更，且spring-cloud-commons 从 1.x.x 版本升级到 2.0.0 版本也有较大的变更，因此我们采取跟SpringBoot 版本号一致的版本:

- 1.5.x 版本适用于 Spring Boot 1.5.x

- 2.0.x 版本适用于 Spring Boot 2.0.x

- 2.1.x 版本适用于 Spring Boot 2.1.x

## 、项目中的依赖

[TABLE]

[TABLE]

> **2、SpringCloud Alibaba-Nacos\[作为注册中心\]**
>
> Nacos 是阿里巴巴开源的一个更易于构建云原生应用的动态服务发现、配置管理和服务管理平台。他是使用 java 编写。需要依赖 java 环境
>
> Nacos 文档地址： <https://nacos.io/zh-cn/docs/quick-start.html>

## 、下载 nacos-server

> https://github.com/alibaba/nacos/releases

## 、启动 nacos-server

- 双击 bin 中的 startup.cmd 文件

- 访问 http://localhost:8848/nacos/

- ![](https://raw.githubusercontent.com/xqy-power/images/main/202308101611519.jpeg)使用默认的 nacos/nacos 进行登录

## 、将微服务注册到 nacos 中

### 1、首先，修改 pom.xml 文件，引入 Nacos Discovery Starter。

[TABLE]

[TABLE]

> **2、在应用的 /src/main/resources/application.properties 配置文件中配置 Nacos Server 地址**

| spring.cloud.nacos.discovery.server-addr=127.0.0.1:8848 |
|---------------------------------------------------------|

> **3****、使用@EnableDiscoveryClient 开启服务注册发现功能**

[TABLE]

> **4****、启动应用，观察nacos 服务列表是否已经注册上服务**

[TABLE]

> **5****、注册更多的服务上去，测试使用feign 远程调用**

[TABLE]

[TABLE]

> **6****、更多配置**
>
> [*https://github.com/alibaba/spring-cloud-alibaba/blob/master/spring-cloud-alibaba-examples/na*](https://github.com/alibaba/spring-cloud-alibaba/blob/master/spring-cloud-alibaba-examples/nacos-example/nacos-discovery-example/readme-zh.md#more) *cos-example/nacos-discovery-example/readme-zh.md#more*

## 3、SpringCloud Alibaba-Nacos\[作为配置中心\]

> **1、pom.xml 引入 Nacos Config Starter。**

[TABLE]

> **2、****在应用的 /src/main/resources/bootstrap.properties 配置文件中配置 Nacos Config 元数据**

[TABLE]

> **3、在 nacos 中添加配置**
>
> 在 nacos 中创建一个 **应用名.properties** 配置文件并编写配置

[TABLE]

## 4、在应用中使用@Value 和@RefreshScope

[TABLE]

> **5、进阶**

### 1、核心概念

[TABLE]

> **2****、原理**

[TABLE]

| **@RefreshScope 或 @ConfigurationProperties 注解，** |
|------------------------------------------------------|

> **3****、加载多配置文件**

[TABLE]

> **4****、namespace 与group 最佳实践**
>
> 每个微服务创建自己的 namespace 进行隔离，group 来区分 dev，beta，prod 等环境

## 4、SpringCloud Alibaba-Sentinel

> **1、简介**

### 1、熔断降级限流

> 什么是熔断
>
> A 服务调用 B 服务的某个功能，由于网络不稳定问题，或者 B 服务卡机，导致功能时间超长。如果这样子的次数太多。我们就可以直接将 B 断路了（A 不再请求 B 接口），凡是调用 B 的直接返回降级数据，不必等待 B 的超长执行。 这样 B 的故障问题，就不会级联影响到 A。
>
> 什么是降级
>
> 整个网站处于流量高峰期，服务器压力剧增，根据当前业务情况及流量，对一些服务和页面进行有策略的降级\[停止服务，所有的调用直接返回降级数据\]。以此缓解服务器资源的的压力，以保证核心业务的正常运行，同时也保持了客户和大部分客户的得到正确的相应。
>
> 异同：
>
> 相同点：
>
> 1、为了保证集群大部分服务的可用性和可靠性，防止崩溃，牺牲小我
>
> 2、用户最终都是体验到某个功能不可用不同点：
>
> 1、熔断是被调用方故障，触发的系统主动规则
>
> 2、降级是基于全局考虑，停止一些正常服务，释放资源
>
> 什么是限流
>
> 对打入服务的请求流量进行控制，使服务能够承担不超过自己能力的流量压力

### 2、Sentinel 简介

> 官方文档：[*https://github.com/alibaba/Sentinel/wiki/%E4%BB%8B%E7%BB%8D*](https://github.com/alibaba/Sentinel/wiki/%E4%BB%8B%E7%BB%8D) 项目地址：[*https://github.com/alibaba/Sentinel*](https://github.com/alibaba/Sentinel)
>
> 随着微服务的流行，服务和服务之间的稳定性变得越来越重要。Sentinel 以流量为切入点， 从流量控制、熔断降级、系统负载保护等多个维度保护服务的稳定性。

#### Sentinel 具有以下特征:

> **丰富的应用场景**：Sentinel 承接了阿里巴巴近 10 年的双十一大促流量的核心场景，例如秒杀（即突发流量控制在系统容量可以承受的范围）、消息削峰填谷、集群流量控制、实时熔断下游不可用应用等。
>
> **完备的实时监控**：Sentinel 同时提供实时的监控功能。您可以在控制台中看到接入应用的单台机器秒级数据，甚至 500 台以下规模的集群的汇总运行情况。
>
> **广泛的开源生态**：Sentinel 提供开箱即用的与其它开源框架/库的整合模块，例如与 Spring Cloud、Dubbo、gRPC 的整合。您只需要引入相应的依赖并进行简单的配置即可快速地接入 Sentinel。
>
> **完善的 SPI 扩展点**：Sentinel 提供简单易用、完善的 SPI 扩展接口。您可以通过实现扩展接口来快速地定制逻辑。例如定制规则管理、适配动态数据源等。

![](https://raw.githubusercontent.com/xqy-power/images/main/202308101611520.png)

#### Sentinel 分为两个部分:

- 核心库（Java 客户端）不依赖任何框架/库，能够运行于所有 Java 运行时环境，同时对 Dubbo / Spring Cloud 等框架也有较好的支持。

- 控制台（Dashboard）基于 Spring Boot 开发，打包后可以直接运行，不需要额外的

> Tomcat 等应用容器。

#### Sentinel 基本概念

- 资源

> 资源是 Sentinel 的关键概念。它可以是 Java 应用程序中的任何内容，例如，由应用程序提供的服务，或由应用程序调用的其它应用提供的服务，甚至可以是一段代码。在接下来的文档中，我们都会用资源来描述代码块。
>
> **只要通过 Sentinel API 定义的代码，就是资源，能够被 Sentinel 保护起来**。大部分情况下， 可以使用方法签名，URL，甚至服务名称作为资源名来标示资源。

- 规则

> 围绕资源的实时状态设定的规则，可以包括**流量控制规则**、**熔断降级规则**以及**系统保护规 则**。所有规则可以动态实时调整。

## 2、Hystrix 与 Sentinel 比较

![](https://raw.githubusercontent.com/xqy-power/images/main/202308101611521.jpeg)

> **3、整合 Feign+Sentinel 测试熔断降级**
>
> <https://github.com/alibaba/Sentinel/wiki/%E4%B8%BB%E9%A1%B5>

#### 什么是熔断降级

> 除了流量控制以外，降低调用链路中的不稳定资源也是 Sentinel 的使命之一。由于调用关系的复杂性，如果调用链路中的某个资源出现了不稳定，最终会导致请求发生堆积。
>
> ![](https://raw.githubusercontent.com/xqy-power/images/main/202308101611522.jpeg)
>
> Sentinel 和 Hystrix 的原则是一致的: 当检测到调用链路中某个资源出现不稳定的表现，例如请求响应时间长或异常比例升高的时候，则对这个资源的调用进行限制，让请求快速失败， 避免影响到其它的资源而导致级联故障。

#### 熔断降级设计理念

> 在限制的手段上，Sentinel 和 Hystrix 采取了完全不一样的方法。
>
> Hystrix 通过 线程池隔离 的方式，来对依赖（在 Sentinel 的概念中对应 资源）进行了隔离。这样做的好处是资源和资源之间做到了最彻底的隔离。缺点是除了增加了线程切换的成 本（过多的线程池导致线程数目过多），还需要预先给各个资源做线程池大小的分配。
>
> *Sentinel 对这个问题采取了两种手段:*

- 通过并发线程数进行限制

> 和资源池隔离的方法不同，Sentinel 通过限制资源并发线程的数量，来减少不稳定资源对其它资源的影响。这样不但没有线程切换的损耗，也不需要您预先分配线程池的大小。当某个 资源出现不稳定的情况下，例如响应时间变长，对资源的直接影响就是会造成线程数的逐步 堆积。当线程数在特定资源上堆积到一定的数量之后，对该资源的新请求就会被拒绝。堆积的线程完成任务后才开始继续接收请求。

- 通过响应时间对资源进行降级

> 除了对并发线程数进行控制以外，Sentinel 还可以通过响应时间来快速降级不稳定的资源。当依赖的资源出现响应时间过长后，所有对该资源的访问都会被直接拒绝，直到过了指定的时间窗口之后才重新恢复。
>
> 整合测试：
>
> [*https://github.com/alibaba/spring-cloud-alibaba/blob/master/spring-cloud-alibaba-examples/se*](https://github.com/alibaba/spring-cloud-alibaba/blob/master/spring-cloud-alibaba-examples/sentinel-example/sentinel-feign-example/readme-zh.md) *ntinel-example/sentinel-feign-example/readme-zh.md*

#### 1、引入依赖

> **2、使用 Nacos 注册中心**
>
> **3、定义 fallback 实现**

[TABLE]

> **4、定义 fallbackfactory 并放在容器中**

[TABLE]

> **5、改造 fallback 类接受异常并实现容错方法**

[TABLE]

[TABLE]

> **6、远程接口配置 feign 客户端容错**

[TABLE]

> 7、开启 sentinel 代理 feign 功能；在 application.properties 中配置

| **feign.sentinel.enabled**=**true** |
|-------------------------------------|

> 测试熔断效果。当远程服务出现问题，会自动调用回调方法返回默认数据，并且
>
> 更快的容错方式

#### 1、使用@SentinelResource，并定义 fallback

[TABLE]

| ![](https://raw.githubusercontent.com/xqy-power/images/main/202308101611523.jpeg) |
| ------------------------------------------------------------ |

> **2、测试降级效果**
>
> 当远程服务停止，前几个服务会尝试调用远程服务，满足降级策略条件以后则不会再尝试调 用远程服务

## 4、整合 Sentinel 测试限流（流量控制）

> [*https://github.com/alibaba/spring-cloud-alibaba/blob/master/spring-cloud-alibaba-examples/se*](https://github.com/alibaba/spring-cloud-alibaba/blob/master/spring-cloud-alibaba-examples/sentinel-example/sentinel-core-example/readme-zh.md) *ntinel-example/sentinel-core-example/readme-zh.md*

#### 什么是流量控制

> 流量控制在网络传输中是一个常用的概念，它用于调整网络包的发送数据。然而，从系统稳 定性角度考虑，在处理请求的速度上，也有非常多的讲究。任意时间到来的请求往往是随机 不可控的，而系统的处理能力是有限的。我们需要根据系统的处理能力对流量进行控制。Sentinel 作为一个调配器，可以根据需要把随机的请求调整成合适的形状，如下图所示：

![](https://raw.githubusercontent.com/xqy-power/images/main/202308101611524.jpeg)

#### 流量控制设计理念

> 流量控制有以下几个角度:

- 资源的调用关系，例如资源的调用链路，资源和资源之间的关系；

- 运行指标，例如 QPS、线程池、系统负载等；

- 控制的效果，例如直接限流、冷启动、排队等。

> Sentinel 的设计理念是让您自由选择控制的角度，并进行灵活组合，从而达到想要的效果。

#### 1、引入 Sentinel starter

[TABLE]

> **2、接入限流埋点**

- HTTP 埋点

> Sentinel starter 默认为所有的 HTTP 服务提供了限流埋点，如果只想对 HTTP 服务进行限流，那么只需要引入依赖，无需修改代码。

- 自定义埋点

> 如果需要对某个特定的方法进行限流或降级，可以通过 @SentinelResource 注解来完成限流的埋点，示例代码如下：
>
> @SentinelResource("resource") public String hello() {
>
> return "Hello";
>
> }
>
> 当然也可以通过原始的 SphU.entry(xxx) 方法进行埋点， 可以参见 Sentinel 文档
>
> （ https://github.com/alibaba/Sentinel/wiki/%E5%A6%82%E4%BD%95%E4%BD%BF%E7%94%A8 \#%E5%AE%9A%E4%B9%89%E8%B5%84%E6%BA%90）。

#### 3、配置限流规则

> Sentinel 提供了两种配置限流规则的方式：代码配置 和 控制台配置。

[TABLE]

[TABLE]

#### 4、启动应用并配置

[TABLE]

> **5、控制台配置限流规则并验证**

[TABLE]

[TABLE]

> **6、自定义流控响应**

| ![](https://raw.githubusercontent.com/xqy-power/images/main/202308101611525.jpeg) |
| ------------------------------------------------------------ |

> **7、持久化流控规则**
>
> 默认的流控规则是保存在项目的内存中，项目停止再启动，流控规则就是失效。我们可以持 久 化 保 存 规 则 ； [*https://github.com/alibaba/Sentinel/wiki/%E5%8A%A8%E6%80%81%E8%A7%84%E5%88%99%E*](https://github.com/alibaba/Sentinel/wiki/%E5%8A%A8%E6%80%81%E8%A7%84%E5%88%99%E6%89%A9%E5%B1%95#datasource-%E6%89%A9%E5%B1%95) *6%89%A9%E5%B1%95#datasource-%E6%89%A9%E5%B1%95*
>
> 生产环境使用模式：

#### 我们推荐 通过控制台设置规则后将规则推送到统一的规则中心， 客户端实现

> **ReadableDataSource 接口端监听规则中心实时获取变更，**

![](https://raw.githubusercontent.com/xqy-power/images/main/202308101611526.png)

> 解决方案：
>
> DataSource 扩展常见的实现方式有:

- **拉模式：**客户端主动向某个规则管理中心定期轮询拉取规则，这个规则中心可以是

> RDBMS、文件，甚至是 VCS 等。这样做的方式是简单，缺点是无法及时获取变更；

- **推模式：**规则中心统一推送，客户端通过注册监听器的方式时刻监听变化，比如使用

> Nacos、Zookeeper 等配置中心。这种方式有更好的实时性和一致性保证。

[TABLE]

[TABLE]

[TABLE]

[TABLE]

## 5、SpringCloud Alibaba-Seata

> **1、简介**
>
> Seata 是一款开源的分布式事务解决方案，致力于在微服务架构下提供高性能和简单易用的分布式事务服务。
>
> [*https://seata.io/zh-cn/*](https://seata.io/zh-cn/)

## 2、核心概念

- TC - 事务协调者

> 维护全局和分支事务的状态，驱动全局事务提交或回滚。

- TM - 事务管理器

> 定义全局事务的范围：开始全局事务、提交或回滚全局事务。

- RM - 资源管理器

> 管理分支事务处理的资源，与 TC 交谈以注册分支事务和报告分支事务的状态，并驱动分支事务提交或回滚。
>
> ![](https://raw.githubusercontent.com/xqy-power/images/main/202308101611527.png)工作原理：

## 3、使用步骤（测试 AT 模式）

### 1、为每个服务创建undo_log 表

[TABLE]

> **2****、需要分布式事务的服务导入seata-starter**

[TABLE]

> **3****、使用seata 数据源代理原数据源**

[TABLE]

> **4****、给微服务加入file.conf 和registry.conf**

[TABLE]

[TABLE]

[TABLE]

[TABLE]

> **5****、启动seata 服务器**

| 从 [*https://github.com/seata/seata/releases*](https://github.com/seata/seata/releases) ,下载服务器软件包，将其解压缩。 |
|-------------------------------------------------------------------------------------------------------------------------|

> **6****、使用事务注解**
>
> @GlobalTransactional：标注在总事务中，其他分支事务，继续使用@Transactional 即可

### 7、测试回滚效果

> 测试本地事务出现问题后，远程事务是否可以回滚

### 8、官方更多示例

| [*https://github.com/seata/seata-samples/tree/master/springcloud-nacos-seata*](https://github.com/seata/seata-samples/tree/master/springcloud-nacos-seata) 整合 nacos      |
|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| [*https://github.com/seata/seata-samples/tree/master/springcloud-jpa-seata*](https://github.com/seata/seata-samples/tree/master/springcloud-jpa-seata) 整合 jpa            |
| [*https://github.com/seata/seata-samples/tree/master/springboot-dubbo-seata*](https://github.com/seata/seata-samples/tree/master/springboot-dubbo-seata) 整合 dubbo        |
| [*https://github.com/seata/seata-samples/tree/master/springboot-shardingsphere-seata*](https://github.com/seata/seata-samples/tree/master/springboot-shardingsphere-seata) |

> **6、SpringCloud Alibaba-OSS**
>
> **1、简介**
>
> 对象存储服务（Object Storage Service，OSS）是一种海量、安全、低成本、高可靠的云存储服务，适合存放任意类型的文件。容量和处理能力弹性扩展，多种存储类型供选择，全面优化存储成本。

## 2、使用步骤

### 1、开通阿里云对象存储服务

![](https://raw.githubusercontent.com/xqy-power/images/main/202308101611528.jpeg)

> [*https://www.aliyun.com/product/oss*](https://www.aliyun.com/product/oss)

### 2、引入SpringCloud Alibaba-OSS

[TABLE]

> **4****、配置阿里云oss 相关的账号信息**

[TABLE]

> 注意：必须申请 RAM 账号信息，并且分配 OSS 操作权限

### 5、测试使用OssClient 上传

[TABLE]

> **二、SpringCloud**
>
> **1、Feign 声明式远程调用**
>
> **1、简介**
>
> Feign 是一个声明式的 HTTP 客户端，它的目的就是让远程调用更加简单。Feign 提供了 HTTP 请求的模板，**通过编写简单的接口和插入注解**，就可以定义好 HTTP 请求的参数、格式、地址等信息。
>
> Feign 整合了 **Ribbon（负载均衡）**和 **Hystrix(服务熔断)**，可以让我们不再需要显式地使用这两个组件。
>
> SpringCloudFeign 在 NetflixFeign 的基础上扩展了对 SpringMVC 注解的支持，在其实现下，我们只需创建一个接口并用注解的方式来配置它，即可完成对服务提供方的接口绑定。简化了SpringCloudRibbon 自行封装服务调用客户端的开发量。

## 2、使用

[TABLE]

[TABLE]

> **3、原理**

![](https://raw.githubusercontent.com/xqy-power/images/main/202308101611529.jpeg)

> **2、Gateway**
>
> **1、简介**
>
> 网关作为流量的入口，常用功能包括路由转发、权限校验、限流控制等。而 springcloud gateway
>
> 作为 SpringCloud 官方推出的第二代网关框架，取代了 Zuul 网关。
>
> ![](https://raw.githubusercontent.com/xqy-power/images/main/202308101611530.jpeg)
>
> 网关提供 API 全托管服务，丰富的 API 管理功能，辅助企业管理大规模的 API，以降低管理成本和安全风险，包括协议适配、协议转发、安全策略、防刷、流量、监控日志等功能。
>
> Spring Cloud Gateway 旨在提供一种简单而有效的方式来对 API 进行路由，并为他们提供切面，例如：安全性，监控/指标 和弹性等。
>
> 官方文档地址：
>
> [*https://cloud.spring.io/spring-cloud-static/spring-cloud-gateway/2.1.3.RELEASE/single/spring-clo*](https://cloud.spring.io/spring-cloud-static/spring-cloud-gateway/2.1.3.RELEASE/single/spring-cloud-gateway.html) *ud-gateway.html*
>
> Spring Cloud Gateway 特点:

- 基于 Spring5，支持响应式编程和 SpringBoot2.0

- 支持使用任何请求属性进行路由匹配

- 特定于路由的断言和过滤器

- 集成 Hystrix 进行断路保护

- 集成服务发现功能

- 易于编写 Predicates 和 Filters

- 支持请求速率限制

- 支持路径重写

> 思考：
>
> 为什么使用 API 网关？
>
> API 网关出现的原因是微服务架构的出现，不同的微服务一般会有不同的网络地址，而外部客户端可能需要调用多个服务的接口才能完成一个业务需求，如果让客户端直接与各个微服 务通信，会有以下的**问题**：

- 客户端会多次请求不同的微服务，增加了客户端的复杂性。

- 存在跨域请求，在一定场景下处理相对复杂。

- 认证复杂，每个服务都需要独立认证。

- 难以重构，随着项目的迭代，可能需要重新划分微服务。例如，可能将多个服务合并成一个或者将一个服务拆分成多个。如果客户端直接与微服务通信，那么重构将 会很难实施。

- 某些微服务可能使用了防火墙 / 浏览器不友好的协议，直接访问会有一定的困难。

> 以上这些问题可以借助 API 网关解决。API 网关是介于客户端和服务器端之间的中间层， 所有的外部请求都会先经过 API 网关这一层。也就是说，API 的实现方面更多的考虑业务逻辑，而安全、性能、监控可以交由 API 网关来做，这样既提高业务灵活性又不缺安全性： 使用 API 网关后的**优点**如下：

- 易于监控。可以在网关收集监控数据并将其推送到外部系统进行分析。

- 易于认证。可以在网关上进行认证，然后再将请求转发到后端的微服务，而无须在每个微服务中进行认证。

- 减少了客户端与各个微服务之间的交互次数。

## 2、核心概念

- 路由。路由是网关最基础的部分，路由信息有一个 ID、一个目的 URL、一组断言和一组Filter 组成。如果断言路由为真，则说明请求的 URL 和配置匹配

- 断言。Java8 中的断言函数。Spring Cloud Gateway 中的断言函数输入类型是 Spring5.0 框架中的 ServerWebExchange。Spring Cloud Gateway 中的断言函数允许开发者去定义匹配来自于 http request 中的任何信息，比如请求头和参数等。

- 过滤器。一个标准的 Spring webFilter。Spring cloud gateway 中的 filter 分为两种类型的Filter，分别是 Gateway Filter 和 Global Filter。过滤器 Filter 将会对请求和响应进行修改处理

> 工作原理：

![](https://raw.githubusercontent.com/xqy-power/images/main/202308101611531.png)

> 客户端发送请求给网关，弯管 HandlerMapping 判断是否请求满足某个路由，满足就发给网关的 WebHandler。这个 WebHandler 将请求交给一个过滤器链，请求到达目标服务之前，会执行所有过滤器的 pre 方法。请求到达目标服务处理之后再依次执行所有过滤器的 post 方
>
> 法。

#### 一句话：满足某些断言（predicates）就路由到指定的地址（uri），使用指定的过滤器（filter）

> **3、使用**
>
> **1、HelloWorld**

[TABLE]

> **2、断言（Predicates）**

![](https://raw.githubusercontent.com/xqy-power/images/main/202308101611532.jpeg)

> **3****、过滤器（filters）**
>
> 1、GatewayFilter

![](https://raw.githubusercontent.com/xqy-power/images/main/202308101611533.jpeg)

> 2、GlobalFilter
>
> ![](https://raw.githubusercontent.com/xqy-power/images/main/202308101611534.png)

## 3、Sleuth+Zipkin 服务链路追踪

> **1、为什么用**
>
> 微服务架构是一个分布式架构，它按业务划分服务单元，一个分布式系统往往有很多个服务单元。由于服务单元数量众多，业务的复杂性，如果**出现了错误和异常，很难去定位**。主要体现在，**一个请求可能需要调用很多个服务**，而内部服务的调用复杂性，决定了问题难以定位。所以微服务架构中，必须实现分布式链路追踪，去跟进一个请求到底有哪些服务参与， 参与的顺序又是怎样的，从而**达到每个请求的步骤清晰可见，出了问题，很快定位**。
>
> 链路追踪组件有 Google 的 Dapper，Twitter 的 Zipkin，以及阿里的 Eagleeye （鹰眼）等，它们都是非常优秀的链路追踪开源组件。

## 2、基本术语

- Span（跨度）：基本工作单元，发送一个远程调度任务 就会产生一个 Span，Span 是一个 64 位 ID 唯一标识的，Trace 是用另一个 64 位 ID 唯一标识的，Span 还有其他数据信息，比如摘要、时间戳事件、Span 的 ID、以及进度 ID。

- Trace（跟踪）：一系列 Span 组成的一个树状结构。请求一个微服务系统的 API 接口， 这个 API 接口，需要调用多个微服务，调用每个微服务都会产生一个新的 Span，所有由这个请求产生的 Span 组成了这个 Trace。

- Annotation（标注）：用来及时记录一个事件的，一些核心注解用来定义一个请求的开 始和结束 。这些注解包括以下：

&nbsp;

- cs - Client Sent -客户端发送一个请求，这个注解描述了这个 Span 的开始

- sr - Server Received -服务端获得请求并准备开始处理它，如果将其 sr 减去 cs 时间戳便可得到网络传输的时间。

- ss - Server Sent （服务端发送响应）–该注解表明请求处理的完成(当请求返回客户端)，如果 ss 的时间戳减去 sr 时间戳，就可以得到服务器请求的时间。

- cr - Client Received （客户端接收响应）-此时 Span 的结束，如果 cr 的时间戳减去

> cs 时间戳便可以得到整个请求所消耗的时间。官方文档：
>
> [*https://cloud.spring.io/spring-cloud-static/spring-cloud-sleuth/2.1.3.RELEASE/single/spring-cloud*](https://cloud.spring.io/spring-cloud-static/spring-cloud-sleuth/2.1.3.RELEASE/single/spring-cloud-sleuth.html)
>
> *-sleuth.html*
>
> 如果服务调用顺序如下
>
> ![](https://raw.githubusercontent.com/xqy-power/images/main/202308101611535.png)
>
> 那么用以上概念完整的表示出来如下：

![](https://raw.githubusercontent.com/xqy-power/images/main/202308101611536.png)

> Span 之间的父子关系如下：
>
> ![](https://raw.githubusercontent.com/xqy-power/images/main/202308101611537.png)
>
> **3、整合 Sleuth**

[TABLE]

> **5、整合 zipkin 可视化观察**
>
> 通过 Sleuth 产生的调用链监控信息，可以得知微服务之间的调用链路，但监控信息只输出到控制台不方便查看。我们需要一个图形化的工具-zipkin。Zipkin 是 Twitter 开源的分布式跟踪系统，主要用来收集系统的时序数据，从而追踪系统的调用问题。zipkin 官网地址如下： [*https://zipkin.io/*](https://zipkin.io/)
>
> ![](https://raw.githubusercontent.com/xqy-power/images/main/202308101611538.jpeg)

[TABLE]

> 发送远程请求，测试 zipkin。
>
> 服务调用链追踪信息统计

![](https://raw.githubusercontent.com/xqy-power/images/main/202308101611539.jpeg)

> 服务依赖信息统计

![](https://raw.githubusercontent.com/xqy-power/images/main/202308101611540.jpeg)

> **5、Zipkin 数据持久化**
>
> Zipkin 默认是将监控数据存储在内存的，如果 Zipkin 挂掉或重启的话，那么监控数据就会丢失。所以如果想要搭建生产可用的 Zipkin，就需要实现监控数据的持久化。而想要实现数据持久化，自然就是得将数据存储至数据库。好在 Zipkin 支持将数据存储至：

- 内存（默认）

- MySQL

- Elasticsearch

- Cassandra

> Zipkin 数据持久化相关的官方文档地址如下：
>
> [*https://github.com/openzipkin/zipkin#storage-component*](https://github.com/openzipkin/zipkin#storage-component)
>
> Zipkin 支持的这几种存储方式中，内存显然是不适用于生产的，这一点开始也说了。而使用MySQL 的话，当数据量大时，查询较为缓慢，也不建议使用。Twitter 官方使用的是 Cassandra 作为 Zipkin 的存储数据库，但国内大规模用 Cassandra 的公司较少，而且 Cassandra 相关文档也不多。
>
> 综上，故采用 Elasticsearch 是个比较好的选择，关于使用 Elasticsearch 作为 Zipkin 的存储数据库的官方文档如下：
>
> elasticsearch-storage：
>
> [*https://github.com/openzipkin/zipkin/tree/master/zipkin-server#elasticsearch-storage*](https://github.com/openzipkin/zipkin/tree/master/zipkin-server#elasticsearch-storage) zipkin-storage/elasticsearch
>
> [*https://github.com/openzipkin/zipkin/tree/master/zipkin-storage/elasticsearch*](https://github.com/openzipkin/zipkin/tree/master/zipkin-storage/elasticsearch)
>
> 通过 docker 的方式
>
> docker run --env STORAGE_TYPE=elasticsearch --env ES_HOSTS=192.168.56.10:9200 openzipkin/zipkin-dependencies
>
> ![](https://raw.githubusercontent.com/xqy-power/images/main/202308101611541.jpeg)
>
> 使用 es 时 Zipkin Dependencies 支持的环境变量
>
> ![](https://raw.githubusercontent.com/xqy-power/images/main/202308101611542.jpeg)
