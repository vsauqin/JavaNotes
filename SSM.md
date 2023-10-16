SSM

---

# 一、Maven简介和快速入门

  ### 1.1 Maven介绍

    https://maven.apache.org/what-is-maven.html
    
    Maven 是一款为 Java 项目构建管理、依赖管理的工具（**软件**），使用 Maven 可以自动化构建、测试、打包和发布项目，大大提高了开发效率和质量。
    
    总结：Maven就是一个软件，掌握软件安装、配置、以及基本功能**（项目构建、依赖管理）**使用就是本课程的主要目标！

  ### 1.2 Maven主要作用理解
1. 场景概念

    **场景1：**例如我们项目需要第三方库（依赖），如Druid连接池、MySQL数据库驱动和Jackson等。那么我们可以将需要的依赖项的信息编写到Maven工程的配置文件，Maven软件就会自动下载并复制这些依赖项到项目中，也会自动下载依赖需要的依赖！确保依赖版本正确无冲突和依赖完整！

    **场景2：**项目开发完成后，想要将项目打成.war文件，并部署到服务器中运行，使用Maven软件，我们可以通过一行构建命令（mvn package）快速项目构建和打包！节省大量时间！
2. **依赖管理：**

    Maven 可以管理项目的依赖，包括自动下载所需依赖库、自动下载依赖需要的依赖并且保证版本没有冲突、依赖版本管理等。通过 Maven，我们可以方便地维护项目所依赖的外部库，而我们仅仅需要编写配置即可。
3. **构建管理：**

    项目构建是指将源代码、配置文件、资源文件等转化为能够运行或部署的应用程序或库的过程！

    Maven 可以管理项目的编译、测试、打包、部署等构建过程。通过实现标准的构建生命周期，Maven 可以确保每一个构建过程都遵循同样的规则和最佳实践。同时，Maven 的插件机制也使得开发者可以对构建过程进行扩展和定制。主动触发构建，只需要简单的命令操作即可。


  ### 1.3 Maven安装和配置

    https://maven.apache.org/docs/history.html
    
    选用版本：


​      

| 发布时间           | maven版本 | jdk最低版本 |
| ------------------ | --------- | ----------- |
| **2019 - 11 - **25 | **3.6.**3 | Java 7      |

1. 安装

    **安装条件：**maven需要本机安装java环境、必需包含java_home环境变量！

    **软件安装：**右键解压即可（绿色免安装）

    **软件结构：**
2. 环境变量

    **环境变量：**配置maven_home 和 path
3. 命令测试

```Bash
mvn -v 
# 输出版本信息即可，如果错误，请仔细检查环境变量即可！
# 友好提示，如果此处错误，绝大部分原因都是java_home变量的事，请仔细检查！！
```
4. 配置文件

    > 我们需要需改**maven/conf/settings.xml**配置文件，来修改maven的一些默认配置。我们主要休要修改的有三个配置：1.依赖本地缓存位置（本地仓库位置）2.maven下载镜像3.maven选用编译项目的jdk版本！

    1. 配置本地仓库地址

```XML
<!-- localRepository
 | The path to the local repository maven will use to store artifacts.
 |
 | Default: ${user.home}/.m2/repository
<localRepository>/path/to/local/repo</localRepository>
-->
<!-- conf/settings.xml 55行 -->
<localRepository>D:\repository</localRepository>
```
        2. 配置国内阿里镜像

```XML
<!--在mirrors节点(标签)下添加中央仓库镜像 160行附近-->
<mirror>
    <id>alimaven</id>
    <name>aliyun maven</name>
    <url>http://maven.aliyun.com/nexus/content/groups/public/</url>
    <mirrorOf>central</mirrorOf>
</mirror>
```
        3. 配置jdk17版本项目构建

```XML
<!--在profiles节点(标签)下添加jdk编译版本 268行附近-->
<profile>
    <id>jdk-17</id>
    <activation>
      <activeByDefault>true</activeByDefault>
      <jdk>17</jdk>
    </activation>
    <properties>
      <maven.compiler.source>17</maven.compiler.source>
      <maven.compiler.target>17</maven.compiler.target>
      <maven.compiler.compilerVersion>17</maven.compiler.compilerVersion>
    </properties>
</profile>
```
5. idea配置本地maven

    > 我们需要将配置好的maven软件，配置到idea开发工具中即可！ 注意：idea工具默认自带maven配置软件，但是因为没有修改配置，建议替换成本地配置好的maven！

    1. 打开idea配置文件，构建工具配置

        依次点击

        file / settings / build / build tool / maven
    2. 选中本地maven软件

    3. 测试是否配置成功
    
    **注意**：如果本地仓库地址不变化，只有一个原因，就是maven/conf/settings.xml配置文件编写错误！仔细检查即可！
    
    

# 二、基于IDEA的Maven工程创建

  ### 2.1梳理Maven工程GAVP属性

> Maven工程相对之前的工程，多出一组gavp属性，gav需要我们在创建项目的时指定，p有默认值，后期通过配置文件修改。既然要填写的属性，我们先行了解下这组属性的含义!

Maven 中的 GAVP 是指 GroupId、ArtifactId、Version、Packaging 等四个属性的缩写，其中前三个是必要的，而 Packaging 属性为可选项。这四个属性主要为每个项目在maven仓库总做一个标识，类似人的《姓-名》。有了具体标识，方便maven软件对项目进行管理和互相引用！

**GAV遵循一下规则：**

  1） **GroupID 格式**：com.{公司/BU }.业务线.[子业务线]，最多 4 级。

    说明：{公司/BU} 例如：alibaba/taobao/tmall/aliexpress 等 BU 一级；子业务线可选。
    
    正例：com.taobao.tddl 或 com.alibaba.sourcing.multilang  com.atguigu.java

  2） **ArtifactID 格式**：产品线名-模块名。语义不重复不遗漏，先到仓库中心去查证一下。

    正例：tc-client / uic-api / tair-tool / bookstore

  3） **Version版本号格式推荐**：主版本号.次版本号.修订号 1.0.0

    1） 主版本号：当做了不兼容的 API 修改，或者增加了能改变产品方向的新功能。
    
    2） 次版本号：当做了向下兼容的功能性新增（新增类、接口等）。
    
    3） 修订号：修复 bug，没有修改方法签名的功能加强，保持 API 兼容性。
    
    例如： 初始→1.0.0  修改bug → 1.0.1  功能调整 → 1.1.1等

**Packaging定义规则：**

  指示将项目打包为什么类型的文件，idea根据packaging值，识别maven项目类型！

  packaging 属性为 jar（默认值），代表普通的Java工程，打包以后是.jar结尾的文件。

  packaging 属性为 war，代表Java的web工程，打包以后.war结尾的文件。

  packaging 属性为 pom，代表不会打包，用来做继承的父工程。

  ### 2.2 Idea构建Maven JavaSE工程

    注意：此处省略了version，直接给了一个默认值<version>1.0-SNAPSHOT</version>
    
    自己后期可以在项目中随意修改！
    
    ![](https://secure2.wostatic.cn/static/oDo2HDrVXHoKqfqRdqLKuV/image.png)

  ### 2.3 Idea构建Maven JavaEE工程
    1. 手动创建
        1. 创建一个javasemaven工程
        2. 手动添加web项目结构文件
    
            注意：结构和命名固定
        3. 修改pom.xml文件打包方式
    
            修改位置：项目下/pom.xml

```XML
<groupId>com.atguigu</groupId>
<artifactId>maven_parent</artifactId>
<version>1.0-SNAPSHOT</version>
<!-- 新增一列打包方式packaging -->
<packaging>war</packaging>
```
        4. 刷新和校验
            项目的webapp文件夹出现小蓝点，代表成功！！
    2. 插件方式创建
        1. 安装插件JBLJavaToWeb
    
            file / settings / plugins / marketplace
        2. 创建一个javasemaven工程
        3. 右键、使用插件快速补全web项目

  ### 2.4 Maven工程项目结构说明

    Maven 是一个强大的构建工具，它提供一种标准化的项目结构，可以帮助开发者更容易地管理项目的依赖、构建、测试和发布等任务。以下是 Maven Web 程序的文件结构及每个文件的作用：

```XML
|-- pom.xml                               # Maven 项目管理文件 
|-- src
    |-- main                              # 项目主要代码
    |   |-- java                          # Java 源代码目录
    |   |   `-- com/example/myapp         # 开发者代码主目录
    |   |       |-- controller            # 存放 Controller 层代码的目录
    |   |       |-- service               # 存放 Service 层代码的目录
    |   |       |-- dao                   # 存放 DAO 层代码的目录
    |   |       `-- model                 # 存放数据模型的目录
    |   |-- resources                     # 资源目录，存放配置文件、静态资源等
    |   |   |-- log4j.properties          # 日志配置文件
    |   |   |-- spring-mybatis.xml        # Spring Mybatis 配置文件
    |   |   `-- static                    # 存放静态资源的目录
    |   |       |-- css                   # 存放 CSS 文件的目录
    |   |       |-- js                    # 存放 JavaScript 文件的目录
    |   |       `-- images                # 存放图片资源的目录
    |   `-- webapp                        # 存放 WEB 相关配置和资源
    |       |-- WEB-INF                   # 存放 WEB 应用配置文件
    |       |   |-- web.xml               # Web 应用的部署描述文件
    |       |   `-- classes               # 存放编译后的 class 文件
    |       `-- index.html                # Web 应用入口页面
    `-- test                              # 项目测试代码
        |-- java                          # 单元测试目录
        `-- resources                     # 测试资源目录
```

    - pom.xml：Maven 项目管理文件，用于描述项目的依赖和构建配置等信息。
    - src/main/java：存放项目的 Java 源代码。
    - src/main/resources：存放项目的资源文件，如配置文件、静态资源等。
    - src/main/webapp/WEB-INF：存放 Web 应用的配置文件。
    - src/main/webapp/index.html：Web 应用的入口页面。
    - src/test/java：存放项目的测试代码。
    - src/test/resources：存放测试相关的资源文件，如测试配置文件等。

# 三、Maven核心功能依赖和构建管理

  ### 3.1 依赖管理和配置

    Maven 依赖管理是 Maven 软件中最重要的功能之一。Maven 的依赖管理能够帮助开发人员自动解决软件包依赖问题，使得开发人员能够轻松地将其他开发人员开发的模块或第三方框架集成到自己的应用程序或模块中，避免出现版本冲突和依赖缺失等问题。
    
    我们通过定义 POM 文件，Maven 能够自动解析项目的依赖关系，并通过 Maven **仓库自动**下载和管理依赖，从而避免了手动下载和管理依赖的繁琐工作和可能引发的版本冲突问题。
    
    重点: 编写pom.xml文件!
    
    maven项目信息属性配置和读取：

```XML
<!-- 模型版本 -->
<modelVersion>4.0.0</modelVersion>
<!-- 公司或者组织的唯一标志，并且配置时生成的路径也是由此生成， 如com.companyname.project-group，maven会将该项目打成的jar包放本地路径：/com/companyname/project-group -->
<groupId>com.companyname.project-group</groupId>
<!-- 项目的唯一ID，一个groupId下面可能多个项目，就是靠artifactId来区分的 -->
<artifactId>project</artifactId>
<!-- 版本号 -->
<version>1.0.0</version>

<!--打包方式
    默认：jar
    jar指的是普通的java项目打包方式！ 项目打成jar包！
    war指的是web项目打包方式！项目打成war包！
    pom不会讲项目打包！这个项目作为父工程，被其他工程聚合或者继承！后面会讲解两个概念
-->
<packaging>jar/pom/war</packaging>
```

    依赖管理和添加：

```XML
<!-- 
   通过编写依赖jar包的gav必要属性，引入第三方依赖！
   scope属性是可选的，可以指定依赖生效范围！
   依赖信息查询方式：
      1. maven仓库信息官网 https://mvnrepository.com/
      2. mavensearch插件搜索
 -->
<dependencies>
    <!-- 引入具体的依赖包 -->
    <dependency>
        <groupId>log4j</groupId>
        <artifactId>log4j</artifactId>
        <version>1.2.17</version>
        <!--
            生效范围
            - compile ：main目录 test目录  打包打包 [默认]
            - provided：main目录 test目录  Servlet
            - runtime： 打包运行           MySQL
            - test:    test目录           junit
         -->
        <scope>runtime</scope>
    </dependency>

</dependencies>
```

    依赖版本提取和维护:

```XML
<!--声明版本-->
<properties>
  <!--命名随便,内部制定版本号即可！-->
  <junit.version>4.11</junit.version>
  <!-- 也可以通过 maven规定的固定的key，配置maven的参数！如下配置编码格式！-->
  <project.build.sourceEncoding>UTF-8</project.build.sourceEncoding>
  <project.reporting.outputEncoding>UTF-8</project.reporting.outputEncoding>
</properties>

<dependencies>
  <dependency>
    <groupId>junit</groupId>
    <artifactId>junit</artifactId>
    <!--引用properties声明版本 -->
    <version>${junit.version}</version>
  </dependency>
</dependencies>
```

  ### 3.2依赖传递和冲突

**依赖传递**：

指的是当一个模块或库 A 依赖于另一个模块或库 B，而 B 又依赖于模块或库 C，那么 A 会间接依赖于 C。这种依赖传递结构可以形成一个依赖树。当我们引入一个库或框架时，构建工具（如 Maven、Gradle）会自动解析和加载其所有的直接和间接依赖，确保这些依赖都可用。

依赖传递的作用是：

1. 减少重复依赖：当多个项目依赖同一个库时，Maven 可以自动下载并且只下载一次该库。这样可以减少项目的构建时间和磁盘空间。
2. 自动管理依赖: Maven 可以自动管理依赖项，使用依赖传递，简化了依赖项的管理，使项目构建更加可靠和一致。
3. 确保依赖版本正确性：通过依赖传递的依赖，之间都不会存在版本兼容性问题，确实依赖的版本正确性！

  最佳导入：直接可以导入data-bind，自动依赖传递需要的依赖

```XML
<!-- https://mvnrepository.com/artifact/com.fasterxml.jackson.core/jackson-databind -->
<dependency>
    <groupId>com.fasterxml.jackson.core</groupId>
    <artifactId>jackson-databind</artifactId>
    <version>2.15.0</version>
</dependency>
```

**依赖冲突演示**：

当直接引用或者间接引用出现了相同的jar包! 这时呢，一个项目就会出现相同的重复jar包，这就算作冲突！依赖冲突避免出现重复依赖，并且终止依赖传递！

maven自动解决依赖冲突问题能力，会按照自己的原则，进行重复依赖选择。同时也提供了手动解决的冲突的方式，不过不推荐！

解决依赖冲突（如何选择重复依赖）方式：
  1. 自动选择原则
      - 短路优先原则（第一原则）

          A—>B—>C—>D—>E—>X(version 0.0.1)

          A—>F—>X(version 0.0.2)

          则A依赖于X(version 0.0.2)。
      - 依赖路径长度相同情况下，则“先声明优先”（第二原则）

          A—>E—>X(version 0.0.1)

          A—>F—>X(version 0.0.2)

          在<depencies></depencies>中，先声明的，路径相同，会优先选择！

```XML
前提：
   A 1.1 -> B 1.1 -> C 1.1 
   F 2.2 -> B 2.2 
   
pom声明：
   F 2.2
   A 1.1 
   
   B 2.2 

```

**注意：**只要发生依赖冲突后续的以来不会继续传递

  ### 3.3 依赖导入失败场景和解决方案

在使用 Maven 构建项目时，可能会发生依赖项下载错误的情况，主要原因有以下几种：

1. 下载依赖时出现网络故障或仓库服务器宕机等原因，导致无法连接至 Maven 仓库，从而无法下载依赖。
2. 依赖项的版本号或配置文件中的版本号错误，或者依赖项没有正确定义，导致 Maven 下载的依赖项与实际需要的不一致，从而引发错误。
3. 本地 Maven 仓库或缓存被污染或损坏，导致 Maven 无法正确地使用现有的依赖项，并且也无法重新下载！

解决方案：

1. 检查网络连接和 Maven 仓库服务器状态。
2. 确保依赖项的版本号与项目对应的版本号匹配，并检查 POM 文件中的依赖项是否正确。
3. 清除本地 Maven 仓库缓存（lastUpdated 文件），因为只要存在lastupdated缓存文件，刷新也不会重新下载。本地仓库中，根据依赖的gav属性依次向下查找文件夹，最终删除内部的文件，刷新重新下载即可！

    例如： pom.xml依赖

```XML
<dependency>
  <groupId>com.alibaba</groupId>
  <artifactId>druid</artifactId>
  <version>1.2.8</version>
</dependency>
```

        文件：
    
        ![](https://secure2.wostatic.cn/static/6mSDgf4nkaRLAu16dqSJk7/image.png)
    
        脚本使用：


​        

```XML
使用记事本打开
set REPOSITORY_PATH=D:\repository  改成你本地仓库地址即可！
点击运行脚本，即可自动清理本地错误缓存文件！！
```

  ### 3.4 扩展构建管理和插件配置

**构建概念:**

项目构建是指将源代码、依赖库和资源文件等转换成可执行或可部署的应用程序的过程，在这个过程中包括编译源代码、链接依赖库、打包和部署等多个步骤。

**主动触发场景：**

- 重新编译 : 编译不充分, 部分文件没有被编译!
- 打包 : 独立部署到外部服务器软件,打包部署
- 部署本地或者私服仓库 : maven工程加入到本地或者私服仓库,供其他工程使用

**命令方式构建:**

语法: mvn 构建命令  构建命令....

| 命令        | 描述                                        |
| ----------- | ------------------------------------------- |
| mvn clean   | 清理编译或打包后的项目结构,删除target文件夹 |
| mvn compile | 编译项目，生成target文件                    |
| mvn test    | 执行测试源码 (测试)                         |
| mvn site    | 生成一个项目依赖信息的展示页面              |
| mvn package | 打包项目，生成war / jar 文件                |
| mvn install | 打包后上传到maven本地仓库(本地部署)         |
| mvn deploy  | 只打包，上传到maven私服仓库(私服部署)       |

**可视化方式构建:**

**构建命令周期:**

构建生命周期可以理解成是一组固定构建命令的有序集合，触发周期后的命令，会自动触发周期前的命令！也是一种简化构建的思路!

- *清理周期*：主要是对项目编译生成文件进行清理

    包含命令：clean
- *默认周期*：定义了真正构件时所需要执行的所有步骤，它是生命周期中最核心的部分

    包含命令：compile - test - package - install / deploy
- *报告周期*

    包含命令：site

    打包: mvn clean package 本地仓库: mvn clean install

**最佳使用方案:**

```text
打包: mvn clean package
重新编译: mvn clean compile
本地部署: mvn clean install 
```

**周期，命令和插件:**

周期→包含若干命令→包含若干插件!

使用周期命令构建，简化构建过程！

最终进行构建的是插件！

插件配置:

```XML
<build>
   <!-- jdk17 和 war包版本插件不匹配 -->
    <plugins>
        <plugin>
            <groupId>org.apache.maven.plugins</groupId>
            <artifactId>maven-war-plugin</artifactId>
            <version>3.2.2</version>
        </plugin>
    </plugins>
</build>
```

# 四、Maven继承和聚合特性

  ## 4.1 Maven工程继承关系
1. 继承概念

    Maven 继承是指在 Maven 的项目中，让一个项目从另一个项目中继承配置信息的机制。继承可以让我们在多个项目中共享同一配置信息，简化项目的管理和维护工作。

2. 继承作用

    作用：在父工程中统一管理项目中的依赖信息,进行统一版本管理!

    它的背景是：

    - 对一个比较大型的项目进行了模块拆分。
    - 一个 project 下面，创建了很多个 module。
    - 每一个 module 都需要配置自己的依赖信息。

    它背后的需求是：

    - 多个模块要使用同一个框架，它们应该是同一个版本，所以整个项目中使用的框架版本需要统一管理。
    - 使用框架时所需要的 jar 包组合（或者说依赖信息组合）需要经过长期摸索和反复调试，最终确定一个可用组合。这个耗费很大精力总结出来的方案不应该在新的项目中重新摸索。

    通过在父工程中为整个项目维护依赖信息的组合既保证了整个项目使用规范、准确的 jar 包；又能够将以往的经验沉淀下来，节约时间和精力。
3. 继承语法
   
    - 父工程

```XML
<groupId>com.atguigu.maven</groupId>
<artifactId>pro03-maven-parent</artifactId>
<version>1.0-SNAPSHOT</version>
<!-- 当前工程作为父工程，它要去管理子工程，所以打包方式必须是 pom -->
<packaging>pom</packaging>

```
​		

- 子工程

```XML
<!-- 使用parent标签指定当前工程的父工程 -->
<parent>
  <!-- 父工程的坐标 -->
  <groupId>com.atguigu.maven</groupId>
  <artifactId>pro03-maven-parent</artifactId>
  <version>1.0-SNAPSHOT</version>
</parent>

<!-- 子工程的坐标 -->
<!-- 如果子工程坐标中的groupId和version与父工程一致，那么可以省略 -->
<!-- <groupId>com.atguigu.maven</groupId> -->
<artifactId>pro04-maven-module</artifactId>
<!-- <version>1.0-SNAPSHOT</version> -->
```
4. 父工程依赖统一管理
    - 父工程声明版本

```XML
<!-- 使用dependencyManagement标签配置对依赖的管理 -->
<!-- 被管理的依赖并没有真正被引入到工程 -->
<dependencyManagement>
  <dependencies>
    <dependency>
      <groupId>org.springframework</groupId>
      <artifactId>spring-core</artifactId>
      <version>4.0.0.RELEASE</version>
    </dependency>
    <dependency>
      <groupId>org.springframework</groupId>
      <artifactId>spring-beans</artifactId>
      <version>4.0.0.RELEASE</version>
    </dependency>
    <dependency>
      <groupId>org.springframework</groupId>
      <artifactId>spring-context</artifactId>
      <version>4.0.0.RELEASE</version>
    </dependency>
    <dependency>
      <groupId>org.springframework</groupId>
      <artifactId>spring-expression</artifactId>
      <version>4.0.0.RELEASE</version>
    </dependency>
    <dependency>
      <groupId>org.springframework</groupId>
      <artifactId>spring-aop</artifactId>
      <version>4.0.0.RELEASE</version>
    </dependency>
  </dependencies>
</dependencyManagement>
```
        - 子工程引用版本

```XML
<!-- 子工程引用父工程中的依赖信息时，可以把版本号去掉。  -->
<!-- 把版本号去掉就表示子工程中这个依赖的版本由父工程决定。 -->
<!-- 具体来说是由父工程的dependencyManagement来决定。 -->
<dependencies>
  <dependency>
    <groupId>org.springframework</groupId>
    <artifactId>spring-core</artifactId>
  </dependency>
  <dependency>
    <groupId>org.springframework</groupId>
    <artifactId>spring-beans</artifactId>
  </dependency>
  <dependency>
    <groupId>org.springframework</groupId>
    <artifactId>spring-context</artifactId>
  </dependency>
  <dependency>
    <groupId>org.springframework</groupId>
    <artifactId>spring-expression</artifactId>
  </dependency>
  <dependency>
    <groupId>org.springframework</groupId>
    <artifactId>spring-aop</artifactId>
  </dependency>
</dependencies>
```

  ## 4.2 Maven工程聚合关系
1. 聚合概念

    Maven 聚合是指将多个项目组织到一个父级项目中，通过触发父工程的构建,统一按顺序触发子工程构建的过程!!
2. 聚合作用
    1. 统一管理子项目构建：通过聚合，可以将多个子项目组织在一起，方便管理和维护。
    2. 优化构建顺序：通过聚合，可以对多个项目进行顺序控制，避免出现构建依赖混乱导致构建失败的情况。
3. 聚合语法

    父项目中包含的子项目列表。

```XML
<project>
  <groupId>com.example</groupId>
  <artifactId>parent-project</artifactId>
  <packaging>pom</packaging>
  <version>1.0.0</version>
  <modules>
    <module>child-project1</module>
    <module>child-project2</module>
  </modules>
</project>
```
4. 聚合演示

    通过触发父工程构建命令、引发所有子模块构建！产生反应堆！

    

# 五、Maven实战案例：搭建微服务Maven工程架构

  ### 5.1 项目需求和结构分析

需求案例：搭建一个电商平台项目，该平台包括用户服务、订单服务、通用工具模块等。

项目架构：

1. 用户服务：负责处理用户相关的逻辑，例如用户信息的管理、用户注册、登录等。
2. 订单服务：负责处理订单相关的逻辑，例如订单的创建、订单支付、退货、订单查看等。
3. 通用模块：负责存储其他服务需要通用工具类，其他服务依赖此模块。

服务依赖：

1. 用户服务 (1.0.1)
    - spring-context 6.0.6 
    - spring-core 6.0.6
    - spring-beans 6.0.6
    - jackson-databind /  jackson-core / jackson-annotations 2.15.0 
2. 订单服务 (1.0.1)
    1. shiro-core 1.10.1 
    2. spring-context 6.0.6 
    3. spring-core 6.0.6
    4. spring-beans 6.0.6
3. 通用模块 (1.0.1)
    1. commons-io 2.11.0

  ### 5.2项目搭建和统一构建
1. 父模块搭建 (micro-shop)
    1. 创建父工程

    2. pom.xml配置

```XML
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
    <modelVersion>4.0.0</modelVersion>

    <groupId>com.atguigu</groupId>
    <artifactId>micro-shop</artifactId>
    <version>1.0.1</version>
    <!-- 父工程不打包，所以选择pom值-->
    <packaging>pom</packaging>

    <properties>
        <spring.version>6.0.6</spring.version>
        <jackson.version>2.15.0</jackson.version>
        <shiro.version>1.10.1</shiro.version>
        <commons.version>2.11.0</commons.version>
        <maven.compiler.source>17</maven.compiler.source>
        <maven.compiler.target>17</maven.compiler.target>
        <project.build.sourceEncoding>UTF-8</project.build.sourceEncoding>
    </properties>

    <!-- 依赖管理 -->
    <dependencyManagement>
        <dependencies>
            <!-- spring-context会依赖传递core/beans -->
            <dependency>
                <groupId>org.springframework</groupId>
                <artifactId>spring-context</artifactId>
                <version>${spring.version}</version>
            </dependency>

            <!-- jackson-databind会依赖传递core/annotations -->
            <dependency>
                <groupId>com.fasterxml.jackson.core</groupId>
                <artifactId>jackson-databind</artifactId>
                <version>${jackson.version}</version>
            </dependency>

            <!-- shiro-core -->
            <dependency>
                <groupId>org.apache.shiro</groupId>
                <artifactId>shiro-core</artifactId>
                <version>${shiro.version}</version>
            </dependency>
            <!-- commons-io -->
            <dependency>
                <groupId>commons-io</groupId>
                <artifactId>commons-io</artifactId>
                <version>${commons.version}</version>
            </dependency>

        </dependencies>

    </dependencyManagement>

    <dependencies>
        <!-- 父工程添加依赖，会自动传递给所有子工程，不推荐！ -->
    </dependencies>

    <!-- 统一更新子工程打包插件-->
    <build>
        <!-- jdk17 和 war包版本插件不匹配 -->
        <plugins>
            <plugin>
                <groupId>org.apache.maven.plugins</groupId>
                <artifactId>maven-war-plugin</artifactId>
                <version>3.2.2</version>
            </plugin>
        </plugins>
    </build>

</project>
```
2. 通用模块 (common-service)
    1. 创建模块

    2. pom.xml配置

```XML
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
    <modelVersion>4.0.0</modelVersion>
    <parent>
        <groupId>com.atguigu</groupId>
        <artifactId>micro-shop</artifactId>
        <version>1.0.1</version>
    </parent>
    <artifactId>common-service</artifactId>
    <!-- 打包方式默认就是jar！ -->
    <packaging>jar</packaging>

    <properties>
        <maven.compiler.source>17</maven.compiler.source>
        <maven.compiler.target>17</maven.compiler.target>
        <project.build.sourceEncoding>UTF-8</project.build.sourceEncoding>
    </properties>

    <dependencies>
        <!-- 声明commons-io，继承父工程版本 -->
        <dependency>
            <groupId>commons-io</groupId>
            <artifactId>commons-io</artifactId>
        </dependency>
    </dependencies>

</project>
```
3. 用户模块 (user-service)
    1. 创建模块

    2. pom.xml配置

```XML
<?xml version="1.0" encoding="UTF-8"?>

<project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">  
  <modelVersion>4.0.0</modelVersion>  
  <parent> 
    <groupId>com.atguigu</groupId>  
    <artifactId>micro-shop</artifactId>  
    <version>1.0.1</version> 
  </parent>  
  <artifactId>user-service</artifactId>  
  <packaging>war</packaging>

  <properties> 
    <maven.compiler.source>17</maven.compiler.source>  
    <maven.compiler.target>17</maven.compiler.target>  
    <project.build.sourceEncoding>UTF-8</project.build.sourceEncoding> 
  </properties>

  <dependencies>
    <!-- 添加spring-context 自动传递 core / beans -->
    <dependency>
      <groupId>org.springframework</groupId>
      <artifactId>spring-context</artifactId>
    </dependency>

    <!-- 添加jackson-databind 自动传递 core / annotations -->
    <dependency>
      <groupId>com.fasterxml.jackson.core</groupId>
      <artifactId>jackson-databind</artifactId>
    </dependency>
  </dependencies>
</project>

```
4. 订单模块 (order-service)
    1. 创建模块

        

    2. pom.xml

```XML
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
    <modelVersion>4.0.0</modelVersion>
    <parent>
        <groupId>com.atguigu</groupId>
        <artifactId>micro-shop</artifactId>
        <version>1.0.1</version>
    </parent>

    <artifactId>order-service</artifactId>
    <packaging>war</packaging>

    <properties>
        <maven.compiler.source>17</maven.compiler.source>
        <maven.compiler.target>17</maven.compiler.target>
        <project.build.sourceEncoding>UTF-8</project.build.sourceEncoding>
    </properties>

    <dependencies>
        <!-- 继承父工程依赖版本 -->
        <dependency>
            <groupId>org.springframework</groupId>
            <artifactId>spring-context</artifactId>
        </dependency>

        <!-- 继承父工程依赖版本 -->
        <dependency>
            <groupId>org.apache.shiro</groupId>
            <artifactId>shiro-core</artifactId>
        </dependency>
    </dependencies>

</project>
```

# 六、Maven核心掌握总结

|            |                                                    |
| ---------- | -------------------------------------------------- |
| 核心点     | 掌握目标                                           |
| 安装       | maven安装、环境变量、maven配置文件修改             |
| 工程创建   | gavp属性理解、JavaSE/EE工程创建、项目结构          |
| 依赖管理   | 依赖添加、依赖传递、版本提取、导入依赖错误解决     |
| 构建管理   | 构建过程、构建场景、构建周期等                     |
| 继承和聚合 | 理解继承和聚合作用、继承语法和实践、聚合语法和实践 |



----

----

-------

----

# 



# Spring

# 



# 七、技术体系结构

  ## 1.1 总体技术体系
- 单一架构

    一个项目，一个工程，导出为一个war包，在一个Tomcat上运行。也叫all in one。

    

    单一架构，项目主要应用技术框架为：Spring , SpringMVC , Mybatis
- 分布式架构

    一个项目（对应 IDEA 中的一个 project），拆分成很多个模块，每个模块是一个 IDEA 中的一个 module。每一个工程都是运行在自己的 Tomcat 上。模块之间可以互相调用。每一个模块内部可以看成是一个单一架构的应用。

    

    分布式架构，项目主要应用技术框架：SpringBoot (SSM), SpringCloud , 中间件等

  ## 1.2 框架概念和理解

框架( Framework )是一个集成了基本结构、规范、设计模式、编程语言和程序库等基础组件的软件系统，它可以用来构建更高级别的应用程序。框架的设计和实现旨在解决特定领域中的常见问题，帮助开发人员更高效、更稳定地实现软件开发目标。



**框架的优点包括以下几点：**

1. 提高开发效率：框架提供了许多预先设计好了的组件和工具，能够帮助开发人员快速进行开发。相较于传统手写代码，在框架提供的规范化环境中，开发者可以更快地实现项目的各种要求。
2. 降低开发成本：框架的提供标准化的编程语言、数据操作等代码片段，避免了重复开发的问题，降低了开发成本，提供深度优化的系统，降低了维护成本，增强了系统的可靠性。
3. 提高应用程序的稳定性：框架通常经过了很长时间的开发和测试，其中的许多组件、代码片段和设计模式都得到了验证。重复利用这些组件有助于减少bug的出现，从而提高了应用程序的稳定性。
4. 提供标准化的解决方案：框架通常是针对某个特定领域的，通过提供标准化的解决方案，可以为开发人员提供一种共同的语言和思想基础，有助于更好地沟通和协作。

**框架的缺点包括以下几个方面：**

1. 学习成本高：框架通常具有特定的语言和编程范式。对于开发人员而言，需要花费时间学习其背后的架构、模式和逻辑，这对于新手而言可能会耗费较长时间。
2. 可能存在局限性：虽然框架提高了开发效率并可以帮助开发人员解决常见问题，但是在某些情况下，特定的应用需求可能超出框架的范围，从而导致应用程序无法满足要求。开发人员可能需要更多的控制权和自由度，同时需要在框架和应用程序之间进行权衡取舍。
3. 版本变更和兼容性问题：框架的版本发布和迭代通常会导致代码库的大规模变更，进而导致应用程序出现兼容性问题和漏洞。当框架变更时，需要考虑框架是否向下兼容，以及如何进行适当的测试、迁移和升级。
4. 架构风险：框架涉及到很多抽象和概念，如果开发者没有足够的理解和掌握其架构，可能会导致系统出现设计和架构缺陷，从而影响系统的健康性和安全性。

站在文件结构的角度理解框架，可以将框架总结：**框架 = jar包+配置文件**





# 八、SpringFramework介绍

  ## 2.1 Spring 和 SpringFramework概念

https://spring.io/projects

**广义的 Spring：Spring 技术栈**（全家桶）

广义上的 Spring 泛指以 Spring Framework 为基础的 Spring 技术栈。

经过十多年的发展，Spring 已经不再是一个单纯的应用框架，而是逐渐发展成为一个由多个不同子项目（模块）组成的成熟技术，例如 Spring Framework、Spring MVC、SpringBoot、Spring Cloud、Spring Data、Spring Security 等，其中 Spring Framework 是其他子项目的基础。

这些子项目涵盖了从企业级应用开发到云计算等各方面的内容，能够帮助开发人员解决软件发展过程中不断产生的各种实际问题，给开发人员带来了更好的开发体验。

**狭义的 Spring：Spring Framework**（基础框架）

狭义的 Spring 特指 Spring Framework，通常我们将它称为 Spring 框架。

Spring Framework（Spring框架）是一个开源的应用程序框架，由SpringSource公司开发，最初是为了解决企业级开发中各种常见问题而创建的。它提供了很多功能，例如：依赖注入（Dependency Injection）、面向切面编程（AOP）、声明式事务管理（TX）等。其主要目标是使企业级应用程序的开发变得更加简单和快速，并且Spring框架被广泛应用于Java企业开发领域。

Spring全家桶的其他框架都是以SpringFramework框架为基础！



  ## 2.2 SpringFramework主要功能模块



| 功能模块       | 功能介绍                                                    |
| -------------- | ----------------------------------------------------------- |
| Core Container | 核心容器，在 Spring 环境下使用任何功能都必须基于 IOC 容器。 |
| AOP&Aspects    | 面向切面编程                                                |
| TX             | 声明式事务管理。                                            |
| Spring MVC     | 提供了面向Web应用程序的集成功能。                           |


  ## 2.3 SpringFramework 主要优势
1. 丰富的生态系统：Spring 生态系统非常丰富，支持许多模块和库，如 Spring Boot、Spring Security、Spring Cloud 等等，可以帮助开发人员快速构建高可靠性的企业应用程序。
2. 模块化的设计：框架组件之间的松散耦合和模块化设计使得 Spring Framework 具有良好的可重用性、可扩展性和可维护性。开发人员可以轻松地选择自己需要的模块，根据自己的需求进行开发。
3. 简化 Java 开发：Spring Framework 简化了 Java 开发，提供了各种工具和 API，可以降低开发复杂度和学习成本。同时，Spring Framework 支持各种应用场景，包括 Web 应用程序、RESTful API、消息传递、批处理等等。
4. 不断创新和发展：Spring Framework 开发团队一直在不断创新和发展，保持与最新技术的接轨，为开发人员提供更加先进和优秀的工具和框架。

因此，这些优点使得 Spring Framework 成为了一个稳定、可靠、且创新的框架，为企业级 Java 开发提供了一站式的解决方案。

Spring 使创建 Java 企业应用程序变得容易。它提供了在企业环境中采用 Java 语言所需的一切，支持 Groovy 和 Kotlin 作为 JVM 上的替代语言，并且可以根据应用程序的需求灵活地创建多种架构。从Spring Framework 6.0.6开始，Spring 需要 Java 17+。

# 九、Spring IoC容器和核心概念

  ## 3.1 组件和组件管理概念



- **3.1.1 Spring充当组件管理角色（IoC）**

  

  组件可以完全交给Spring 框架进行管理，Spring框架替代了程序员原有的new对象和对象属性赋值动作等！

  Spring具体的组件管理动作包含：

  - 组件对象实例化
  - 组件属性属性赋值
  - 组件对象之间引用
  - 组件对象存活周期管理
  - ......

  我们只需要编写元数据（配置文件）告知Spring 管理哪些类组件和他们的关系即可！

  注意：组件是映射到应用程序中所有可重用组件的Java对象，应该是可复用的功能对象！

  - 组件一定是对象
  - 对象不一定是组件

  综上所述，Spring 充当一个组件容器，创建、管理、存储组件，减少了我们的编码压力，让我们更加专注进行业务编写！

- **3.1.2 组件交给Spring管理优势**!

  1. 降低了组件之间的耦合性：Spring IoC容器通过依赖注入机制，将组件之间的依赖关系削弱，减少了程序组件之间的耦合性，使得组件更加松散地耦合。
  2. 提高了代码的可重用性和可维护性：将组件的实例化过程、依赖关系的管理等功能交给Spring IoC容器处理，使得组件代码更加模块化、可重用、更易于维护。
  3. 方便了配置和管理：Spring IoC容器通过XML文件或者注解，轻松的对组件进行配置和管理，使得组件的切换、替换等操作更加的方便和快捷。
  4. 交给Spring管理的对象（组件），方可享受Spring框架的其他功能（AOP,声明事务管理）等


## 3.2Spring IoC**容器和容器实现**

### **3.2.1 普通和复杂容器**

**普通容器**

  生活中的普通容器

  ![](http://heavy_code_industry.gitee.io/code_heavy_industry/assets/img/img002.6e874877.png)

> 普通容器只能用来存储，没有更多功能。

  程序中的普通容器

  - 数组
  - 集合：List
  - 集合：Set

**复杂容器**

  生活中的复杂容器

  ![](http://heavy_code_industry.gitee.io/code_heavy_industry/assets/img/img003.6f9c041c.png)

> 政府管理我们的一生，生老病死都和政府有关。

  程序中的复杂容器

  Servlet 容器能够管理 Servlet(init,service,destroy)、Filter、Listener 这样的组件的一生，所以它是一个复杂容器。

| 名称       | 时机                                                         | 次数 |
| ---------- | ------------------------------------------------------------ | ---- |
| 创建对象   | 默认情况：接收到第一次请求  修改启动顺序后：Web应用启动过程中 | 一次 |
| 初始化操作 | 创建对象之后                                                 | 一次 |
| 处理请求   | 接收到请求                                                   | 多次 |
| 销毁操作   | Web应用卸载之前                                              | 一次 |

  我们即将要学习的 SpringIoC 容器也是一个复杂容器。它们不仅要负责创建组件的对象、存储组件的对象，还要负责调用组件的方法让它们工作，最终在特定情况下销毁组件。

  总结：Spring管理组件的容器，就是一个复杂容器，不仅存储组件，也可以管理组件之间依赖关系，并且创建和销毁组件等！

### 3.2.2 SpringIoC容器介绍

Spring IoC 容器，负责实例化、配置和组装 bean（组件）。容器通过读取配置元数据来获取有关要实例化、配置和组装组件的指令。配置元数据以 XML、Java 注解或 Java 代码形式表现。它允许表达组成应用程序的组件以及这些组件之间丰富的相互依赖关系。

### 3.2.3 SpringIoC容器具体接口和实现类

**SpringIoc容器接口**： 

`BeanFactory` 接口提供了一种高级配置机制，能够管理任何类型的对象，它是SpringIoC容器标准化超接口！

`ApplicationContext` 是 `BeanFactory` 的子接口。它扩展了以下功能：

- 更容易与 Spring 的 AOP 功能集成
- 消息资源处理（用于国际化）
- 特定于应用程序给予此接口实现，例如Web 应用程序的 `WebApplicationContext`

简而言之， `BeanFactory` 提供了配置框架和基本功能，而 `ApplicationContext` 添加了更多特定于企业的功能。 `ApplicationContext` 是 `BeanFactory` 的完整超集！

**ApplicationContext容器实现类**：

![](http://heavy_code_industry.gitee.io/code_heavy_industry/assets/img/img004.f6680aef.png)

| 类型名                             | 简介                                                         |
| ---------------------------------- | ------------------------------------------------------------ |
| ClassPathXmlApplicationContext     | 通过读取类路径下的 XML 格式的配置文件创建 IOC 容器对象       |
| FileSystemXmlApplicationContext    | 通过文件系统路径读取 XML 格式的配置文件创建 IOC 容器对象     |
| AnnotationConfigApplicationContext | 通过读取Java配置类创建 IOC 容器对象                          |
| WebApplicationContext              | 专门为 Web 应用准备，基于 Web 环境创建 IOC 容器对象，并将对象引入存入 ServletContext 域中。 |

### 3.2.4 SpringIoC容器管理配置方式

Spring IoC 容器使用多种形式的配置元数据。此配置元数据表示作为应用程序开发人员如何告诉 Spring 容器实例化、配置和组装应用程序中的对象。



Spring框架提供了多种配置方式：XML配置方式、注解方式和Java配置类方式

1. XML配置方式：是Spring框架最早的配置方式之一，通过在XML文件中定义Bean及其依赖关系、Bean的作用域等信息，让Spring IoC容器来管理Bean之间的依赖关系。该方式从Spring框架的第一版开始提供支持。
2. 注解方式：从Spring 2.5版本开始提供支持，可以通过在Bean类上使用注解来代替XML配置文件中的配置信息。通过在Bean类上加上相应的注解（如@Component, @Service, @Autowired等），将Bean注册到Spring IoC容器中，这样Spring IoC容器就可以管理这些Bean之间的依赖关系。
3. **Java配置类**方式：从Spring 3.0版本开始提供支持，通过Java类来定义Bean、Bean之间的依赖关系和配置信息，从而代替XML配置文件的方式。Java配置类是一种使用Java编写配置信息的方式，通过@Configuration、@Bean等注解来实现Bean和依赖关系的配置。



  ## 3.3 Spring IoC / DI概念总结

- **IoC容器**

  Spring IoC 容器，负责实例化、配置和组装 bean（组件）核心容器。容器通过读取配置元数据来获取有关要实例化、配置和组装组件的指令。

- **IoC（Inversion of Control）控制反转**

  IoC 主要是针对对象的创建和调用控制而言的，也就是说，当应用程序需要使用一个对象时，不再是应用程序直接创建该对象，而是由 IoC 容器来创建和管理，即控制权由应用程序转移到 IoC 容器中，也就是“反转”了控制权。这种方式基本上是通过依赖查找的方式来实现的，即 IoC 容器维护着构成应用程序的对象，并负责创建这些对象。

- **DI (Dependency Injection) 依赖注入**

  DI 是指在组件之间传递依赖关系的过程中，将依赖关系在容器内部进行处理，这样就不必在应用程序代码中硬编码对象之间的依赖关系，实现了对象之间的解耦合。在 Spring 中，DI 是通过 XML 配置文件或注解的方式实现的。它提供了三种形式的依赖注入：构造函数注入、Setter 方法注入和接口注入。

# 十、Spring IoC实践和应用

## 4.1 Spring IoC / DI 实现步骤

> 我们总结下，组件交给Spring IoC容器管理，并且获取和使用的基本步骤！

1. **配置元数据（配置）**

    配置元数据，既是编写交给SpringIoC容器管理组件的信息，配置方式有三种。

    基于 XML 的配置元数据的基本结构：

    <bean id="..." [1] class="..." [2]>  
<!-- collaborators and configuration for this bean go here -->

  </bean>

```XML
<?xml version="1.0" encoding="UTF-8"?>
<!-- 此处要添加一些约束，配置文件的标签并不是随意命名 -->
<beans xmlns="http://www.springframework.org/schema/beans"
  xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
  xsi:schemaLocation="http://www.springframework.org/schema/beans
    https://www.springframework.org/schema/beans/spring-beans.xsd">

  <bean id="..." [1] class="..." [2]>  
    <!-- collaborators and configuration for this bean go here -->
  </bean>

  <bean id="..." class="...">
    <!-- collaborators and configuration for this bean go here -->
  </bean>
  <!-- more bean definitions go here -->
</beans>
```

Spring IoC 容器管理一个或多个组件。这些 组件是使用你提供给容器的配置元数据（例如，以 XML `<bean/>` 定义的形式）创建的。

    <bean /> 标签 == 组件信息声明
    
    - `id` 属性是标识单个 Bean 定义的字符串。
    - `class` 属性定义 Bean 的类型并使用完全限定的类名。
2. **实例化IoC容器**

    提供给 `ApplicationContext` 构造函数的位置路径是资源字符串地址，允许容器从各种外部资源（如本地文件系统、Java `CLASSPATH` 等）加载配置元数据。

    我们应该选择一个合适的容器实现类，进行IoC容器的实例化工作：

```Java
//实例化ioc容器,读取外部配置文件,最终会在容器内进行ioc和di动作
ApplicationContext context = 
           new ClassPathXmlApplicationContext("services.xml", "daos.xml");
```
3. **获取Bean（组件）**

    `ApplicationContext` 是一个高级工厂的接口，能够维护不同 bean 及其依赖项的注册表。通过使用方法 `T getBean(String name, Class<T> requiredType)` ，您可以检索 bean 的实例。

    允许读取 Bean 定义并访问它们，如以下示例所示：

```Java
//创建ioc容器对象，指定配置文件，ioc也开始实例组件对象
ApplicationContext context = new ClassPathXmlApplicationContext("services.xml", "daos.xml");
//获取ioc容器的组件对象
PetStoreService service = context.getBean("petStore", PetStoreService.class);
//使用组件对象
List<String> userList = service.getUsernameList();
```

  ## 4.2 基于XML配置方式组件管理

#### 4.2.1 实验一： 组件（Bean）信息声明配置（IoC）
  1. 目标

      Spring IoC 容器管理一个或多个 bean。这些 Bean 是使用您提供给容器的配置元数据创建的（例如，以 XML `<bean/>` 定义的形式）。

      
  2. 思路

      ![](http://heavy_code_industry.gitee.io/code_heavy_industry/assets/img/img006.c8bae859.png)
  3. 准备项目
      1. 创建maven工程（spring-ioc-xml-01）
      2. 导入SpringIoC相关依赖

          pom.xml

```XML
<dependencies>
    <!--spring context依赖-->
    <!--当你引入Spring Context依赖之后，表示将Spring的基础依赖引入了-->
    <dependency>
        <groupId>org.springframework</groupId>
        <artifactId>spring-context</artifactId>
        <version>6.0.6</version>
    </dependency>
    <!--junit5测试-->
    <dependency>
        <groupId>org.junit.jupiter</groupId>
        <artifactId>junit-jupiter-api</artifactId>
        <version>5.3.1</version>
    </dependency>
</dependencies>
```
 4. 基于无参数构造函数

      > 当通过构造函数方法创建一个 bean（组件对象） 时，所有普通类都可以由 Spring 使用并与之兼容。也就是说，正在开发的类不需要实现任何特定的接口或以特定的方式进行编码。只需指定 Bean 类信息就足够了。但是，默认情况下，我们需要一个默认（空）构造函数。

      1. 准备组件类

```Java
package com.atguigu.ioc;


public class HappyComponent {

    //默认包含无参数构造函数

    public void doWork() {
        System.out.println("HappyComponent.doWork");
    }
}
```
 2. xml配置文件编写

          创建携带spring约束的xml配置文件

        

          编写配置文件：

          文件：resources/spring-bean-01.xml

```Java
<!-- 实验一 [重要]创建bean -->
<bean id="happyComponent" class="com.atguigu.ioc.HappyComponent"/>
```

- bean标签：通过配置bean标签告诉IOC容器需要创建对象的组件信息
          - id属性：bean的唯一标识,方便后期获取Bean！
          - class属性：组件类的全限定符！
          - 注意：要求当前组件类必须包含无参数构造函数！
  5. 基于静态工厂方法实例化

      > 除了使用构造函数实例化对象，还有一类是通过工厂模式实例化对象。接下来我们讲解如何定义使用静态工厂方法创建Bean的配置 ！

      1. 准备组件类

```Java
public class ClientService {
  private static ClientService clientService = new ClientService();
  private ClientService() {}

  public static ClientServicecreateInstance() {
  
    return clientService;
  }
}
```
- bean标签：通过配置bean标签告诉IOC容器需要创建对象的组件信息
          - id属性：bean的唯一标识,方便后期获取Bean！
          - class属性：组件类的全限定符！
          - 注意：要求当前组件类必须包含无参数构造函数！
  5. 基于静态工厂方法实例化

      > 除了使用构造函数实例化对象，还有一类是通过工厂模式实例化对象。接下来我们讲解如何定义使用静态工厂方法创建Bean的配置 ！

      1. 准备组件类

```XML
<bean id="clientService"
  class="examples.ClientService"
  factory-method="createInstance"/>
```

- class属性：指定工厂类的全限定符！
          - factory-method: 指定静态工厂方法，注意，该方法必须是static方法。
  6. 基于实例工厂方法实例化

      > 接下来我们讲解下如何定义使用实例工厂方法创建Bean的配置 ！

      1. 准备组建类

```Java
public class DefaultServiceLocator {

  private static ClientServiceImplclientService = new ClientServiceImpl();

  public ClientService createClientServiceInstance() {
    return clientService;
  }
}
```
2. xml配置文件编写

          文件：resources/spring-bean-01.xml

```XML
<!-- 将工厂类进行ioc配置 -->
<bean id="serviceLocator" class="examples.DefaultServiceLocator">
</bean>

<!-- 根据工厂对象的实例工厂方法进行实例化组件对象 -->
<bean id="clientService"
  factory-bean="serviceLocator"
  factory-method="createClientServiceInstance"/>
```

 - factory-bean属性：指定当前容器中工厂Bean 的名称。
          - factory-method:  指定实例工厂方法名。注意，实例方法必须是非static的！



#### 4.2.2 实验二： 组件（Bean）依赖注入配置（DI）
  1. 目标

      通过配置文件,实现IoC容器中Bean之间的引用（依赖注入DI配置）。

      主要涉及注入场景：基于构造函数的依赖注入和基于 Setter 的依赖注入。
      
      
      
  3. 基于构造函数的依赖注入（单个构造参数）
      1. 介绍

          基于构造函数的 DI 是通过容器调用具有多个参数的构造函数来完成的，每个参数表示一个依赖项。

          下面的示例演示一个只能通过构造函数注入进行依赖项注入的类！
      2. 准备组件类

```Java
public class UserDao {
}


public class UserService {
    
    private UserDao userDao;

    public UserService(UserDao userDao) {
        this.userDao = userDao;
    }
}

```
3. 编写配置文件

          文件：resources/spring-02.xml

```XML
<beans>
  <!-- 引用类bean声明 -->
  <bean id="userService" class="x.y.UserService">
   <!-- 构造函数引用 -->
    <constructor-arg ref="userDao"/>
  </bean>
  <!-- 被引用类bean声明 -->
  <bean id="userDao" class="x.y.UserDao"/>
</beans>
```

 - constructor-arg标签：可以引用构造参数 ref引用其他bean的标识。
  4. 基于构造函数的依赖注入（多构造参数解析）
      1. 介绍

          基于构造函数的 DI 是通过容器调用具有多个参数的构造函数来完成的，每个参数表示一个依赖项。

          下面的示例演示通过构造函数注入多个参数，参数包含其他bean和基本数据类型！
      2. 准备组件类

```Java
public class UserDao {
}


public class UserService {
    
    private UserDao userDao;
    
    private int age;
    
    private String name;

    public UserService(int age , String name ,UserDao userDao) {
        this.userDao = userDao;
        this.age = age;
        this.name = name;
    }
}
```
3. 编写配置文件

```XML
<!-- 场景1: 多参数，可以按照相应构造函数的顺序注入数据 -->
<beans>
  <bean id="userService" class="x.y.UserService">
    <!-- value直接注入基本类型值 -->
    <constructor-arg  value="18"/>
    <constructor-arg  value="赵伟风"/>
    
    <constructor-arg  ref="userDao"/>
  </bean>
  <!-- 被引用类bean声明 -->
  <bean id="userDao" class="x.y.UserDao"/>
</beans>


<!-- 场景2: 多参数，可以按照相应构造函数的名称注入数据 -->
<beans>
  <bean id="userService" class="x.y.UserService">
    <!-- value直接注入基本类型值 -->
    <constructor-arg name="name" value="赵伟风"/>
    <constructor-arg name="userDao" ref="userDao"/>
    <constructor-arg name="age"  value="18"/>
  </bean>
  <!-- 被引用类bean声明 -->
  <bean id="userDao" class="x.y.UserDao"/>
</beans>

<!-- 场景2: 多参数，可以按照相应构造函数的角标注入数据 
           index从0开始 构造函数(0,1,2....)
-->
<beans>
    <bean id="userService" class="x.y.UserService">
    <!-- value直接注入基本类型值 -->
    <constructor-arg index="1" value="赵伟风"/>
    <constructor-arg index="2" ref="userDao"/>
    <constructor-arg index="0"  value="18"/>
  </bean>
  <!-- 被引用类bean声明 -->
  <bean id="userDao" class="x.y.UserDao"/>
</beans>

```
- constructor-arg标签：指定构造参数和对应的值
          - constructor-arg标签：name属性指定参数名、index属性指定参数角标、value属性指定普通属性值
  5. **基于Setter方法依赖注入**
      1. 介绍

          开发中，除了构造函数注入（DI）更多的使用的Setter方法进行注入！

          下面的示例演示一个只能使用纯 setter 注入进行依赖项注入的类。
      2. 准备组件类

```Java
public Class MovieFinder{

}

public class SimpleMovieLister {

  private MovieFinder movieFinder;
  
  private String movieName;

  public void setMovieFinder(MovieFinder movieFinder) {
    this.movieFinder = movieFinder;
  }
  
  public void setMovieName(String movieName){
    this.movieName = movieName;
  }

  // business logic that actually uses the injected MovieFinder is omitted...
}
```
3. 编写配置文件

```XML
<bean id="simpleMovieLister" class="examples.SimpleMovieLister">
  <!-- setter方法，注入movieFinder对象的标识id
       name = 属性名  ref = 引用bean的id值
   -->
  <property name="movieFinder" ref="movieFinder" />

  <!-- setter方法，注入基本数据类型movieName
       name = 属性名 value= 基本类型值
   -->
  <property name="movieName" value="消失的她"/>
</bean>

<bean id="movieFinder" class="examples.MovieFinder"/>

```
 - property标签： 可以给setter方法对应的属性赋值
          - property 标签： name属性代表**set方法标识**、ref代表引用bean的标识id、value属性代表基本属性值

  **总结：**

    依赖注入（DI）包含引用类型和基本数据类型，同时注入的方式也有多种！主流的注入方式为setter方法注入和构造函数注入，两种注入语法都需要掌握！
    
    需要特别注意：引用其他bean，使用ref属性。直接注入基本类型值，使用value属性。

#### 4.2.3 实验三： IoC容器创建和使用
  1. 介绍

      上面的实验只是讲解了如何在XML格式的配置文件编写IoC和DI配置！

      想要配置文件中声明组件类信息真正的进行实例化成Bean对象和形成Bean之间的引用关系，我们需要声明IoC容器对象，读取配置文件，实例化组件和关系维护的过程都是在IoC容器中实现的！
  2. 容器实例化

```Java
//方式1:实例化并且指定配置文件
//参数：String...locations 传入一个或者多个配置文件
ApplicationContext context = 
           new ClassPathXmlApplicationContext("services.xml", "daos.xml");
           
//方式2:先实例化，再指定配置文件，最后刷新容器触发Bean实例化动作 [springmvc源码和contextLoadListener源码方式]  
ApplicationContext context = 
           new ClassPathXmlApplicationContext();   
//设置配置配置文件,方法参数为可变参数,可以设置一个或者多个配置
iocContainer1.setConfigLocations("services.xml", "daos.xml");
//后配置的文件,需要调用refresh方法,触发刷新配置
iocContainer1.refresh();           

```
3. Bean对象读取

```Java
//方式1: 根据id获取
//没有指定类型,返回为Object,需要类型转化!
HappyComponent happyComponent = 
        (HappyComponent) iocContainer.getBean("bean的id标识");
        
//使用组件对象        
happyComponent.doWork();

//方式2: 根据类型获取
//根据类型获取,但是要求,同类型(当前类,或者之类,或者接口的实现类)只能有一个对象交给IoC容器管理
//配置两个或者以上出现: org.springframework.beans.factory.NoUniqueBeanDefinitionException 问题
HappyComponent happyComponent = iocContainer.getBean(HappyComponent.class);
happyComponent.doWork();

//方式3: 根据id和类型获取
HappyComponent happyComponent = iocContainer.getBean("bean的id标识", HappyComponent.class);
happyComponent.doWork();

根据类型来获取bean时，在满足bean唯一性的前提下，其实只是看：『对象 instanceof 指定的类型』的返回结果，
只要返回的是true就可以认定为和类型匹配，能够获取到。
```

#### 4.2.4 实验四： 高级特性：组件（Bean）作用域和周期方法配置
  1. 组件周期方法配置
      1. 周期方法概念

          我们可以在组件类中定义方法，然后当IoC容器实例化和销毁组件对象的时候进行调用！这两个方法我们成为生命周期方法！

          类似于Servlet的init/destroy方法,我们可以在周期方法完成初始化和释放资源等工作。
      2. 周期方法声明

```Java
public class BeanOne {

  //周期方法要求： 方法命名随意，但是要求方法必须是 public void 无形参列表
  public void init() {
    // 初始化逻辑
  }
}

public class BeanTwo {

  public void cleanup() {
    // 释放资源逻辑
  }
}
```
3. 周期方法配置

```XML
<beans>
  <bean id="beanOne" class="examples.BeanOne" init-method="init" />
  <bean id="beanTwo" class="examples.BeanTwo" destroy-method="cleanup" />
</beans>
```
2. 组件作用域配置
      1. Bean作用域概念

          `<bean` 标签声明Bean，只是将Bean的信息配置给SpringIoC容器！

          在IoC容器中，这些`<bean`标签对应的信息转成Spring内部 `BeanDefinition` 对象，`BeanDefinition` 对象内，包含定义的信息（id,class,属性等等）！

          这意味着，`BeanDefinition`与`类`概念一样，SpringIoC容器可以可以根据`BeanDefinition`对象反射创建多个Bean对象实例。

          具体创建多少个Bean的实例对象，由Bean的作用域Scope属性指定！
      2. 作用域可选值

| 取值      | 含义                                        | 创建对象的时机   | 默认值 |
| --------- | ------------------------------------------- | ---------------- | ------ |
| singleton | 在 IOC 容器中，这个 bean 的对象始终为单实例 | IOC 容器初始化时 | 是     |
| prototype | 这个 bean 在 IOC 容器中有多个实例           | 获取 bean 时     | 否     |


              如果是在WebApplicationContext环境下还会有另外两个作用域（但不常用）：

| 取值    | 含义                 | 创建对象的时机 | 默认值 |
| ------- | -------------------- | -------------- | ------ |
| request | 请求范围内有效的实例 | 每次请求       | 否     |
| session | 会话范围内有效的实例 | 每次会话       | 否     |

3. 作用域配置

      配置scope范围

```XML
<!--bean的作用域 
    准备两个引用关系的组件类即可！！
-->
<!-- scope属性：取值singleton（默认值），bean在IOC容器中只有一个实例，IOC容器初始化时创建对象 -->
<!-- scope属性：取值prototype，bean在IOC容器中可以有多个实例，getBean()时创建对象 -->
<bean id="happyMachine8" scope="prototype" class="com.atguigu.ioc.HappyMachine">
    <property name="machineName" value="happyMachine"/>
</bean>

<bean id="happyComponent8" scope="singleton" class="com.atguigu.ioc.HappyComponent">
    <property name="componentName" value="happyComponent"/>
</bean>
```
4. 作用域测试

```Java
@Test
public void testExperiment08()  {
    ApplicationContext iocContainer = new ClassPathXmlApplicationContext("配置文件名");

    HappyMachine bean = iocContainer.getBean(HappyMachine.class);
    HappyMachine bean1 = iocContainer.getBean(HappyMachine.class);
    //多例对比 false
    System.out.println(bean == bean1);

    HappyComponent bean2 = iocContainer.getBean(HappyComponent.class);
    HappyComponent bean3 = iocContainer.getBean(HappyComponent.class);
    //单例对比 true
    System.out.println(bean2 == bean3);
}
```

#### 4.2.5 实验五： 高级特性：FactoryBean特性和使用
  1. FactoryBean简介

      `FactoryBean` 接口是Spring IoC容器实例化逻辑的可插拔性点。

      用于配置复杂的Bean对象，可以将创建过程存储在`FactoryBean` 的getObject方法！

      `FactoryBean<T>` 接口提供三种方法：

      - `T getObject()`: 

          返回此工厂创建的对象的实例。该返回值会被存储到IoC容器！
      - `boolean isSingleton()`: 

          如果此 `FactoryBean` 返回单例，则返回 `true` ，否则返回 `false` 。此方法的默认实现返回 `true` （注意，lombok插件使用，可能影响效果）。
      - `Class<?> getObjectType()`: 返回 `getObject()` 方法返回的对象类型，如果事先不知道类型，则返回 `null` 。

  2. FactoryBean使用场景
      1. 代理类的创建
      2. 第三方框架整合
      3. 复杂对象实例化等
  3. Factorybean应用
      1. 准备FactoryBean实现类

```Java
// 实现FactoryBean接口时需要指定泛型
// 泛型类型就是当前工厂要生产的对象的类型
public class HappyFactoryBean implements FactoryBean<HappyMachine> {
    
    private String machineName;
    
    public String getMachineName() {
        return machineName;
    }
    
    public void setMachineName(String machineName) {
        this.machineName = machineName;
    }
    
    @Override
    public HappyMachine getObject() throws Exception {
    
        // 方法内部模拟创建、设置一个对象的复杂过程
        HappyMachine happyMachine = new HappyMachine();
    
        happyMachine.setMachineName(this.machineName);
    
        return happyMachine;
    }
    
    @Override
    public Class<?> getObjectType() {
    
        // 返回要生产的对象的类型
        return HappyMachine.class;
    }
}
```
2. 配置FactoryBean实现类

```XML
<!-- FactoryBean机制 -->
<!-- 这个bean标签中class属性指定的是HappyFactoryBean，但是将来从这里获取的bean是HappyMachine对象 -->
<bean id="happyMachine7" class="com.atguigu.ioc.HappyFactoryBean">
    <!-- property标签仍然可以用来通过setXxx()方法给属性赋值 -->
    <property name="machineName" value="iceCreamMachine"/>
</bean>
```
3. 测试读取FactoryBean和FactoryBean.getObject对象

```Java
@Test
public void testExperiment07()  {

    ApplicationContext iocContainer = new ClassPathXmlApplicationContext("spring-bean-07.xml");

    //注意: 直接根据声明FactoryBean的id,获取的是getObject方法返回的对象
    HappyMachine happyMachine = iocContainer.getBean("happyMachine7",HappyMachine.class);
    System.out.println("happyMachine = " + happyMachine);

    //如果想要获取FactoryBean对象, 直接在id前添加&符号即可!  &happyMachine7 这是一种固定的约束
    Object bean = iocContainer.getBean("&happyMachine7");
    System.out.println("bean = " + bean);
}
```
4. FactoryBean和BeanFactory区别

      **FactoryBean **是 Spring 中一种特殊的 bean，可以在 getObject() 工厂方法自定义的逻辑创建Bean！是一种能够生产其他 Bean 的 Bean。FactoryBean 在容器启动时被创建，而在实际使用时则是通过调用 getObject() 方法来得到其所生产的 Bean。因此，FactoryBean 可以自定义任何所需的初始化逻辑，生产出一些定制化的 bean。

      一般情况下，整合第三方框架，都是通过定义FactoryBean实现！！！

      **BeanFactory** 是 Spring 框架的基础，其作为一个顶级接口定义了容器的基本行为，例如管理 bean 的生命周期、配置文件的加载和解析、bean 的装配和依赖注入等。BeanFactory 接口提供了访问 bean 的方式，例如 getBean() 方法获取指定的 bean 实例。它可以从不同的来源（例如 Mysql 数据库、XML 文件、Java 配置类等）获取 bean 定义，并将其转换为 bean 实例。同时，BeanFactory 还包含很多子类（例如，ApplicationContext 接口）提供了额外的强大功能。

      总的来说，FactoryBean 和 BeanFactory 的区别主要在于前者是用于创建 bean 的接口，它提供了更加灵活的初始化定制功能，而后者是用于管理 bean 的框架基础接口，提供了基本的容器功能和 bean 生命周期管理。

#### 4.2.6 实验六： 基于XML方式整合三层架构组件
  1. 需求分析

      搭建一个三层架构案例，模拟查询全部学生（学生表）信息，持久层使用JdbcTemplate和Druid技术，使用XML方式进行组件管理！

  2. 数据库准备

```Java
create database studb;

use studb;

CREATE TABLE students (
  id INT PRIMARY KEY,
  name VARCHAR(50) NOT NULL,
  gender VARCHAR(10) NOT NULL,
  age INT,
  class VARCHAR(50)
);

INSERT INTO students (id, name, gender, age, class)
VALUES
  (1, '张三', '男', 20, '高中一班'),
  (2, '李四', '男', 19, '高中二班'),
  (3, '王五', '女', 18, '高中一班'),
  (4, '赵六', '女', 20, '高中三班'),
  (5, '刘七', '男', 19, '高中二班'),
  (6, '陈八', '女', 18, '高中一班'),
  (7, '杨九', '男', 20, '高中三班'),
  (8, '吴十', '男', 19, '高中二班');

```
3. 项目准备
      1. 项目创建

          spring-xml-practice-02
      2. 依赖导入

```XML
<dependencies>
      <!--spring context依赖-->
      <!--当你引入SpringContext依赖之后，表示将Spring的基础依赖引入了-->
      <dependency>
          <groupId>org.springframework</groupId>
          <artifactId>spring-context</artifactId>
          <version>6.0.6</version>
      </dependency>

      <!-- 数据库驱动和连接池-->
      <dependency>
          <groupId>mysql</groupId>
          <artifactId>mysql-connector-java</artifactId>
          <version>8.0.25</version>
      </dependency>

      <dependency>
          <groupId>com.alibaba</groupId>
          <artifactId>druid</artifactId>
          <version>1.2.8</version>
      </dependency>

      <!-- spring-jdbc -->
      <dependency>
          <groupId>org.springframework</groupId>
          <artifactId>spring-jdbc</artifactId>
          <version>6.0.6</version>
      </dependency>

</dependencies> 
```
3. 实体类准备

```Java
public class Student {

    private Integer id;
    private String name;
    private String gender;
    private Integer age;
    private String classes;

    public Integer getId() {
        return id;
    }

    public void setId(Integer id) {
        this.id = id;
    }

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }

    public String getGender() {
        return gender;
    }

    public void setGender(String gender) {
        this.gender = gender;
    }

    public Integer getAge() {
        return age;
    }

    public void setAge(Integer age) {
        this.age = age;
    }

    public String getClasses() {
        return classes;
    }

    public void setClasses(String classes) {
        this.classes = classes;
    }

    @Override
    public String toString() {
        return "Student{" +
                "id=" + id +
                ", name='" + name + '\'' +
                ", gender='" + gender + '\'' +
                ", age=" + age +
                ", classes='" + classes + '\'' +
                '}';
    }
}

```
4. JdbcTemplate技术讲解

      > 为了在特定领域帮助我们简化代码，Spring 封装了很多 『Template』形式的模板类。例如：RedisTemplate、RestTemplate 等等，包括我们今天要学习的 JdbcTemplate。

      jdbc.properties

      提取数据库连接信息

```.properties
atguigu.url=jdbc:mysql://localhost:3306/studb
atguigu.driver=com.mysql.cj.jdbc.Driver
atguigu.username=root
atguigu.password=root
```

          springioc配置文件

```XML
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xmlns:context="http://www.springframework.org/schema/context"
       xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd 
       http://www.springframework.org/schema/context https://www.springframework.org/schema/context/spring-context.xsd">


    <!-- 导入外部属性文件 -->
    <context:property-placeholder location="classpath:jdbc.properties" />

    <!-- 配置数据源 -->
    <bean id="druidDataSource" class="com.alibaba.druid.pool.DruidDataSource">
        <property name="url" value="${atguigu.url}"/>
        <property name="driverClassName" value="${atguigu.driver}"/>
        <property name="username" value="${atguigu.username}"/>
        <property name="password" value="${atguigu.password}"/>
    </bean>

    <!-- 配置 JdbcTemplate -->
    <bean id="jdbcTemplate" class="org.springframework.jdbc.core.JdbcTemplate">
        <!-- 装配数据源 -->
        <property name="dataSource" ref="druidDataSource"/>
    </bean>
    
</beans>
```

          基于jdbcTemplate的CRUD使用

```Java
public class JdbcTemplateTest {


    /**
     * 使用jdbcTemplate进行DML动作
     */
    @Test
    public void testDML(){

        ApplicationContext applicationContext =
                new ClassPathXmlApplicationContext("spring-ioc.xml");

        JdbcTemplate jdbcTemplate = applicationContext.getBean(JdbcTemplate.class);

        //TODO 执行插入一条学员数据
        String sql = "insert into students (id,name,gender,age,class) values (?,?,?,?,?);";
    /*
        参数1: sql语句
        参数2: 可变参数,占位符的值
     */
        int rows = jdbcTemplate.update(sql, 9,"十一", "男", 18, "二年三班");

        System.out.println("rows = " + rows);

    }


    /**
     * 查询单条实体对象
     *   public class Student {
     *     private Integer id;
     *     private String name;
     *     private String gender;
     *     private Integer age;
     *     private String classes;
     */
    @Test
    public void testDQLForPojo(){

        String sql = "select id , name , age , gender , class as classes from students where id = ? ;";

        ApplicationContext applicationContext =
                new ClassPathXmlApplicationContext("spring-ioc.xml");

        JdbcTemplate jdbcTemplate = applicationContext.getBean(JdbcTemplate.class);

        //根据id查询
        Student student = jdbcTemplate.queryForObject(sql,  (rs, rowNum) -> {
            //自己处理结果映射
            Student stu = new Student();
            stu.setId(rs.getInt("id"));
            stu.setName(rs.getString("name"));
            stu.setAge(rs.getInt("age"));
            stu.setGender(rs.getString("gender"));
            stu.setClasses(rs.getString("classes"));
            return stu;
        }, 2);

        System.out.println("student = " + student);
    }



    /**
     * 查询实体类集合
     */
    @Test
    public void testDQLForListPojo(){

        String sql = "select id , name , age , gender , class as classes from students  ;";

        ApplicationContext applicationContext =
                new ClassPathXmlApplicationContext("spring-ioc.xml");

        JdbcTemplate jdbcTemplate = applicationContext.getBean(JdbcTemplate.class);
    /*
        query可以返回集合!
        BeanPropertyRowMapper就是封装好RowMapper的实现,要求属性名和列名相同即可
     */
        List<Student> studentList = jdbcTemplate.query(sql, new BeanPropertyRowMapper<>(Student.class));

        System.out.println("studentList = " + studentList);
    }

}

```
5. 三层架构搭建和实现
      1. 持久层

```Java
//接口
public interface StudentDao {

    /**
     * 查询全部学生数据
     * @return
     */
    List<Student> queryAll();
}

//实现类
public class StudentDaoImpl implements StudentDao {

    private JdbcTemplate jdbcTemplate;

    public void setJdbcTemplate(JdbcTemplate jdbcTemplate) {
        this.jdbcTemplate = jdbcTemplate;
    }

    /**
     * 查询全部学生数据
     * @return
     */
    @Override
    public List<Student> queryAll() {

        String sql = "select id , name , age , gender , class as classes from students ;";

        /*
          query可以返回集合!
          BeanPropertyRowMapper就是封装好RowMapper的实现,要求属性名和列名相同即可
         */
        List<Student> studentList = jdbcTemplate.query(sql, new BeanPropertyRowMapper<>(Student.class));

        return studentList;
   }
}

```
2. 业务层

```Java
//接口
public interface StudentService {

    /**
     * 查询全部学员业务
     * @return
     */
    List<Student> findAll();

}

//实现类
public class StudentServiceImpl  implements StudentService {
    
    private StudentDao studentDao;

    public void setStudentDao(StudentDao studentDao) {
        this.studentDao = studentDao;
    }

    /**
     * 查询全部学员业务
     * @return
     */
    @Override
    public List<Student> findAll() {
        
        List<Student> studentList =  studentDao.queryAll();
        
        return studentList;
    }
}

```
3. 表述层

```Java
public class StudentController {
    
    private StudentService studentService;

    public void setStudentService(StudentService studentService) {
        this.studentService = studentService;
    }
    
    public void  findAll(){
       List<Student> studentList =  studentService.findAll();
        System.out.println("studentList = " + studentList);
    }
}
```
6. 三层架构IoC配置

```XML
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xmlns:context="http://www.springframework.org/schema/context"
       xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd http://www.springframework.org/schema/context https://www.springframework.org/schema/context/spring-context.xsd">


    <!-- 导入外部属性文件 -->
    <context:property-placeholder location="classpath:jdbc.properties" />

    <!-- 配置数据源 -->
    <bean id="druidDataSource" class="com.alibaba.druid.pool.DruidDataSource">
        <property name="url" value="${atguigu.url}"/>
        <property name="driverClassName" value="${atguigu.driver}"/>
        <property name="username" value="${atguigu.username}"/>
        <property name="password" value="${atguigu.password}"/>
    </bean>

    <!-- 配置 JdbcTemplate -->
    <bean id="jdbcTemplate" class="org.springframework.jdbc.core.JdbcTemplate">
        <!-- 装配数据源 -->
        <property name="dataSource" ref="druidDataSource"/>
    </bean>


    <bean id="studentDao" class="com.atguigu.dao.impl.StudentDaoImpl">
        <property name="jdbcTemplate" ref="jdbcTemplate" />
    </bean>

    <bean id="studentService" class="com.atguigu.service.impl.StudentServiceImpl">
        <property name="studentDao" ref="studentDao" />
    </bean>

    <bean id="studentController" class="com.atguigu.controller.StudentController">
        <property name="studentService" ref="studentService" />
    </bean>

</beans>
```
7. 运行测试

```Java
public class ControllerTest {

    @Test
    public  void testRun(){
        ApplicationContext applicationContext =
                new ClassPathXmlApplicationContext("spring-ioc.xml");
        StudentController studentController = applicationContext.getBean(StudentController.class);
        studentController.findAll();
    }
}
```
8. XMLIoC方式问题总结
      1. 注入的属性必须添加setter方法、代码结构乱！
      2. 配置文件和Java代码分离、编写不是很方便！
      3. XML配置文件解析效率低

  ## 4.3 基于 注解 方式管理 Bean

#### 4.3.1 实验一： Bean注解标记和扫描 (IoC)
  1. **注解理解**

      和 XML 配置文件一样，注解本身并不能执行，注解本身仅仅只是做一个标记，具体的功能是框架检测到注解标记的位置，然后针对这个位置按照注解标记的功能来执行具体操作。

      本质上：所有一切的操作都是 Java 代码来完成的，XML 和注解只是告诉框架中的 Java 代码如何执行。

      举例：元旦联欢会要布置教室，蓝色的地方贴上元旦快乐四个字，红色的地方贴上拉花，黄色的地方贴上气球。

      ![](http://heavy_code_industry.gitee.io/code_heavy_industry/assets/img/img015.a6b65329.png)

      班长做了所有标记，同学们来完成具体工作。墙上的标记相当于我们在代码中使用的注解，后面同学们做的工作，相当于框架的具体操作。
  2. **扫描理解**

      Spring 为了知道程序员在哪些地方标记了什么注解，就需要通过扫描的方式，来进行检测。然后根据注解进行后续操作。
  3. **准备Spring项目和组件**
      1. 准备项目pom.xml

```XML
<dependencies>
    <!--spring context依赖-->
    <!--当你引入Spring Context依赖之后，表示将Spring的基础依赖引入了-->
    <dependency>
        <groupId>org.springframework</groupId>
        <artifactId>spring-context</artifactId>
        <version>6.0.6</version>
    </dependency>

    <!--junit5测试-->
    <dependency>
        <groupId>org.junit.jupiter</groupId>
        <artifactId>junit-jupiter-api</artifactId>
        <version>5.3.1</version>
    </dependency>
</dependencies>
```
 2. 准备组件类

          普通组件

```Java
/**
 * projectName: com.atguigu.components
 *
 * description: 普通的组件
 */
public class CommonComponent {
}

```

              Controller组件

```Java
/**
 * projectName: com.atguigu.components
 *
 * description: controller类型组件
 */
public class XxxController {
}

```

              Service组件

```Java
/**
 * projectName: com.atguigu.components
 *
 * description: service类型组件
 */
public class XxxService {
}

```

              Dao组件

```Java
/**
 * projectName: com.atguigu.components
 *
 * description: dao类型组件
 */
public class XxxDao {
}

```
 4. **组件添加标记注解**
      1. 组件标记注解和区别

          Spring 提供了以下多个注解，这些注解可以直接标注在 Java 类上，将它们定义成 Spring Bean。

| 注解        | 说明                                                         |
| ----------- | ------------------------------------------------------------ |
| @Component  | 该注解用于描述 Spring 中的 Bean，它是一个泛化的概念，仅仅表示容器中的一个组件（Bean），并且可以作用在应用的任何层次，例如 Service 层、Dao 层等。 使用时只需将该注解标注在相应类上即可。 |
| @Repository | 该注解用于将数据访问层（Dao 层）的类标识为 Spring 中的 Bean，其功能与 @Component 相同。 |
| @Service    | 该注解通常作用在业务层（Service 层），用于将业务层的类标识为 Spring 中的 Bean，其功能与 @Component 相同。 |
| @Controller | 该注解通常作用在控制层（如SpringMVC 的 Controller），用于将控制层的类标识为 Spring 中的 Bean，其功能与 @Component 相同。 |

 ![](http://heavy_code_industry.gitee.io/code_heavy_industry/assets/img/img017.93fb56c5.png)

通过查看源码我们得知，@Controller、@Service、@Repository这三个注解只是在@Component注解的基础上起了三个新的名字。

      对于Spring使用IOC容器管理这些组件来说没有区别，也就是语法层面没有区别。所以@Controller、@Service、@Repository这三个注解只是给开发人员看的，让我们能够便于分辨组件的作用。
    
      注意：虽然它们本质上一样，但是为了代码的可读性、程序结构严谨！我们肯定不能随便胡乱标记。
  2. 使用注解标记

      普通组件

```Java
/**
 * projectName: com.atguigu.components
 *
 * description: 普通的组件
 */
@Component
public class CommonComponent {
}

```

              Controller组件

```Java
/**
 * projectName: com.atguigu.components
 *
 * description: controller类型组件
 */
@Controller
public class XxxController {
}

```

              Service组件

```Java
/**
 * projectName: com.atguigu.components
 *
 * description: service类型组件
 */
@Service
public class XxxService {
}

```

              Dao组件

```Java
/**
 * projectName: com.atguigu.components
 *
 * description: dao类型组件
 */
@Repository
public class XxxDao {
}

```
5. **配置文件确定扫描范围**

      情况1：基本扫描配置

```XML
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xmlns:context="http://www.springframework.org/schema/context"
       xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd http://www.springframework.org/schema/context https://www.springframework.org/schema/context/spring-context.xsd">
    <!-- 配置自动扫描的包 -->
    <!-- 1.包要精准,提高性能!
         2.会扫描指定的包和子包内容
         3.多个包可以使用,分割 例如: com.atguigu.controller,com.atguigu.service等
    -->
    <context:component-scan base-package="com.atguigu.components"/>
  
</beans>
```

          情况2：指定排除组件

```XML
<!-- 情况三：指定不扫描的组件 -->
<context:component-scan base-package="com.atguigu.components">
    
    <!-- context:exclude-filter标签：指定排除规则 -->
    <!-- type属性：指定根据什么来进行排除，annotation取值表示根据注解来排除 -->
    <!-- expression属性：指定排除规则的表达式，对于注解来说指定全类名即可 -->
    <context:exclude-filter type="annotation" expression="org.springframework.stereotype.Controller"/>
</context:component-scan>
```

          情况3：指定扫描组件

```XML
<!-- 情况四：仅扫描指定的组件 -->
<!-- 仅扫描 = 关闭默认规则 + 追加规则 -->
<!-- use-default-filters属性：取值false表示关闭默认扫描规则 -->
<context:component-scan base-package="com.atguigu.ioc.components" use-default-filters="false">
    
    <!-- context:include-filter标签：指定在原有扫描规则的基础上追加的规则 -->
    <context:include-filter type="annotation" expression="org.springframework.stereotype.Controller"/>
</context:component-scan>
```
6. **组件BeanName问题**

      在我们使用 XML 方式管理 bean 的时候，每个 bean 都有一个唯一标识——id 属性的值，便于在其他地方引用。现在使用注解后，每个组件仍然应该有一个唯一标识。

      默认情况：

      类名首字母小写就是 bean 的 id。例如：SoldierController 类对应的 bean 的 id 就是 soldierController。

      使用value属性指定：

```Java
@Controller(value = "tianDog")
public class SoldierController {
}
```

          当注解中只设置一个属性时，value属性的属性名可以省略：

```Java
@Service("smallDog")
public class SoldierService {
}
```
 7. **总结**
      1. 注解方式IoC只是标记哪些类要被Spring管理
      2. 最终，我们还需要XML方式或者后面讲解Java配置类方式指定注解生效的包
      3. **现阶段配置方式为 注解 （标记）+ XML（扫描）**

#### 4.3.2 实验二： 组件（Bean）作用域和周期方法注解 
  1. 组件周期方法配置
      1. 周期方法概念

          我们可以在组件类中定义方法，然后当IoC容器实例化和销毁组件对象的时候进行调用！这两个方法我们成为生命周期方法！

          类似于Servlet的init/destroy方法,我们可以在周期方法完成初始化和释放资源等工作。
      2. 周期方法声明

```Java
public class BeanOne {

  //周期方法要求： 方法命名随意，但是要求方法必须是 public void 无形参列表
  @PostConstruct  //注解制指定初始化方法
  public void init() {
    // 初始化逻辑
  }
}

public class BeanTwo {
  
  @PreDestroy //注解指定销毁方法
  public void cleanup() {
    // 释放资源逻辑
  }
}
```
2. 组件作用域配置
      1. Bean作用域概念

          `<bean` 标签声明Bean，只是将Bean的信息配置给SpringIoC容器！

          在IoC容器中，这些`<bean`标签对应的信息转成Spring内部 `BeanDefinition` 对象，`BeanDefinition` 对象内，包含定义的信息（id,class,属性等等）！

          这意味着，`BeanDefinition`与`类`概念一样，SpringIoC容器可以可以根据`BeanDefinition`对象反射创建多个Bean对象实例。

          具体创建多少个Bean的实例对象，由Bean的作用域Scope属性指定！
      2. 作用域可选值

| 取值      | 含义                                        | 创建对象的时机   | 默认值 |
| --------- | ------------------------------------------- | ---------------- | ------ |
| singleton | 在 IOC 容器中，这个 bean 的对象始终为单实例 | IOC 容器初始化时 | 是     |
| prototype | 这个 bean 在 IOC 容器中有多个实例           | 获取 bean 时     | 否     |


              如果是在WebApplicationContext环境下还会有另外两个作用域（但不常用）：

| 取值    | 含义                 | 创建对象的时机 | 默认值 |
| ------- | -------------------- | -------------- | ------ |
| request | 请求范围内有效的实例 | 每次请求       | 否     |
| session | 会话范围内有效的实例 | 每次会话       | 否     |

          3. 作用域配置

```Java
@Scope(scopeName = ConfigurableBeanFactory.SCOPE_SINGLETON) //单例,默认值
@Scope(scopeName = ConfigurableBeanFactory.SCOPE_PROTOTYPE) //多例  二选一
public class BeanOne {

  //周期方法要求： 方法命名随意，但是要求方法必须是 public void 无形参列表
  @PostConstruct  //注解制指定初始化方法
  public void init() {
    // 初始化逻辑
  }
}
```

#### 4.3.3 实验三： Bean属性赋值：引用类型自动装配 (DI)
  1. **设定场景**
      - SoldierController 需要 SoldierService
      - SoldierService 需要 SoldierDao

        同时在各个组件中声明要调用的方法。

      - SoldierController中声明方法

```Java
import org.springframework.stereotype.Controller;

@Controller(value = "tianDog")
public class SoldierController {

    private SoldierService soldierService;

    public void getMessage() {
        soldierService.getMessage();
    }

}
```
          - SoldierService中声明方法

```Java
@Service("smallDog")
public class SoldierService {

    private SoldierDao soldierDao;

    public void getMessage() {
        soldierDao.getMessage();
    }
}
```
          - SoldierDao中声明方法

```Java
@Repository
public class SoldierDao {

    public void getMessage() {
        System.out.print("I am a soldier");
    }

}
```
2. **自动装配实现**
      1. 前提

          参与自动装配的组件（需要装配、被装配）全部都必须在IoC容器中。

          注意：不区分IoC的方式！XML和注解都可以！
      2. @Autowired注解

          在成员变量上直接标记@Autowired注解即可，不需要提供setXxx()方法。以后我们在项目中的正式用法就是这样。
      3. 给Controller装配Service

```Java
@Controller(value = "tianDog")
public class SoldierController {
    
    @Autowired
    private SoldierService soldierService;
    
    public void getMessage() {
        soldierService.getMessage();
    }
    
}
```
          4. 给Service装配Dao

```Java
@Service("smallDog")
public class SoldierService {
    
    @Autowired
    private SoldierDao soldierDao;
    
    public void getMessage() {
        soldierDao.getMessage();
    }
}
```
3. **@Autowired注解细节**
      1. 标记位置
          1. 成员变量

              这是最主要的使用方式！

              与xml进行bean ref引用不同，他不需要有set方法！

```Java
@Service("smallDog")
public class SoldierService {
    
    @Autowired
    private SoldierDao soldierDao;
    
    public void getMessage() {
        soldierDao.getMessage();
    }
}
```
              2. 构造器

```Java
@Controller(value = "tianDog")
public class SoldierController {
    
    private SoldierService soldierService;
    
    @Autowired
    public SoldierController(SoldierService soldierService) {
        this.soldierService = soldierService;
    }
    ……
```
              3. setXxx()方法

```Java
@Controller(value = "tianDog")
public class SoldierController {

    private SoldierService soldierService;

    @Autowired
    public void setSoldierService(SoldierService soldierService) {
        this.soldierService = soldierService;
    }
    ……
```
2. 工作流程

      ![](http://heavy_code_industry.gitee.io/code_heavy_industry/assets/img/img018.2ff0ae09.png)

      - 首先根据所需要的组件类型到 IOC 容器中查找
          - 能够找到唯一的 bean：直接执行装配
          - 如果完全找不到匹配这个类型的 bean：装配失败
          - 和所需类型匹配的 bean 不止一个
              - 没有 @Qualifier 注解：根据 @Autowired 标记位置成员变量的变量名作为 bean 的 id 进行匹配
                  - 能够找到：执行装配
                  - 找不到：装配失败
              - 使用 @Qualifier 注解：根据 @Qualifier 注解中指定的名称作为 bean 的id进行匹配
                  - 能够找到：执行装配
                  - 找不到：装配失败

```Java
@Controller(value = "tianDog")
public class SoldierController {
    
    @Autowired
    @Qualifier(value = "maomiService222")
    // 根据面向接口编程思想，使用接口类型引入Service组件
    private ISoldierService soldierService;
```
4. **佛系装配**

      给 @Autowired 注解设置 required = false 属性表示：能装就装，装不上就不装。但是实际开发时，基本上所有需要装配组件的地方都是必须装配的，用不上这个属性

```Java
@Controller(value = "tianDog")
public class SoldierController {

    // 给@Autowired注解设置required = false属性表示：能装就装，装不上就不装
    @Autowired(required = false)
    private ISoldierService soldierService;
```
5. **扩展JSR-250注解@Resource**
      - 理解JSR系列注解

          JSR（Java Specification Requests）是Java平台标准化进程中的一种技术规范，而JSR注解是其中一部分重要的内容。按照JSR的分类以及注解语义的不同，可以将JSR注解分为不同的系列，主要有以下几个系列：

          1. JSR-175: 这个JSR是Java SE 5引入的，是Java注解最早的规范化版本，Java SE 5后的版本中都包含该JSR中定义的注解。主要包括以下几种标准注解：
          - `@Deprecated`: 标识一个程序元素（如类、方法或字段）已过时，并且在将来的版本中可能会被删除。
          - `@Override`: 标识一个方法重写了父类中的方法。
          - `@SuppressWarnings`: 抑制编译时产生的警告消息。
          - `@SafeVarargs`: 标识一个有安全性警告的可变参数方法。
          - `@FunctionalInterface`: 标识一个接口只有一个抽象方法，可以作为lambda表达式的目标。
          1. JSR-250: 这个JSR主要用于在Java EE 5中定义一些支持注解。该JSR主要定义了一些用于进行对象管理的注解，包括：
          - `@Resource`: 标识一个需要注入的资源，是实现Java EE组件之间依赖关系的一种方式。
          - `@PostConstruct`: 标识一个方法作为初始化方法。
          - `@PreDestroy`: 标识一个方法作为销毁方法。
          - `@Resource.AuthenticationType`: 标识注入的资源的身份验证类型。
          - `@Resource.AuthenticationType`: 标识注入的资源的默认名称。
          1. JSR-269: 这个JSR主要是Java SE 6中引入的一种支持编译时元数据处理的框架，即使用注解来处理Java源文件。该JSR定义了一些可以用注解标记的注解处理器，用于生成一些元数据，常用的注解有：
          - `@SupportedAnnotationTypes`: 标识注解处理器所处理的注解类型。
          - `@SupportedSourceVersion`: 标识注解处理器支持的Java源码版本。
          1. JSR-330: 该JSR主要为Java应用程序定义了一个依赖注入的标准，即Java依赖注入标准（javax.inject）。在此规范中定义了多种注解，包括：
          - `@Named`: 标识一个被依赖注入的组件的名称。
          - `@Inject`: 标识一个需要被注入的依赖组件。
          - `@Singleton`: 标识一个组件的生命周期只有一个唯一的实例。
          1. JSR-250: 这个JSR主要是Java EE 5中定义一些支持注解。该JSR包含了一些支持注解，可以用于对Java EE组件进行管理，包括：
          - `@RolesAllowed`: 标识授权角色
          - `@PermitAll`: 标识一个活动无需进行身份验证。
          - `@DenyAll`: 标识不提供针对该方法的访问控制。
          - `@DeclareRoles`: 声明安全角色。

          但是你要理解JSR是Java提供的**技术规范**，也就是说，他只是规定了注解和注解的含义，**JSR并不是直接提供特定的实现**，而是提供标准和指导方针，由第三方框架（Spring）和库来实现和提供对应的功能。
      - JSR-250 @Resource注解

          @Resource注解也可以完成属性注入。那它和@Autowired注解有什么区别？

          - @Resource注解是JDK扩展包中的，也就是说属于JDK的一部分。所以该注解是标准注解，更加具有通用性。(JSR-250标准中制定的注解类型。JSR是Java规范提案。)
          - @Autowired注解是Spring框架自己的。
          - **@Resource注解默认根据Bean名称装配，未指定name时，使用属性名作为name。通过name找不到的话会自动启动通过类型装配。**
          - **@Autowired注解默认根据类型装配，如果想根据名称装配，需要配合@Qualifier注解一起用。**
          - @Resource注解用在属性上、setter方法上。
          - @Autowired注解用在属性上、setter方法上、构造方法上、构造方法参数上。

          @Resource注解属于JDK扩展包，所以不在JDK当中，需要额外引入以下依赖：【**高于JDK11或低于JDK8需要引入以下依赖**】

```XML
<dependency>
    <groupId>jakarta.annotation</groupId>
    <artifactId>jakarta.annotation-api</artifactId>
    <version>2.1.1</version>
</dependency>
```
          - @Resource使用

```Java
@Controller
public class XxxController {
    /**
     * 1. 如果没有指定name,先根据属性名查找IoC中组件xxxService
     * 2. 如果没有指定name,并且属性名没有对应的组件,会根据属性类型查找
     * 3. 可以指定name名称查找!  @Resource(name='test') == @Autowired + @Qualifier(value='test')
     */
    @Resource
    private XxxService xxxService;

    //@Resource(name = "指定beanName")
    //private XxxService xxxService;

    public void show(){
        System.out.println("XxxController.show");
        xxxService.show();
    }
}
```

#### 4.3.4 实验四： Bean属性赋值：基本类型属性赋值 (DI)

  `@Value` 通常用于注入外部化属性

  **声明外部配置**

  application.properties

```Java
catalog.name=MovieCatalog
```

      **xml引入外部配置**

```Java
<!-- 引入外部配置文件-->
<context:property-placeholder location="application.properties" />
```

      **@Value注解读取配置**

```Java
package com.atguigu.components;

import org.springframework.beans.factory.annotation.Value;
import org.springframework.stereotype.Component;

/**
 * projectName: com.atguigu.components
 *
 * description: 普通的组件
 */
@Component
public class CommonComponent {

    /**
     * 情况1: ${key} 取外部配置key对应的值!
     * 情况2: ${key:defaultValue} 没有key,可以给与默认值
     */
    @Value("${catalog:hahaha}")
    private String name;

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }
}

```

      catalog
    
    #### 4.3.5 实验五： 基于注解+XML方式整合三层架构组件
      1. 需求分析
    
          搭建一个三层架构案例，模拟查询全部学生（学生表）信息，持久层使用JdbcTemplate和Druid技术，使用XML+注解方式进行组件管理！
    
          ![](https://secure2.wostatic.cn/static/6WsK3n5TJvotqmmNNjxY54/image.png)
      2. 数据库准备

```Java
create database studb;

use studb;

CREATE TABLE students (
  id INT PRIMARY KEY,
  name VARCHAR(50) NOT NULL,
  gender VARCHAR(10) NOT NULL,
  age INT,
  class VARCHAR(50)
);

INSERT INTO students (id, name, gender, age, class)
VALUES
  (1, '张三', '男', 20, '高中一班'),
  (2, '李四', '男', 19, '高中二班'),
  (3, '王五', '女', 18, '高中一班'),
  (4, '赵六', '女', 20, '高中三班'),
  (5, '刘七', '男', 19, '高中二班'),
  (6, '陈八', '女', 18, '高中一班'),
  (7, '杨九', '男', 20, '高中三班'),
  (8, '吴十', '男', 19, '高中二班');

```
      3. 项目准备
          1. 项目创建
    
              spring-annotation-practice-04
          2. 依赖导入

```XML
<dependencies>
      <!--spring context依赖-->
      <!--当你引入SpringContext依赖之后，表示将Spring的基础依赖引入了-->
      <dependency>
          <groupId>org.springframework</groupId>
          <artifactId>spring-context</artifactId>
          <version>6.0.6</version>
      </dependency>

      <!-- 数据库驱动和连接池-->
      <dependency>
          <groupId>mysql</groupId>
          <artifactId>mysql-connector-java</artifactId>
          <version>8.0.25</version>
      </dependency>

      <dependency>
          <groupId>com.alibaba</groupId>
          <artifactId>druid</artifactId>
          <version>1.2.8</version>
      </dependency>
      
      <dependency>
            <groupId>jakarta.annotation</groupId>
            <artifactId>jakarta.annotation-api</artifactId>
            <version>2.1.1</version>
       </dependency>

      <!-- spring-jdbc -->
      <dependency>
          <groupId>org.springframework</groupId>
          <artifactId>spring-jdbc</artifactId>
          <version>6.0.6</version>
      </dependency>

</dependencies> 
```
          3. 实体类准备

```Java
public class Student {

    private Integer id;
    private String name;
    private String gender;
    private Integer age;
    private String classes;

    public Integer getId() {
        return id;
    }

    public void setId(Integer id) {
        this.id = id;
    }

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }

    public String getGender() {
        return gender;
    }

    public void setGender(String gender) {
        this.gender = gender;
    }

    public Integer getAge() {
        return age;
    }

    public void setAge(Integer age) {
        this.age = age;
    }

    public String getClasses() {
        return classes;
    }

    public void setClasses(String classes) {
        this.classes = classes;
    }

    @Override
    public String toString() {
        return "Student{" +
                "id=" + id +
                ", name='" + name + '\'' +
                ", gender='" + gender + '\'' +
                ", age=" + age +
                ", classes='" + classes + '\'' +
                '}';
    }
}

```
      4. 三层架构搭建和实现
          1. 持久层

```Java
//接口
public interface StudentDao {

    /**
     * 查询全部学生数据
     * @return
     */
    List<Student> queryAll();
}

//实现类
@Repository
public class StudentDaoImpl implements StudentDao {

    @Autowired
    private JdbcTemplate jdbcTemplate;

    /**
     * 查询全部学生数据
     * @return
     */
    @Override
    public List<Student> queryAll() {

        String sql = "select id , name , age , gender , class as classes from students ;";

        /*
          query可以返回集合!
          BeanPropertyRowMapper就是封装好RowMapper的实现,要求属性名和列名相同即可
         */
        List<Student> studentList = jdbcTemplate.query(sql, new BeanPropertyRowMapper<>(Student.class));

        return studentList;
    }
}

```
          2. 业务层

```Java
//接口
public interface StudentService {

    /**
     * 查询全部学员业务
     * @return
     */
    List<Student> findAll();

}

//实现类
@Service
public class StudentServiceImpl  implements StudentService {

    @Autowired
    private StudentDao studentDao;

    /**
     * 查询全部学员业务
     * @return
     */
    @Override
    public List<Student> findAll() {

        List<Student> studentList =  studentDao.queryAll();

        return studentList;
    }
}

```
          3. 表述层

```Java
@Controller
public class StudentController {

    @Autowired
    private StudentService studentService;

    public void  findAll(){
       List<Student> studentList =  studentService.findAll();
        System.out.println("studentList = " + studentList);
    }
}

```
      5. 三层架构IoC配置

```XML
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xmlns:context="http://www.springframework.org/schema/context"
       xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd http://www.springframework.org/schema/context https://www.springframework.org/schema/context/spring-context.xsd">


    <!-- 导入外部属性文件 -->
    <context:property-placeholder location="classpath:jdbc.properties" />

    <!-- 配置数据源 -->
    <bean id="druidDataSource" class="com.alibaba.druid.pool.DruidDataSource">
        <property name="url" value="${atguigu.url}"/>
        <property name="driverClassName" value="${atguigu.driver}"/>
        <property name="username" value="${atguigu.username}"/>
        <property name="password" value="${atguigu.password}"/>
    </bean>

    <bean class="org.springframework.jdbc.core.JdbcTemplate">
        <property name="dataSource" ref="druidDataSource" />
    </bean>

    <!-- 扫描Ioc/DI注解 -->
    <context:component-scan base-package="com.atguigu.dao,com.atguigu.service,com.atguigu.controller" />

</beans>
```
      6. 运行测试

```Java
public class ControllerTest {

    @Test
    public  void testRun(){
        ApplicationContext applicationContext =
                new ClassPathXmlApplicationContext("spring-ioc.xml");
        StudentController studentController = applicationContext.getBean(StudentController.class);
        studentController.findAll();
    }
}
```
      7. 注解+XML IoC方式问题总结
          1. 自定义类可以使用注解方式，但是第三方依赖的类依然使用XML方式！
          2. XML格式解析效率低！

  ## 4.4 基于 配置类 方式管理 Bean

    #### 4.4.1 完全注解开发理解
    
      Spring 完全注解配置（Fully Annotation-based Configuration）是指通过 Java配置类 代码来配置 Spring 应用程序，使用注解来替代原本在 XML 配置文件中的配置。相对于 XML 配置，完全注解配置具有更强的类型安全性和更好的可读性。
    
      **两种方式思维转化**：
    
      ![](https://secure2.wostatic.cn/static/uhRgky6LmFBAaYDJfS5SEm/image.png)
    
    #### 4.4.2 实验一：配置类和扫描注解
    
      **xml+注解方式**
    
      配置文件application.xml

```XML
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xmlns:context="http://www.springframework.org/schema/context"
       xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd http://www.springframework.org/schema/context https://www.springframework.org/schema/context/spring-context.xsd">


    <!-- 配置自动扫描的包 -->
    <!-- 1.包要精准,提高性能!
         2.会扫描指定的包和子包内容
         3.多个包可以使用,分割 例如: com.atguigu.controller,com.atguigu.service等
    -->
    <context:component-scan base-package="com.atguigu.components"/>

    <!-- 引入外部配置文件-->
    <context:property-placeholder location="application.properties" />
</beans>
```

      测试创建IoC容器

```Java
 // xml方式配置文件使用ClassPathXmlApplicationContext容器读取
 ApplicationContext applicationContext =
                new ClassPathXmlApplicationContext("application.xml");
```

      **配置类+注解方式（完全注解方式）**
    
      配置类
    
      使用 @Configuration 注解将一个普通的类标记为 Spring 的配置类。

```Java
import org.springframework.context.annotation.ComponentScan;
import org.springframework.context.annotation.Configuration;
import org.springframework.context.annotation.PropertySource;

//标注当前类是配置类，替代application.xml    
@Configuration
//使用注解读取外部配置，替代 <context:property-placeholder标签
@PropertySource("classpath:application.properties")
//使用@ComponentScan注解,可以配置扫描包,替代<context:component-scan标签
@ComponentScan(basePackages = {"com.atguigu.components"})
public class MyConfiguration {
    
}
```

      测试创建IoC容器

```Java
// AnnotationConfigApplicationContext 根据配置类创建 IOC 容器对象
ApplicationContext iocContainerAnnotation = 
new AnnotationConfigApplicationContext(MyConfiguration.class);
```

      可以使用 no-arg 构造函数实例化 `AnnotationConfigApplicationContext` ，然后使用 `register()` 方法对其进行配置。此方法在以编程方式生成 `AnnotationConfigApplicationContext` 时特别有用。以下示例演示如何执行此操作：

```Java
// AnnotationConfigApplicationContext-IOC容器对象
ApplicationContext iocContainerAnnotation = 
new AnnotationConfigApplicationContext();
//外部设置配置类
iocContainerAnnotation.register(MyConfiguration.class);
//刷新后方可生效！！
iocContainerAnnotation.refresh();

```

      **总结：**
    
        @Configuration指定一个类为配置类，可以添加配置注解，替代配置xml文件
    
        @ComponentScan(basePackages = {"包","包"}) 替代<context:component-scan标签实现注解扫描
    
        @PropertySource("classpath:配置文件地址") 替代 <context:property-placeholder标签
    
        配合IoC/DI注解，可以进行完整注解开发！
    
    #### 4.4.3 实验二：@Bean定义组件
    
      **场景需求**：将Druid连接池对象存储到IoC容器
    
      **需求分析**：第三方jar包的类，添加到ioc容器，无法使用@Component等相关注解！因为源码jar包内容为只读模式！
    
      **xml方式实现**：

```XML
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xmlns:context="http://www.springframework.org/schema/context"
       xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd http://www.springframework.org/schema/context https://www.springframework.org/schema/context/spring-context.xsd">


    <!-- 引入外部属性文件 -->
    <context:property-placeholder location="classpath:jdbc.properties"/>

    <!-- 实验六 [重要]给bean的属性赋值：引入外部属性文件 -->
    <bean id="druidDataSource" class="com.alibaba.druid.pool.DruidDataSource">
        <property name="url" value="${jdbc.url}"/>
        <property name="driverClassName" value="${jdbc.driver}"/>
        <property name="username" value="${jdbc.user}"/>
        <property name="password" value="${jdbc.password}"/>
    </bean>

</beans>
```

      **配置类方式实现**：
    
        `@Bean` 注释用于指示方法实例化、配置和初始化要由 Spring IoC 容器管理的新对象。对于那些熟悉 Spring 的 `<beans/>` XML 配置的人来说， `@Bean` 注释与 `<bean/>` 元素起着相同的作用。

```Java
//标注当前类是配置类，替代application.xml    
@Configuration
//引入jdbc.properties文件
@PropertySource({"classpath:application.properties","classpath:jdbc.properties"})
@ComponentScan(basePackages = {"com.atguigu.components"})
public class MyConfiguration {

    //如果第三方类进行IoC管理,无法直接使用@Component相关注解
    //解决方案: xml方式可以使用<bean标签
    //解决方案: 配置类方式,可以使用方法返回值+@Bean注解
    @Bean
    public DataSource createDataSource(@Value("${jdbc.user}") String username,
                                       @Value("${jdbc.password}")String password,
                                       @Value("${jdbc.url}")String url,
                                       @Value("${jdbc.driver}")String driverClassName){
        //使用Java代码实例化
        DruidDataSource dataSource = new DruidDataSource();
        dataSource.setUsername(username);
        dataSource.setPassword(password);
        dataSource.setUrl(url);
        dataSource.setDriverClassName(driverClassName);
        //返回结果即可
        return dataSource;
    }
}
```

    #### 4.4.4 实验三：高级特性：@Bean注解细节
      1. **@Bean生成BeanName问题**
    
          @Bean注解源码：

```Java
public @interface Bean {
    //前两个注解可以指定Bean的标识
    @AliasFor("name")
    String[] value() default {};
    @AliasFor("value")
    String[] name() default {};
  
    //autowireCandidate 属性来指示该 Bean 是否候选用于自动装配。
    //autowireCandidate 属性默认值为 true，表示该 Bean 是一个默认的装配目标，
    //可被候选用于自动装配。如果将 autowireCandidate 属性设置为 false，则说明该 Bean 不是默认的装配目标，不会被候选用于自动装配。
    boolean autowireCandidate() default true;

    //指定初始化方法
    String initMethod() default "";
    //指定销毁方法
    String destroyMethod() default "(inferred)";
}

```

          指定@Bean的名称：

```Java
@Configuration
public class AppConfig {

  @Bean("myThing") //指定名称
  public Thing thing() {
    return new Thing();
  }
}
```

          `@Bean` 注释注释方法。使用此方法在指定为方法返回值的类型的 `ApplicationContext` 中注册 Bean 定义。缺省情况下，Bean 名称与方法名称相同。下面的示例演示 `@Bean` 方法声明：

```Java
@Configuration
public class AppConfig {

  @Bean
  public TransferServiceImpl transferService() {
    return new TransferServiceImpl();
  }
}
```

          前面的配置完全等同于下面的Spring XML：

```Java
<beans>
  <bean id="transferService" class="com.acme.TransferServiceImpl"/>
</beans>
```
      2. **@Bean 初始化和销毁方法指定**
    
          `@Bean` 注解支持指定任意初始化和销毁回调方法，非常类似于 Spring XML 在 `bean` 元素上的 `init-method` 和 `destroy-method` 属性，如以下示例所示：

```Java
public class BeanOne {

  public void init() {
    // initialization logic
  }
}

public class BeanTwo {

  public void cleanup() {
    // destruction logic
  }
}

@Configuration
public class AppConfig {

  @Bean(initMethod = "init")
  public BeanOne beanOne() {
    return new BeanOne();
  }

  @Bean(destroyMethod = "cleanup")
  public BeanTwo beanTwo() {
    return new BeanTwo();
  }
}
```
      3. **@Bean Scope作用域**
    
          可以指定使用 `@Bean` 注释定义的 bean 应具有特定范围。您可以使用在 Bean 作用域部分中指定的任何标准作用域。
    
          默认作用域为 `singleton` ，但您可以使用 `@Scope` 注释覆盖此范围，如以下示例所示：

```Java
@Configuration
public class MyConfiguration {

  @Bean
  @Scope("prototype")
  public Encryptor encryptor() {
    // ...
  }
}
```
      4. **@Bean方法之间依赖**
    
          **准备组件**

```Java
public class HappyMachine {
    
    private String machineName;
    
    public String getMachineName() {
        return machineName;
    }
    
    public void setMachineName(String machineName) {
        this.machineName = machineName;
    }
}
```

```Java
public class HappyComponent {
    //引用新组件
    private HappyMachine happyMachine;

    public HappyMachine getHappyMachine() {
        return happyMachine;
    }

    public void setHappyMachine(HappyMachine happyMachine) {
        this.happyMachine = happyMachine;
    }

    public void doWork() {
        System.out.println("HappyComponent.doWork");
    }

}
```

          **Java配置类实现：**
    
          方案1：
    
          直接调用方法返回 Bean 实例：在一个 `@Bean` 方法中直接调用其他 `@Bean` 方法来获取 Bean 实例，虽然是方法调用，也是通过IoC容器获取对应的Bean，例如：

```Java
@Configuration
public class JavaConfig {

    @Bean
    public HappyMachine happyMachine(){
        return new HappyMachine();
    }

    @Bean
    public HappyComponent happyComponent(){
        HappyComponent happyComponent = new HappyComponent();
        //直接调用方法即可! 
        happyComponent.setHappyMachine(happyMachine());
        return happyComponent;
    }

}
```

          方案2：
    
          参数引用法：通过方法参数传递 Bean 实例的引用来解决 Bean 实例之间的依赖关系，例如：

```Java
package com.atguigu.config;

import com.atguigu.ioc.HappyComponent;
import com.atguigu.ioc.HappyMachine;
import org.springframework.context.annotation.Bean;
import org.springframework.context.annotation.Configuration;

/**
 * projectName: com.atguigu.config
 * description: 配置HappyComponent和HappyMachine关系
 */

@Configuration
public class JavaConfig {

    @Bean
    public HappyMachine happyMachine(){
        return new HappyMachine();
    }

    /**
     * 可以直接在形参列表接收IoC容器中的Bean!
     *    情况1: 直接指定类型即可
     *    情况2: 如果有多个bean,(HappyMachine 名称 ) 形参名称等于要指定的bean名称!
     *           例如:
     *               @Bean
     *               public Foo foo1(){
     *                   return new Foo();
     *               }
     *               @Bean
     *               public Foo foo2(){
     *                   return new Foo()
     *               }
     *               @Bean
     *               public Component component(Foo foo1 / foo2 通过此处指定引入的bean)
     */
    @Bean
    public HappyComponent happyComponent(HappyMachine happyMachine){
        HappyComponent happyComponent = new HappyComponent();
        //赋值
        happyComponent.setHappyMachine(happyMachine);
        return happyComponent;
    }

}
```

    #### 4.4.5 实验四：高级特性：@Import扩展
    
      `@Import` 注释允许从另一个配置类加载 `@Bean` 定义，如以下示例所示：

```Java
@Configuration
public class ConfigA {

  @Bean
  public A a() {
    return new A();
  }
}

@Configuration
@Import(ConfigA.class)
public class ConfigB {

  @Bean
  public B b() {
    return new B();
  }
}
```

      现在，在实例化上下文时不需要同时指定 `ConfigA.class` 和 `ConfigB.class` ，只需显式提供 `ConfigB` ，如以下示例所示：

```Java
public static void main(String[] args) {
  ApplicationContext ctx = new AnnotationConfigApplicationContext(ConfigB.class);

  // now both beans A and B will be available...
  A a = ctx.getBean(A.class);
  B b = ctx.getBean(B.class);
}
```

      此方法简化了容器实例化，因为只需要处理一个类，而不是要求您在构造期间记住可能大量的 `@Configuration` 类。
    
    #### 4.4.6 实验五：基于注解+配置类方式整合三层架构组件
      1. 需求分析
    
          搭建一个三层架构案例，模拟查询全部学生（学生表）信息，持久层使用JdbcTemplate和Druid技术，使用注解+配置类方式进行组件管理！
    
          ![](https://secure2.wostatic.cn/static/spSLnBnMYbqJXYLqjr2C7y/image.png)
      2. 数据库准备

```Java
create database studb;

use studb;

CREATE TABLE students (
  id INT PRIMARY KEY,
  name VARCHAR(50) NOT NULL,
  gender VARCHAR(10) NOT NULL,
  age INT,
  class VARCHAR(50)
);

INSERT INTO students (id, name, gender, age, class)
VALUES
  (1, '张三', '男', 20, '高中一班'),
  (2, '李四', '男', 19, '高中二班'),
  (3, '王五', '女', 18, '高中一班'),
  (4, '赵六', '女', 20, '高中三班'),
  (5, '刘七', '男', 19, '高中二班'),
  (6, '陈八', '女', 18, '高中一班'),
  (7, '杨九', '男', 20, '高中三班'),
  (8, '吴十', '男', 19, '高中二班');

```
      3. 项目准备
          1. 项目创建
    
              spring-java-practice-06
          2. 依赖导入

```XML
<dependencies>
      <!--spring context依赖-->
      <!--当你引入SpringContext依赖之后，表示将Spring的基础依赖引入了-->
      <dependency>
          <groupId>org.springframework</groupId>
          <artifactId>spring-context</artifactId>
          <version>6.0.6</version>
      </dependency>

      <!-- 数据库驱动和连接池-->
      <dependency>
          <groupId>mysql</groupId>
          <artifactId>mysql-connector-java</artifactId>
          <version>8.0.25</version>
      </dependency>

      <dependency>
          <groupId>com.alibaba</groupId>
          <artifactId>druid</artifactId>
          <version>1.2.8</version>
      </dependency>
      
      <dependency>
            <groupId>jakarta.annotation</groupId>
            <artifactId>jakarta.annotation-api</artifactId>
            <version>2.1.1</version>
       </dependency>

      <!-- spring-jdbc -->
      <dependency>
          <groupId>org.springframework</groupId>
          <artifactId>spring-jdbc</artifactId>
          <version>6.0.6</version>
      </dependency>

</dependencies> 
```
          3. 实体类准备

```Java
public class Student {

    private Integer id;
    private String name;
    private String gender;
    private Integer age;
    private String classes;

    public Integer getId() {
        return id;
    }

    public void setId(Integer id) {
        this.id = id;
    }

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }

    public String getGender() {
        return gender;
    }

    public void setGender(String gender) {
        this.gender = gender;
    }

    public Integer getAge() {
        return age;
    }

    public void setAge(Integer age) {
        this.age = age;
    }

    public String getClasses() {
        return classes;
    }

    public void setClasses(String classes) {
        this.classes = classes;
    }

    @Override
    public String toString() {
        return "Student{" +
                "id=" + id +
                ", name='" + name + '\'' +
                ", gender='" + gender + '\'' +
                ", age=" + age +
                ", classes='" + classes + '\'' +
                '}';
    }
}

```
      4. 三层架构搭建和实现
          1. 持久层

```Java
//接口
public interface StudentDao {

    /**
     * 查询全部学生数据
     * @return
     */
    List<Student> queryAll();
}

//实现类
@Repository
public class StudentDaoImpl implements StudentDao {

    @Autowired
    private JdbcTemplate jdbcTemplate;

    /**
     * 查询全部学生数据
     * @return
     */
    @Override
    public List<Student> queryAll() {

        String sql = "select id , name , age , gender , class as classes from students ;";

        /*
          query可以返回集合!
          BeanPropertyRowMapper就是封装好RowMapper的实现,要求属性名和列名相同即可
         */
        List<Student> studentList = jdbcTemplate.query(sql, new BeanPropertyRowMapper<>(Student.class));

        return studentList;
    }
}

```
          2. 业务层

```Java
//接口
public interface StudentService {

    /**
     * 查询全部学员业务
     * @return
     */
    List<Student> findAll();

}

//实现类
@Service
public class StudentServiceImpl  implements StudentService {

    @Autowired
    private StudentDao studentDao;

    /**
     * 查询全部学员业务
     * @return
     */
    @Override
    public List<Student> findAll() {

        List<Student> studentList =  studentDao.queryAll();

        return studentList;
    }
}

```
          3. 表述层

```Java
@Controller
public class StudentController {

    @Autowired
    private StudentService studentService;

    public void  findAll(){
       List<Student> studentList =  studentService.findAll();
        System.out.println("studentList = " + studentList);
    }
}

```
      5. 三层架构IoC配置类

```Java
@Configuration
@ComponentScan(basePackages = "com.atguigu")
@PropertySource("classpath:jdbc.properties")
public class JavaConfig {

    @Value("${atguigu.url}")
    private String url;
    @Value("${atguigu.driver}")
    private String driver;
    @Value("${atguigu.username}")
    private String username;
    @Value("${atguigu.password}")
    private String password;

    @Bean(destroyMethod = "close")
    public DruidDataSource dataSource(){
        DruidDataSource dataSource = new DruidDataSource();
        dataSource.setUrl(url);
        dataSource.setDriverClassName(driver);
        dataSource.setUsername(username);
        dataSource.setPassword(password);
        return dataSource;
    }

    @Scope(ConfigurableBeanFactory.SCOPE_PROTOTYPE)
    @Bean
    public JdbcTemplate jdbcTemplate(DataSource dataSource){
        JdbcTemplate jdbcTemplate = new JdbcTemplate();
        jdbcTemplate.setDataSource(dataSource);
        return jdbcTemplate;
    }

}
```
      6. 运行测试

```Java
public class ControllerTest {

    @Test
    public  void testRun(){

        AnnotationConfigApplicationContext applicationContext =
                new AnnotationConfigApplicationContext(JavaConfig.class);

        StudentController studentController = applicationContext.getBean(StudentController.class);

        studentController.findAll();

    }
}
```
      7. 注解+配置类 IoC方式总结
          1. 完全摒弃了XML配置文件
          2. 自定义类使用IoC和DI注解标记
          3. 第三方类使用配置类声明方法+@Bean方式处理
          4. 完全注解方式（配置类+注解）是现在主流配置方式

  ## 4.5 三种配置方式总结

    #### 4.5.1 XML方式配置总结
      1. 所有内容写到xml格式配置文件中
      2. 声明bean通过<bean标签
      3. <bean标签包含基本信息（id,class）和属性信息 <property name value / ref
      4. 引入外部的properties文件可以通过<context:property-placeholder
      5. IoC具体容器实现选择ClassPathXmlApplicationContext对象
    
    #### 4.5.2 XML+注解方式配置总结
      1. 注解负责标记IoC的类和进行属性装配
      2. xml文件依然需要，需要通过<context:component-scan标签指定注解范围
      3. 标记IoC注解：@Component,@Service,@Controller,@Repository 
      4. 标记DI注解：@Autowired @Qualifier @Resource @Value
      5. IoC具体容器实现选择ClassPathXmlApplicationContext对象
    
    #### 4.5.3 完全注解方式配置总结
      1. 完全注解方式指的是去掉xml文件，使用配置类 + 注解实现
      2. xml文件替换成使用@Configuration注解标记的类
      3. 标记IoC注解：@Component,@Service,@Controller,@Repository 
      4. 标记DI注解：@Autowired @Qualifier @Resource @Value
      5. <context:component-scan标签指定注解范围使用@ComponentScan(basePackages = {"com.atguigu.components"})替代
      6. <context:property-placeholder引入外部配置文件使用@PropertySource({"classpath:application.properties","classpath:jdbc.properties"})替代
      7. <bean 标签使用@Bean注解和方法实现
      8. IoC具体容器实现选择AnnotationConfigApplicationContext对象

## 4.6 整合Spring5-Test5搭建测试环境

    1. 整合测试环境作用
    
        好处1：不需要自己创建IOC容器对象了
    
        好处2：任何需要的bean都可以在测试类中直接享受自动装配
    2. 导入相关依赖

```XML
<!--junit5测试-->
<dependency>
    <groupId>org.junit.jupiter</groupId>
    <artifactId>junit-jupiter-api</artifactId>
    <version>5.3.1</version>
</dependency>
<dependency>
    <groupId>org.springframework</groupId>
    <artifactId>spring-test</artifactId>
    <version>6.0.6</version>
    <scope>test</scope>
</dependency>
```
    3. 整合测试注解使用

```Java
//@SpringJUnitConfig(locations = {"classpath:spring-context.xml"})  //指定配置文件xml
@SpringJUnitConfig(value = {BeanConfig.class})  //指定配置类
public class Junit5IntegrationTest {
    
    @Autowired
    private User user;
    
    @Test
    public void testJunit5() {
        System.out.println(user);
    }
}
```

# 十一、Spring AOP面向切面编程

  ## 5.1 场景设定和问题复现
    1. 准备AOP项目
    
        项目名：spring-aop-annotation
    
        pom.xml

```XML
<dependencies>
    <!--spring context依赖-->
    <!--当你引入Spring Context依赖之后，表示将Spring的基础依赖引入了-->
    <dependency>
        <groupId>org.springframework</groupId>
        <artifactId>spring-context</artifactId>
        <version>6.0.6</version>
    </dependency>

    <!--junit5测试-->
    <dependency>
        <groupId>org.junit.jupiter</groupId>
        <artifactId>junit-jupiter-api</artifactId>
        <version>5.3.1</version>
    </dependency>


    <dependency>
        <groupId>org.springframework</groupId>
        <artifactId>spring-test</artifactId>
        <version>6.0.6</version>
        <scope>test</scope>
    </dependency>

    <dependency>
        <groupId>jakarta.annotation</groupId>
        <artifactId>jakarta.annotation-api</artifactId>
        <version>2.1.1</version>
    </dependency>
</dependencies>
```
    2. 声明接口

```Java
/**
 *       + - * / 运算的标准接口!
 */
public interface Calculator {
    
    int add(int i, int j);
    
    int sub(int i, int j);
    
    int mul(int i, int j);
    
    int div(int i, int j);
    
}
```
    3. 接口实现

```Java
package com.atguigu.proxy;


/**
 * 实现计算接口,单纯添加 + - * / 实现! 掺杂其他功能!
 */
public class CalculatorPureImpl implements Calculator {
    
    @Override
    public int add(int i, int j) {
    
        int result = i + j;
    
        return result;
    }
    
    @Override
    public int sub(int i, int j) {
    
        int result = i - j;
    
        return result;
    }
    
    @Override
    public int mul(int i, int j) {
    
        int result = i * j;
    
        return result;
    }
    
    @Override
    public int div(int i, int j) {
    
        int result = i / j;
    
        return result;
    }
}
```
    4. 声明带日志接口实现
    
        新需求： 需要在每个方法中，添加控制台输出，输出参数和输出计算后的返回值！
    
        ![](http://heavy_code_industry.gitee.io/code_heavy_industry/assets/img/img002.f8e54219.png)

```Java
package com.atguigu.proxy;

/**
 * 在每个方法中,输出传入的参数和计算后的返回结果!
 */
public class CalculatorLogImpl implements Calculator {
    
    @Override
    public int add(int i, int j) {
    
        System.out.println("参数是：" + i + "," + j);
        int result = i + j;
        System.out.println("方法内部 result = " + result);
      
        return result;
    }
    
    @Override
    public int sub(int i, int j) {
    
        System.out.println("参数是：" + i + "," + j);
    
        int result = i - j;
    
        System.out.println("方法内部 result = " + result);
        return result;
    }
    
    @Override
    public int mul(int i, int j) {
    
        System.out.println("参数是：" + i + "," + j);
    
        int result = i * j;
    
        System.out.println("方法内部 result = " + result);
    
        return result;
    }
    
    @Override
    public int div(int i, int j) {
    
        System.out.println("参数是：" + i + "," + j);
    
        int result = i / j;
    
        System.out.println("方法内部 result = " + result);
        
        return result;
    }
}
```
    5. 代码问题分析
        1. 代码缺陷
            - 对核心业务功能有干扰，导致程序员在开发核心业务功能时分散了精力
            - 附加功能代码重复，分散在各个业务功能方法中！冗余，且不方便统一维护！
        2. 解决思路
    
              核心就是：解耦。我们需要把附加功能从业务功能代码中抽取出来。
    
              将重复的代码统一提取，并且[[动态插入]]到每个业务方法！
        3. 技术困难
    
            解决问题的困难：提取重复附加功能代码到一个类中，可以实现
    
            但是如何将代码插入到各个方法中，我们不会，我们需要引用新技术！！！

  ## 5.2 解决技术代理模式
    1. **代理模式**
    
        二十三种设计模式中的一种，属于结构型模式。它的作用就是通过提供一个代理类，让我们在调用目标方法的时候，不再是直接对目标方法进行调用，而是通过代理类间接调用。让不属于目标方法核心逻辑的代码从目标方法中剥离出来——解耦。调用目标方法时先调用代理对象的方法，减少对目标方法的调用和打扰，同时让附加功能能够集中在一起也有利于统一维护。
    
        无代理场景：
    
        ![](http://heavy_code_industry.gitee.io/code_heavy_industry/assets/img/img004.e76b3080.png)
    
        有代理场景：
    
        ![](http://heavy_code_industry.gitee.io/code_heavy_industry/assets/img/img005.74dd7746.png)
    
        生活中的代理：
    
        - 广告商找大明星拍广告需要经过经纪人
        - 合作伙伴找大老板谈合作要约见面时间需要经过秘书
        - 房产中介是买卖双方的代理
        - 太监是大臣和皇上之间的代理


​        

        相关术语：
    
        - 代理：将非核心逻辑剥离出来以后，封装这些非核心逻辑的类、对象、方法。(中介)
            - 动词：指做代理这个动作，或这项工作
            - 名词：扮演代理这个角色的类、对象、方法
        - 目标：**被代理**“套用”了核心逻辑代码的类、对象、方法。(房东)
    
        代理在开发中实现的方式具体有两种：静态代理，[动态代理技术]
    2. **静态代理**
    
        主动创建代理类：

```Java
public class CalculatorStaticProxy implements Calculator {
    
    // 将被代理的目标对象声明为成员变量
    private Calculator target;
    
    public CalculatorStaticProxy(Calculator target) {
        this.target = target;
    }
    
    @Override
    public int add(int i, int j) {
    
        // 附加功能由代理类中的代理方法来实现
        System.out.println("参数是：" + i + "," + j);
    
        // 通过目标对象来实现核心业务逻辑
        int addResult = target.add(i, j);
    
        System.out.println("方法内部 result = " + result);
    
        return addResult;
    }
    ……
```

        静态代理确实实现了解耦，但是由于代码都写死了，完全不具备任何的灵活性。就拿日志功能来说，将来其他地方也需要附加日志，那还得再声明更多个静态代理类，那就产生了大量重复的代码，日志功能还是分散的，没有统一管理。
    
        提出进一步的需求：将日志功能集中到一个代理类中，将来有任何日志需求，都通过这一个代理类来实现。这就需要使用动态代理技术了。
    3. **动态代理**
    
        动态代理技术分类
    
        - JDK动态代理：JDK原生的实现方式，需要被代理的目标类必须**实现接口**！他会根据目标类的接口动态生成一个代理对象！代理对象和目标对象有相同的接口！（拜把子）
        - cglib：通过继承被代理的目标类实现代理，所以不需要目标类实现接口！（认干爹）
    
        JDK动态代理技术实现（了解）
    
          ![](http://heavy_code_industry.gitee.io/code_heavy_industry/assets/img/img003.2fe524a2.png)
    
          代理工程：基于jdk代理技术，生成代理对象

```Java
public class ProxyFactory {

    private Object target;

    public ProxyFactory(Object target) {
        this.target = target;
    }

    public Object getProxy(){

        /**
         * newProxyInstance()：创建一个代理实例
         * 其中有三个参数：
         * 1、classLoader：加载动态生成的代理类的类加载器
         * 2、interfaces：目标对象实现的所有接口的class对象所组成的数组
         * 3、invocationHandler：设置代理对象实现目标对象方法的过程，即代理类中如何重写接口中的抽象方法
         */
        ClassLoader classLoader = target.getClass().getClassLoader();
        Class<?>[] interfaces = target.getClass().getInterfaces();
        InvocationHandler invocationHandler = new InvocationHandler() {
            @Override
            public Object invoke(Object proxy, Method method, Object[] args) throws Throwable {
                /**
                 * proxy：代理对象
                 * method：代理对象需要实现的方法，即其中需要重写的方法
                 * args：method所对应方法的参数
                 */
                Object result = null;
                try {
                    System.out.println("[动态代理][日志] "+method.getName()+"，参数："+ Arrays.toString(args));
                    result = method.invoke(target, args);
                    System.out.println("[动态代理][日志] "+method.getName()+"，结果："+ result);
                } catch (Exception e) {
                    e.printStackTrace();
                    System.out.println("[动态代理][日志] "+method.getName()+"，异常："+e.getMessage());
                } finally {
                    System.out.println("[动态代理][日志] "+method.getName()+"，方法执行完毕");
                }
                return result;
            }
        };

        return Proxy.newProxyInstance(classLoader, interfaces, invocationHandler);
    }
}
```

          测试代码：

```Java
@Test
public void testDynamicProxy(){
    ProxyFactory factory = new ProxyFactory(new CalculatorLogImpl());
    Calculator proxy = (Calculator) factory.getProxy();
    proxy.div(1,0);
    //proxy.div(1,1);
}
```
    4. **代理总结**
    
        **代理方式可以解决附加功能代码干扰核心代码和不方便统一维护的问题！**
    
        他主要是将附加功能代码提取到代理中执行，不干扰目标核心代码！
    
        但是我们也发现，无论使用静态代理和动态代理(jdk,cglib)，程序员的工作都比较繁琐！
    
        需要自己编写代理工厂等！
    
        但是，提前剧透，我们在实际开发中，不需要编写代理代码，我们可以使用[Spring AOP]框架，
    
        他会简化动态代理的实现！！！

  ## 5.3 面向切面编程思维（AOP）
    1. **面向切面编程思想AOP**
    
        AOP：Aspect Oriented Programming面向切面编程
    
        AOP可以说是OOP（Object Oriented Programming，面向对象编程）的补充和完善。OOP引入封装、继承、多态等概念来建立一种对象层次结构，用于模拟公共行为的一个集合。不过OOP允许开发者定义纵向的关系，但并不适合定义横向的关系，例如日志功能。日志代码往往横向地散布在所有对象层次中，而与它对应的对象的核心功能毫无关系对于其他类型的代码，如安全性、异常处理和透明的持续性也都是如此，这种散布在各处的无关的代码被称为横切（cross cutting），在OOP设计中，它导致了大量代码的重复，而不利于各个模块的重用。
    
        ![](https://secure2.wostatic.cn/static/7xBHASmuNUSNpC3bZmWUHT/image.png)
    
        AOP技术恰恰相反，它利用一种称为"横切"的技术，剖解开封装的对象内部，并将那些影响了多个类的公共行为封装到一个可重用模块，并将其命名为"Aspect"，即切面。所谓"切面"，简单说就是那些与业务无关，却为业务模块所共同调用的逻辑或责任封装起来，便于减少系统的重复代码，降低模块之间的耦合度，并有利于未来的可操作性和可维护性。
    
        使用AOP，可以在不修改原来代码的基础上添加新功能。
    
        ![](https://secure2.wostatic.cn/static/pSbvngwba8MqmH69aQfzjj/image.png)
    2. **AOP思想主要的应用场景**
    
        AOP（面向切面编程）是一种编程范式，它通过将通用的横切关注点（如日志、事务、权限控制等）与业务逻辑分离，使得代码更加清晰、简洁、易于维护。AOP可以应用于各种场景，以下是一些常见的AOP应用场景：
    
        1. 日志记录：在系统中记录日志是非常重要的，可以使用AOP来实现日志记录的功能，可以在方法执行前、执行后或异常抛出时记录日志。
        2. 事务处理：在数据库操作中使用事务可以保证数据的一致性，可以使用AOP来实现事务处理的功能，可以在方法开始前开启事务，在方法执行完毕后提交或回滚事务。
        3. 安全控制：在系统中包含某些需要安全控制的操作，如登录、修改密码、授权等，可以使用AOP来实现安全控制的功能。可以在方法执行前进行权限判断，如果用户没有权限，则抛出异常或转向到错误页面，以防止未经授权的访问。
        4. 性能监控：在系统运行过程中，有时需要对某些方法的性能进行监控，以找到系统的瓶颈并进行优化。可以使用AOP来实现性能监控的功能，可以在方法执行前记录时间戳，在方法执行完毕后计算方法执行时间并输出到日志中。
        5. 异常处理：系统中可能出现各种异常情况，如空指针异常、数据库连接异常等，可以使用AOP来实现异常处理的功能，在方法执行过程中，如果出现异常，则进行异常处理（如记录日志、发送邮件等）。
        6. 缓存控制：在系统中有些数据可以缓存起来以提高访问速度，可以使用AOP来实现缓存控制的功能，可以在方法执行前查询缓存中是否有数据，如果有则返回，否则执行方法并将方法返回值存入缓存中。
        7. 动态代理：AOP的实现方式之一是通过动态代理，可以代理某个类的所有方法，用于实现各种功能。
    
        综上所述，AOP可以应用于各种场景，它的作用是将通用的横切关注点与业务逻辑分离，使得代码更加清晰、简洁、易于维护。
    3. **AOP术语名词介绍**
    
        1-横切关注点
    
        从每个方法中抽取出来的同一类非核心业务。在同一个项目中，我们可以使用多个横切关注点对相关方法进行多个不同方面的增强。
    
        这个概念不是语法层面天然存在的，而是根据附加功能的逻辑上的需要：有十个附加功能，就有十个横切关注点。
    
        ![](http://heavy_code_industry.gitee.io/code_heavy_industry/assets/img/img007.9ad7afe5.png)
    
        AOP把软件系统分为两个部分：核心关注点和横切关注点。业务处理的主要流程是核心关注点，与之关系不大的部分是横切关注点。横切关注点的一个特点是，他们经常发生在核心关注点的多处，而各处基本相似，比如权限认证、日志、事务、异常等。AOP的作用在于分离系统中的各种关注点，将核心关注点和横切关注点分离开来。
    
        2-通知(增强)
    
        每一个横切关注点上要做的事情都需要写一个方法来实现，这样的方法就叫通知方法。
    
        - 前置通知：在被代理的目标方法前执行
        - 返回通知：在被代理的目标方法成功结束后执行（**寿终正寝**）
        - 异常通知：在被代理的目标方法异常结束后执行（**死于非命**）
        - 后置通知：在被代理的目标方法最终结束后执行（**盖棺定论**）
        - 环绕通知：使用try...catch...finally结构围绕整个被代理的目标方法，包括上面四种通知对应的所有位置
    
        ![](http://heavy_code_industry.gitee.io/code_heavy_industry/assets/img/img008.ea600562.png)


​        

        3-连接点 joinpoint
    
        这也是一个纯逻辑概念，不是语法定义的。
    
        指那些被拦截到的点。在 Spring 中，可以被动态代理拦截目标类的方法
    
        ![](http://heavy_code_industry.gitee.io/code_heavy_industry/assets/img/img010.5af189f7.png)
    
        4-切入点 pointcut
    
        定位连接点的方式，或者可以理解成被选中的连接点！
    
        是一个表达式，比如execution(* com.spring.service.impl.*.*(..))。符合条件的每个方法都是一个具体的连接点。


​        

        5-切面 aspect
    
        切入点和通知的结合。是一个类。
    
        ![](http://heavy_code_industry.gitee.io/code_heavy_industry/assets/img/img009.a0b70cb3.png)
    
        6-目标 target
    
        被代理的目标对象。
    
        7-代理 proxy
    
        向目标对象应用通知之后创建的代理对象。
    
        8-织入 weave
    
        指把通知应用到目标上，生成代理对象的过程。可以在编译期织入，也可以在运行期织入，Spring采用后者。

  ## 5.4 Spring AOP框架介绍和关系梳理
    1. AOP一种区别于OOP的编程思维，用来完善和解决OOP的非核心代码冗余和不方便统一维护问题！
    2. 代理技术（动态代理|静态代理）是实现AOP思维编程的具体技术，但是自己使用动态代理实现代码比较繁琐！
    3. Spring AOP框架，基于AOP编程思维，封装动态代理技术，简化动态代理技术实现的框架！SpringAOP内部帮助我们实现动态代理，我们只需写少量的配置，指定生效范围即可,即可完成面向切面思维编程的实现！

  ## 5.5 Spring AOP基于注解方式实现和细节

    #### 5.5.1 Spring AOP底层技术组成
    
      ![](http://heavy_code_industry.gitee.io/code_heavy_industry/assets/img/img006.84eb95b7.png)
    
      - 动态代理（InvocationHandler）：JDK原生的实现方式，需要被代理的目标类必须实现接口。因为这个技术要求代理对象和目标对象实现同样的接口（兄弟两个拜把子模式）。
      - cglib：通过继承被代理的目标类（认干爹模式）实现代理，所以不需要目标类实现接口。
      - AspectJ：早期的AOP实现的框架，SpringAOP借用了AspectJ中的AOP注解。
    
    #### 5.5.2 初步实现
      1. 加入依赖

```XML
<!-- spring-aspects会帮我们传递过来aspectjweaver -->
<dependency>
    <groupId>org.springframework</groupId>
    <artifactId>spring-aop</artifactId>
    <version>6.0.6</version>
</dependency>

<dependency>
    <groupId>org.springframework</groupId>
    <artifactId>spring-aspects</artifactId>
    <version>6.0.6</version>
</dependency>
```
      2. 准备接口

```Java
public interface Calculator {
    
    int add(int i, int j);
    
    int sub(int i, int j);
    
    int mul(int i, int j);
    
    int div(int i, int j);
    
}
```
      3. 纯净实现类

```Java
package com.atguigu.proxy;


/**
 * 实现计算接口,单纯添加 + - * / 实现! 掺杂其他功能!
 */
@Component
public class CalculatorPureImpl implements Calculator {
    
    @Override
    public int add(int i, int j) {
    
        int result = i + j;
    
        return result;
    }
    
    @Override
    public int sub(int i, int j) {
    
        int result = i - j;
    
        return result;
    }
    
    @Override
    public int mul(int i, int j) {
    
        int result = i * j;
    
        return result;
    }
    
    @Override
    public int div(int i, int j) {
    
        int result = i / j;
    
        return result;
    }
}
```
      4. 声明切面类

```Java
package com.atguigu.advice;

import org.aspectj.lang.annotation.*;
import org.springframework.stereotype.Component;

// @Aspect表示这个类是一个切面类
@Aspect
// @Component注解保证这个切面类能够放入IOC容器
@Component
public class LogAspect {
        
    // @Before注解：声明当前方法是前置通知方法
    // value属性：指定切入点表达式，由切入点表达式控制当前通知方法要作用在哪一个目标方法上
    @Before(value = "execution(public int com.atguigu.proxy.CalculatorPureImpl.add(int,int))")
    public void printLogBeforeCore() {
        System.out.println("[AOP前置通知] 方法开始了");
    }
    
    @AfterReturning(value = "execution(public int com.atguigu.proxy.CalculatorPureImpl.add(int,int))")
    public void printLogAfterSuccess() {
        System.out.println("[AOP返回通知] 方法成功返回了");
    }
    
    @AfterThrowing(value = "execution(public int com.atguigu.proxy.CalculatorPureImpl.add(int,int))")
    public void printLogAfterException() {
        System.out.println("[AOP异常通知] 方法抛异常了");
    }
    
    @After(value = "execution(public int com.atguigu.proxy.CalculatorPureImpl.add(int,int))")
    public void printLogFinallyEnd() {
        System.out.println("[AOP后置通知] 方法最终结束了");
    }
    
}
```
      5. 开启aspectj注解支持
          1. xml方式

```XML
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xmlns:context="http://www.springframework.org/schema/context"
       xmlns:aop="http://www.springframework.org/schema/aop"
       xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd http://www.springframework.org/schema/context https://www.springframework.org/schema/context/spring-context.xsd http://www.springframework.org/schema/aop https://www.springframework.org/schema/aop/spring-aop.xsd">

    <!-- 进行包扫描-->
    <context:component-scan base-package="com.atguigu" />
    <!-- 开启aspectj框架注解支持-->
    <aop:aspectj-autoproxy />
</beans>
```
          2. 配置类方式

```Java
@Configuration
@ComponentScan(basePackages = "com.atguigu")
//作用等于 <aop:aspectj-autoproxy /> 配置类上开启 Aspectj注解支持!
@EnableAspectJAutoProxy
public class MyConfig {
}

```
      6. 测试效果

```Java
//@SpringJUnitConfig(locations = "classpath:spring-aop.xml")
@SpringJUnitConfig(value = {MyConfig.class})
public class AopTest {

    @Autowired
    private Calculator calculator;

    @Test
    public void testCalculator(){
        calculator.add(1,1);
    }
}

```

          输出结果：

```Java
"C:\Program Files\Java\jdk-17\bin\java.exe" -ea -Didea.test.cyclic.buffer.size=1048576 "-javaagent:D:\Program Files\JetBrains\IntelliJ IDEA 2022.3.2\lib\idea_rt.jar=65511:D:\Program Files\JetBrains\IntelliJ IDEA 2022.3.2\bin" -Dfile.encoding=UTF-8 -classpath "C:\Users\Jackiechan\.m2\repository\org\junit\platform\junit-platform-launcher\1.3.1\junit-platform-launcher-1.3.1.jar;C:\Users\Jackiechan\.m2\repository\org\apiguardian\apiguardian-api\1.0.0\apiguardian-api-1.0.0.jar;C:\Users\Jackiechan\.m2\repository\org\junit\platform\junit-platform-engine\1.3.1\junit-platform-engine-1.3.1.jar;C:\Users\Jackiechan\.m2\repository\org\junit\platform\junit-platform-commons\1.3.1\junit-platform-commons-1.3.1.jar;C:\Users\Jackiechan\.m2\repository\org\opentest4j\opentest4j\1.1.1\opentest4j-1.1.1.jar;C:\Users\Jackiechan\.m2\repository\org\junit\jupiter\junit-jupiter-engine\5.3.1\junit-jupiter-engine-5.3.1.jar;C:\Users\Jackiechan\.m2\repository\org\junit\jupiter\junit-jupiter-api\5.3.1\junit-jupiter-api-5.3.1.jar;D:\Program Files\JetBrains\IntelliJ IDEA 2022.3.2\lib\idea_rt.jar;D:\Program Files\JetBrains\IntelliJ IDEA 2022.3.2\plugins\junit\lib\junit5-rt.jar;D:\Program Files\JetBrains\IntelliJ IDEA 2022.3.2\plugins\junit\lib\junit-rt.jar;D:\javaprojects\backend-engineering\part01-spring\spring-aop-annotation\target\test-classes;D:\javaprojects\backend-engineering\part01-spring\spring-aop-annotation\target\classes;D:\repository\org\springframework\spring-context\6.0.6\spring-context-6.0.6.jar;D:\repository\org\springframework\spring-beans\6.0.6\spring-beans-6.0.6.jar;D:\repository\org\springframework\spring-core\6.0.6\spring-core-6.0.6.jar;D:\repository\org\springframework\spring-jcl\6.0.6\spring-jcl-6.0.6.jar;D:\repository\org\springframework\spring-expression\6.0.6\spring-expression-6.0.6.jar;D:\repository\org\junit\jupiter\junit-jupiter-api\5.3.1\junit-jupiter-api-5.3.1.jar;D:\repository\org\apiguardian\apiguardian-api\1.0.0\apiguardian-api-1.0.0.jar;D:\repository\org\opentest4j\opentest4j\1.1.1\opentest4j-1.1.1.jar;D:\repository\org\junit\platform\junit-platform-commons\1.3.1\junit-platform-commons-1.3.1.jar;D:\repository\org\springframework\spring-test\6.0.6\spring-test-6.0.6.jar;D:\repository\jakarta\annotation\jakarta.annotation-api\2.1.1\jakarta.annotation-api-2.1.1.jar;D:\repository\mysql\mysql-connector-java\8.0.25\mysql-connector-java-8.0.25.jar;D:\repository\com\google\protobuf\protobuf-java\3.11.4\protobuf-java-3.11.4.jar;D:\repository\com\alibaba\druid\1.2.8\druid-1.2.8.jar;D:\repository\javax\annotation\javax.annotation-api\1.3.2\javax.annotation-api-1.3.2.jar;D:\repository\org\springframework\spring-aop\6.0.6\spring-aop-6.0.6.jar;D:\repository\org\springframework\spring-aspects\6.0.6\spring-aspects-6.0.6.jar;D:\repository\org\aspectj\aspectjweaver\1.9.9.1\aspectjweaver-1.9.9.1.jar" com.intellij.rt.junit.JUnitStarter -ideVersion5 -junit5 com.atguigu.test.AopTest,testCalculator
[AOP前置通知] 方法开始了
[AOP返回通知] 方法成功返回了
[AOP后置通知] 方法最终结束了
```

    #### 5.5.3 获取通知细节信息
      1. **JointPoint接口**
    
          需要获取方法签名、传入的实参等信息时，可以在通知方法声明JoinPoint类型的形参。
    
          - 要点1：JoinPoint 接口通过 getSignature() 方法获取目标方法的签名（方法声明时的完整信息）
          - 要点2：通过目标方法签名对象获取方法名
          - 要点3：通过 JoinPoint 对象获取外界调用目标方法时传入的实参列表组成的数组

```Java
// @Before注解标记前置通知方法
// value属性：切入点表达式，告诉Spring当前通知方法要套用到哪个目标方法上
// 在前置通知方法形参位置声明一个JoinPoint类型的参数，Spring就会将这个对象传入
// 根据JoinPoint对象就可以获取目标方法名称、实际参数列表
@Before(value = "execution(public int com.atguigu.aop.api.Calculator.add(int,int))")
public void printLogBeforeCore(JoinPoint joinPoint) {
    
    // 1.通过JoinPoint对象获取目标方法签名对象
    // 方法的签名：一个方法的全部声明信息
    Signature signature = joinPoint.getSignature();
    
    // 2.通过方法的签名对象获取目标方法的详细信息
    String methodName = signature.getName();
    System.out.println("methodName = " + methodName);
    
    int modifiers = signature.getModifiers();
    System.out.println("modifiers = " + modifiers);
    
    String declaringTypeName = signature.getDeclaringTypeName();
    System.out.println("declaringTypeName = " + declaringTypeName);
    
    // 3.通过JoinPoint对象获取外界调用目标方法时传入的实参列表
    Object[] args = joinPoint.getArgs();
    
    // 4.由于数组直接打印看不到具体数据，所以转换为List集合
    List<Object> argList = Arrays.asList(args);
    
    System.out.println("[AOP前置通知] " + methodName + "方法开始了，参数列表：" + argList);
}
```
      2. **方法返回值**
    
          在返回通知中，通过**@AfterReturning**注解的returning属性获取目标方法的返回值！

```Java
// @AfterReturning注解标记返回通知方法
// 在返回通知中获取目标方法返回值分两步：
// 第一步：在@AfterReturning注解中通过returning属性设置一个名称
// 第二步：使用returning属性设置的名称在通知方法中声明一个对应的形参
@AfterReturning(
        value = "execution(public int com.atguigu.aop.api.Calculator.add(int,int))",
        returning = "targetMethodReturnValue"
)
public void printLogAfterCoreSuccess(JoinPoint joinPoint, Object targetMethodReturnValue) {
    
    String methodName = joinPoint.getSignature().getName();
    
    System.out.println("[AOP返回通知] "+methodName+"方法成功结束了，返回值是：" + targetMethodReturnValue);
}
```
      3. **异常对象捕捉**
    
          在异常通知中，通过@AfterThrowing注解的throwing属性获取目标方法抛出的异常对象

```Java
// @AfterThrowing注解标记异常通知方法
// 在异常通知中获取目标方法抛出的异常分两步：
// 第一步：在@AfterThrowing注解中声明一个throwing属性设定形参名称
// 第二步：使用throwing属性指定的名称在通知方法声明形参，Spring会将目标方法抛出的异常对象从这里传给我们
@AfterThrowing(
        value = "execution(public int com.atguigu.aop.api.Calculator.add(int,int))",
        throwing = "targetMethodException"
)
public void printLogAfterCoreException(JoinPoint joinPoint, Throwable targetMethodException) {
    
    String methodName = joinPoint.getSignature().getName();
    
    System.out.println("[AOP异常通知] "+methodName+"方法抛异常了，异常类型是：" + targetMethodException.getClass().getName());
}
```

    #### 5.5.4 切点表达式语法
      1. **切点表达式作用**
    
          AOP切点表达式（Pointcut Expression）是一种用于指定切点的语言，它可以通过定义匹配规则，来选择需要被切入的目标对象。
    
          ![](http://heavy_code_industry.gitee.io/code_heavy_industry/assets/img/img028.cb7f2153.png)


​          
​      2. **切点表达式语法**
​    
          切点表达式总结
    
          ![](http://heavy_code_industry.gitee.io/code_heavy_industry/assets/img/img011.dde1a79a.png)
    
          语法细节
    
          - 第一位：execution( ) 固定开头
          - 第二位：方法访问修饰符

```Java
public private 直接描述对应修饰符即可
```
          - 第三位：方法返回值

```Java
int String void 直接描述返回值类型

```

              注意：
    
              特殊情况 不考虑 访问修饰符和返回值
    
                execution(* * ) 这是错误语法
    
                execution(*) == 你只要考虑返回值 或者 不考虑访问修饰符 相当于全部不考虑了
          - 第四位：指定包的地址

```Java
 固定的包: com.atguigu.api | service | dao
 单层的任意命名: com.atguigu.*  = com.atguigu.api  com.atguigu.dao  * = 任意一层的任意命名
 任意层任意命名: com.. = com.atguigu.api.erdaye com.a.a.a.a.a.a.a  ..任意层,任意命名 用在包上!
 注意: ..不能用作包开头   public int .. 错误语法  com..
 找到任何包下: *..
```
          - 第五位：指定类名称

```Java
固定名称: UserService
任意类名: *
部分任意: com..service.impl.*Impl
任意包任意类: *..*

```
          - 第六位：指定方法名称

```Java
语法和类名一致
任意访问修饰符,任意类的任意方法: * *..*.*
```
          - 第七位：方法参数

```Java
第七位: 方法的参数描述
       具体值: (String,int) != (int,String) 没有参数 ()
       模糊值: 任意参数 有 或者 没有 (..)  ..任意参数的意识
       部分具体和模糊:
         第一个参数是字符串的方法 (String..)
         最后一个参数是字符串 (..String)
         字符串开头,int结尾 (String..int)
         包含int类型(..int..)
```
      3. **切点表达式案例**

```Java
1.查询某包某类下，访问修饰符是公有，返回值是int的全部方法
2.查询某包下类中第一个参数是String的方法
3.查询全部包下，无参数的方法！
4.查询com包下，以int参数类型结尾的方法
5.查询指定包下，Service开头类的私有返回值int的无参数方法

```

    #### 5.5.5 重用（提取）切点表达式
      1. 重用切点表达式优点

```Java
 // @Before注解：声明当前方法是前置通知方法
// value属性：指定切入点表达式，由切入点表达式控制当前通知方法要作用在哪一个目标方法上
@Before(value = "execution(public int com.atguigu.proxy.CalculatorPureImpl.add(int,int))")
public void printLogBeforeCore() {
    System.out.println("[AOP前置通知] 方法开始了");
}

@AfterReturning(value = "execution(public int com.atguigu.proxy.CalculatorPureImpl.add(int,int))")
public void printLogAfterSuccess() {
    System.out.println("[AOP返回通知] 方法成功返回了");
}

@AfterThrowing(value = "execution(public int com.atguigu.proxy.CalculatorPureImpl.add(int,int))")
public void printLogAfterException() {
    System.out.println("[AOP异常通知] 方法抛异常了");
}

@After(value = "execution(public int com.atguigu.proxy.CalculatorPureImpl.add(int,int))")
public void printLogFinallyEnd() {
    System.out.println("[AOP后置通知] 方法最终结束了");
}
```

          上面案例，是我们之前编写切点表达式的方式，发现， 所有增强方法的切点表达式相同！
    
          出现了冗余，如果需要切换也不方便统一维护！
    
          我们可以将切点提取，在增强上进行引用即可！
      2. 同一类内部引用
    
          提取

```Java
// 切入点表达式重用
@Pointcut("execution(public int com.atguigu.aop.api.Calculator.add(int,int)))")
public void declarPointCut() {}
```

          注意：提取切点注解使用@Pointcut(切点表达式) ， 需要添加到一个无参数无返回值方法上即可！
    
          引用

```Java
@Before(value = "declarPointCut()")
public void printLogBeforeCoreOperation(JoinPoint joinPoint) {
```
      3. 不同类中引用
    
          不同类在引用切点，只需要添加类的全限定符+方法名即可！

```Java
@Before(value = "com.atguigu.spring.aop.aspect.LogAspect.declarPointCut()")
public Object roundAdvice(ProceedingJoinPoint joinPoint) {
```
      4. 切点统一管理
    
          建议：将切点表达式统一存储到一个类中进行集中管理和维护！

```Java
@Component
public class AtguiguPointCut {
    
    @Pointcut(value = "execution(public int *..Calculator.sub(int,int))")
    public void atguiguGlobalPointCut(){}
    
    @Pointcut(value = "execution(public int *..Calculator.add(int,int))")
    public void atguiguSecondPointCut(){}
    
    @Pointcut(value = "execution(* *..*Service.*(..))")
    public void transactionPointCut(){}
}
```

    #### 5.5.6 环绕通知
    
      环绕通知对应整个 try...catch...finally 结构，包括前面四种通知的所有功能。

```Java
// 使用@Around注解标明环绕通知方法
@Around(value = "com.atguigu.aop.aspect.AtguiguPointCut.transactionPointCut()")
public Object manageTransaction(
    
        // 通过在通知方法形参位置声明ProceedingJoinPoint类型的形参，
        // Spring会将这个类型的对象传给我们
        ProceedingJoinPoint joinPoint) {
    
    // 通过ProceedingJoinPoint对象获取外界调用目标方法时传入的实参数组
    Object[] args = joinPoint.getArgs();
    
    // 通过ProceedingJoinPoint对象获取目标方法的签名对象
    Signature signature = joinPoint.getSignature();
    
    // 通过签名对象获取目标方法的方法名
    String methodName = signature.getName();
    
    // 声明变量用来存储目标方法的返回值
    Object targetMethodReturnValue = null;
    
    try {
    
        // 在目标方法执行前：开启事务（模拟）
        log.debug("[AOP 环绕通知] 开启事务，方法名：" + methodName + "，参数列表：" + Arrays.asList(args));
    
        // 过ProceedingJoinPoint对象调用目标方法
        // 目标方法的返回值一定要返回给外界调用者
        targetMethodReturnValue = joinPoint.proceed(args);
    
        // 在目标方法成功返回后：提交事务（模拟）
        log.debug("[AOP 环绕通知] 提交事务，方法名：" + methodName + "，方法返回值：" + targetMethodReturnValue);
    
    }catch (Throwable e){
    
        // 在目标方法抛异常后：回滚事务（模拟）
        log.debug("[AOP 环绕通知] 回滚事务，方法名：" + methodName + "，异常：" + e.getClass().getName());
    
    }finally {
    
        // 在目标方法最终结束后：释放数据库连接
        log.debug("[AOP 环绕通知] 释放数据库连接，方法名：" + methodName);
    
    }
    
    return targetMethodReturnValue;
}
```

    #### 5.5.7 切面优先级设置
    
      相同目标方法上同时存在多个切面时，切面的优先级控制切面的内外嵌套顺序。
    
      - 优先级高的切面：外面
      - 优先级低的切面：里面
    
      使用 @Order 注解可以控制切面的优先级：
    
      - @Order(较小的数)：优先级高
      - @Order(较大的数)：优先级低
    
      ![](http://heavy_code_industry.gitee.io/code_heavy_industry/assets/img/img012.b353bc56.png)
    
      实际意义
    
      实际开发时，如果有多个切面嵌套的情况，要慎重考虑。例如：如果事务切面优先级高，那么在缓存中命中数据的情况下，事务切面的操作都浪费了。
    
      ![](http://heavy_code_industry.gitee.io/code_heavy_industry/assets/img/img013.53c41dc7.png)


​      

      此时应该将缓存切面的优先级提高，在事务操作之前先检查缓存中是否存在目标数据。
    
      ![](http://heavy_code_industry.gitee.io/code_heavy_industry/assets/img/img014.ee4ed40a.png)
    
    #### 5.5.8 CGLib动态代理生效
    
      在目标类没有实现任何接口的情况下，Spring会自动使用cglib技术实现代理。为了证明这一点，我们做下面的测试：

```Java
@Service
public class EmployeeService {
    
    public void getEmpList() {
       System.out.print("方法内部 com.atguigu.aop.imp.EmployeeService.getEmpList");
    }
}
```

      测试：

```Java
  @Autowired
  private EmployeeService employeeService;
  
  @Test
  public void testNoInterfaceProxy() {
      employeeService.getEmpList();
  }
```

      没有接口：
    
      ![](http://heavy_code_industry.gitee.io/code_heavy_industry/assets/img/img029.d45d40f4.png)
    
      有接口：
    
      ![](http://heavy_code_industry.gitee.io/code_heavy_industry/assets/img/img030.e2f27997.png)
    
      使用总结：
    
        a.  如果目标类有接口,选择使用jdk动态代理
    
        b.  如果目标类没有接口,选择cglib动态代理
    
        c.  如果有接口,接口接值
    
        d.  如果没有接口,类进行接值
    
    #### 5.5.9 注解实现小结
    
      ![](http://heavy_code_industry.gitee.io/code_heavy_industry/assets/img/img015.9c921baf.png)

  ## 5.6 Spring AOP基于XML方式实现(了解)
    1. 准备工作
    
        加入依赖
    
        和基于注解的 AOP 时一样。
    
        准备代码
    
        把测试基于注解功能时的Java类复制到新module中，去除所有注解。
    2. 配置Spring配置文件

```XML
<!-- 配置目标类的bean -->
<bean id="calculatorPure" class="com.atguigu.aop.imp.CalculatorPureImpl"/>
    
<!-- 配置切面类的bean -->
<bean id="logAspect" class="com.atguigu.aop.aspect.LogAspect"/>
    
<!-- 配置AOP -->
<aop:config>
    
    <!-- 配置切入点表达式 -->
    <aop:pointcut id="logPointCut" expression="execution(* *..*.*(..))"/>
    
    <!-- aop:aspect标签：配置切面 -->
    <!-- ref属性：关联切面类的bean -->
    <aop:aspect ref="logAspect">
        <!-- aop:before标签：配置前置通知 -->
        <!-- method属性：指定前置通知的方法名 -->
        <!-- pointcut-ref属性：引用切入点表达式 -->
        <aop:before method="printLogBeforeCore" pointcut-ref="logPointCut"/>
    
        <!-- aop:after-returning标签：配置返回通知 -->
        <!-- returning属性：指定通知方法中用来接收目标方法返回值的参数名 -->
        <aop:after-returning
                method="printLogAfterCoreSuccess"
                pointcut-ref="logPointCut"
                returning="targetMethodReturnValue"/>
    
        <!-- aop:after-throwing标签：配置异常通知 -->
        <!-- throwing属性：指定通知方法中用来接收目标方法抛出异常的异常对象的参数名 -->
        <aop:after-throwing
                method="printLogAfterCoreException"
                pointcut-ref="logPointCut"
                throwing="targetMethodException"/>
    
        <!-- aop:after标签：配置后置通知 -->
        <aop:after method="printLogCoreFinallyEnd" pointcut-ref="logPointCut"/>
    
        <!-- aop:around标签：配置环绕通知 -->
        <!--<aop:around method="……" pointcut-ref="logPointCut"/>-->
    </aop:aspect>
    
</aop:config>

```
    3. 测试

```Java
@SpringJUnitConfig(locations = "classpath:spring-aop.xml")
public class AopTest {

    @Autowired
    private Calculator calculator;

    @Test
    public void testCalculator(){
        System.out.println(calculator);
        calculator.add(1,1);
    }
}
```

  ## 5.7 Spring AOP对获取Bean的影响理解

    #### 5.7.1 根据类型装配 bean
      1. 情景一
          - bean 对应的类没有实现任何接口
          - 根据 bean 本身的类型获取 bean
              - 测试：IOC容器中同类型的 bean 只有一个
    
                  正常获取到 IOC 容器中的那个 bean 对象
              - 测试：IOC 容器中同类型的 bean 有多个
    
                  会抛出 NoUniqueBeanDefinitionException 异常，表示 IOC 容器中这个类型的 bean 有多个
      2. 情景二
          - bean 对应的类实现了接口，这个接口也只有这一个实现类
              - 测试：根据接口类型获取 bean
              - 测试：根据类获取 bean
              - 结论：上面两种情况其实都能够正常获取到 bean，而且是同一个对象
      3. 情景三
          - 声明一个接口
          - 接口有多个实现类
          - 接口所有实现类都放入 IOC 容器
              - 测试：根据接口类型获取 bean
    
                  会抛出 NoUniqueBeanDefinitionException 异常，表示 IOC 容器中这个类型的 bean 有多个
              - 测试：根据类获取bean
    
                  正常
      4. 情景四
          - 声明一个接口
          - 接口有一个实现类
          - 创建一个切面类，对上面接口的实现类应用通知
              - 测试：根据接口类型获取bean
    
                  正常
              - 测试：根据类获取bean
    
                  无法获取
    
          原因分析：
    
          - 应用了切面后，真正放在IOC容器中的是代理类的对象
          - 目标类并没有被放到IOC容器中，所以根据目标类的类型从IOC容器中是找不到的
    
              ![](http://heavy_code_industry.gitee.io/code_heavy_industry/assets/img/img021.3e0da1cc.png)
      5. 情景五
          - 声明一个类
          - 创建一个切面类，对上面的类应用通知
              - 测试：根据类获取 bean，能获取到
    
              ![](http://heavy_code_industry.gitee.io/code_heavy_industry/assets/img/img023.b5696f3e.png)
    
              debug查看实际类型：
    
              ![](http://heavy_code_industry.gitee.io/code_heavy_industry/assets/img/img024.558f6062.png)
    
    #### 5.7.2 使用总结
    
      对实现了接口的类应用切面
    
      ![](https://secure2.wostatic.cn/static/dJxjyGJAQazCzzNRQCyPMb/image.png)
    
      对没实现接口的类应用切面new
    
      ![](https://secure2.wostatic.cn/static/mRgDnd1d6a3oa73t2A7LDK/image.png)
    
      **如果使用AOP技术，目标类有接口，必须使用接口类型接收IoC容器中代理组件！**

# 十二、Spring 声明式事务

  ## 6.1 声明式事务概念

    #### 6.1.1 编程式事务
    
      编程式事务是指手动编写程序来管理事务，即通过编写代码的方式直接控制事务的提交和回滚。在 Java 中，通常使用事务管理器(如 Spring 中的 `PlatformTransactionManager`)来实现编程式事务。
    
      编程式事务的主要优点是灵活性高，可以按照自己的需求来控制事务的粒度、模式等等。但是，编写大量的事务控制代码容易出现问题，对代码的可读性和可维护性有一定影响。

```Java
Connection conn = ...;
  
try {
    // 开启事务：关闭事务的自动提交
    conn.setAutoCommit(false);
    // 核心操作
    // 业务代码
    // 提交事务
    conn.commit();
  
}catch(Exception e){
  
    // 回滚事务
    conn.rollBack();
  
}finally{
  
    // 释放数据库连接
    conn.close();
  
}
```

      编程式的实现方式存在缺陷：
    
      - 细节没有被屏蔽：具体操作过程中，所有细节都需要程序员自己来完成，比较繁琐。
      - 代码复用性不高：如果没有有效抽取出来，每次实现功能都需要自己编写代码，代码就没有得到复用。
    
    #### 6.1.2 声明式事务
    
      声明式事务是指使用注解或 XML 配置的方式来控制事务的提交和回滚。
    
      开发者只需要添加配置即可， 具体事务的实现由第三方框架实现，避免我们直接进行事务操作！
    
      使用声明式事务可以将事务的控制和业务逻辑分离开来，提高代码的可读性和可维护性。
    
      区别：
    
      - 编程式事务需要手动编写代码来管理事务
      - 而声明式事务可以通过配置文件或注解来控制事务。
    
    #### 6.1.3 Spring事务管理器
      1. Spring声明式事务对应依赖
          - spring-tx: 包含声明式事务实现的基本规范（事务管理器规范接口和事务增强等等）
          - spring-jdbc: 包含DataSource方式事务管理器实现类DataSourceTransactionManager
          - spring-orm: 包含其他持久层框架的事务管理器实现类例如：Hibernate/Jpa等
      2. Spring声明式事务对应事务管理器接口
    
          ![](https://secure2.wostatic.cn/static/cTpSy6E9Vzq4H8i1x7MLEf/image.png)
    
          我们现在要使用的事务管理器是org.springframework.jdbc.datasource.DataSourceTransactionManager，将来整合 JDBC方式、JdbcTemplate方式、Mybatis方式的事务实现！
    
          DataSourceTransactionManager类中的主要方法：
    
          - doBegin()：开启事务
          - doSuspend()：挂起事务
          - doResume()：恢复挂起的事务
          - doCommit()：提交事务
          - doRollback()：回滚事务

  ## 6.2 基于注解的声明式事务

    #### 6.2.1 准备工作
      1. 准备项目

```XML
<dependencies>
  <!--spring context依赖-->
  <!--当你引入Spring Context依赖之后，表示将Spring的基础依赖引入了-->
  <dependency>
      <groupId>org.springframework</groupId>
      <artifactId>spring-context</artifactId>
      <version>6.0.6</version>
  </dependency>

  <!--junit5测试-->
  <dependency>
      <groupId>org.junit.jupiter</groupId>
      <artifactId>junit-jupiter-api</artifactId>
      <version>5.3.1</version>
  </dependency>


  <dependency>
      <groupId>org.springframework</groupId>
      <artifactId>spring-test</artifactId>
      <version>6.0.6</version>
      <scope>test</scope>
  </dependency>

  <dependency>
      <groupId>jakarta.annotation</groupId>
      <artifactId>jakarta.annotation-api</artifactId>
      <version>2.1.1</version>
  </dependency>

  <!-- 数据库驱动 和 连接池-->
  <dependency>
      <groupId>mysql</groupId>
      <artifactId>mysql-connector-java</artifactId>
      <version>8.0.25</version>
  </dependency>

  <dependency>
      <groupId>com.alibaba</groupId>
      <artifactId>druid</artifactId>
      <version>1.2.8</version>
  </dependency>

  <!-- spring-jdbc -->
  <dependency>
      <groupId>org.springframework</groupId>
      <artifactId>spring-jdbc</artifactId>
      <version>6.0.6</version>
  </dependency>

  <!-- 声明式事务依赖-->
  <dependency>
      <groupId>org.springframework</groupId>
      <artifactId>spring-tx</artifactId>
      <version>6.0.6</version>
  </dependency>


  <dependency>
      <groupId>org.springframework</groupId>
      <artifactId>spring-aop</artifactId>
      <version>6.0.6</version>
  </dependency>

  <dependency>
      <groupId>org.springframework</groupId>
      <artifactId>spring-aspects</artifactId>
      <version>6.0.6</version>
  </dependency>
</dependencies>
```
      2. 外部配置文件
    
          jdbc.properties

```.properties
atguigu.url=jdbc:mysql://localhost:3306/studb
atguigu.driver=com.mysql.cj.jdbc.Driver
atguigu.username=root
atguigu.password=root
```
      3. spring配置文件

```Java
@Configuration
@ComponentScan("com.atguigu")
@PropertySource("classpath:jdbc.properties")
public class JavaConfig {

    @Value("${atguigu.driver}")
    private String driver;
    @Value("${atguigu.url}")
    private String url;
    @Value("${atguigu.username}")
    private String username;
    @Value("${atguigu.password}")
    private String password;



    //druid连接池
    @Bean
    public DataSource dataSource(){
        DruidDataSource dataSource = new DruidDataSource();
        dataSource.setDriverClassName(driver);
        dataSource.setUrl(url);
        dataSource.setUsername(username);
        dataSource.setPassword(password);
        return dataSource;
    }


    @Bean
    //jdbcTemplate
    public JdbcTemplate jdbcTemplate(DataSource dataSource){
        JdbcTemplate jdbcTemplate = new JdbcTemplate();
        jdbcTemplate.setDataSource(dataSource);
        return jdbcTemplate;
    }

}

```
      4. 准备dao/service层
    
          dao

```Java
@Repository
public class StudentDao {
    
    @Autowired
    private JdbcTemplate jdbcTemplate;
    
    public void updateNameById(String name,Integer id){
        String sql = "update students set name = ? where id = ? ;";
        int rows = jdbcTemplate.update(sql, name, id);
    }

    public void updateAgeById(Integer age,Integer id){
        String sql = "update students set age = ? where id = ? ;";
        jdbcTemplate.update(sql,age,id);
    }
}

```

          service

```Java
@Service
public class StudentService {
    
    @Autowired
    private StudentDao studentDao;
    
    public void changeInfo(){
        studentDao.updateAgeById(100,1);
        System.out.println("-----------");
        studentDao.updateNameById("test1",1);
    }
}

```
      5. 测试环境搭建

```Java
/**
 * projectName: com.atguigu.test
 *
 * description:
 */
@SpringJUnitConfig(JavaConfig.class)
public class TxTest {

    @Autowired
    private StudentService studentService;

    @Test
    public void  testTx(){
        studentService.changeInfo();
    }
}

```

    #### 6.2.2 基本事务控制
      1. 配置事务管理器
    
          数据库相关的配置

```Java
/**
 * projectName: com.atguigu.config
 *
 * description: 数据库和连接池配置类
 */

@Configuration
@ComponenScan("com.atguigu")
@PropertySource(value = "classpath:jdbc.properties")
@EnableTransactionManagement
public class DataSourceConfig {

    /**
     * 实例化dataSource加入到ioc容器
     * @param url
     * @param driver
     * @param username
     * @param password
     * @return
     */
    @Bean
    public DataSource dataSource(@Value("${atguigu.url}")String url,
                                 @Value("${atguigu.driver}")String driver,
                                 @Value("${atguigu.username}")String username,
                                 @Value("${atguigu.password}")String password){
        DruidDataSource dataSource = new DruidDataSource();
        dataSource.setDriverClassName(driver);
        dataSource.setUrl(url);
        dataSource.setUsername(username);
        dataSource.setPassword(password);

        return dataSource;
    }

    /**
     * 实例化JdbcTemplate对象,需要使用ioc中的DataSource
     * @param dataSource
     * @return
     */
    @Bean
    public JdbcTemplate jdbcTemplate(DataSource dataSource){
        JdbcTemplate jdbcTemplate = new JdbcTemplate();
        jdbcTemplate.setDataSource(dataSource);
        return jdbcTemplate;
    }
    
    /**
     * 装配事务管理实现对象
     * @param dataSource
     * @return
     */
    @Bean
    public TransactionManager transactionManager(DataSource dataSource){
        return new DataSourceTransactionManager(dataSource);
    }

}

```
      2. 使用声明事务注解@Transactional

```Java
/**
 * projectName: com.atguigu.service
 *
 */
@Service
public class StudentService {

    @Autowired
    private StudentDao studentDao;

    @Transactional
    public void changeInfo(){
        studentDao.updateAgeById(100,1);
        System.out.println("-----------");
        int i = 1/0;
        studentDao.updateNameById("test1",1);
    }
}

```
      3. 测试事务效果

```Java
/**
 * projectName: com.atguigu.test
 *
 * description:
 */
//@SpringJUnitConfig(locations = "classpath:application.xml")
@SpringJUnitConfig(classes = DataSourceConfig.class)
public class TxTest {

    @Autowired
    private StudentService studentService;

    @Test
    public void  testTx(){
        studentService.changeInfo();
    }
}

```

    #### 6.2.3 事务属性：只读
      1. 只读介绍
    
          对一个查询操作来说，如果我们把它设置成只读，就能够明确告诉数据库，这个操作不涉及写操作。这样数据库就能够针对查询操作来进行优化。
      2. 设置方式

```Java
// readOnly = true把当前事务设置为只读 默认是false!
@Transactional(readOnly = true)
```
      3. 针对DML动作设置只读模式
    
          会抛出下面异常：
    
          Caused by: java.sql.SQLException: Connection is read-only. Queries leading to data modification are not allowed
      4. @Transactional注解放在类上
          1. 生效原则
    
              如果一个类中每一个方法上都使用了 @Transactional 注解，那么就可以将 @Transactional 注解提取到类上。反过来说：@Transactional 注解在类级别标记，会影响到类中的每一个方法。同时，类级别标记的 @Transactional 注解中设置的事务属性也会延续影响到方法执行时的事务属性。除非在方法上又设置了 @Transactional 注解。
    
              对一个方法来说，离它最近的 @Transactional 注解中的事务属性设置生效。
          2. 用法举例
    
              在类级别@Transactional注解中设置只读，这样类中所有的查询方法都不需要设置@Transactional注解了。因为对查询操作来说，其他属性通常不需要设置，所以使用公共设置即可。
    
              然后在这个基础上，对增删改方法设置@Transactional注解 readOnly 属性为 false。

```Java
@Service
@Transactional(readOnly = true)
public class EmpService {
    
    // 为了便于核对数据库操作结果，不要修改同一条记录
    @Transactional(readOnly = false)
    public void updateTwice(……) {
    ……
    }
    
    // readOnly = true把当前事务设置为只读
    // @Transactional(readOnly = true)
    public String getEmpName(Integer empId) {
    ……
    }
    
}
```

    #### 6.2.4 事务属性：超时时间
      1. 需求
    
          事务在执行过程中，有可能因为遇到某些问题，导致程序卡住，从而长时间占用数据库资源。而长时间占用资源，大概率是因为程序运行出现了问题（可能是Java程序或MySQL数据库或网络连接等等）。
    
          此时这个很可能出问题的程序应该被回滚，撤销它已做的操作，事务结束，把资源让出来，让其他正常程序可以执行。
    
          概括来说就是一句话：超时回滚，释放资源。
      2. 设置超时时间

```Java
@Service
public class StudentService {

    @Autowired
    private StudentDao studentDao;

    /**
     * timeout设置事务超时时间,单位秒! 默认: -1 永不超时,不限制事务时间!
     */
    @Transactional(readOnly = false,timeout = 3)
    public void changeInfo(){
        studentDao.updateAgeById(100,1);
        //休眠4秒,等待方法超时!
        try {
            Thread.sleep(4000);
        } catch (InterruptedException e) {
            throw new RuntimeException(e);
        }
        studentDao.updateNameById("test1",1);
    }
}

```
      3. 测试超时效果
    
          执行抛出事务超时异常

```Java
org.springframework.transaction.TransactionTimedOutException: Transaction timed out: deadline was Wed May 24 09:10:43 IRKT 2023

  at org.springframework.transaction.support.ResourceHolderSupport.checkTransactionTimeout(ResourceHolderSupport.java:155)
  at org.springframework.transaction.support.ResourceHolderSupport.getTimeToLiveInMillis(ResourceHolderSupport.java:144)
  at org.springframework.transaction.support.ResourceHolderSupport.getTimeToLiveInSeconds(ResourceHolderSupport.java:128)
  at org.springframework.jdbc.datasource.DataSourceUtils.applyTimeout(DataSourceUtils.java:341)
  at org.springframework.jdbc.core.JdbcTemplate.applyStatementSettings(JdbcTemplate.java:1467)

```

    #### 6.2.5 事务属性：事务异常
      1. 默认情况
    
          默认只针对运行时异常回滚，编译时异常不回滚。情景模拟代码如下：

```Java
@Service
public class StudentService {

    @Autowired
    private StudentDao studentDao;

    /**
     * timeout设置事务超时时间,单位秒! 默认: -1 永不超时,不限制事务时间!
     * rollbackFor = 指定哪些异常才会回滚,默认是 RuntimeException and Error 异常方可回滚!
     * noRollbackFor = 指定哪些异常不会回滚, 默认没有指定,如果指定,应该在rollbackFor的范围内!
     */
    @Transactional(readOnly = false,timeout = 3)
    public void changeInfo() throws FileNotFoundException {
        studentDao.updateAgeById(100,1);
        //主动抛出一个检查异常,测试! 发现不会回滚,因为不在rollbackFor的默认范围内! 
        new FileInputStream("xxxx");
        studentDao.updateNameById("test1",1);
    }
}
```
      2. 设置回滚异常
    
          rollbackFor属性：指定哪些异常类才会回滚,默认是 RuntimeException and Error 异常方可回滚!

```Java
/**
 * timeout设置事务超时时间,单位秒! 默认: -1 永不超时,不限制事务时间!
 * rollbackFor = 指定哪些异常才会回滚,默认是 RuntimeException and Error 异常方可回滚!
 * noRollbackFor = 指定哪些异常不会回滚, 默认没有指定,如果指定,应该在rollbackFor的范围内!
 */
@Transactional(readOnly = false,timeout = 3,rollbackFor = Exception.class)
public void changeInfo() throws FileNotFoundException {
    studentDao.updateAgeById(100,1);
    //主动抛出一个检查异常,测试! 发现不会回滚,因为不在rollbackFor的默认范围内! 
    new FileInputStream("xxxx");
    studentDao.updateNameById("test1",1);
}
```
      3. 设置不回滚的异常
    
          在默认设置和已有设置的基础上，再指定一个异常类型，碰到它不回滚。
    
          noRollbackFor属性：指定哪些异常不会回滚, 默认没有指定,如果指定,应该在rollbackFor的范围内!

```Java
@Service
public class StudentService {

    @Autowired
    private StudentDao studentDao;

    /**
     * timeout设置事务超时时间,单位秒! 默认: -1 永不超时,不限制事务时间!
     * rollbackFor = 指定哪些异常才会回滚,默认是 RuntimeException and Error 异常方可回滚!
     * noRollbackFor = 指定哪些异常不会回滚, 默认没有指定,如果指定,应该在rollbackFor的范围内!
     */
    @Transactional(readOnly = false,timeout = 3,rollbackFor = Exception.class,noRollbackFor = FileNotFoundException.class)
    public void changeInfo() throws FileNotFoundException {
        studentDao.updateAgeById(100,1);
        //主动抛出一个检查异常,测试! 发现不会回滚,因为不在rollbackFor的默认范围内!
        new FileInputStream("xxxx");
        studentDao.updateNameById("test1",1);
    }
}

```

    #### 6.2.6 事务属性：事务隔离级别
      1. 事务隔离级别
    
          数据库事务的隔离级别是指在多个事务并发执行时，数据库系统为了保证数据一致性所遵循的规定。常见的隔离级别包括：
    
          1. 读未提交（Read Uncommitted）：事务可以读取未被提交的数据，容易产生脏读、不可重复读和幻读等问题。实现简单但不太安全，一般不用。
          2. 读已提交（Read Committed）：事务只能读取已经提交的数据，可以避免脏读问题，但可能引发不可重复读和幻读。
          3. 可重复读（Repeatable Read）：在一个事务中，相同的查询将返回相同的结果集，不管其他事务对数据做了什么修改。可以避免脏读和不可重复读，但仍有幻读的问题。
          4. 串行化（Serializable）：最高的隔离级别，完全禁止了并发，只允许一个事务执行完毕之后才能执行另一个事务。可以避免以上所有问题，但效率较低，不适用于高并发场景。
    
          不同的隔离级别适用于不同的场景，需要根据实际业务需求进行选择和调整。
      2. 事务隔离级别设置

```Java
package com.atguigu.service;

import com.atguigu.dao.StudentDao;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.stereotype.Service;
import org.springframework.transaction.annotation.Isolation;
import org.springframework.transaction.annotation.Transactional;

import java.io.FileInputStream;
import java.io.FileNotFoundException;

/**
 * projectName: com.atguigu.service
 */
@Service
public class StudentService {

    @Autowired
    private StudentDao studentDao;

    /**
     * timeout设置事务超时时间,单位秒! 默认: -1 永不超时,不限制事务时间!
     * rollbackFor = 指定哪些异常才会回滚,默认是 RuntimeException and Error 异常方可回滚!
     * noRollbackFor = 指定哪些异常不会回滚, 默认没有指定,如果指定,应该在rollbackFor的范围内!
     * isolation = 设置事务的隔离级别,mysql默认是repeatable read!
     */
    @Transactional(readOnly = false,
                   timeout = 3,
                   rollbackFor = Exception.class,
                   noRollbackFor = FileNotFoundException.class,
                   isolation = Isolation.REPEATABLE_READ)
    public void changeInfo() throws FileNotFoundException {
        studentDao.updateAgeById(100,1);
        //主动抛出一个检查异常,测试! 发现不会回滚,因为不在rollbackFor的默认范围内!
        new FileInputStream("xxxx");
        studentDao.updateNameById("test1",1);
    }
}

```

    #### 6.2.7 事务属性：事务传播行为
      1. 事务传播行为要研究的问题
    
          ![](http://heavy_code_industry.gitee.io/code_heavy_industry/assets/img/img012.faac2cb7.png)
    
          举例代码：

```Java
@Transactional
public void MethodA(){
    // ...
    MethodB();
    // ...
}

//在被调用的子方法中设置传播行为，代表如何处理调用的事务！ 是加入，还是新事务等！
@Transactional(propagation = Propagation.REQUIRES_NEW)
public void MethodB(){
    // ...
}

```
      2. propagation属性
    
          @Transactional 注解通过 propagation 属性设置事务的传播行为。它的默认值是：

```Java
Propagation propagation() default Propagation.REQUIRED;

```

          propagation 属性的可选值由 org.springframework.transaction.annotation.Propagation 枚举类提供：

| 名称             | 含义                                               |
| ---------------- | -------------------------------------------------- |
| REQUIRED  默认值 | 如果父方法有事务，就加入，如果没有就新建自己独立！ |
| REQUIRES_NEW     | 不管父方法是否有事务，我都新建事务，都是独立的！   |

      3. 测试
          1. 声明两个业务方法

```Java
@Service
public class StudentService {

    @Autowired
    private StudentDao studentDao;

    /**
     * timeout设置事务超时时间,单位秒! 默认: -1 永不超时,不限制事务时间!
     * rollbackFor = 指定哪些异常才会回滚,默认是 RuntimeException and Error 异常方可回滚!
     * noRollbackFor = 指定哪些异常不会回滚, 默认没有指定,如果指定,应该在rollbackFor的范围内!
     * isolation = 设置事务的隔离级别,mysql默认是repeatable read!
     */
    @Transactional(readOnly = false,
                   timeout = 3,
                   rollbackFor = Exception.class,
                   noRollbackFor = FileNotFoundException.class,
                   isolation = Isolation.REPEATABLE_READ)
    public void changeInfo() throws FileNotFoundException {
        studentDao.updateAgeById(100,1);
        //主动抛出一个检查异常,测试! 发现不会回滚,因为不在rollbackFor的默认范围内!
        new FileInputStream("xxxx");
        studentDao.updateNameById("test1",1);
    }
    

    /**
     * 声明两个独立修改数据库的事务业务方法
     */
    @Transactional(propagation = Propagation.REQUIRED)
    public void changeAge(){
        studentDao.updateAgeById(99,1);
    }

    @Transactional(propagation = Propagation.REQUIRED)
    public void changeName(){
        studentDao.updateNameById("test2",1);
        int i = 1/0;
    }

}
```
          2. 声明一个整合业务方法

```Java
@Service
public class TopService {

    @Autowired
    private StudentService studentService;

    @Transactional
    public void  topService(){
        studentService.changeAge();
        studentService.changeName();
    }
}

```
          3. 添加传播行为测试

```Java
@SpringJUnitConfig(classes = AppConfig.class)
public class TxTest {

    @Autowired
    private StudentService studentService;

    @Autowired
    private TopService topService;

    @Test
    public void  testTx() throws FileNotFoundException {
        topService.topService();
    }
}

```

          **注意：**
    
            在同一个类中，对于@Transactional注解的方法调用，事务传播行为不会生效。这是因为Spring框架中使用代理模式实现了事务机制，在同一个类中的方法调用并不经过代理，而是通过对象的方法调用，因此@Transactional注解的设置不会被代理捕获，也就不会产生任何事务传播行为的效果。
      4. 其他传播行为值（了解）
          1. Propagation.REQUIRED：如果当前存在事务，则加入当前事务，否则创建一个新事务。
          2. Propagation.REQUIRES_NEW：创建一个新事务，并在新事务中执行。如果当前存在事务，则挂起当前事务，即使新事务抛出异常，也不会影响当前事务。
          3. Propagation.NESTED：如果当前存在事务，则在该事务中嵌套一个新事务，如果没有事务，则与Propagation.REQUIRED一样。
          4. Propagation.SUPPORTS：如果当前存在事务，则加入该事务，否则以非事务方式执行。
          5. Propagation.NOT_SUPPORTED：以非事务方式执行，如果当前存在事务，挂起该事务。
          6. Propagation.MANDATORY：必须在一个已有的事务中执行，否则抛出异常。
          7. Propagation.NEVER：必须在没有事务的情况下执行，否则抛出异常。

# 十三、Spring核心掌握总结

|                 |                                                    |
| --------------- | -------------------------------------------------- |
| 核心点          | 掌握目标                                           |
| spring框架理解  | spring家族和spring framework框架                   |
| spring核心功能  | ioc/di , aop , tx                                  |
| spring ioc / di | 组件管理、ioc容器、ioc/di , 三种配置方式           |
| spring aop      | aop和aop框架和代理技术、基于注解的aop配置          |
| spring tx       | 声明式和编程式事务、动态事务管理器、事务注解、属性 |



