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

  

- 第二步java程序

```java
@Test
public void testInsertCarByPOJO(){
 // 创建POJO，封装数据
 Car car = new Car();
 car.setCarNum("103");
 car.setBrand("奔驰C200");
 car.setGuidePrice(33.23);
 car.setProduceTime("2020-10-11");
 car.setCarType("燃油⻋");
 // 获取SqlSession对象
 SqlSession sqlSession = SqlSessionUtil.openSession();
 // 执⾏SQL，传数据
 int count = sqlSession.insert("insertCarByPOJO", car);
 System.out.println("插⼊了⼏条记录" + count);
}
```

- 第三步SQL语句

```.xml
<insert id="insertCarByPOJO">
 <!--#{} ⾥写的是POJO的属性名-->
 insert into t_car(car_num,brand,guide_price,produce_time,car_type) values
(#{carNum},#{brand},#{guidePrice},#{produceTime},#{carType})
</insert>

```

**总结：**

如果使用map集合传参，#{}里面写的是map集合的key，如果key不存在不会报错，数据表中会插入null

如果采用pojo传参，#{}里面写的是get方法名去掉get之后将剩下的单词首字母小写

## 2.2delect（Delect）

需求是根据car_num进行删除

SQL语句这样写

```java
<delect id="delectByCarNum">
	delect from t_car where car_num = #{随便写}
</delect>
```

java程序这样写

```java
@Test
public void testDeleteByCarNum(){
 // 获取SqlSession对象
 SqlSession sqlSession = SqlSessionUtil.openSession();
 // 执⾏SQL语句
 int count = sqlSession.delete("deleteByCarNum", "102");
 System.out.println("删除了⼏条记录：" + count);
}
```

**当占位符只有一个是，#{}里面可以随便写**

## 2.3update(Update)

需求：修改id=34的Car信息

SQL语句如下

```java
<update id="updateCarByPOJO">
 update t_car set
 car_num = #{carNum}, brand = #{brand},
 guide_price = #{guidePrice}, produce_time = #{produceTime},
 car_type = #{carType}
 where id = #{id}
</update>
```



java代码如下

```java
@Test
 public void testUpdateCarByPOJO(){
 // 准备数据
 Car car = new Car();
 car.setId(34L);
 car.setCarNum("102");
 car.setBrand("⽐亚迪汉");
 car.setGuidePrice(30.23);
 car.setProduceTime("2018-09-10");
 car.setCarType("电⻋");
 // 获取SqlSession对象
 SqlSession sqlSession = SqlSessionUtil.openSession();
 // 执⾏SQL语句
 int count = sqlSession.update("updateCarByPOJO", car);
 System.out.println("更新了⼏条记录：" + count);
 }
```

## 2.4select(Retrieve)

和其他语句不一样的是，select语句查执行后会返回一个结果集

### 查询一条语句

SQL语句如下

```java
<select id="selectCarById">
	select * from t_car where id = #{id}
</select>
```

java程序如下：

```java
public void testSelectCarById(){
	SqlSession sqlSession = SqlSessionUtil.openSession();
	//执行sql语句
	Object car = sqlSession.selectOne("selectCarById",1);
	System.out.println("car");
}
```

运行结果如下：

```java
//结果出现异常
### Error querying database. Cause: org.apache.ibatis.executor.ExecutorExc
eption:
 A query was run and no Result Maps were found for the Mapped Statement
'car.selectCarById'. 【翻译】：对于⼀个查询语句来说，没有找到查询的结果映射。
 It's likely that neither a Result Type nor a Result Map was specified.
【翻译】：很可能既没有指定结果类型，也没有指定结果映射。
```

以上的大致意思是是要指出一个查询语句的“结果类型“或者”结果映射“

所以如果想让mybatis返回一个java对象的话，需要在<select>标签中添加resultType属性，用来指定查询要转换的类型

代码如下

```java
<select id="selectCarById" resultType="com.powernode.mybatis.pojo.Car">
	select * from t_car where id = #{id}
</select>
```

再次运行后异常不在出现，但是有的属性值为null

查询结果集的列名：id, car_num, brand, guide_price, produce_time, car_type

 Car类的属性名：id, carNum, brand, guidePrice, produceTime, carType

因为结果集的列名和Car类中的属性名不一致，导致无法获得返回值

修改后的sql语句如下

```java
<select id="selectCarById" resultType="com.powernode.mybatis.pojo.Car">
	 select id, car_num as carNum, brand, 
	 guide_price as guidePrice, produce_time 
	 as produceTime, car_type as carType
 from t_car
 where id = #{id}
</select>
```

### 查询多条语句

SQL语句如下

```java
<!--虽然结果是List集合，但是resultType属性需要指定的是List集合中元素的类型。-->
<select id="selectCarAll" resultType="com.powernode.mybatis.pojo.Car">
 <!--记得使⽤as起别名，让查询结果的字段名和java类的属性名对应上。-->
 select
 id, car_num as carNum, brand, guide_price as guidePrice, produce_time a
s produceTime, car_type as carType
 from
 t_car
</select>
```

java代码如下：

```java
@Test
public void testSelectCarAll(){
	SqlSession sqlSession = SqlSessionUtil.openSession();
	//zhixingsql语句
	List<Object> cars = sqlSession.selectList("selectCarAll");
	cars.forEach(car->System.out.println(car));
}
```





## 2.5 有关命名空间

在SQL Mapper的配置文件中<mapper>标签的namespace属性可以翻译为命名空间，这个命名空间的主要作用是方式SQLid冲突

示例如下

创建CarMapper2.xml，代码如下

```java
<?xml version="1.0" encoding="UTF-8" ?>
<!DOCTYPE mapper
 PUBLIC "-//mybatis.org//DTD Mapper 3.0//EN"
 "http://mybatis.org/dtd/mybatis-3-mapper.dtd">
<mapper namespace="car2">
 <select id="selectCarAll" resultType="com.powernode.mybatis.pojo.Car">
 select
 id, car_num as carNum, brand, guide_price as guidePrice, produ
ce_time as produceTime, car_type as carType
 from
 t_car
 </select>
</mapper>
```

此时CarMapper.xml和CarMapper2.xml都有id=“selectCarAll”

将其配置到mybatis.xml中

```.xml
<mappers>
 <mapper resource="CarMapper.xml"/>
 <mapper resource="CarMapper2.xml"/>
</mappers>

```

编写的java代码如下

```java
@Test
public void testNamespace(){
 // 获取SqlSession对象
 SqlSession sqlSession = SqlSessionUtil.openSession();
 // 执⾏SQL语句
 List<Object> cars = sqlSession.selectList("selectCarAll");
 // 输出结果
 cars.forEach(car -> System.out.println(car));
}

```

运行结果

```java
org.apache.ibatis.exceptions.PersistenceException:
### Error querying database. Cause: java.lang.IllegalArgumentException:
 selectCarAll is ambiguous in Mapped Statements collection (try using the
full name including the namespace, or rename one of the entries)
 【翻译】selectCarAll在Mapped Statements集合中不明确（请尝试使⽤包含名称空间的全
名，或重命名其中⼀个条⽬）
 【⼤致意思是】selectCarAll重名了，你要么在selectCarAll前添加⼀个名称空间，要有你改
个其它名字。
```

Java代码修改后

```java
@Test
public void testNamespace(){
 // 获取SqlSession对象
 SqlSession sqlSession = SqlSessionUtil.openSession();
 // 执⾏SQL语句
 //List<Object> cars = sqlSession.selectList("car.selectCarAll");
 List<Object> cars = sqlSession.selectList("car2.selectCarAll");
 // 输出结果
 cars.forEach(car -> System.out.println(car));
}
```

运行正常



# 三.MyBatis配置文件核心详解

文件如下

```java
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
 <property name="url" value="jdbc:mysql://localhost:3306/po
wernode"/>
 <property name="username" value="root"/>
 <property name="password" value="root"/>
 </dataSource>
 </environment>
 </environments>
 <mappers>
 <mapper resource="CarMapper.xml"/>
 <mapper resource="CarMapper2.xml"/>
 </mappers>
</configuration>
```

- configuration：根标签，表示配置信息

- environments：环境，表示数据源

  - default属性：表示默认使用的是哪一个环境，default后面写的是environment的id，default的值只需要和environment的id一致即可

- envirment：具体的环境配置（主要包括：事务管理器的配置和数据源的配置）

  - id：当前环境的唯一标识，

- transactionManager：配置事务管理器

  - type属性：指定事务管理器具体是用什么方式，两个可选
    - JDBC：
    - MANAGER：交给其他容器管理，如果没有事务管理容器，则执行一条DML语句就提交一次

- dataSource：指定数据源

  - type：用来指定使用的数据连接池的策略，可选值有三个

    - UNPOOLED：采用传统的获取链接方式，实现了javax.sql.DataSource接口，但是没有使用池的思想

    ```
    driver – 这是 JDBC 驱动的 Java 类全限定名（并不是 JDBC 驱动中可能包含的数据源类）。
    url – 这是数据库的 JDBC URL 地址。
    username – 登录数据库的用户名。
    password – 登录数据库的密码。
    defaultTransactionIsolationLevel – 默认的连接事务隔离级别。
    defaultNetworkTimeout – 等待数据库操作完成的默认网络超时时间（单位：毫秒）。查看 java.sql.Connection#setNetworkTimeout() 的 API 文档以获取更多信息。
    作为可选项，你也可以传递属性给数据库驱动。只需在属性名加上“driver.”前缀即可，例如：
    
    driver.encoding=UTF8
    这将通过 DriverManager.getConnection(url, driverProperties) 方法传递值为 UTF8 的 encoding 属性给数据库驱动
    ```

    - POOLED利用了池的概念

    ```java
    除了上述提到 UNPOOLED 下的属性外，还有更多属性用来配置 POOLED 的数据源：
    
    poolMaximumActiveConnections – 在任意时间可存在的活动（正在使用）连接数量，默认值：10
    poolMaximumIdleConnections – 任意时间可能存在的空闲连接数。
    poolMaximumCheckoutTime – 在被强制返回之前，池中连接被检出（checked out）时间，默认值：20000 毫秒（即 20 秒）
    poolTimeToWait – 这是一个底层设置，如果获取连接花费了相当长的时间，连接池会打印状态日志并重新尝试获取一个连接（避免在误配置的情况下一直失败且不打印日志），默认值：20000 毫秒（即 20 秒）。
    poolMaximumLocalBadConnectionTolerance – 这是一个关于坏连接容忍度的底层设置， 作用于每一个尝试从缓存池获取连接的线程。 如果这个线程获取到的是一个坏的连接，那么这个数据源允许这个线程尝试重新获取一个新的连接，但是这个重新尝试的次数不应该超过 poolMaximumIdleConnections 与 poolMaximumLocalBadConnectionTolerance 之和。 默认值：3（新增于 3.4.5）
    poolPingQuery – 发送到数据库的侦测查询，用来检验连接是否正常工作并准备接受请求。默认是“NO PING QUERY SET”，这会导致多数数据库驱动出错时返回恰当的错误消息。
    poolPingEnabled – 是否启用侦测查询。若开启，需要设置 poolPingQuery 属性为一个可执行的 SQL 语句（最好是一个速度非常快的 SQL 语句），默认值：false。
    poolPingConnectionsNotUsedFor – 配置 poolPingQuery 的频率。可以被设置为和数据库连接超时时间一样，来避免不必要的侦测，默认值：0（即所有连接每一时刻都被侦测 — 当然仅当 poolPingEnabled 为 true 时适用）。
    ```

    - JNDI：采用服务器提供的JNDI技术实现来获取DataSource对象，不同服务器拿到的DataSource不一样

    property可以是以下属性，但是只能含有两个

    ```
    initial_context – 这个属性用来在 InitialContext 中寻找上下文（即，initialContext.lookup(initial_context)）。这是个可选属性，如果忽略，那么将会直接从 InitialContext 中寻找 data_source 属性。
    data_source – 这是引用数据源实例位置的上下文路径。提供了 initial_context 配置时会在其返回的上下文中进行查找，没有提供时则直接在 InitialContext 中查找。
    和其他数据源配置类似，可以通过添加前缀“env.”直接把属性传递给 InitialContext。比如：
    
    env.encoding=UTF8
    ```

    

## 3.1environment

核心配置文件代码如下

```java
<?xml version="1.0" encoding="UTF-8" ?>
<!DOCTYPE configuration
 PUBLIC "-//mybatis.org//DTD Config 3.0//EN"
 "http://mybatis.org/dtd/mybatis-3-config.dtd">
<configuration>
 
 <environments default="production">
    
 <!--开发环境-->
 <environment id="dev">
 <transactionManager type="JDBC"/>
 <dataSource type="POOLED">
 <property name="driver" value="com.mysql.cj.jdbc.Driver"/>
 <property name="url" value="jdbc:mysql://localhost:3306/po
wernode"/>
 <property name="username" value="root"/>
 <property name="password" value="root"/>
 </dataSource>
 </environment>
    
 <!--⽣产环境-->
 <environment id="production">
 <transactionManager type="JDBC" />
 <dataSource type="POOLED">
 <property name="driver" value="com.mysql.cj.jdbc.Driver"/>
 <property name="url" value="jdbc:mysql://localhost:3306/mybatis"/>
 <property name="username" value="root"/>
 <property name="password" value="root"/>
 </dataSource>
 </environment>
 </environments>
    
 <mappers>
 <mapper resource="CarMapper.xml"/>
 </mappers>
    
</configuration>
```

SQL配置文件如下

```java
<?xml version="1.0" encoding="UTF-8" ?>
<!DOCTYPE mapper
 PUBLIC "-//mybatis.org//DTD Mapper 3.0//EN"
 "http://mybatis.org/dtd/mybatis-3-mapper.dtd">
<mapper namespace="car">
 <insert id="insertCar">
 insert into t_car(id,car_num,brand,guide_price,produce_time,car_type) 
    values(null,#{carNum},#{brand},#{guidePrice},#{produceTime},#{carType})
 </insert>
</mapper>

```

测试类如下

```java
package com.powernode.mybatis;
import com.powernode.mybatis.pojo.Car;
import org.apache.ibatis.io.Resources;
import org.apache.ibatis.session.SqlSession;
import org.apache.ibatis.session.SqlSessionFactory;
import org.apache.ibatis.session.SqlSessionFactoryBuilder;
import org.junit.Test;
public class ConfigurationTest {
 @Test
 public void testEnvironment() throws Exception{
 // 准备数据
 Car car = new Car();
 car.setCarNum("133");
 car.setBrand("丰⽥霸道");
 car.setGuidePrice(50.3);
 car.setProduceTime("2020-01-10");
 car.setCarType("燃油⻋");
 // ⼀个数据库对应⼀个SqlSessionFactory对象
 // 两个数据库对应两个SqlSessionFactory对象，以此类推
 SqlSessionFactoryBuilder sqlSessionFactoryBuilder = new SqlSession
FactoryBuilder();
 // 使⽤默认数据库
 SqlSessionFactory sqlSessionFactory = sqlSessionFactoryBuilder.bui
ld(Resources.getResourceAsStream("mybatis-config.xml"));
 SqlSession sqlSession = sqlSessionFactory.openSession(true);
 int count = sqlSession.insert("insertCar", car);
 System.out.println("插⼊了⼏条记录：" + count);
 // 使⽤指定数据库
 SqlSessionFactory sqlSessionFactory1 = sqlSessionFactoryBuilder.bu
ild(Resources.getResourceAsStream("mybatis-config.xml"), "dev");
 SqlSession sqlSession1 = sqlSessionFactory1.openSession(true);
 int count1 = sqlSession1.insert("insertCar", car);
 System.out.println("插⼊了⼏条记录：" + count1);
 }
}
```



## 3.2transactionManager

核心配置文件如下

```java
<?xml version="1.0" encoding="UTF-8" ?>
<!DOCTYPE configuration
 PUBLIC "-//mybatis.org//DTD Config 3.0//EN"
 "http://mybatis.org/dtd/mybatis-3-config.dtd">
<configuration>
 <environments default="dev">
    
 <environment id="dev">
 <transactionManager type="MANAGED"/>
 <dataSource type="POOLED">
 <property name="driver" value="com.mysql.cj.jdbc.Driver"/>
 <property name="url" value="jdbc:mysql://localhost:3306/powernode"/>
 <property name="username" value="root"/>
 <property name="password" value="root"/>
 </dataSource>
 </environment>
    
 </environments>
    
 <mappers>
 <mapper resource="CarMapper.xml"/>
 </mappers>
</configuration>
```

测试类如下

```java
@Test
public void testTransactionManager() throws Exception{
 // 准备数据
 Car car = new Car();
 car.setCarNum("133");
 car.setBrand("丰⽥霸道");
 car.setGuidePrice(50.3);
 car.setProduceTime("2020-01-10");
 car.setCarType("燃油⻋");
 // 获取SqlSessionFactory对象
 SqlSessionFactoryBuilder sqlSessionFactoryBuilder = new SqlSessionFact
oryBuilder();
 SqlSessionFactory sqlSessionFactory = sqlSessionFactoryBuilder.build(R
esources.getResourceAsStream("mybatis-config2.xml"));
 // 获取SqlSession对象
 SqlSession sqlSession = sqlSessionFactory.openSession();
 // 执⾏SQL
 int count = sqlSession.insert("insertCar", car);
 System.out.println("插⼊了⼏条记录：" + count);
}
```

当事务管理器是：JDBC 

采⽤JDBC的原⽣事务机制：

 开启事务：conn.setAutoCommit(false);

 处理业务...... 

提交事务：conn.commit(); 

当事务管理器是：MANAGED

 交给容器去管理事务，但⽬前使⽤的是本地程序，没有容器的⽀持，当mybatis找不到容器的⽀持 时：没有事务。也就是说只要执⾏⼀条DML语句，则提交⼀次。





## 3.3dataSource

- 当数据源类型是UNPOOLED

每次创建链接对象都是不一样的



- 当type是POOLED

会使用mybatis自己的连接池

核心配置文件如下

```java
<?xml version="1.0" encoding="UTF-8" ?>
<!DOCTYPE configuration
 PUBLIC "-//mybatis.org//DTD Config 3.0//EN"
 "http://mybatis.org/dtd/mybatis-3-config.dtd">
<configuration>
 <environments default="dev">
    
 <environment id="dev">
 <transactionManager type="JDBC"/>
 <dataSource type="POOLED">
 <property name="driver" value="com.mysql.cj.jdbc.Driver"/>
 <property name="url" value="jdbc:mysql://localhost:3306/po
wernode"/>
 <property name="username" value="root"/>
 <property name="password" value="root"/>
 <!--最⼤连接数-->
 <property name="poolMaximumActiveConnections" value="3"/>
 <!--最多空闲数量-->
 <property name="poolMaximumIdleConnections" value="1"/>
 <!--强⾏回归池的时间-->
 <property name="poolMaximumCheckoutTime" value="20000"/>
 <!--这是⼀个底层设置，如果获取连接花费了相当⻓的时间，连接池会打印状
态⽇志并重新尝试获取⼀个连接（避免在误配置的情况下⼀直失败且不打印⽇志），默认值：20000
毫秒（即 20 秒）。-->
 <property name="poolTimeToWait" value="20000"/>
 </dataSource>
 </environment>
    
 </environments>
    
 <mappers>
 <mapper resource="CarMapper.xml"/>
 </mappers>
    
</configuration>
```

poolMaximumActiveConnections：最⼤的活动的连接数量。默认值10

 poolMaximumIdleConnections：最⼤的空闲连接数量。默认值5

 poolMaximumCheckoutTime：强⾏回归池的时间。默认值20秒。 

poolTimeToWait：当⽆法获取到空闲连接时，每隔20秒打印⼀次⽇志，避免因代码配置有误，导致傻 等。（时⻓是可以配置的）

当然，还有其他属性。对于连接池来说，以上⼏个属性⽐较重要。 

最⼤的活动的连接数量就是连接池连接数量的上限。默认值10，如果有10个请求正在使⽤这10个连接， 第11个请求只能等待空闲连接。

最大的空闲连接数量。默认值5，如果已经有了5个空闲连接，当地六个连接要空闲下来的时候，连接池就会关闭该链接对象

- 当type是JNDI

此时可以使用第三方连接池接口

## 3.4properties

mybatis提供了灵活的配置，连接数据库的信息可以单独写到一个属性资源文件中，假设在类的根路径下创建一个jdbc.properties文件

```
jdbc.driver=com.mysql.cj.jdbc.Driver
jdbc.url=jdbc:mysql://localhost:3306/powernode
```

 在mybatis核心配置文件中使用：

```java
<?xml version="1.0" encoding="UTF-8" ?>
<!DOCTYPE configuration
 PUBLIC "-//mybatis.org//DTD Config 3.0//EN"
 "http://mybatis.org/dtd/mybatis-3-config.dtd">
<configuration>
 <!--引⼊外部属性资源⽂件-->
 <properties resource="jdbc.properties">
 <property name="jdbc.username" value="root"/>
 <property name="jdbc.password" value="root"/>
 </properties>
 <environments default="dev">
 <environment id="dev">
 <transactionManager type="JDBC"/>
 <dataSource type="POOLED">
 <!--${key}使⽤-->
 <property name="driver" value="${jdbc.driver}"/>
 <property name="url" value="${jdbc.url}"/>
 <property name="username" value="${jdbc.username}"/>
 <property name="password" value="${jdbc.password}"/>
 </dataSource>
 </environment>
 </environments>
 <mappers>
 <mapper resource="CarMapper.xml"/>
 </mappers>
</configuration>
```

编写Java程序进行测试

```java
@Test
public void testProperties() throws Exception{
 SqlSessionFactoryBuilder sqlSessionFactoryBuilder = new SqlSessionFacto
ryBuilder();
 SqlSessionFactory sqlSessionFactory = sqlSessionFactoryBuilder.build(Re
sources.getResourceAsStream("mybatis-config4.xml"));
 SqlSession sqlSession = sqlSessionFactory.openSession();
 Object car = sqlSession.selectOne("selectCarByCarNum");
 System.out.println(car);
}
```

properties有两个属性：

resouce：这个属性从类的根路径下开始加载

url：从指定的url加载

## 3.5mapper

mapper标签用来是定SQL映射文件的路径，包含多种指定方式，其中两种为：

**第一种:**resource,从类的根路径下进行加载

```java
<mappers>
	<mapper resource="CarMapper.xml">
</mappers>
```

如果这样写必须保证类路径下必须有Carmapper.xml文件

如果类路径下有一个test包，CarMapper.xml在这个包下，配置文件应该这样写

```java
<mappers>
	<mapper="test/CarMapper.xml">
</mappers>
```

**第二种：**url，从指定的url位置进行加载

假设CarMapper.xml文件放在D盘的根目录下，配置写法如下

```java
<mappers>
	<mapper url="file:///d:/CarMapper.xml"
</mappers>
```

# 四，手写mybatis基本框架 



## 4.1dom4j解析xml文件

配置config.xml文件

```java
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
        <environment id="mybatisDB">
            <transactionManager type="JDBC"/>
            <dataSource type="POOLED">
                <property name="driver" value="com.mysql.cj.jdbc.Driver"/>
                <property name="url" value="jdbc:mysql://localhost:3306/mybatis"/>
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



解析config.xml

```java
public void testParseMybatisConfigXML() throws Exception{
        //获取SAXReader对象
        SAXReader saxReader = new SAXReader();
        //获取输入流
        InputStream is = ClassLoader.getSystemClassLoader().getResourceAsStream("mybatisconfig.xml");
        //读取XML文件，返回document对象，document是文档对象代表XML文件
        Document document = saxReader.read(is);
        //System.out.println(document);

        //获取文档中的根标签
        Element rootElt = document.getRootElement();
        String rootEltname = rootElt.getName();
        System.out.println(rootEltname);

        //获取enviroments标签的default属性
        //以下的Xpath代表：从根下查找configuration标签然后找configuration标签下的environment
        String Xpath = "/configuration/environments";
        Element enviromentsElt = (Element) document.selectSingleNode(Xpath);
        String defaultId = enviromentsElt.attributeValue("default");
        //System.out.println(defaultId);
        //获取enviroment标签
        Xpath = "/configuration/environments/environment[@id='"+ defaultId +"']";
        Element enviromentElt = (Element) document.selectSingleNode(Xpath);
        System.out.println(enviromentElt);
        //获取enviroment节点下的transactionManager节点(Element的element()方法用来获取子节点)
        Element transactionType = enviromentElt.element("transactionManager");
        Attribute transaction = transactionType.attribute("type");
        System.out.println(transaction);
        //获取datasource
        Element dataSource = enviromentElt.element("dataSource");
        Attribute type = dataSource.attribute("type");
        System.out.println(type);
        //获取datasource下的所有节点
        List<Element> propertyElts = dataSource.elements();
        propertyElts.forEach(propertyElt -> {
            Attribute name = propertyElt.attribute("name");
            Attribute value = propertyElt.attribute("value");
            System.out.println(name + "=" + value);
        });
        //获取所有的mapper标签
        //不想从根标签获取，想从任意位置获取，xpath写法如下
        Xpath = "//mapper";
        List<Node> mappers = document.selectNodes(Xpath);
        mappers.forEach(mapper -> {
            Element element = (Element) mapper;
            Attribute resource = element.attribute("resource");
            System.out.println(resource);
        });

    }
```

配置CarMapper.xml文件

```java
<?xml version="1.0" encoding="UTF-8" ?>
<mapper namespace="car">
 <insert id="insertCar">
 insert into t_car(id,car_num,brand,guide_price,produce_time,car_ty
pe) values(null,#{carNum},#{brand},#{guidePrice},#{produceTime},#{carTyp
e})
 </insert>
 <select id="selectCarByCarNum" resultType="com.powernode.mybatis.pojo.
Car">
 select id,car_num carNum,brand,guide_price guidePrice,produce_tim
e produceTime,car_type carType from t_car where car_num = #{carNum}
 </select>
</mapper>
```

解析CarMapper.xml文件

```java
public void testparseSqlMapperXML() throws Exception{
        SAXReader saxReader = new SAXReader();
        InputStream is = ClassLoader.getSystemClassLoader().getResourceAsStream("CarMapper.xml");
        Document document = saxReader.read(is);
        //获取namespace
        Element mapperElt = (Element) document.selectSingleNode("/mapper");
        String namespace = mapperElt.attributeValue("namespace");
        System.out.println(namespace);
        //获取SQL id
        mapperElt.elements().forEach(statementElt ->{
            //标签名
            String name = statementElt.getName();
            System.out.println(name);
            //如果是select标签，还要获取resultType
            String resultType = statementElt.attributeValue("resuletType");
            System.out.println(resultType);
            //sql id
            String id = statementElt.attributeValue("id");
            System.out.println(id);
            //sql 语句
            String sql = statementElt.getTextTrim();
            System.out.println(sql);
        });
    }
```

## 4.2GodBatis







