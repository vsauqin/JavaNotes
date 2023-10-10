**Maven**

# 1.实验操作一

## 使用命令生成Maven工程

指令：mvn archetype:generate

## 解读pom.xml文件

```xml
<!--project标签：表示对当前工程进行配置，管理-->
<project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
  xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
<!--  代表pom.xml所采用的标签结构-->
  <modelVersion>4.0.0</modelVersion>
<!--  坐标信息-->
<!--  groupId标签：坐标向量之一：代表公司开发的某一个项目-->
  <groupId>com.xq.maven</groupId>
<!--  artifactId标签：坐标向量之一：代表项目下的某一个模块-->
  <artifactId>pro01-maven-java</artifactId>
<!--  version：坐标向量之一：代表当前模块的版本-->
  <version>1.0-SNAPSHOT</version>
<!--  packaging标签：打包方式-->
<!--  取值jar生成jar包；取值war生成war包-->
  <packaging>jar</packaging>

  <name>pro01-maven-java</name>
  <url>http://maven.apache.org</url>
<!--properties标签：定义属性值-->
  <properties>
<!--    在构建过程中读取源码时使用的字符集-->
    <project.build.sourceEncoding>UTF-8</project.build.sourceEncoding>
  </properties>
<!--dependencies标签  ：配置具体依赖的信息，可以包含多个dependency子标签-->
  <dependencies>
    <dependency>
<!--      坐标信息：导入哪个jar包，就配置他的坐标信息即可-->
      <groupId>junit</groupId>
      <artifactId>junit</artifactId>
      <version>4.12</version>
<!--      scope：配置当前依赖的范围-->
      <scope>test</scope>
    </dependency>
  </dependencies>
</project>
```



## 核心概念POM

**含义：**

POM：项目对象模型，是模型化思想的具体体现

**模型化思想：**

POM将工程抽象为一个模型，再用程序中的对象来描述这个模型，这样我们就可以用程序来管理项目了

**对应的配置文件**

POM的理念集中体系那再Maven工程根目录下的pom.xml这个配置文件中

## 核心概念：约定的目录结构

**各个目录的作用**

src：源码目录

main：主体程序目录

java：java源代码目录

com：package目录

test：测试目录

还有一个target目录专门存放构建操作输出的结果

**约定目录的意义**

尽可能让构建自动化完成

**约定大于配置**

..............

# 2.实验操作二

## 1.要求

运行Maven中的构建操作相关的命令时，必须进入到pom.xml所在的目录下运行

操作哪一个工程就进入哪一个工程的pom.xml目录

## 2.清理操作

mvn clean

效果：删除target目录

## 3.编译操作

主程序编译：mvn compile

测试程序编译：mvn test-compile

主体程序编译结果存放的目录：target/classes

测试程序编译结果存放的目录：target/test-classes

## 4.测试操作

mvn test

测试的报告存放的目录：target/surefire-reports

## 5.package操作

mvn package

java打jar包

web打war包

## 6.安装操作

mvn install

# 3.实验操作三

**生成web工程目录结构**

mvn archetype:generate -DarchetypeGroupID=org.apache.maven.archetypes -Darchetype -Darc
hetypeArtifactId=maven-archetype-webapp -DarchetypeVersion=1.4

### 创建servlet

# POM文件

## POM示例

```java
<project xmlns="http://maven.apache.org/POM/4.0.0"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 https://maven.apache.org/xsd/maven-4.0.0.xsd">
    <modelVersion>4.0.0</modelVersion>
    <groupId>net.biancheng.www</groupId>
    <artifactId>maven</artifactId>
    <version>0.0.1-SNAPSHOT</version>
</project>
```

所有的Maven项目都有一个POM文件，都必须有三个字段：groupId，artifactId和version

| 节点       | 描述                                                         |
| ---------- | ------------------------------------------------------------ |
| groupId    | 项目组 ID，定义当前 Maven 项目隶属的组织或公司，通常是唯一的。它的取值一般是项目所属公司或组织的网址或 URL 的反写，例如 net.biancheng.www。 |
| artifactId | 项目 ID，通常是项目的名称。groupId 和 artifactId 一起定义了项目在仓库中的位置。 |
| version    | 项目版本。                                                   |

## Super POM

所有的POM文件都继承一个父类POM

Maven 使用 effective pom (Super POM 的配置加上项目的配置）来执行相关任务，它替开发人员在 pom.xml 中做了一些最基本的配置。当然，开发人员依然可以根据需要重写其中的配置信息。

执行以下命令 ，就可以查看 Super POM 的默认配置。

```java
mvn help:effective-pom
```

# Maven坐标

Maven 坐标主要由以下元素组成：

- groupId： 项目组 ID，定义当前 Maven 项目隶属的组织或公司，通常是唯一的。它的取值一般是项目所属公司或组织的网址或 URL 的反写，例如 net.biancheng.www。
- artifactId： 项目 ID，通常是项目的名称。
- version：版本。
- packaging：项目的打包方式，默认值为 jar。

# Maven依赖

当Maven项目需要某个依赖时只需要配置相应的坐标信息即可

假如某个项目使用servlet-api作为依赖时，其配置如下

```xml
<project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/maven-v4_0_0.xsd">
...
    <dependencies>
        <dependency>
            <groupId>javax.servlet</groupId>
            <artifactId>servlet-api</artifactId>
            <version>2.5</version>
            <scope>provided</scope>
        </dependency>
    </dependencies>
</project>
```

dependencies 元素可以包含一个或者多个 dependency 子元素，用以声明一个或者多个项目依赖，每个依赖都可以包含以下元素：

- groupId、artifactId 和 version：依赖的基本坐标，对于任何一个依赖来说，基本坐标是最重要的，Maven 根据坐标才能找到需要的依赖。
- type：依赖的类型，对应于项目坐标定义的 packaging。大部分情况下，该元素不必声明，其默认值是 jar。
- scope：依赖的范围。
- optional：标记依赖是否可选。
- exclusions：用来排除传递性依赖。

# Maven聚合

