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



# 1.Mybatis入门程序

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

