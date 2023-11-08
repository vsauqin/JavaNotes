MyBatis：可以把Java对象转换成数据库表中的一条记录，或者把一条记录转换成 Java对象

MyBatis框架的特点：

1. 支持定制化SQL，存储过程，基本映射以及高级映射
2. 支持XML开发和注解开发
3. 完全做到SQL解耦
4. 提供了基本映射
5. 提供了高级映射标签
6. 提供了XML标签，支持dongtaiSQL编写

ORM:

1. O：object：jvm中的Java对象
2. R：Relstional：关系型数据库
3. M：Mapping：映射



# 一.Mybatis入门程序

sql语句文件

```CarMapper.xml
<?xml version="1.0" encoding="UTF-8" ?>
<!DOCTYPE mapper
        PUBLIC "-//mybatis.org//DTD Mapper 3.0//EN"
        "http://mybatis.org/dtd/mybatis-3-mapper.dtd">
<mapper namespace="javabuhaoxue">
    <insert id="insertCar">
        insert into t_car(id,car_unm,brand,guide,produce,car_type)
        values (3,'1002','丰田',20,'1231231','燃油车')
    </insert>
</mapper>
```

**注意：**

1. sql语句可以不用以分号结尾
2. 

核心配置文件

```Mybatis.xml
<?xml version="1.0" encoding="UTF-8" ?>
<!DOCTYPE configuration
        PUBLIC "-//mybatis.org//DTD Config 3.0//EN"
        "http://mybatis.org/dtd/mybatis-3-config.dtd">
<configuration>
    <environments default="development">
        <environment id="development">
            <transactionManager type="JDBC"/>
            <dataSource type="POOLED">
                <property name="driver" value="com.mysql.cj.jdbc.Driver"/>
                <property name="url" value="jdbc:mysql://localhost:3306/sias"/>
                <property name="username" value="root"/>
                <property name="password" value="223515"/>
            </dataSource>
        </environment>
    </environments>
    <mappers>
<!--        指定Mapper文件的路径-->
        <mapper resource="CarMapper.xml"/>
    </mappers>
</configuration>
```

**注意：**

1. 核心配置文件一半放在类路径下，但是经常放在类路径下可以让程序更加健壮
2. 

和数据库交互的Java代码

```java
package com.powernode.mybatis.test;

import org.apache.ibatis.io.Resources;
import org.apache.ibatis.session.SqlSession;
import org.apache.ibatis.session.SqlSessionFactory;
import org.apache.ibatis.session.SqlSessionFactoryBuilder;

import java.io.InputStream;

/**
 * @Author:XQ
 * @Date:
 */
public class MyBatisIntroductionTest{
    public static void main(String[] args) throws Exception{
//        获取sqlsessionfactorybuilder对象
        SqlSessionFactoryBuilder sqlSessionFactoryBuilder = new SqlSessionFactoryBuilder();
//        获取sqlsessionfactory对象
        InputStream is = Resources.getResourceAsStream("mybitaisconfig.xml");
        SqlSessionFactory build = sqlSessionFactoryBuilder.build(is);
//        获取sqlsession对象
        SqlSession sqlSession = build.openSession();
//        执行sql语句
        int count = sqlSession.insert("insertCar");
        System.out.println("插入了几条语句：" + count);
//        手动提交
        sqlSession.commit();
    }
}

```

## 1.1mybatis的事务管理机制

提供了两种事务管理机制

JDBC和MANAGED

- 在mybatisConfig.xml为文件中可以通过以下配置进行mybatis事务管理

<transactionManager type="JDBC"/>

type的属性值有两个一个是MANAGER另一个是JDBC

- MANAGED事务管理器

mybatis不在管理事务，交由spring等其他容器管理

- JDBC事务管理器

mybatis自己管理

手动提交事务

## 1.2引入日志框架

引入日志框架的目的是为了看清mybatis执行的具体情况

启用日志组件需要在mybatis-config.xml文件中添加以下配置

```java
<setting>
	<setting name="logImpl" value="STDOUT_LOGGING">
</setting>
```

以上是标准日志，配置不够灵活可以集成其他日志组件例如：log4j，logback等等



- logback性能较好，引入步骤

  - 第一步：引入logback相关依赖

  ```.xml
  <dependency>
   <groupId>ch.qos.logback</groupId>
   <artifactId>logback-classic</artifactId>
   <version>1.2.11</version>
   <scope>test</scope>
  </dependency>
  ```

  - 第二步：引入logback相关配置文件（文件名只能叫做logback.xml或logback-test.xml，放到类路径中）

    ```java
    <?xml version="1.0" encoding="UTF-8"?>
    <configuration debug="false">
     <!--定义⽇志⽂件的存储地址-->
     <property name="LOG_HOME" value="/home"/>
     <!-- 控制台输出 -->
     <appender name="STDOUT" class="ch.qos.logback.core.ConsoleAppender">
     <encoder class="ch.qos.logback.classic.encoder.PatternLayoutEncode
    r">
     <!--格式化输出：%d表示⽇期，%thread表示线程名，%-5level：级别从左显示5
    个字符宽度%msg：⽇志消息，%n是换⾏符-->
     <pattern>%d{yyyy-MM-dd HH:mm:ss.SSS} [%thread] %-5level %logge
    r{50} - %msg%n</pattern>
     </encoder>
     </appender>
     <!-- 按照每天⽣成⽇志⽂件 -->
     <appender name="FILE" class="ch.qos.logback.core.rolling.RollingFileAp
    pender">
     <rollingPolicy class="ch.qos.logback.core.rolling.TimeBasedRolling
    Policy">
     <!--⽇志⽂件输出的⽂件名-->
     <FileNamePattern>${LOG_HOME}/TestWeb.log.%d{yyyy-MM-dd}.log</F
    ileNamePattern>
     <!--⽇志⽂件保留天数-->
     <MaxHistory>30</MaxHistory>
     </rollingPolicy>
     <encoder class="ch.qos.logback.classic.encoder.PatternLayoutEncode
    r">
     <!--格式化输出：%d表示⽇期，%thread表示线程名，%-5level：级别从左显示5
    个字符宽度%msg：⽇志消息，%n是换⾏符-->
     <pattern>%d{yyyy-MM-dd HH:mm:ss.SSS} [%thread] %-5level %logge
    r{50} - %msg%n</pattern>
     </encoder>
     <!--⽇志⽂件最⼤的⼤⼩-->
     <triggeringPolicy class="ch.qos.logback.core.rolling.SizeBasedTrig
    geringPolicy">
     <MaxFileSize>100MB</MaxFileSize>
     </triggeringPolicy>
     </appender>
     <!--mybatis log configure-->
     <logger name="com.apache.ibatis" level="TRACE"/>
     <logger name="java.sql.Connection" level="DEBUG"/>
     <logger name="java.sql.Statement" level="DEBUG"/>
     <logger name="java.sql.PreparedStatement" level="DEBUG"/>
     <!-- ⽇志输出级别,logback⽇志级别包括五个：TRACE < DEBUG < INFO < WARN < ER
    ROR -->
     <root level="DEBUG">
     <appender-ref ref="STDOUT"/>
     <appender-ref ref="FILE"/>
     </root>
    </configuration>
    ```

    

## 1.3Mybatis工具类的封装

- 目的：每次获取SqlSession对象的代码太繁琐，所以封装一个工具类

**具体代码如下**

```java
package com.atsias1.utils;

import org.apache.ibatis.io.Resources;
import org.apache.ibatis.session.SqlSession;
import org.apache.ibatis.session.SqlSessionFactory;
import org.apache.ibatis.session.SqlSessionFactoryBuilder;

import java.io.IOException;

/**
 * @Author:XQ
 * @Date:
 */
public class SqlSessionUtil {
    private SqlSessionUtil(){}
    private static SqlSessionFactory build;
    static {
        try {
            build = new SqlSessionFactoryBuilder().build(Resources.getResourceAsStream("mybitaisconfig.xml"));
        } catch (IOException e) {
            throw new RuntimeException(e);
        }
    }
    public static SqlSession openSession(){

        SqlSession sqlSession = build.openSession();
        return sqlSession;
    }
}

```

**测试代码**

```java
@Test
public void testInsertCar(){
	SqlSession sqlSession = SqlSessionUtil.openSession();
	//执行sql
	int count = sqlSession.insert("insertCar");
	System.out.println("插入了几条记录：" + count);
	sqlSession.close();
}
```





# 二.使用MyBatis完成crud

**准备工作**

- pom.xml
  - 打包方式jar
  - 依赖
    - mybatis依赖
    - mysql驱动依赖
    - junit依赖
    - logback依赖
  - mybatis-config.xml放在类路径下
  - CarMapper.xml放在类路径下
  - logback.xml放在类路径下
  - 提供SqlSessionUtil工具类

## 2.1insert（Create）

```.xml
<?xml version="1.0" encoding="UTF-8" ?>
<!DOCTYPE mapper
 PUBLIC "-//mybatis.org//DTD Mapper 3.0//EN"
 "http://mybatis.org/dtd/mybatis-3-mapper.dtd">
<!--namespace先随便写-->
<mapper namespace="car">
 <insert id="insertCar">
 insert into t_car(car_num,brand,guide_price,produce_time,car_typ
e) values('103', '奔驰E300L', 50.3, '2022-01-01', '燃油⻋')
 </insert>
</mapper>

```

以上代码有缺点：SQL语句中的值不能写死，值应该有用户提供，之气那的jdbc代码如下

```java
// JDBC中使⽤ ? 作为占位符。那么MyBatis中会使⽤什么作为占位符呢？
String sql = "insert into t_car(car_num,brand,guide_price,produce_time,car_
type) values(?,?,?,?,?)";
// ......
// 给 ? 传值。那么MyBatis中应该怎么传值呢？
ps.setString(1,"103");
ps.setString(2,"奔驰E300L");
ps.setDouble(3,50.3);
ps.setString(4,"2022-01-01");
ps.setString(5,"燃油⻋");
```

在MyBatis中可以这样做：



### Map集合传入数据

**将数据放到Map集合中去**

**在sql语句中使用#{map集合的key}来完成传播，#{}等同于jdbc中的 ？，#{}就是占位符**

Java程序这样写

```java
public class CarMapperTest{
	@Test
 public void testInsertCar(){
 // 准备数据
 Map<String, Object> map = new HashMap<>();
 map.put("k1", "103");
 map.put("k2", "奔驰E300L");
 map.put("k3", 50.3);
 map.put("k4", "2020-10-01");
 map.put("k5", "燃油⻋");
 // 获取SqlSession对象
 SqlSession sqlSession = SqlSessionUtil.openSession();
 // 执⾏SQL语句（使⽤map集合给sql语句传递数据）
 int count = sqlSession.insert("insertCar", map);
 System.out.println("插⼊了⼏条记录：" + count);
 }
}
```

SQL语句这样写

```java
<?xml version="1.0" encoding="UTF-8" ?>
<!DOCTYPE mapper
 PUBLIC "-//mybatis.org//DTD Mapper 3.0//EN"
 "http://mybatis.org/dtd/mybatis-3-mapper.dtd">
<!--namespace先随便写-->
<mapper namespace="car">
 <insert id="insertCar">
 insert into t_car(car_num,brand,guide_price,produce_time,car_typ
e) values(#{k1},#{k2},#{k3},#{k4},#{k5})
 </insert>
</mapper>
```

**注意：**#{}的里面必须写map集合的key，不能随便写

如果写map集合中不存在的key，那么对应的字段就不会正常获取到值而为null

### pojo类传入数据

- 第一步定义一个pojo类，并提供相关属性

- ```java
  package com.powernode.mybatis.pojo;
  /**
   * POJOs，简单普通的Java对象。封装数据⽤的。
   * @author ⽼杜
   * @version 1.0
   * @since 1.0
   */
  public class Car {
   private Long id;
   private String carNum;
   private String brand;
   private Double guidePrice;
   private String produceTime;
   private String carType;
   @Override
   public String toString() {
   return "Car{" +
   "id=" + id +
   ", carNum='" + carNum + '\'' +
   ", brand='" + brand + '\'' +
   ", guidePrice=" + guidePrice +
   ", produceTime='" + produceTime + '\'' +
   ", carType='" + carType + '\'' +
   '}';
   }
   public Car() {
   }
   public Car(Long id, String carNum, String brand, Double guidePrice, St
  ring produceTime, String carType) {
   this.id = id;
   this.carNum = carNum;
   this.brand = brand;
   this.guidePrice = guidePrice;
   this.produceTime = produceTime;
   this.carType = carType;
   }
   public Long getId() {
   return id;
   }
   public void setId(Long id){
   this.id= id; 
  }
   public String getCarNum()
  {
   return carNum; 
  }
   public void setCarNum(String carNum){
   	this.carNum= carNum; 
  }
   public String getBrand(){
   	return brand; 
  }
   public void setBrand(String brand)
  {
   this.brand= brand; 
  }
   public Double getGuidePrice()
  {
   return guidePric; 
  }
   public void setGuidePrice(Double guidePrice)
  {
   this.guidePrice= guidePrice; 
  }
   public String getProduceTime()
  { return produceTime; 
  }
   public void setProduceTime(String produceTime)
  {
   this.produceTime= produceTime; 
  }
   public String getCarType()
  {
   return carType; 
  }
   public void setCarType(String carType)
  {
   this.carType= carType; 
  }
  }
  
  ```

  
