## Spring Cloud Eureka

Spring Cloud Eureka 是 Spring cloud Netflix 微服务套件中的一部分，用于构件服务治理功能。服务治理主要用来实现各个微服务实例的自动化注册与发现。
Eureka Server：服务注册中心，维护服务单元注册的信息（主机、端口、版本号、协议等），以心跳方式检测服务单元是否可用，若不可用则从注册中心剔除，从而达到排除故障服务的效果。
Eureka Client：Eureka 客户端，用于处理服务的注册和发现，向注册中心注册自身提供的服务并周期性的发送心跳来更新它的服务租约。它也能从注册中心查询注册的服务信息缓存到本地并周期性的刷新服务的状态。

### 搭建服务注册中心

> 创建 Spring Boot 工程，引入相关项目依赖

```
<dependency>
    <groupId>org.springframework.cloud</groupId>
    <artifactId>spring-cloud-starter-netflix-eureka-server</artifactId>
</dependency>
```

> 添加 @EnableEurekaServer 注解，启动一个服务注册中心

```
@SpringBootApplication
@EnableEurekaServer
public class Application {
    public static void main(String[] args) {
        new SpringApplicationBuilder(Application.class).web(true).run(args);
    }
}
```

> 简单配置

```
server:
  port: 8761    # 服务端口

eureka:
  instance:
    hostname: localhost
  client:
    registerWithEureka: false   # 代表不想注册中心进行注册
    fetchRegistry: false            # 代表不去检索服务
    serviceUrl:
      defaultZone: http://${eureka.instance.hostname}:${server.port}/eureka/    # 注册中心的地址
```