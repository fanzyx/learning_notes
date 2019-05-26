
# 说明

- 多模块聚合项目中各个项目的pom配置

# 配置说明

**1.对根项目的配置改造**

根项目需要对各个子模块的包和插件进行管理，所以根项目中要将可能用到的包和插件全部列出。
![包和插件版本控制](https://github.com/wyd288/learning_notes/blob/master/repo-image/%E9%A1%B9%E7%9B%AE%E6%9E%84%E5%BB%BA/maven%2Bspringboot%E5%A4%9A%E6%A8%A1%E5%9D%97%E9%A1%B9%E7%9B%AE%E7%9A%84%E9%85%8D%E7%BD%AE%E5%8F%8A%E5%AE%9E%E7%8E%B0%EF%BC%88IDEA%E7%89%88%EF%BC%89/1-%E6%A0%B9%E9%A1%B9%E7%9B%AE%E8%BF%9B%E8%A1%8C%E5%8C%85%E5%92%8C%E6%8F%92%E4%BB%B6%E7%9A%84%E7%89%88%E6%9C%AC%E6%8E%A7%E5%88%B6.png?raw=true)
![包管理节点](https://github.com/wyd288/learning_notes/blob/master/repo-image/%E9%A1%B9%E7%9B%AE%E6%9E%84%E5%BB%BA/maven%2Bspringboot%E5%A4%9A%E6%A8%A1%E5%9D%97%E9%A1%B9%E7%9B%AE%E7%9A%84%E9%85%8D%E7%BD%AE%E5%8F%8A%E5%AE%9E%E7%8E%B0%EF%BC%88IDEA%E7%89%88%EF%BC%89/2-1-%E5%BC%95%E5%85%A5%E5%8F%AF%E8%83%BD%E7%94%A8%E5%88%B0%E7%9A%84%E4%BE%9D%E8%B5%96%E5%8C%85.png?raw=true)
![插件管理节点](https://github.com/wyd288/learning_notes/blob/master/repo-image/%E9%A1%B9%E7%9B%AE%E6%9E%84%E5%BB%BA/maven%2Bspringboot%E5%A4%9A%E6%A8%A1%E5%9D%97%E9%A1%B9%E7%9B%AE%E7%9A%84%E9%85%8D%E7%BD%AE%E5%8F%8A%E5%AE%9E%E7%8E%B0%EF%BC%88IDEA%E7%89%88%EF%BC%89/2-2-%E5%BC%95%E5%85%A5%E5%8F%AF%E8%83%BD%E7%94%A8%E5%88%B0%E7%9A%84%E6%8F%92%E4%BB%B6.png?raw=true)

**2.对common模块配置的改造**

common模块需要存储VO类，引入了lombok包，具体内容见下方配置文件。

**3.对mapper模块配置的改造**

mapper模块需要引入common模块，具体内容见下方配置文件。

**4.对service模块配置的改造**

service模块需要引入common和mapper模块，具体内容见下方配置文件。

**5.对api模块配置的改造**

api模块需要引入common和service模块，具体内容见下方配置文件。

# 配置文件

1.根项目配置pom文件

```xml
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
    <modelVersion>4.0.0</modelVersion>

    <!-- 根项目中springboot-parent-->
    <parent>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-parent</artifactId>
        <version>2.1.5.RELEASE</version>
        <relativePath/> <!-- lookup parent from repository -->
    </parent>

    <groupId>com.fanyi</groupId>
    <artifactId>fanyi_scms</artifactId>
    <version>1.0-SNAPSHOT</version>
    <modules>
        <module>scms_common</module>
        <module>scms_mapper</module>
        <module>scms_service</module>
        <!-- 将api模块手动添加到根项目中-->
        <module>scms_api</module>
    </modules>
    <packaging>pom</packaging>

    <!-- 集中版本控制设置 -->
    <properties>
        <project.build.sourceEncoding>UTF-8</project.build.sourceEncoding>
        <project.reporting.outputEncoding>UTF-8</project.reporting.outputEncoding>
        <java.version>1.8</java.version>
        <mybatis-spring-boot-starter.version>1.3.2</mybatis-spring-boot-starter.version>
        <mysql-connector-java.version>5.1.46</mysql-connector-java.version>
        <alibaba-druid.version>1.1.10</alibaba-druid.version>
        <alibaba-fastjson.version>1.2.49</alibaba-fastjson.version>
        <commons-lang.version>2.1</commons-lang.version>
        <commons-io.version>2.5</commons-io.version>
        <maven-resources-plugin.version>3.0.2</maven-resources-plugin.version>
        <maven-compiler-plugin.version>3.8.0</maven-compiler-plugin.version>
        <maven-surefire-plugin.version>2.18.1</maven-surefire-plugin.version>
        <springloaded.version>1.2.6.RELEASE</springloaded.version>
        <lombok.version>1.16.20</lombok.version>
    </properties>

    <dependencyManagement>
        <dependencies>
            <!-- 引入mybatis框架-->
            <dependency>
                <groupId>org.mybatis.spring.boot</groupId>
                <artifactId>mybatis-spring-boot-starter</artifactId>
                <version>${mybatis-spring-boot-starter.version}</version>
            </dependency>

            <!-- 引入mysql驱动 -->
            <dependency>
                <groupId>mysql</groupId>
                <artifactId>mysql-connector-java</artifactId>
                <version>${mysql-connector-java.version}</version>
                <scope>runtime</scope>
            </dependency>

            <!-- 引入数据库连接池 -->
            <dependency>
                <groupId>com.alibaba</groupId>
                <artifactId>druid</artifactId>
                <version>${alibaba-druid.version}</version>
            </dependency>

            <!-- 引入json格式数据转换工具-->
            <dependency>
                <groupId>com.alibaba</groupId>
                <artifactId>fastjson</artifactId>
                <version>${alibaba-fastjson.version}</version>
            </dependency>

            <dependency>
                <groupId>commons-lang</groupId>
                <artifactId>commons-lang</artifactId>
                <version>${commons-lang.version}</version>
            </dependency>
            <dependency>
                <groupId>commons-io</groupId>
                <artifactId>commons-io</artifactId>
                <version>${commons-io.version}</version>
            </dependency>

            <!-- 引入热启动依赖包-->
            <dependency>
                <groupId>org.springframework.boot</groupId>
                <artifactId>spring-boot-devtools</artifactId>
                <version>${spring-boot-starter-parent.version}</version>
                <optional>true</optional>
            </dependency>

            <!--减少重复编码的插件，可自动生成bean的getter、setter和构造方法等-->
            <dependency>
                <groupId>org.projectlombok</groupId>
                <artifactId>lombok</artifactId>
                <version>${lombok.version}</version>
                <scope>provided</scope>
            </dependency>
        </dependencies>
    </dependencyManagement>

    <build>
        <pluginManagement>
            <plugins>
                <plugin>
                    <groupId>org.springframework.boot</groupId>
                    <artifactId>spring-boot-maven-plugin</artifactId>
                    <version>${spring-boot-starter-parent.version}</version>
                    <!--全部打包,可以解决启动jar没有主属性清单的问题-->
                    <executions>
                        <execution>
                            <goals>
                                <goal>repackage</goal>
                            </goals>
                        </execution>
                    </executions>
                    <dependencies>
                        <!-- 热部署 -->
                        <dependency>
                            <groupId>org.springframework</groupId>
                            <artifactId>springloaded</artifactId>
                            <version>${springloaded.version}</version>
                        </dependency>
                    </dependencies>
                </plugin>

                <!--资源拷贝插件-->
                <plugin>
                    <groupId>org.apache.maven.plugins</groupId>
                    <artifactId>maven-resources-plugin</artifactId>
                    <version>${maven-resources-plugin.version}</version>
                    <configuration>
                        <encoding>UTF-8</encoding>
                    </configuration>
                </plugin>

                <!--编译插件，可设置编译的jdk和编码-->
                <plugin>
                    <groupId>org.apache.maven.plugins</groupId>
                    <artifactId>maven-compiler-plugin</artifactId>
                    <version>${maven-compiler-plugin.version}</version>
                    <configuration>
                        <compilerVersion>1.8</compilerVersion>
                        <source>1.8</source>
                        <target>1.8</target>
                        <encoding>UTF-8</encoding>
                    </configuration>
                </plugin>

                <!--单元测试插件-->
                <plugin>
                    <groupId>org.apache.maven.plugins</groupId>
                    <artifactId>maven-surefire-plugin</artifactId>
                    <version>${maven-surefire-plugin.version}</version>
                    <configuration>
                        <skipTests>true</skipTests>
                    </configuration>
                </plugin>


            </plugins>
        </pluginManagement>
    </build>
    
</project>
```

2.common模块配置pom文件

```xml
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
    <parent>
        <artifactId>fanyi_scms</artifactId>
        <groupId>com.fanyi</groupId>
        <version>1.0-SNAPSHOT</version>
    </parent>
    <modelVersion>4.0.0</modelVersion>

    <artifactId>scms_common</artifactId>

    <dependencies>
        <!--common模块存放VO类，引入lombok-->
        <dependency>
            <groupId>org.projectlombok</groupId>
            <artifactId>lombok</artifactId>
        </dependency>
    </dependencies>

</project>
```

3.mapper模块配置pom文件

```xml
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
    <parent>
        <artifactId>fanyi_scms</artifactId>
        <groupId>com.fanyi</groupId>
        <version>1.0-SNAPSHOT</version>
    </parent>
    <modelVersion>4.0.0</modelVersion>

    <artifactId>scms_mapper</artifactId>

    <dependencies>
        <!--引入common模块依赖-->
        <dependency>
            <groupId>com.fanyi</groupId>
            <artifactId>scms_common</artifactId>
            <version>1.0-SNAPSHOT</version>
        </dependency>
        <!-- 引入mybatis框架-->
        <dependency>
            <groupId>org.mybatis.spring.boot</groupId>
            <artifactId>mybatis-spring-boot-starter</artifactId>
            <version>${mybatis-spring-boot-starter.version}</version>
        </dependency>

        <!-- 引入mysql驱动 -->
        <dependency>
            <groupId>mysql</groupId>
            <artifactId>mysql-connector-java</artifactId>
            <version>${mysql-connector-java.version}</version>
            <scope>runtime</scope>
        </dependency>

        <!-- 引入数据库连接池 -->
        <dependency>
            <groupId>com.alibaba</groupId>
            <artifactId>druid</artifactId>
            <version>${alibaba-druid.version}</version>
        </dependency>
    </dependencies>

    <build>
        <!--mapper放在java路径下，需加入java，防止编译时忽略mapper文件-->
        <resources>
            <resource>
                <directory>src/main/java</directory>
                <includes>
                    <include>**/*.xml</include>
                </includes>
            </resource>
        </resources>
    </build>

</project>
```

4.service模块配置pom文件

```xml
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
    <parent>
        <artifactId>fanyi_scms</artifactId>
        <groupId>com.fanyi</groupId>
        <version>1.0-SNAPSHOT</version>
    </parent>
    <modelVersion>4.0.0</modelVersion>

    <artifactId>scms_service</artifactId>

    <dependencies>
        <!--引入common模块依赖-->
        <dependency>
            <groupId>com.fanyi</groupId>
            <artifactId>scms_common</artifactId>
            <version>1.0-SNAPSHOT</version>
        </dependency>
        <!--引入mapper模块依赖-->
        <dependency>
            <groupId>com.fanyi</groupId>
            <artifactId>scms_mapper</artifactId>
            <version>1.0-SNAPSHOT</version>
        </dependency>
    </dependencies>

</project>
```

5.api模块配置pom文件和application.properties配置文件

```xml
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
    <modelVersion>4.0.0</modelVersion>

    <!-- 将api项目的父依赖改为根项目-->
    <parent>
        <artifactId>fanyi_scms</artifactId>
        <groupId>com.fanyi</groupId>
        <version>1.0-SNAPSHOT</version>
    </parent>

    <groupId>com.fanyi</groupId>
    <artifactId>scms_api</artifactId>
    <version>0.0.1-SNAPSHOT</version>
    <name>scms_api</name>
    <description>Demo project for Spring Boot</description>

    <properties>
        <java.version>1.8</java.version>
    </properties>

    <dependencies>
        <!--引入common模块依赖-->
        <dependency>
            <groupId>com.fanyi</groupId>
            <artifactId>scms_common</artifactId>
            <version>1.0-SNAPSHOT</version>
        </dependency>
        <!--引入service模块依赖-->
        <dependency>
            <groupId>com.fanyi</groupId>
            <artifactId>scms_service</artifactId>
            <version>1.0-SNAPSHOT</version>
        </dependency>
        <!--引入springboot-web包-->
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-web</artifactId>
        </dependency>
        <!--引入springboot-test包-->
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-test</artifactId>
            <scope>test</scope>
        </dependency>

        <!-- 引入json格式数据转换工具-->
        <dependency>
            <groupId>com.alibaba</groupId>
            <artifactId>fastjson</artifactId>
            <version>${alibaba-fastjson.version}</version>
        </dependency>

        <!-- 引入热启动依赖包-->
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-devtools</artifactId>
            <optional>true</optional>
        </dependency>
    </dependencies>

    <build>
        <!--在IDEA中使用时，需加入resources和java，防止编译时忽略静态资源和配置文件-->
        <resources>
            <resource>
                <directory>src/main/resources</directory>
                <includes>
                    <include>**/*.*</include>
                </includes>
                <!--这里是false，用true会报 数据库连接 错误-->
                <filtering>false</filtering>
            </resource>
            <resource>
                <directory>src/main/java</directory>
                <includes>
                    <include>**/*.xml</include>
                </includes>
            </resource>
        </resources>

        <plugins>
            <plugin>
                <groupId>org.springframework.boot</groupId>
                <artifactId>spring-boot-maven-plugin</artifactId>
                <!--这里配置启动类，如果不配置，maven在打包时会报错-->
                <configuration>
                    <mainClass>com.fanyi.ScmsApiApplication</mainClass>
                </configuration>
                <!--全部打包,可以解决启动jar没有主属性清单的问题-->
                <executions>
                    <execution>
                        <goals>
                            <goal>repackage</goal>
                        </goals>
                    </execution>
                </executions>
            </plugin>
        </plugins>
    </build>

</project>

```
application.properties

```properties

#数据源在启动的这个模块项目中配置就可以了
spring.datasource.driverClassName=com.mysql.jdbc.Driver
#改成自己的数据库地址
spring.datasource.url=jdbc:mysql://127.0.0.1:3306/数据库名?useSSL=false
#改成自己的用户名
spring.datasource.username=用户名
#改成自己的密码
spring.datasource.password=密码
#数据源类型为阿里巴巴的druid
spring.datasource.type=com.alibaba.druid.pool.DruidDataSource

#对VO类起别名
mybatis.type-aliases-package=com.fanyi.vo

#配置集成tomcat的端口，可自行修改
server.port=3333


```


各个模块的功能不同，使用的包和插件也不相同，可以分别进行依赖管理。

