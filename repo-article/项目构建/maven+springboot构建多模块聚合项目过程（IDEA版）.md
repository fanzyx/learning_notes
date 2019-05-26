
# 说明

- 使用idea+maven构建多模块项目的一次过程记录，对内容会不定期更新。
- 更新地址：https://github.com/wyd288/learning_notes

# 使用工具

工具 | 版本/说明
---|---
JDK | 1.8.0_191
IDE | IDEA 2018.3.1
Maven | 3.5.4
MySql | 5.7


# 项目结构

![项目结构](https://github.com/wyd288/learning_notes/blob/master/repo-image/%E9%A1%B9%E7%9B%AE%E6%9E%84%E5%BB%BA/maven+springboot%E6%9E%84%E5%BB%BA%E5%A4%9A%E6%A8%A1%E5%9D%97%E8%81%9A%E5%90%88%E9%A1%B9%E7%9B%AE/1-%E9%A1%B9%E7%9B%AE%E6%A8%A1%E5%9D%97%E7%BB%93%E6%9E%84%E5%9B%BE.png?raw=true)

# 构建过程

1.打开IDEA，点击 Create New Project 创建一个新项目。

![创建一个新项目](https://github.com/wyd288/learning_notes/blob/master/repo-image/%E9%A1%B9%E7%9B%AE%E6%9E%84%E5%BB%BA/maven%2Bspringboot%E6%9E%84%E5%BB%BA%E5%A4%9A%E6%A8%A1%E5%9D%97%E8%81%9A%E5%90%88%E9%A1%B9%E7%9B%AE/2-%E5%88%9B%E5%BB%BA%E4%B8%80%E4%B8%AA%E6%96%B0%E9%A1%B9%E7%9B%AE.png?raw=true)

2.选择Maven 并选择好项目所依赖的SDK（JAVA项目就是JDK），然后点击 Next。

![创建maven根项目](https://github.com/wyd288/learning_notes/blob/master/repo-image/%E9%A1%B9%E7%9B%AE%E6%9E%84%E5%BB%BA/maven%2Bspringboot%E6%9E%84%E5%BB%BA%E5%A4%9A%E6%A8%A1%E5%9D%97%E8%81%9A%E5%90%88%E9%A1%B9%E7%9B%AE/3-%E5%88%9B%E5%BB%BAmaven%E6%A0%B9%E9%A1%B9%E7%9B%AE.png?raw=true)

3.填写项目的坐标信息，名字根据自己的需求填写，版本可以用默认的，也可以自己填写，然后点击Next。

![填写坐标信息](https://github.com/wyd288/learning_notes/blob/master/repo-image/%E9%A1%B9%E7%9B%AE%E6%9E%84%E5%BB%BA/maven%2Bspringboot%E6%9E%84%E5%BB%BA%E5%A4%9A%E6%A8%A1%E5%9D%97%E8%81%9A%E5%90%88%E9%A1%B9%E7%9B%AE/4-%E5%A1%AB%E5%86%99%E7%9B%B8%E5%BA%94%E7%9A%84%E5%9D%90%E6%A0%87%E4%BF%A1%E6%81%AF.png?raw=true)

4.项目名会根据填写的ArtifactId自动生成，用默认的就好。

![完成根项目创建](https://github.com/wyd288/learning_notes/blob/master/repo-image/%E9%A1%B9%E7%9B%AE%E6%9E%84%E5%BB%BA/maven%2Bspringboot%E6%9E%84%E5%BB%BA%E5%A4%9A%E6%A8%A1%E5%9D%97%E8%81%9A%E5%90%88%E9%A1%B9%E7%9B%AE/5-%E5%AE%8C%E6%88%90%E6%A0%B9%E9%A1%B9%E7%9B%AE%E7%9A%84%E5%88%9B%E5%BB%BA.png?raw=true)

5.根项目作为包和插件的管理项目，可以不用src目录，可删可不删，这里我们将其删除。

![删除src并在pom中加入打包方式](https://github.com/wyd288/learning_notes/blob/master/repo-image/%E9%A1%B9%E7%9B%AE%E6%9E%84%E5%BB%BA/maven%2Bspringboot%E6%9E%84%E5%BB%BA%E5%A4%9A%E6%A8%A1%E5%9D%97%E8%81%9A%E5%90%88%E9%A1%B9%E7%9B%AE/6-%E5%88%A0%E9%99%A4%E6%A0%B9%E7%9B%AE%E5%BD%95src%E5%B9%B6%E5%9C%A8pom%E4%B8%AD%E6%B7%BB%E5%8A%A0%E6%89%93%E5%8C%85%E6%96%B9%E5%BC%8F.png?raw=true)

6.右键根项目，选择Module，创建所需要的模块项目。

![新建module](https://github.com/wyd288/learning_notes/blob/master/repo-image/%E9%A1%B9%E7%9B%AE%E6%9E%84%E5%BB%BA/maven%2Bspringboot%E6%9E%84%E5%BB%BA%E5%A4%9A%E6%A8%A1%E5%9D%97%E8%81%9A%E5%90%88%E9%A1%B9%E7%9B%AE/7-%E6%96%B0%E5%BB%BAmodule.png?raw=true)

7.模块项目的类型：api为spring,其他为maven类型。

![选择不同项目类型](https://github.com/wyd288/learning_notes/blob/master/repo-image/%E9%A1%B9%E7%9B%AE%E6%9E%84%E5%BB%BA/maven%2Bspringboot%E6%9E%84%E5%BB%BA%E5%A4%9A%E6%A8%A1%E5%9D%97%E8%81%9A%E5%90%88%E9%A1%B9%E7%9B%AE/8-%E9%80%89%E6%8B%A9%E4%B8%8D%E5%90%8Cmodule%E9%A1%B9%E7%9B%AE%E7%B1%BB%E5%9E%8B.png?raw=true)

8.module项目和根项目一样，需要填写坐标信息，maven类型的module项目只需要填写ArtifactId就可以了。

![填写module名称](https://github.com/wyd288/learning_notes/blob/master/repo-image/%E9%A1%B9%E7%9B%AE%E6%9E%84%E5%BB%BA/maven%2Bspringboot%E6%9E%84%E5%BB%BA%E5%A4%9A%E6%A8%A1%E5%9D%97%E8%81%9A%E5%90%88%E9%A1%B9%E7%9B%AE/9-%E5%A1%AB%E5%86%99module%E5%90%8D%E7%A7%B0.png?raw=true)

9.api模块项目选择的类型为spring。

![api新建项目为spring](https://github.com/wyd288/learning_notes/blob/master/repo-image/%E9%A1%B9%E7%9B%AE%E6%9E%84%E5%BB%BA/maven%2Bspringboot%E6%9E%84%E5%BB%BA%E5%A4%9A%E6%A8%A1%E5%9D%97%E8%81%9A%E5%90%88%E9%A1%B9%E7%9B%AE/10-api%E9%A1%B9%E7%9B%AE%E6%96%B0%E5%BB%BA%E4%B8%BAspring.png?raw=true)

10. api模块项目需要填写的信息比maven类型的多一些，Group要与根项目和其他模块保持一致，Package会根据Artifact自动生成，这里我们修改一下，改成根项目包路径。

![api模块填写信息](https://github.com/wyd288/learning_notes/blob/master/repo-image/%E9%A1%B9%E7%9B%AE%E6%9E%84%E5%BB%BA/maven%2Bspringboot%E6%9E%84%E5%BB%BA%E5%A4%9A%E6%A8%A1%E5%9D%97%E8%81%9A%E5%90%88%E9%A1%B9%E7%9B%AE/11-api%E6%A8%A1%E5%9D%97%E5%A1%AB%E5%86%99%E7%9B%B8%E5%BA%94%E4%BF%A1%E6%81%AF.png?raw=true)

11.spring项目可以自助选择需要依赖的包，我们后期会手动填写，这里暂时就什么都不选了。

![api模块的依赖](https://github.com/wyd288/learning_notes/blob/master/repo-image/%E9%A1%B9%E7%9B%AE%E6%9E%84%E5%BB%BA/maven%2Bspringboot%E6%9E%84%E5%BB%BA%E5%A4%9A%E6%A8%A1%E5%9D%97%E8%81%9A%E5%90%88%E9%A1%B9%E7%9B%AE/12-api%E6%A8%A1%E5%9D%97%E7%9A%84%E4%BE%9D%E8%B5%96.png?raw=true)

12.api选的模块类型为spring,默认是不在根项目的modules下存在的，需我们手动添加

![将api模块手动添加到根项目](https://github.com/wyd288/learning_notes/blob/master/repo-image/%E9%A1%B9%E7%9B%AE%E6%9E%84%E5%BB%BA/maven%2Bspringboot%E6%9E%84%E5%BB%BA%E5%A4%9A%E6%A8%A1%E5%9D%97%E8%81%9A%E5%90%88%E9%A1%B9%E7%9B%AE/13-%E4%B8%BA%E6%A0%B9%E9%A1%B9%E7%9B%AE%E6%89%8B%E5%8A%A8%E6%B7%BB%E5%8A%A0module.png?raw=true)

13.api模块新建后，其parent默认为springboot,这里我们需要将其parent放到根项目的pom中，然后在api的pom中引入根项目作为父依赖。

![修改parent](https://github.com/wyd288/learning_notes/blob/master/repo-image/%E9%A1%B9%E7%9B%AE%E6%9E%84%E5%BB%BA/maven%2Bspringboot%E6%9E%84%E5%BB%BA%E5%A4%9A%E6%A8%A1%E5%9D%97%E8%81%9A%E5%90%88%E9%A1%B9%E7%9B%AE/13-1-%E4%BF%AE%E6%94%B9parent%E4%BE%9D%E8%B5%96.png?raw=true)

![更改pom和最终的项目结构](https://github.com/wyd288/learning_notes/blob/master/repo-image/%E9%A1%B9%E7%9B%AE%E6%9E%84%E5%BB%BA/maven%2Bspringboot%E6%9E%84%E5%BB%BA%E5%A4%9A%E6%A8%A1%E5%9D%97%E8%81%9A%E5%90%88%E9%A1%B9%E7%9B%AE/14-%E6%9B%B4%E6%94%B9pom%E5%92%8C%E6%9C%80%E7%BB%88%E7%9A%84%E9%A1%B9%E7%9B%AE%E7%BB%93%E6%9E%84.png?raw=true)


# 项目配置文件

1.根项目：fanyi_scms

```xml
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
    <modelVersion>4.0.0</modelVersion>

    <!-- 将api项目中的parent 放在根项目中-->
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

    
</project>

```

2.公共模块：scms_common

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


</project>

```

3.Mapper模块：scms_mapper

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


</project>
```

4.Service模块：scms_service

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


</project>
```

5.Api模块：scms_api

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
    

    <build>
        <plugins>
            <plugin>
                <groupId>org.springframework.boot</groupId>
                <artifactId>spring-boot-maven-plugin</artifactId>
            </plugin>
        </plugins>
    </build>

</project>

```

以上为构建聚合项目的基本过程，如有疑问欢迎留言。

