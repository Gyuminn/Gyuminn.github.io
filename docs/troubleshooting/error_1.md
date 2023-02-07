---
layout: default
title: "[Error] starting Tomcat context. Exception: org.springframework.beans.factory.UnsatisfiedDependencyException."
nav_order: 1
parent: Trouble Shooting
---

# **[Error] starting Tomcat context. Exception: org.springframework.beans.factory.UnsatisfiedDependencyException.**

{: .bg-purple-000}

---

{: .note-title}

> 개밟환경
>
> spring boot(mvn)

{: .warning-title}

> 에러정보
>
> Error starting Tomcat context. Exception: org.springframework.beans.factory.UnsatisfiedDependencyException. Message: Error creating bean with name 'webMvcMetricsFilter' defined in class path resource [org/springframework/boot/actuate/autoconfigure/metrics/web/servlet/WebMvcMetricsAutoConfiguration.class]: Unsatisfied dependency expressed through method 'webMvcMetricsFilter' parameter 0; nested exception is org.springframework.beans.factory.BeanCreationException: Error creating bean with name 'simpleMeterRegistry' defined in class path resource [org/springframework/boot/actuate/autoconfigure/metrics/export/simple/SimpleMetricsExportAutoConfiguration.class]: Initialization of bean failed; nested exception is org.springframework.beans.factory.UnsatisfiedDependencyException: Error creating bean with name 'dataSourcePoolMetadataMeterBinder' defined in class path resource [org/springframework/boot/actuate/autoconfigure/metrics/jdbc/DataSourcePoolMetricsAutoConfiguration$DataSourcePoolMetadataMetricsConfiguration.class]: Unsatisfied dependency expressed through method 'dataSourcePoolMetadataMeterBinder' parameter 0; nested exception is org.springframework.beans.factory.BeanCreationException: Error creating bean with name 'dataSource' defined in class path resource [org/springframework/boot/autoconfigure/jdbc/DataSourceConfiguration$Hikari.class]: Bean instantiation via factory method failed; nested exception is org.springframework.beans.BeanInstantiationException: Failed to instantiate [com.zaxxer.hikari.HikariDataSource]: Factory method 'dataSource' threw exception; nested exception is org.springframework.boot.autoconfigure.jdbc.DataSourceProperties$DataSourceBeanCreationException: Failed to determine a suitable driver class

{: .bg-purple-000}

---

## 원인

이 에러는 dataSource 문제로 데이터베이스 관련 설정을 추가했는데 연결시켜주는 설정을 하지 않았을 때 발생한다고 한다.\
나의 경우 처음 spring boot starter를 통해 프로젝트를 생성할 때 jpa 의존성을 추가해 주었었다.\
그렇지만 디비 설정을 하지 않고 간단한 코드를 작성해서 실행 후 확인을 하려고 하니 에러가 발생하였다.

{: .bg-purple-000}

---

## 해결

추후 데이터베이스를 사용할 때 다시 의존성을 추가해주면 되므로 우선 pom.xml 파일에서 jpa 의존성을 삭제해주고 실행시켰더니 정상 실행되었다!

```xml
<dependency>
   <groupId>org.springframework.boot</groupId>
   <artifactId>spring-boot-starter-data-jpa</artifactId>
</dependency>
```

build tool로 gradle을 사용한다면 build.gradle 파일에서 변경해주거나 application.yml 파일에서 디비 설정을 해준다면 해결될 것이다.
