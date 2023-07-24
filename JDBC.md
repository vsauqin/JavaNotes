JDBC:**JDBC的全称是Java数据库连接(Java Database connect)，它是一套用于执行SQL语句的Java API。应用程序可通过这套API连接到关系数据库，并使用SQL语句来完成对数据库中数据的查询、更新和删除等操作**

# 1.jdbc基本操作

## 1.1变成六步

```Java
package com.jdbc_;



import java.sql.*;


/**
 * @author 谢钦
 */
public class JDBCTest01 {
    public static void main(String[] args){
        Connection conn = null;
        Statement stmt = null;

        try {
            //注册驱动
            //Driver driver = new com.mysql.jdbc.Driver();
            //DriverManager.registerDriver(driver);
            //注册驱动的第二种方式,因为参数是一个字符串，可以写到配置文件中
            try {
                Class.forName("com.mysql.jdbc.Driver");
            } catch (ClassNotFoundException e) {
                e.printStackTrace();
            }
            //获取连接
            String url = "jdbc:mysql://localhost:3306/xq001";
            String user = "root";
            String password = "223515";
            conn = DriverManager.getConnection(url,user,password);
            System.out.println("数据库连接对象" + conn);
            //获取数据库操作对象
            stmt = conn.createStatement();
            //执行sql语句
            String sql = "insert into t17 values ( 4, 'x', 'xq@fsfs' )";
             int count = stmt.executeUpdate(sql);
             //返回数据库中的记录条数
            System.out.println(count == 1 ? "保存成功" : "保存失败");
        } catch (SQLException throwables) {
            throwables.printStackTrace();
        } finally{
            //释放资源，遵循从小到大依次关闭
            if (stmt != null){
                try {
                    stmt.close();
                } catch (SQLException throwables) {
                    throwables.printStackTrace();
                }
            }
            if (conn != null){
                try {
                    conn.close();
                } catch (SQLException throwables) {
                    throwables.printStackTrace();
                }
            }
        }
    }
}

```

## 1.2 从属性文件中读取连接数据库信息

```Java

```

# 2 SQL注入的根本原因

* 用户输入的信息中含有原来sql语句的关键字，并且这些关键字参与了sql语句的编译过程

导致sql语句的原意被扭曲

```java
import java.sql.*;
import java.util.HashMap;
import java.util.Map;
import java.util.Scanner;
import java.sql.PreparedStatement;

/**
 * @author 谢钦
 */
public class JDBCTest03 {
    public static void main(String[] args){
        //初始化一个界面
        Map<String,String> userLoginInfo = initUI();
        //验证用户名和密码
        boolean loginSuccess = login (userLoginInfo);
        System.out.println(loginSuccess ? "登陆成功" : "登陆失败");
    }
        /**
         * 用户登录
         * @ param userLoginInfo 用户登录信息成功
         * @return false表示失败，true表示成功
         * */
    private static boolean login(Map<String, String> userLoginInfo) {
        Connection conn = null;
        Statement stmt = null;
        ResultSet rs = null;
        boolean loginSuccess = false;
        try {
            //注册驱动
            Class.forName("com.mysql.jdbc.Driver");
            //获取连接
            String url = "jdbc:mysql://localhost:3306/xq001";
            String user = "root";
            String password = "223515";
            conn = DriverManager.getConnection(url,user,password);
            System.out.println("数据库连接对象" + conn);
            //获取操作对象
            stmt = conn.createStatement();
            //执行sql语句
            String sql = "select * from t_user where loginName = '"+
                    userLoginInfo.get("loginName")+"' and loginPwd = '"+ userLoginInfo.get("loginPwd") +"'";
            rs = stmt.executeQuery(sql);
            //处理结果集
            if (rs.next()){
                loginSuccess = true;
            }
        } catch (Exception e) {
            e.printStackTrace();
        }finally{
            if (rs != null){
                try {
                    rs.close();
                } catch (SQLException throwables) {
                    throwables.printStackTrace();
                }
            }
            if (stmt != null){
                try {
                    stmt.close();
                } catch (SQLException throwables) {
                    throwables.printStackTrace();
                }
            }
            if (conn != null){
                try {
                    conn.close();
                } catch (SQLException throwables) {
                    throwables.printStackTrace();
                }
            }
        }
        return loginSuccess;

    }

    /**
         * 初始化用户界面
         * @return用户输入的用户名和密码等登录信息
         * */
    private static Map<String,String> initUI() {
        Scanner scanner = new Scanner(System.in);
        System.out.println("用户名：");
        String loginName = scanner.nextLine();
        System.out.println("密码：");
        String loginPwd = scanner.nextLine();
        Map<String,String> userLogInfo = new HashMap<>();
        userLogInfo.put("loginName", loginName);
        userLogInfo.put("loginPwd", loginPwd);
        return userLogInfo;
    }
}
//未修改的代码，存在sql注入
```

## 2.1解决方法：

* 用户提供的信息不参与sql语句的编译
* 使用Java.sql.PreparedStatement
* PreparedStatement继承了java.sql.Statement
* PreparedStatement是预先编译的数据库操作对象，其原理是预先对sql语句的框架进行编译，再给sql语句传值

```java
package com;
import java.sql.*;
import java.util.HashMap;
import java.util.Map;
import java.util.Scanner;
import java.sql.PreparedStatement;
import java.util.StringJoiner;

/**
 * @author 谢钦
 */
public class JDBCTest03 {
    public static void main(String[] args){
        //初始化一个界面
        Map<String,String> userLoginInfo = initUI();
        //验证用户名和密码
        boolean loginSuccess = login (userLoginInfo);
        System.out.println(loginSuccess ? "登陆成功" : "登陆失败");
    }
        /**
         * 用户登录
         * @ param userLoginInfo 用户登录信息成功
         * @return false表示失败，true表示成功
         * */
    private static boolean login(Map<String, String> userLoginInfo) {
        Connection conn = null;
        PreparedStatement ps = null;
        ResultSet rs = null;
        String loginName = userLoginInfo.get("loginName");
        String loginPwd = userLoginInfo.get("loginPwd");
        boolean loginSuccess = false;
        try {
            //注册驱动
            Class.forName("com.mysql.jdbc.Driver");
            //获取连接
            String url = "jdbc:mysql://localhost:3306/xq001";
            String user = "root";
            String password = "223515";
            conn = DriverManager.getConnection(url,user,password);
            System.out.println("数据库连接对象" + conn);
            //获取预编译的数据库的操作对象
            String sql = "select * from t_user where loginName = ? and loginPwd = ?";//问号：占位符，一个问号接收一个值
            ps = conn.prepareStatement(sql);
            //给占位符传值（第一个问号是一，第二个是二）
            ps.setString(1, loginName);
            ps.setString(2, loginPwd);
            rs = ps.executeQuery();
            //处理结果集
            if (rs.next()){
                loginSuccess = true;
            }
        } catch (Exception e) {
            e.printStackTrace();
        }finally{
            if (rs != null){
                try {
                    rs.close();
                } catch (SQLException throwables) {
                    throwables.printStackTrace();
                }
            }
            if (ps != null){
                try {
                    ps.close();
                } catch (SQLException throwables) {
                    throwables.printStackTrace();
                }
            }
            if (conn != null){
                try {
                    conn.close();
                } catch (SQLException throwables) {
                    throwables.printStackTrace();
                }
            }
        }
        return loginSuccess;

    }

    /**
         * 初始化用户界面
         * @return用户输入的用户名和密码等登录信息
         * */
    private static Map<String,String> initUI() {
        Scanner scanner = new Scanner(System.in);
        System.out.println("用户名：");
        String loginName = scanner.nextLine();
        System.out.println("密码：");
        String loginPwd = scanner.nextLine();
        Map<String,String> userLogInfo = new HashMap<>();
        userLogInfo.put("loginName", loginName);
        userLogInfo.put("loginPwd", loginPwd);
        return userLogInfo;
    }
}

```

# 3.jdbc事务控制

* 三行代码：

  ```mysql
  conn.setAutoCommit(false);//开启事务，将自动提交机制关闭
  conn.commit();// 提交事务
  conn.rollback();//回滚事务
  
  
  
  
  
  
  ```

  
