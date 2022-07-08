# 1.No bean named 'springSecurityFilterChain' available

不使用ContextLoaderListener，让DispatcherServlet加载所有spring配置文件

```xml
   注释 context-param和listener
    <!--<context-param>-->
    <!--    <param-name>contextConfigLocation</param-name>-->
    <!--    <param-value>classpath:spring-persist-mybatis.xml</param-value>-->
    <!--</context-param>-->


    <!--<listener>-->
    <!--    <listener-class>org.springframework.web.context.ContextLoaderListener</listener-class>-->
    <!--</listener>-->

    <servlet>
        <servlet-name>DispatcherServlet</servlet-name>
        <servlet-class>org.springframework.web.servlet.DispatcherServlet</servlet-class>
        <init-param>
           <param-name>contextConfigLocation</param-name>


            改为扫描所有spring配置文件
            <param-value>classpath:spring*.xml</param-value>


        </init-param>
        <load-on-startup>1</load-on-startup>
    </servlet>
```

**弊端：破坏程序结构**

改完之后报错

java.lang.IllegalStateException: No WebApplicationContext found: no ContextLoaderListener or DispatcherServlet registered?

Spring 和SpringSecurity版本冲突,修改为合适的版本

# 2.java.lang.NoClassDefFoundError: org/springframework/core/log/LogMessage

**与springboot版本相比过高，改为合适版本**

```xml
        <dependency>
            <groupId>org.springframework.cloud</groupId>
            <artifactId>spring-cloud-netflix-eureka-server</artifactId>
            <version>3.0.5</version>
        </dependency>
```

```xml
            <dependency>
                <groupId>org.springframework.boot</groupId>
                <artifactId>spring-boot-dependencies</artifactId>
                <version>2.1.6.RELEASE</version>
                <scope>import</scope>
            </dependency>
```

**改为：**

```xml
         <dependency>
            <groupId>org.springframework.cloud</groupId>
            <artifactId>spring-cloud-netflix-eureka-server</artifactId>
            <version>2.1.6.RELE</version>
        </dependency>
```

# 3.Caused by: java.lang.ClassNotFoundException: org.springframework.boot.logging.DeferredLogFactory

**SpringBoot 与SpringCloud版本不匹配，修改为合适版本**

# 4.Origin parameter: http://localhost:1000/actuator/hystrix.stream is not in the allowed list of proxy host names.  If it should be allowed add it to hystrix.dashboard.proxyStreamAllowList.

**在HystrixDashboard工程加入配置。就可以了

```yml
hystrix.dashboard.proxy-stream-allow-list= localhost
```

# 5.org.junit.runners.model.InvalidTestClassError: Invalid test class

导包错误

import org.junit.jupiter.api.Test;

改为

org.junit.Test;

# 6.java.lang.IllegalStateException: Unable to find a @SpringBootConfiguration, you need to use @ContextConfiguration or @SpringBootTest(classes=...) with your test

@SpringBootTest(classes = MybatisTest.class)

# 7.Caused by: java.lang.ClassNotFoundException: com.alibaba.druid.filter.logging.Log4j2Filter

低版本的druid没有这个类，升级到新版；指定druid-spring-boot-starter但没指定druid也可能出现这个错误

```xml
 <dependency>
            <groupId>com.alibaba</groupId>
            <artifactId>druid</artifactId>
            <version>1.1.24</version>
        </dependency>
        <dependency>
            <groupId>com.alibaba</groupId>
            <artifactId>druid-spring-boot-starter</artifactId>
            <version>1.1.24</version>
        </dependency>
```

# 8.You aren't using a compiler supported by lombok,so lombok will not work and has been disabled

更新lombok版本不低于1.18.12

<!--Lombok-->

<dependency>
    <groupId>org.projectlombok</groupId>
    <artifactId>lombok</artifactId>
    <version>1.18.14</version>
    <scope>provided</scope>
</dependency>

# 9. 非法字符 “\ufeff”

导入项目的时候，你可以碰到以上的编码问题，这一般这个项目是用eclipse开发的。主要原因是: Eclipse可以自动把UTF-8+BOM文件转为普通的UTF-8文件，不使用eclipse需要手动修改移除Bom。

# 10.ORA-12514: TNS :*no* *listener*

命令行中输入netca回车;

运行Oracle net configuration assistant,选择监听程序设置，然后按步骤进行。

# centos7

## 1.重启网络服务失败

 Job for network.service failed because the control process exited with error code. See "systemctl status network.service" and "journalctl -xe" for details.
                                                           [FAILED]

```
service NetworkManager stop 关闭 NetworkManger 服务
```

```
chkconfig NetworkManager off 永久关闭 Manager网卡
```

```
service network restart 重启network网卡
```
