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











































