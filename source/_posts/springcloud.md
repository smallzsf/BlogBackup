---
title: springcloud
date: 2020-09-25 07:15:41
tags:
---

## 介绍

> Spring Cloud 是一系列框架的有序集合。它利用Spring Boot的开发便利性巧妙的简化了分布式系统基础设施的开发。如**服务发现注册、配置中心、消息总线、负载均衡、断路器、数据监控** 等，都可以用Spring Boot的开发风格做到一键启动和部署。Spring Cloud并没有重复造轮子，它只是将目前各家公司开发的比较成熟、经得起考验的服务框架组合起来，通过Spring Boot风格进行再次封装屏蔽掉了负责的配置和实现原理，最终给开发者留出了一套简单易懂、易部署和易维护的分布式系统开发工具包

## SpringCloud的架构
### SpringCloud中的核心组件
> Spring Cloud的本质是在Spring Boot的基础上，增加了一堆微服务相关的规范，并对应用上下文（Application Context）进行了功能增强。
#### Spring Cloud Netflix组件

| 组件名称 | 作用 |
| :----: | :----: |
| Eurka | 服务注册中心 |
| Ribbon | 客户端负载均衡 |
| Feign | 声明试服务调用 |
| Hystrix | 客户端容错保护 |
| Zuul | API服务网关 |

#### Spring Cloud Alibaba 组件

| 组件名称 | 作用 |
| :----: | :----: |
| Nacos | 服务注册中心|
| Sentinel | 客户端容错保护 |

#### Spring Cloud原生及其他组件

| 组件名称 | 作用 |
| :----: | :----: |
| Consul | 服务注册中心 |
| Config | 分布式配置中心 |
| Gateway | API服务网关 |
| Sleuth/Zipkin | 分布式链路追踪 |

### Spring Cloud 的体系结构


