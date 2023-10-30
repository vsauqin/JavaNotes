# 1.Java流程控制语句

# 2.Java字符串处理

# 3.Java数字和日期处理

# 4.Java内置包装类

## 4.1包装类，装箱和拆箱

 Java 为每种基本数据类型分别设计了对应的类，称之为包装类（Wrapper Classes），也有地方称为外覆类或数据类型类。

| 序号 | 基本数据类型 | 包装类    |
| ---- | ------------ | --------- |
| 1    | byte         | Byte      |
| 2    | short        | Short     |
| 3    | int          | Integer   |
| 4    | long         | Long      |
| 5    | char         | Character |
| 6    | float        | Float     |
| 7    | double       | Double    |
| 8    | boolean      | Boolean   |

### 装箱与拆箱

基本数据类型转换为包装类的过程称为装箱，例如把 int 包装成 Integer 类的对象；

包装类变为基本数据类型的过程称为拆箱，例如把 Integer 类的对象重新简化为 int。

手动实例化一个包装类称为手动拆箱装箱。Java 1.5 版本之前必须手动拆箱装箱，之后可以自动拆箱装箱，也就是在进行基本数据类型和对应的包装类转换时，系统将自动进行装箱及拆箱操作，不用在进行手工操作，为开发者提供了更多的方便。例如：

```java
public class Demo {
    public static void main(String[] args) {
        int m = 500;
        Integer obj = m;  // 自动装箱
        int n = obj;  // 自动拆箱
        System.out.println("n = " + n);
      
        Integer obj1 = 500;
        System.out.println("obj等价于obj1返回结果为" + obj.equals(obj1));
    }
}
```

运行结果：

```java
n = 500
obj等价于obj1返回结果为true
```

### 包装类的应用

**1）实现int和Integer的相互转换**

可以通过 Integer 类的构造方法将 int 装箱，通过 Integer 类的 intValue 方法将 Integer 拆箱。例如：

```java
public class Demo {
    public static void main(String[] args) {
        int m = 500;
        Integer obj = new Integer(m);  // 手动装箱
        int n = obj.intValue();  // 手动拆箱
        System.out.println("n = " + n);
       
        Integer obj1 = new Integer(500);
        System.out.println("obj等价于obj1的返回结果为" + obj.equals(obj1));
    }
}
```

运行结果：

```
n = 500
obj等价于obj1的返回结果为true
```

**2) 将字符串转换为数值类型**

在 Integer 和 Float 类中分别提供了以下两种方法：

① Integer 类（String 转 int 型）

```
int parseInt(String s);
```

s 为要转换的字符串。

② Float 类（String 转 float 型）

```
float parseFloat(String s)
```

注意：使用以上两种方法时，字符串中的数据必须由数字组成，否则转换时会出现程序错误。

下面为字符串转换为数值类型的例子：

```java
public class Demo {    
	public static void main(String[] args) {
    	String str1 = "30";        
    	String str2 = "30.3";       
        // 将字符串变为int型        
    	int x = Integer.parseInt(str1);        
        // 将字符串变为float型        
    	float f = Float.parseFloat(str2);        
    	System.out.println("x = " + x + "；f = " + f);   
        }
        }
```

运行结果：

```
x = 30；f = 30.3
```

**3）将整数转换为字符串**

Integer 类有一个静态的 toString() 方法，可以将整数转换为字符串。例如：

```java
public class Demo {    
public static void main(String[] args) {        
int m = 500;        
String s = Integer.toString(m);        
System.out.println("s = " + s);    
}
}
```

运行结果：

```
s = 500
```





## 4.2Object类详解

Object 是java类库中的一个特殊类，也是所有类的父类。也就是说，Java 允许把任何类型的对象赋给 Object 类型的变量。当一个类被定义后，如果没有指定继承的父类，那么默认父类就是 Object 类。因此：

```java
public class MyClass{…}
```

等价于

```java
public class MyClass extends Object {…}
```

由于 Java 所有的类都是 Object 类的子类，所以任何 Java 对象都可以调用 Object 类的方法。

常见方法如表所示：

| 方法                       | 说明                                                         |
| -------------------------- | ------------------------------------------------------------ |
| Object clone()             | 创建与该对象的类相同的新对象                                 |
| **boolean equals(Object)** | **比较两对象是否相等**                                       |
| void finalize()            | 当垃圾回收器确定不存在对该对象的更多引用时，对象垃圾回收器调用该方法 |
| **Class getClass()**       | **返回一个对象运行时的实例类**                               |
| int hashCode()             | 返回该对象的散列码值                                         |
| void notify()              | 激活等待在该对象的监视器上的一个线程                         |
| void notifyAll()           | 激活等待在该对象的监视器上的全部线程                         |
| **String toString()**      | **返回该对象的字符串表示**                                   |
| void wait()                | 在其他线程调用此对象的 notify() 方法或 notifyAll() 方法前，导致当前线程等待 |





**toString（）方法**





toString() 方法返回该对象的字符串，当程序输出一个对象或者把某个对象和字符串进行连接运算时，系统会自动调用该对象的 toString() 方法返回该对象的字符串表示。

Object 类的 toString() 方法返回“运行时类名@十六进制哈希码”格式的字符串，但很多类都重写了 Object 类的 toString() 方法，用于返回可以表述该对象信息的字符串。

> 哈希码（hashCode），每个 Java 对象都有哈希码属性，哈希码可以用来标识对象，提高对象在集合操作中的执行效率。

先看以下代码：

```java
// 定义Demo类，实际上继承Object类
class Demo {

}
public class ObjectDemo01 {    
public static void main(String[] args) {        
Demo d = new Demo(); 
// 实例化Demo对象        
System.out.println("不加toString()输出：" + d);        
System.out.println("加上toString()输出：" + d.toString());    
}
}
```

输出结果为：

```Java
不加toString()输出：Demo@15db9742
加上toString()输出：Demo@15db9742
```



以上的程序是随机输出了一些地址信息，从程序的运行结果可以清楚的发现，加和不加 toString() 的最终输出结果是一样的，也就是说对象输出时一定会调用 Object 类中的 toString() 方法打印内容。所以利用此特性就可以通过 toString() 取得一些对象的信息，如下面代码。

```java
public class Person {    
private String name;    
private int age;    
public Person(String name, int age) {        
this.name = name;        
this.age = age;    
}    
public String toString() {        
return "姓名：" + this.name + "：年龄" + this.age;    
}    
public static void main(String[] args) {       
Person per = new Person("谢钦", 30);
// 实例化Person对象        
System.out.println("对象信息：" + per);
// 打印对象调用toString()方法    
}
}
```



输出结果为：

```
对象信息：姓名：谢钦：年龄30
```

程序中的 Person 类中重写了 Object 类中的 toString() 方法，这样直接输出对象时调用的是被子类重写过的 toString() 方法。





**equal()方法**





`==`运算符是比较两个引用变量是否指向同一个实例，equals() 方法是比较两个对象的内容是否相等，通常字符串的比较只是关心内容是否相等。

其使用格式如下：

```
boolean result = obj.equals(Object o);
```

其中，obj 表示要进行比较的一个对象，o 表示另一个对象。





例一：

编写一个 Java 程序，实现用户登录的验证功能。要求用户从键盘输入登录用户名和密码，当用户输入的用户名等于 admin 并且密码也等于 admin 时，则表示该用户为合法用户，提示登录成功，否则提示用户名或者密码错误信息。

在这里使用 equals() 方法将用户输入的字符串与保存 admin 的字符串对象进行比较，具体的代码如下：

```java
import java.util.Scanner;
public class Test01 {
    // 验证用户名和密码
    public static boolean validateLogin(String uname, String upwd) {
        boolean con = false;
        if (uname.equals("admin") && upwd.equals("admin")) { // 比较两个 String 对象
            con = true;
        } else {
            con = false;
        }
        return con;
    }
    public static void main(String[] args) {
        Scanner input = new Scanner(System.in);
        System.out.println("------欢迎使用大数据管理平台------");
        System.out.println("用户名：");
        String username = input.next(); // 获取用户输入的用户名
        System.out.println("密码：");
        String pwd = input.next(); // 获取用户输入的密码
        boolean con = validateLogin(username, pwd);
        if (con) {
            System.out.println("登录成功！");
        } else {
            System.out.println("用户名或密码有误！");
        }
    }
}
```

上述代码在 validateLogin() 方法中又使用 equals() 方法将两个 String 类型的对象进行了比较，当 uname 对象与保存 admin 的 String 对象相同时，uname.equals("admin") 为 true；与此相同，当 upwd 对象与保存 admin 的 String 对象相同时，upwd.equals("admin") 为 true。当用户输入的用户名和密码都为 admin 时，表示该用户为合法用户，提示登录成功信息，否则提示用户名或密码有误的错误信息。

该程序的运行结果下所示：

```java
------欢迎使用大数据管理平台------
用户名：
adinm
密码：
admin
用户名或密码有误！
```

```java
------欢迎使用大数据管理平台------
用户名：
admin
密码：
admin
登录成功！
```





**getClass方法**





*getClass() 方法返回对象所属的类，是一个 Class 对象。*通过 Class 对象可以获取该类的各种信息，包括类名、父类以及它所实现接口的名字等。

#### 例 2

编写一个实例，演示如何对 String 类型调用 getClass() 方法，然后输出其父类及实现的接口信息。具体实现代码如下：

```java
public class Test02 {
    public static void printClassInfo(Object obj) {
        // 获取类名
        System.out.println("类名：" + obj.getClass().getName());
        // 获取父类名
        System.out.println("父类：" + obj.getClass().getSuperclass().getName());
        System.out.println("实现的接口有：");
        // 获取实现的接口并输出
        for (int i = 0; i < obj.getClass().getInterfaces().length; i++) {
            System.out.println(obj.getClass().getInterfaces()[i]);
        }
    }
    public static void main(String[] args) {
        String strObj = new String();
        printClassInfo(strObj);
    }
}
```

程序运行结果如下：

```java
类名：java.lang.String
父类：java.lang.Object
实现的接口有：
interface java.io.Serializable
interface java.lang.Comparable
interface java.lang.CharSequence
```





**接受任意引用类型的对象**



既然Object类是所有对象的父类，则所有的对象都可以向Object进行转换，在这其中也包含了数组和接口类型，即一切的引用数据类型都可以使用Object进行接收

```java
interface A {
    public String getInfo();
}
class B implements A {
    public String getInfo() {
        return "Hello World!!!";
    }
}
public class ObjectDemo04 {
    public static void main(String[] args) {
        // 为接口实例化
        A a = new B();
        // 对象向上转型
        Object obj = a;
        // 对象向下转型
        A x = (A) obj;
        System.out.println(x.getInfo());
    }
}
```

输出结果是：

```Java
Hello World！！！
```

通过以上代码可以发现，虽然接口不能继承一个类，但是依然是 Object 类的子类，因为接口本身是引用数据类型，所以可以进行向上转型操作。

同理，也可以使用 Object 接收一个数组，因为数组本身也是引用数据类型。

```java
public class ObjectDemo05 {
    public static void main(String[] args) {
        int temp[] = { 1, 3, 5, 7, 9 };
        // 使用object接收数组
        Object obj = temp;
        // 传递数组引用
        print(obj);
    }
    public static void print(Object o) {
        // 判断对象的类型
        if (o instanceof int[]) {
            // 向下转型
            int x[] = (int[]) o;
            // 循环输出
            for (int i = 0; i < x.length; i++) {
                System.out.print(x[i] + "\t");
            }
        }
    }
}
```

输出结果为：

```java
1 3 5 7 9 
```

以上程序使用Object接收一个整型数组，因为数组本身属于引用数据类型，所以可以使用Object接收数组内容，在输出时通过instanceof判断类型是否是一个整型数组，然后进行输出操作

## 4.3Integer类

### **Integer类的构造方法**

Integer类中的构造方法有两个

1. Integer(int value)：构造一个新分配的 Integer 对象，它表示指定的 int 值。
2. Integer(String s)：构造一个新分配的 Integer 对象，它表示 String 参数所指示的 int 值

例如，以下代码分别使用以上两个构造方法来获取 Integer 对象：

```java
Integer integer1 = new Integer(100);    // 以 int 型变量作为参数创建 Integer 对象
Integer integer2 = new Integer("100");    // 以 String 型变量作为参数创建 Integer 对象
```

### **Integer类的常用方法**

在Integer类内部包含一些和int类型操作有关的方法，如表1

| 方法                              | 返回值  | 功能                                                         |
| --------------------------------- | ------- | ------------------------------------------------------------ |
| byteValue()                       | byte    | 以 byte 类型返回该 Integer 的值                              |
| shortValue()                      | short   | 以 short 类型返回该 Integer 的值                             |
| intValue()                        | int     | 以 int 类型返回该 Integer 的值                               |
| toString()                        | String  | 返回一个表示该 Integer 值的 String 对象                      |
| equals(Object obj)                | boolean | 比较此对象与指定对象是否相等                                 |
| compareTo(Integer anotherlnteger) | int     | 在数字上比较两个 Integer 对象，如相等，则返回 0； 如调用对象的数值小于 anotherlnteger 的数值，则返回负值； 如调用对象的数值大于 anotherlnteger 的数值，则返回正值 |
| valueOf(String s)                 | Integer | 返回保存指定的 String 值的 Integer 对象                      |
| parseInt(String s)                | int     | 将数字字符串转换为 int 数值                                  |

*在实际编程中，经常将字符串转换为int类型的数值，或将int类型的数值转换为对应的字符串*，以下代码演示如何实现这两种功能：

```java
String str = "456";
int num = Integer.parseInt(str);    // 将字符串转换为int类型的数值
int i = 789;
String s = Integer.toString(i);    // 将int类型的数值转换为字符串
```

*注意：在实现将字符串转换为 int 类型数值的过程中，如果字符串中包含非数值类型的字符，则程序执行将出现异常。*

例一：

编写一个程序，在程序中创建一个String类型的变量，然后将他转化为二进制，八进制，十进制，十六进制输出

```java
public class Test03 {
    public static void main(String[] args) {
        int num = 40;
        String str = Integer.toString(num); // 将数字转换成字符串
        String str1 = Integer.toBinaryString(num); // 将数字转换成二进制
        String str2 = Integer.toHexString(num); // 将数字转换成八进制
        String str3 = Integer.toOctalString(num); // 将数字转换成十六进制
        System.out.println(str + "的二进制数是：" + str1);
        System.out.println(str + "的八进制数是：" + str3);
        System.out.println(str + "的十进制数是：" + str);
        System.out.println(str + "的十六进制数是：" + str2);
    }
}
```

输出结果如下：

```java
40的二进制数是：101000
40的八进制数是：50
40的十进制数是：40
40的十六进制数是：28
```

### Integer类的常量

Integer 类包含以下 4 个常量。

- MAX_VALUE：值为 231-1 的常量，它表示 int 类型能够表示的最大值。
- MIN_VALUE：值为 -231 的常量，它表示 int 类型能够表示的最小值。
- SIZE：用来以二进制补码形式表示 int 值的比特位数。
- TYPE：表示基本类型 int 的 Class 实例。

下面用一段代码演示Integer类中常量的使用

```java
int max_value = Integer.MAX_VALUE;//获取int类型的最大值
int min_value = Integer.MIN_VALUE;//获取int可取的最小值
int size = Integer.SIZE;//获取int的二进制位
Class c = Integer.TYPE;//获取基本数据类型int的Class实例
```

## 4.4Float类

Float 类在对象中包装了一个基本类型 float 的值。Float 类对象包含一个 float 类型的字段。此外，该类提供了多个方法，能在 float 类型与 String 类型之间互相转换，同时还提供了处理 float 类型时比较常用的常量和方法。

### Float类的构造方法

Float类中的构造方法有以下三个

- Float(double value)：构造一个新分配的 Float 对象，它表示转换为 float 类型的参数。
- Float(float value)：构造一个新分配的 Float 对象，它表示基本的 float 参数。
- Float(String s)：构造一个新分配的 Float 对象，它表示 String 参数所指示的 float 值。

代码演示：

```java
Float float1 = new Float(3.14145);    // 以 double 类型的变量作为参数创建 Float 对象
Float float2 = new Float(6.5);    // 以 float 类型的变量作为参数创建 Float 对象
Float float3 = new Float("3.1415");    // 以 String 类型的变量作为参数创建 Float 对象
```



在Float类内部还包含了一些和float操作有关的方法如表所示

| 方法                 | 返回值  | 功能                                                       |
| -------------------- | ------- | ---------------------------------------------------------- |
| byteValue()          | byte    | 以 byte 类型返回该 Float 的值                              |
| doubleValue()        | double  | 以 double 类型返回该 Float 的值                            |
| floatValue()         | float   | 以 float 类型返回该 Float 的值                             |
| intValue()           | int     | 以 int 类型返回该 Float 的值（强制转换为 int 类型）        |
| longValue()          | long    | 以 long 类型返回该 Float 的值（强制转换为 long 类型）      |
| shortValue()         | short   | 以 short 类型返回该 Float 的值（强制转换为 short 类型）    |
| isNaN()              | boolean | 如果此 Float 值是一个非数字值，则返回 true，否则返回 false |
| isNaN(float v)       | boolean | 如果指定的参数是一个非数字值，则返回 true，否则返回 false  |
| toString()           | String  | 返回一个表示该 Float 值的 String 对象                      |
| valueOf(String s)    | Float   | 返回保存指定的 String 值的 Float 对象                      |
| parseFloat(String s) | float   | 将数字字符串转换为 float 数值                              |

例如，将字符串 456.7 转换为 float 类型的数值，或者将 float 类型的数值 123.4 转换为对应的字符串，以下代码演示如何实现这两种功能：

```java
String str = "456.7";
float num = Float.parseFloat(str);    // 将字符串转换为 float 类型的数值
float f = 123.4f;
String s = Float.toString(f);    // 将 float 类型的数值转换为字符串
```

注意：在实现将字符串转换为float类型数值的过程中，如果字符串中包含非数值类型的字符，则程序执行异常

### Float类的常用常量

在Float类中包含了很多常量，其中常用的常量如下：

- MAX_VALUE：值为 1.4E38 的常量，它表示 float 类型能够表示的最大值。
- MIN_VALUE：值为 3.4E-45 的常量，它表示 float 类型能够表示的最小值。
- MAX_EXPONENT:有限 float 变量可能具有的最大指数。
- MIN_EXPONENT：标准化 float 变量可能具有的最小指数。
- MIN_NORMAL：保存 float 类型数值的最小标准值的常量，即 2-126。
- NaN：保存 float 类型的非数字值的常量。
- SIZE：用来以二进制补码形式表示 float 值的比特位数。
- TYPE：表示基本类型 float 的 Class 实例。

下面的代码演示了Float类中常量的使用：

```java
float max_value = Float.MAX_VALUE;    // 获取 float 类型可取的最大值
float min_value = Float.MIN_VALUE;    // 获取 float 类型可取的最小值
float min_normal = Float.MIN_NORMAL;    // 获取 float 类型可取的最小标准值
float size = Float.SIZE;    // 获取 float 类型的二进制位
```



## 4.5Double类

Double 类在对象中包装了一个基本类型 double 的值。Double 类对象包含一个 double 类型的字段。此外，该类还提供了多个方法，可以将 double 类型与 String 类型相互转换，同时 还提供了处理 double 类型时比较常用的常量和方法。

### Double类的构造方法

Double类中的构造方法有如下两个：

- Double(double value)：构造一个新分配的 Double 对象，它表示转换为 double 类型的参数。
- Double(String s)：构造一个新分配的 Double 对象，它表示 String 参数所指示的 double 值。

例如，以下代码分别使用以上两个构造方法获取 Double 对象：

```java
Double double1 = new Double(5.456);    // 以 double 类型的变量作为参数创建 Double 对象
Double double2 = new Double("5.456");       // 以 String 类型的变量作为参数创建 Double 对象
```

### Double类的常用方法

在Double类内部包含一些和double操作有关的方法，见表一

| 方法                  | 返回值  | 功能                                                        |
| --------------------- | ------- | ----------------------------------------------------------- |
| byteValue()           | byte    | 以 byte 类型返回该 Double 的值                              |
| doubleValue()         | double  | 以 double 类型返回该 Double 的值                            |
| fioatValue()          | float   | 以 float 类型返回该 Double 的值                             |
| intValue()            | int     | 以 int 类型返回该 Double 的值（强制转换为 int 类型）        |
| longValue()           | long    | 以 long 类型返回该 Double 的值（强制转换为 long 类型）      |
| shortValue()          | short   | 以 short 类型返回该 Double 的值（强制转换为 short 类型）    |
| isNaN()               | boolean | 如果此 Double 值是一个非数字值，则返回 true，否则返回 false |
| isNaN(double v)       | boolean | 如果指定的参数是一个非数字值，则返回 true，否则返回 false   |
| toString()            | String  | 返回一个表示该 Double 值的 String 对象                      |
| valueOf(String s)     | Double  | 返回保存指定的 String 值的 Double 对象                      |
| parseDouble(String s) | double  | 将数字字符串转换为 Double 数值                              |

例如，将字符串 56.7809 转换为 double 类型的数值，或者将 double 类型的数值 56.7809 转换为对应的字符串，以下代码演示如何实现这两种功能：

```java
String str = "56.7809";double num = Double.parseDouble(str);    // 将字符串转换为 double 类型的数值double d = 56.7809;String s = Double.toString(d);    // 将double类型的数值转换为字符串
```

在将字符串转换为 double 类型的数值的过程中，如果字符串中包含非数值类型的字符，则程序执行将出现异常。

### Double类的常用常量

在Double类中包含了很多的常量，其中较为常用的常量如下：

- MAX_VALUE:值为 1.8E308 的常量，它表示 double 类型的最大正有限值的常量。
- MIN_VALUE：值为 4.9E-324 的常量，它表示 double 类型数据能够保持的最小正非零值的常量。
- NaN：保存 double 类型的非数字值的常量。
- NEGATIVE_INFINITY：保持 double 类型的负无穷大的常量。
- POSITIVE_INFINITY：保持 double 类型的正无穷大的常量。
- SIZE：用来以二进制补码形式表示 double 值的比特位数。
- TYPE：表示基本类型 double 的 Class 实例。



## 4.6Number类

Number类是一个抽象类，也是一个超类，即父类。该类属于Java.lang包，所有的包装类(如 Double、Float、Byte、Short、Integer 以及 Long）都是抽象类Number的子类

Number 类定义了一些抽象方法，以各种不同数字格式返回对象的值。如 xxxValue() 方法，它将 Number 对象转换为 xxx 数据类型的值并返回。方法如下表

| 方法                  | 说明                 |
| --------------------- | -------------------- |
| byte byteValue();     | 返回 byte 类型的值   |
| double doubleValue(); | 返回 double 类型的值 |
| float floatValue();   | 返回 float 类型的值  |
| int intValue();       | 返回 int 类型的值    |
| long longValue();     | 返回 long 类型的值   |
| short shortValue();   | 返回 short 类型的值  |

*抽象类不能直接实例化，而是必须实例化其具体的子类*如下代码演示了Number类的使用

```java
Number num = new Double(12.5);
System.out.println("返回 double 类型的值：" + num.doubleValue());
System.out.println("返回 int 类型的值：" + num.intValue());
System.out.println("返回 float 类型的值：" + num.floatValue());
```

执行上述代码，输出结果如下：

```java
返回 double 类型的值：12.5
返回 int 类型的值：12
返回 float 类型的值：12.5
```



## 4.7Character类

Character 类是字符数据类型 char 的包装类。Character 类的对象包含类型为 char 的单个字段，这样能把基本数据类型当对象来处理，其常用方法见下表

| 方法                                       | 描述                                                         |
| ------------------------------------------ | ------------------------------------------------------------ |
| void Character(char value)                 | 构造一个新分配的 Character 对象，用以表示指定的 char 值      |
| char charValue()                           | 返回此 Character 对象的值，此对象表示基本 char 值            |
| int compareTo(Character anotherCharacter)  | 根据数字比较两个 Character 对象                              |
| boolean equals(Character anotherCharacter) | 将此对象与指定对象比较，当且仅当参数不是 null，而 是一个与此对象 包含相同 char 值的 Character 对象时， 结果才是 true |
| boolean isDigit(char ch)                   | 确定指定字符是否为数字，如果通过 Character. getType(ch) 提供的字 符的常规类别类型为 DECIMAL_DIGIT_NUMBER，则字符为数字 |
| boolean isLetter(int codePoint)            | 确定指定字符（Unicode 代码点）是否为字母                     |
| boolean isLetterOrDigit(int codePoint)     | 确定指定字符（Unicode 代码点）是否为字母或数字               |
| boolean isLowerCase(char ch)               | 确定指定字符是否为小写字母                                   |
| boolean isUpperCase(char ch)               | 确定指定字符是否为大写字母                                   |
| char toLowerCase(char ch)                  | 使用来自 UnicodeData 文件的大小写映射信息将字符参数转换为小写 |
| char toUpperCase(char ch)                  | 使用来自 UnicodeData 文件的大小写映射信息将字符参数转换为大写 |

可以从char值中创建一个Character对象，例如：

```java
Character character = new Character('S');
```

CompareTo()方法将这个字符与其他字符比较，并且返回一个整型数组，这个至三十两个字符比较后的标准代码的差值，当且仅当两个字符相同时，方法才会返回true，如下代码：

```java
Character character = new Character('A');
int result1 = character.compareTo(new Character('V'));
System.out.println(result1);    // 输出：0
int result2 = character.compareTo(new Character('B'));
System.out.println(resuit2);    // 输出：-1
int result3 = character.compareTo(new Character('1'));
System.out.println(result3);    // 输出：-2
```

例一：

在注册会员时，需要验证用户输入的用户名、密码、性别、年龄和邮箱地址等信息是否符合标准，如果符合标准方可进行注册。那么，下面就使用 Character 类中的一些静态方法来完成这个程序，具体的实现步骤如下。

1）创建 Register 类，在该类中创建 validateUser() 方法，对用户输入的用户名、密码和年龄进行验证，代码如下：

```java
public class Register {
    public static boolean validateUser(String uname,String upwd,String age) {
        boolean conUname = false;       // 用户名是否符合要求
        boolean conPwd = false;    // 密码是否符合要求
        boolean conAge = false;    // 年龄是否符合要求
        boolean con = false;    // 验证是否通过
        if (uname.length() > 0) {
            for (int i = 0;i < uname.length();i++) {
                // 验证用户名是否全部为字母，不能含有空格
                if (Character.isLetter(uname.charAt(i))) {
                    conUname = true;
                } else {
                    conUname = false;
                    System.out.println("用户名只能由字母组成，且不能含有空格！");
                    break;
                }
            }
        } else {
            System.out.println("用户名不能为空！");
        }
        if (upwd.length() > 0) {
            for (int j=0;j<upwd.length();j++) {
                // 验证密码是否由数字和字母组成，不能含有空格
                if (Character.isLetterOrDigit(upwd.charAt(j))) {
                    conPwd = true;
                } else {
                    conPwd = false;
                    System.out.println("密码只能由数字或字母组成！");
                    break;
                }
            }
        } else {
            System.out.println("密码不能为空！");
        }
        if (age.length() > 0) {
            for (int k = 0;k < age.length();k++) {
                // 验证年龄是否由数字组成
                if (Character.isDigit(age.charAt(k))) {
                    conAge = true;
                } else {
                    conAge = false;
                    System.out.println("年龄输入有误!");
                    break;
                }
            }
        } else {
            System.out.println("年龄必须输入！");
        }
        if (conUname && conPwd && conAge) {
            con = true;
        } else {
            con = false;
        }
        return con;
    }
}
```

在 validateUser() 方法中，使用 for 循环遍历用户输入的用户名、密码和年龄，对其每个字符进行验证，判断其是否符合要求。在验证的过程中，分别使用了 Character 类的 isLetter() 方法、isLetterOrDigit() 方法和 isDigit() 方法。

2）编写测试类 Test04，调用 Register 类中的 validateUser() 方法，对用户输入的数据进行验证，并输出验证结果，代码如下：

```java
import java.util.Scanner;
public class Test04 {
    public static void main(String[] args) {
        Scanner input = new Scanner(System.in);
        System.out.println("------------用户注册--------------");
        System.out.println("用户名：");
        String username = input.next();
        System.out.println("密码：");
        String pwd = input.next();
        System.out.println("年龄：");
        String age = input.next();
        boolean con = Register.validateUser(username,pwd,age);
        if (con) {
            System.out.println("注册成功！");
        } else {
            System.out.println("注册失败！");
        }
    }
}
```

## 4.8Boolean类

Boolean 类将基本类型为 boolean 的值包装在一个对象中。一个 Boolean 类的对象只包含一个类型为 boolean 的字段。此外，此类还为 boolean 和 String 的相互转换提供了很多方法，并提供了处理 boolean 时非常有用的其他一些常用方法。

### Boolean类的构造方法

Boolean类有以下两种构造形式

```Java
Boolean(boolean boolValue);
Boolean(String boolString);
```

其中 boolValue 必须是 true 或 false（不区分大小写），boolString 包含字符串 true（不区分大小写），那么新的 Boolean 对象将包含 true；否则将包含 false。

### Boolean类的常用方法

| 方法                   | 返回值  | 功能                                                         |
| ---------------------- | ------- | ------------------------------------------------------------ |
| booleanValue()         | boolean | 将 Boolean 对象的值以对应的 boolean 值返回                   |
| equals(Object obj)     | boolean | 判断调用该方法的对象与 obj 是否相等。当且仅当参数不是 null，且与调用该 方法的对象一样都表示同一个 boolean 值的 Boolean 对象时，才返回 true |
| parseBoolean(String s) | boolean | 将字符串参数解析为 boolean 值                                |
| toString()             | string  | 返回表示该 boolean 值的 String 对象                          |
| valueOf(String s)      | boolean | 返回一个用指定的字符串表示的 boolean 值                      |

例一：

编写一个java程序，演示如何使用不同的构造方法创建Boolean对象，并调用booleanValue（）方法将创建的对象重新转换为boolean数据输出，代码如下

```java
public class Test05 {
    public static void main(String[] args) {
        Boolean b1 = new Boolean(true);
        Boolean b2 = new Boolean("ok");
        Boolean b3 = new Boolean("true");
        System.out.println("b1 转换为 boolean 值是：" + b1);
        System.out.println("b2 转换为 boolean 值是：" + b2);
        System.out.println("b3 转换为 boolean 值是：" + b3);
    }
}
```

运行后的输出结果如下：

```java
b1 转换为 boolean 值是：true
b2 转换为 boolean 值是：false
b3 转换为 boolean 值是：true
```

### Boolean类的常量

在Boolean类中包含了很多常量，其中较为常用的常量如下：

- TRUE：对应基值 true 的 Boolean 对象。
- FALSE：对应基值 false 的 Boolean 对象。
- TYPE：表示基本类型 boolean 的 Class 对象。



## 4.9Byte类

Byte 类将基本类型为 byte 的值包装在一个对象中。一个 Byte 类的对象只包含一个类型为 byte 的字段。此外，该类还为 byte 和 String 的相互转换提供了方法，并提供了一些处理 byte 时非常有用的常量和方法。

### Byte类的构造方法

Byte 类提供了两个构造方法来创建 Byte 对象。

**1. Byte(byte value)**

通过这种方法创建的 Byte 对象，可以表示指定的 byte 值。例如，下面的示例将 5 作为 byte 类型变量，然后再创建 Byte 对象。

```java
byte my_byte = 5;
Byte b = new Byte(my_byte);
```

**2. Byte(String s)**

通过这个方法创建的 Byte 对象，可表示 String 参数所指定的 byte 值。例如，下面的示例将 5 作为 String 类型变量，然后再创建 Byte 对象。

```java

String my_byte = "5";
Byte b = new Byte(my_byte);
```

注意：必须使用数值型的 String 变量作为参数才能创建成功，否则会抛出 NumberFormatException 异常

### Byte类的常用方法

在Byte类内部包含了一些方法如下表：

| 方法                  | 返回值  | 功能                                                         |
| --------------------- | ------- | ------------------------------------------------------------ |
| byteValue()           | byte    | 以一个 byte 值返回 Byte 对象                                 |
| compareTo(Byte bytel) | int     | 在数字上比较两个 Byte 对象                                   |
| doubleValue()         | double  | 以一个 double 值返回此 Byte 的值                             |
| intValue()            | int     | 以一个 int 值返回此 Byte 的值                                |
| parseByte(String s)   | byte    | 将 String 型参数解析成等价的 byte 形式                       |
| toStringO             | String  | 返回表示此 byte 值的 String 对象                             |
| valueOf(String s)     | Byte    | 返回一个保持指定 String 所给出的值的 Byte 对象               |
| equals(Object obj)    | boolean | 将此对象与指定对象比较，如果调用该方法的对象与 obj 相等 则返回 true，否则返回 false |

### Byte类常用的常用常量

在 Byte 类中包含了很多的常量，其中较为常用的常量如下。

- MIN_VALUE：byte 类可取的最小值。
- MAX_VALUE：byte 类可取的最大值。
- SIZE：用于以二进制补码形式表示的 byte 值的位数。
- TYPE：表示基本类 byte 的 Class 实例。



## 4.10System类

System类位于java.long 包，代表当前java程序运行的平台，系统级的很多属性和控制方法都放置在该类的内部，由于该类的构造方法时private的，所以无法创建该类的对象，也就是无法实例化该类

System类提供了一些变量和类方法，允许直接通过System类来调用这些类变量和类方法

### System类的成员变量

System类有三个静态成员变量，分别是PrintStream out、InputStream in 和 PrintStream err。



**1. PrintStream out**



标准输出流。此流已打开并准备接收输出数据。通常，此流对应于显示器输出或者由主机环境或用户指定的另一个输出目标。

例如，编写一行输出数据的典型方式是：

```
System.out.println(data);
```

其中，println 方法是属于流类 PrintStream 的方法，而不是 System 中的方法。



**2. InputStream in**



标准输入流。此流已打开并准备提供输入数据。通常，此流对应于键盘输入或者由主机环境或用户指定的另一个输入源。



**3. PrintStream err**



标准的错误输出流。其语法与 System.out 类似，不需要提供参数就可输出错误信息。也可以用来输出用户指定的其他信息，包括变量的值。

例一：编写一个Java程序，

```java
import java.io.IOException;
public class Test06 {
    public static void main(String[] args) {
        System.out.println("请输入字符，按回车键结束输入:");
        int c;
        try {
            c = System.in.read();    // 读取输入的字符
            while(c != '\r') {    // 判断输入的字符是不是回车
                System.out.print((char) c);    // 输出字符
                c = System.in.read();
            }
        } catch(IOException e) {
            System.out.println(e.toString());
        } finally {
            System.err.println();
        }
    }
}
```

以上代码中，System.in.read() 语句读入一个字符，read() 方法是 InputStream 类拥有的方法。变量 c 必须用 int 类型而不能用 char 类型，否则会因为丢失精度而导致编译失败。

以上的程序如果输入汉字将不能正常输出。如果要正常输出汉字，需要把 System.in 声明为 InputStreamReader 类型的实例，最终在 try 语句块中的代码为：

```java
InputStreamReader in = new InputStreamReader(System.in, "GB2312");
c = in.read();
while(c != '\r') {
    System.out.print((char) c);
    c = in.read();
}
```

上述代码所示，语句 InputStreamReader in=new InputStreamReader(System.in,"GB2312") 声明一个新对象 in，它从 Reader 继承而来，此时就可以读入完整的 Unicode 码，显示正常的汉字

### System类的成员方法

System 类中提供了一些系统级的操作方法，常用的方法有 arraycopy()、currentTimeMillis()、exit()、gc() 和 getProperty()。

**1.arraycopy()方法**

该方法是数组复制，即从指定源数组中复制一个数组，从指定的位置开始，到数组的指定位置结束，该方法具体定义如下：

```java
public static void arraycopy(Object src,Object dest,int destPos,int length)
```

其中，src 表示源数组，srcPos 表示从源数组中复制的起始位置，dest 表示目标数组，destPos 表示要复制到的目标数组的起始位置，length 表示复制的个数。

例二：演示arraycopy()方法使用：

```java
public class System_arrayCopy {
    public static void main(String[] args) {
        char[] srcArray = {'A','B','C','D'};
        char[] destArray = {'E','F','G','H'};
        System.arraycopy(srcArray,1,destArray,1,2);
        System.out.println("源数组：");
        for(int i = 0;i < srcArray.length;i++) {
            System.out.println(srcArray[i]);
        }
        System.out.println("目标数组：");
        for(int j = 0;j < destArray.length;j++) {
            System.out.println(destArray[j]);
        }
    }
}
```

如上述代码，将数组 srcArray 中，从下标 1 开始的数据复制到数组 destArray 从下标 1 开始的位置，总共复制两个。也就是将 srcArray[1] 复制给 destArray[1]，将 srcArray[2] 复制给 destArray[2]。这样经过复制之后，数组 srcArray 中的元素不发生变化，而数组 destArray 中的元素将变为 E、B、C、 H，下面为输出结果：

```java
源数组：
A
B
C
D
目标数组：
E
B
C
H
```

**2.currentTimeMillis()方法**

该方法作用是返回当前的计算机时间，时间的格式为当前计算机时间与 GMT 时间（格林尼治时间）1970 年 1 月 1 日 0 时 0 分 0 秒所差的毫秒数。一般用它来测试程序的执行时间。例如：

```java
long m = System.currentTimeMillis();
```

例三：

使用该方法显示时间不直观，但是可以很方便的计算例如下面这段代码：

```java
public class System_currentTimeMillis {
    public static void main(String[] args) {
        long start = System.currentTimeMillis();
        for(int i = 0;i < 100000000;i++) {
            int temp = 0;
        }
        long end = System.currentTimeMillis();
        long time = end - start;
        System.out.println("程序执行时间" + time + "秒");
    }
}
```

上述代码中的变量 time 的值表示代码中 for 循环执行所需要的毫秒数，使用这种方法可以测试不同算法的程序的执行效率高低，也可以用于后期线程控制时的精确延时实现。

**3.exit()方法**

该方法是终止当前运行的虚拟机，具体格式如下：

```java
public static void exit(int status)
```



status的值为零时是正常退出，非零时表示异常退出

**4.gc()方法**

该方法的作用是请求系统进行垃圾回收，完成内存中的垃圾清除。至于系统是否立刻回收，取决于系统中垃圾回收算法的实现以及系统执行时的情况。定义如下：

```java
public static void gc()
```

**5.getProperty()方法**

该方法的作用是获得系统中属性名为key的属性对应的值，具体定义如下：

```java
public static String getProperty(String key)
```

系统中常见的属性名以及属性的说明如表 1 所示。

| 属性名       | 属性说明            |
| ------------ | ------------------- |
| java.version | Java 运行时环境版本 |
| java.home    | Java 安装目录       |
| os.name      | 操作系统的名称      |
| os.version   | 操作系统的版本      |
| user.name    | 用户的账户名称      |
| user.home    | 用户的主目录        |
| user.dir     | 用户的当前工作目录  |

例 4

下面的示例演示了 getProperty() 方法的使用。

```java
public class System_getProperty {
    public static void main(String[] args) {
        String jversion = System.getProperty("java.version");
        String oName = System.getProperty("os.name");
        String user = System.getProperty("user.name");
        System.out.println("Java 运行时环境版本："+jversion);
        System.out.println("当前操作系统是："+oName);
        System.out.println("当前用户是："+user);
    }
}
```



运行该程序，输出的结果如下：

```java

Java 运行时环境版本：1.6.0_26
当前操作系统是：Windows 7
当前用户是：Administrator
```

提示：使用 getProperty() 方法可以获得很多系统级的参数以及对应的值。

# 5.Java数组处理

## 5.1数组的简介

**数组（array）是一种最简单的复合数据类型，它是有序数据的集合，数组中的每个元素具有相同的数据类型，可以用一个统一的数组名和不同的下标来确定数组中唯一的元素。根据数组的维度，可以将其分为一维数组、二维数组和多维数组等。**



在计算机语言中数组是非常重要的集合类型，大部分计算机语言中数组具有如下三个基本特性：

1.  一致性：数组只能保存相同数据类型元素，元素的数据类型可以是任何相同的数据类型。
2. 有序性：数组中的元素是有序的，通过下标访问。
3. 不可变性：数组一旦初始化，则长度（数组中元素的个数）不可变。



总的来说，数组具有以下特点：

- 数组可以是一维数组、二维数组或多维数组。
- 数值数组元素的默认值为 0，而引用元素的默认值为 null。
- 数组的索引从 0 开始，如果数组有 n 个元素，那么数组的索引是从 0 到（n-1）。
- 数组元素可以是任何类型，包括数组类型。
- 数组类型是从抽象基类 Array 派生的引用类型。

## 5.2一维数组

### 创建一维数组

两种语法：

```java
type[] arrayName;
```

或者

```java
type arrayName[];
```

推荐第一种声明方式因为第二种阅读体验差

数组名可以是任意合法的变量名。例如

```java
int[] acore;//存储学生的成绩，类型为整形
double[] price;//存储商品的价格，类型为浮点型
String[] name;//存储商品名称，类型为字符串型
```

在声明数组时不需要规定数组的长度，例如：

```java
int score[10];    // 这是错误的
```

### 分配空间

声明了数组，只是得到了一个存放数组的变量，并没有为数组元素分配内存空间，不能使用。因此要为数组分配内存空间，这样数组的每一个元素才有一个空间进行存储。

简单地说，分配空间就是要告诉计算机在内存中为它分配几个连续的位置来存储数据。在 Java 中可以使用 new 关键字来给数组分配空间。分配空间的语法格式如下：

```java
arrayName = new type[size];    // 数组名 = new 数据类型[数组长度];
```

其中，数组长度就是数组中能存放的元素个数，显然应该为大于 0 的整数，例如：

```java
score = new int[10];price = new double[30];name = new String[20];
```

这里的 score 是已经声明过的 int[] 类型的变量，当然也可以在声明数组时就给它分配空间，语法格式如下：

```java
type[] arrayName = new type[size];    // 数据类型[] 数组名 = new 数据类型[数组长度];
```

**例一**：声明并分配一个长度为五的int类型数组arr

```java
int[] arr = new int[5];
```

注意：一旦声明了数组的大小，就不能再修改。这里的数组长度也是必需的，不能少。



尽管数组可以存储一组基本数据类型的元素，但是数组整体属于引用数据类型。当声明一个数组变量时，其实是创建了一个类型为“数据类型[]”（如 int[]、double[]、String[]）的数组对象，它具有以下的方法和属性

| 名称                         | 返回值   |
| ---------------------------- | -------- |
| clone()                      | Object   |
| equals(Object obj)           | boolean  |
| getClass()                   | Class<?> |
| hashCode()                   | int      |
| notify()                     | void     |
| notify All()                 | void     |
| toString()                   | String   |
| wait()                       | void     |
| wait(long timeout)           | void     |
| wait(long timeout,int nanos) | void     |

| 名称   | 返回值 |
| ------ | ------ |
| length | int    |

### 初始化一维数组

java中不能之分配内存空间而不赋初始值

数组初始化有以下三种格式：

**1使用new指定数组大小后进行初始化**

```java
type[] arrayName = new int[size];
```

如果程序员只指定了数组的长度，那么系统将负责为这些数组元素分配初始值。指定初始值时，系统按如下规则分配初始值。

- 数组元素的类型是基本类型中的整数类型（byte、short、int 和 long），则数组元素的值是 0。
- 数组元素的类型是基本类型中的浮点类型（float、double），则数组元素的值是 0.0。
- 数组元素的类型是基本类型中的字符类型（char），则数组元素的值是‘\u0000’。
- 数组元素的类型是基本类型中的布尔类型（boolean），则数组元素的值是 false。
- 数组元素的类型是引用类型（类、接口和数组），则数组元素的值是 null。

**2使用new指定数组元素的值**

```java
type[] arrayName = new type[]{值 1,值 2,值 3,值 4,• • •,值 n};
```

例如：

```java
int[] number = new int[]{1, 2, 3, 5, 8};
```

**3直接指定数组元素的值**

```java
type[] arrayName = {值 1,值 2,值 3,...,值 n};
```

 例如：

在前面例子的基础上更改代码，直接使用上述语法实现 number 数组的初始化。代码如下：

```java
int[] number = {1,2,3,5,8};
```

使用这种方式时，数组的声明和初始化操作要同步，即不能省略数组变量的类型。如下的代码就是错误的：

```java
int[] number;number = {1,2,3,5,8};
```

### 获取单个元素

指定元素下标即可：

```java
arrayName[index];
```

注意：当下标值超过数组长度是会抛出异常

### 获取全部元素

使用循环语句即可

例如

```java
int[] arr = {1,2,4,5,65};
for(int i = 1 ; i < arr.length - 1;i++){
	System.out.println(arr[i]);
}
```





## 5.3二维数组

### 创建二维数组

在 [Java](http://c.biancheng.net/java/) 中二维数组被看作数组的数组，即二维数组为一个特殊的一维数组，其每个元素又是一个一维数组。Java 并不直接支持二维数组，但是允许定义数组元素是一维数组的一维数组，以达到同样的效果。声明二维数组的语法如下：

```
type arrayName[][];    // 数据类型 数组名[][];
```

或

```java
type[][] arrayName;    // 数据类型[][] 数组名;
```

其中，type 表示二维数组的类型，arrayName 表示数组名称，第一个中括号表示行，第二个中括号表示列。

下面分别声明 int 类型和 char 类型的数组，代码如下：

```java
int[][] age;char[][] sex;
```

### 初始化二维数组

三种初始化方法：

```java
type[][] arrayName = new type[][]{值 1,值 2,值 3,…,值 n};    // 在定义时初始化
type[][] arrayName = new type[size1][size2];    // 给定空间，在赋值
type[][] arrayName = new type[size][];    // 数组第二维长度为空，可变化
```

### 获取单个元素

使用下标来获取

```java
arrayName[i-1][j-1];
```

i表示行j表示列

### 获取全部元素

在一维数组中直接使用数组的 length 属性获取数组元素的个数。而在二维数组中，直接使用 length 属性获取的是数组的行数，在指定的索引后加上 length（如 array[0].length）表示的是该行拥有多少个元素，即列数。



想在二维数组中获取全部元素是使用两层循环结构

```java
public static void main(String[] args) {
    double[][] class_score = { { 100, 99, 99 }, { 100, 98, 97 }, { 100, 100, 99.5 }, { 99.5, 99, 98.5 } };
    for (int i = 0; i < class_score.length; i++) { // 遍历行
        for (int j = 0; j < class_score[i].length; j++) {
            System.out.println("class_score[" + i + "][" + j + "]=" + class_score[i][j]);
        }
    }
}
```

提示：要想快速地打印一个二维数组的数据元素列表，可以调用：

```java
System.out.println(Arrays.deepToString(arrayName));
```

### 获取整行元素

获取指定行元素时，需要将行数固定，然后遍历改行中所有的列即可

```java
public static void main(String[] args) {
    double[][] class_score = { { 100, 99, 99 }, { 100, 98, 97 }, { 100, 100, 99.5 }, { 99.5, 99, 98.5 } };
    Scanner scan = new Scanner(System.in);
    System.out.println("当前数组只有" + class_score.length + "行，您想查看第几行的元素？请输入：");
    int number = scan.nextInt();
    for (int j = 0; j < class_score[number - 1].length; j++) {
        System.out.println("第" + number + "行的第[" + j + "]个元素的值是：" + class_score[number - 1][j]);
    }
}
```

### 获取整列元素

保持列不变，遍历每一行的该列即可

```java
public static void main(String[] args) {
    double[][] class_score = { { 100, 99, 99 }, { 100, 98, 97 }, { 100, 100, 99.5 }, { 99.5, 99, 98.5 } };
    Scanner scan = new Scanner(System.in);
    System.out.println("您要获取哪一列的值？请输入：");
    int number = scan.nextInt();
    for (int i = 0; i < class_score.length; i++) {
        System.out.println("第 " + (i + 1) + " 行的第[" + number + "]个元素的值是" + class_score[i][number]);
    }
}
```



## 5.4多维数组

在二维的基础上加一个括号即可

例如

```java
public static void main(String[] args) {
    String[][][] namelist = { { { "张阳", "李风", "陈飞" }, { "乐乐", "飞飞", "小曼" } },
            { { "Jack", "Kimi" }, { "Lucy", "Lily", "Rose" } }, { { "徐璐璐", "陈海" }, { "李丽丽", "陈海清" } } };
    for (int i = 0; i < namelist.length; i++) {
        for (int j = 0; j < namelist[i].length; j++) {
            for (int k = 0; k < namelist[i][j].length; k++) {
                System.out.println("namelist[" + i + "][" + j + "][" + k + "]=" + namelist[i][j][k]);
            }
        }
    }
}
```

运行结果

```java
namelist[0][0][0]=张阳
namelist[0][0][1]=李风
namelist[0][0][2]=陈飞
namelist[0][1][0]=乐乐
namelist[0][1][1]=飞飞
namelist[0][1][2]=小曼
namelist[1][0][0]=Jack
namelist[1][0][1]=Kimi
namelist[1][1][0]=Lucy
namelist[1][1][1]=Lily
namelist[1][1][2]=Rose
namelist[2][0][0]=徐璐璐
namelist[2][0][1]=陈海
namelist[2][1][0]=李丽丽
namelist[2][1][1]=陈海清
```



## 5.5不规则数组

### 静态初始化不规则数组

```
int intArray[][] = {{1,2}, {11}, {21,22,23}, {31,32,33}};
```

### 动态初始化不规则数组

先初始化高维数组，然后再分别逐个初始化低维数组。

```java
int intArray[][] = new int[4][]; //先初始化高维数组为4
// 逐一初始化低维数组
intArray[0] = new int[2];
intArray[1] = new int[1];
intArray[2] = new int[3];
intArray[3] = new int[3];
```



## 5.6数组也是一种数据类型

哈哈

## 5.7Arrays工具类

### java8之前

Arrays 类是一个工具类，其中包含了数组操作的很多方法。这个 Arrays 类里均为 static 修饰的方法（static 修饰的方法可以直接通过类名调用），可以直接通过 Arrays.xxx(xxx) 的形式调用方法。

**1）int binarySearch(type[] a, type key)**

使用二分法查询 key 元素值在 a 数组中出现的索引，如果 a 数组不包含 key 元素值，则返回负数。调用该方法时要求数组中元素己经按升序排列，这样才能得到正确结果。

**2）int binarySearch(type[] a, int fromIndex, int toIndex, type key)**

这个方法与前一个方法类似，但它只搜索 a 数组中 fromIndex 到 toIndex 索引的元素。调用该方法时要求数组中元素己经按升序排列，这样才能得到正确结果。

**3）type[] copyOf(type[] original, int length)**

这个方法将会把 original 数组复制成一个新数组，其中 length 是新数组的长度。如果 length 小于 original 数组的长度，则新数组就是原数组的前面 length 个元素，如果 length 大于 original 数组的长度，则新数组的前面元索就是原数组的所有元素，后面补充 0（数值类型）、false（布尔类型）或者 null（引用类型）。

**4）type[] copyOfRange(type[] original, int from, int to)**

这个方法与前面方法相似，但这个方法只复制 original 数组的 from 索引到 to 索引的元素。

**5）boolean equals(type[] a, type[] a2)**

如果 a 数组和 a2 数组的长度相等，而且 a 数组和 a2 数组的数组元素也一一相同，该方法将返回 true。

**6）void fill(type[] a, type val)**

该方法将会把 a 数组的所有元素都赋值为 val。

**7）void fill(type[] a, int fromIndex, int toIndex, type val)**

该方法与前一个方法的作用相同，区别只是该方法仅仅将 a 数组的 fromIndex 到 toIndex 索引的数组元素赋值为 val。

**8）void sort(type[] a)**

该方法对 a 数组的数组元素进行排序。

**9）void sort(type[] a, int fromIndex, int toIndex)**

该方法与前一个方法相似，区别是该方法仅仅对 fromIndex 到 toIndex 索引的元素进行排序。

**10）String toString(type[] a)**

该方法将一个数组转换成一个字符串。该方法按顺序把多个数组元素连缀在一起，多个数组元素使用英文逗号`,`和空格隔开。



部分用法示例

```java
public class ArraysTest {
    public static void main(String[] args) {
        // 定义一个a数组
        int[] a = new int[] { 3, 4, 5, 6 };
        // 定义一个a2数组
        int[] a2 = new int[] { 3, 4, 5, 6 };
        // a数组和a2数组的长度相等，毎个元素依次相等，将输出true
        System.out.println("a数组和a2数组是否相等：" + Arrays.equals(a, a2));
        // 通过复制a数组，生成一个新的b数组
        int[] b = Arrays.copyOf(a, 6);
        System.out.println("a数组和b数组是否相等：" + Arrays.equals(a, b));
        // 输出b数组的元素，将输出[3, 4, 5, 6, 0, 0]
        System.out.println("b 数组的元素为：" + Arrays.toString(b));
        // 将b数组的第3个元素（包括）到第5个元素（不包括）賦值为1
        Arrays.fill(b, 2, 4, 1);
        // 输出b数组的元素，将输出[3, 4, 1, 1, 0, 0]
        System.out.println("b 数组的元素为：" + Arrays.toString(b));
        // 对b数组进行排序
        Arrays.sort(b);
        // 输出b数组的元素.将输出[0,0,1,1,3,4]
        System.out.println("b数组的元素为：" + Arrays.toString(b));
    }
}
```



System类中也包含一个

`static void arraycopy(Object src, int srePos, Object dest, int dcstPos, int length)`方法，该方法可以将 src 数组里的元素值赋给 dest 数组的元素，其中 srcPos 指定从 src 数组的第几个元素开始赋值，length 参数指定将 src 数组的多少个元素值赋给 dest 数组的元素

### java8之后

**1）oid parallelPrefix(xxx[] array, XxxBinaryOperator op)**

该方法使用 op 参数指定的计算公式计算得到的结果作为新的元素。op 计算公式包括 left、right 两个形参，其中 left 代表数组中前一个索引处的元素，right 代表数组中当前索引处的元素，当计算第一个新数组元素时，left 的值默认为 1。

**2）void parallelPrefix(xxx[] array, int fromIndex, int toIndex, XxxBinaryOperator op)**

该方法与上一个方法相似，区别是该方法仅重新计算 fromIndex 到 toIndex 索引的元素。

**3）void setAll(xxx[] array, IntToXxxFunction generator)**

该方法使用指定的生成器（generator）为所有数组元素设置值，该生成器控制数组元素的值的生成算法。

**4）void parallelSetAll(xxx[] array, IntToXxxFunction generator)**

该方法的功能与上一个方法相同，只是该方法增加了并行能力，可以利用多 CPU 并行来提高性能。

**5）void parallelSort(xxx[] a)**

该方法的功能与 Arrays 类以前就有的 sort() 方法相似，只是该方法增加了并行能力，可以利用多 CPU 并行来提高性能。

**6）void parallelSort(xxx[] a，int fromIndex, int toIndex)**

该方法与上一个方法相似，区別是该方法仅对 fromIndex 到 toIndex 索引的元素进行排序。

**7）Spliterator.OfXxx spliterator(xxx[] array)**

将该数组的所有元素转换成对应的 Spliterator 对象。

**8）Spliterator.OfXxx spliterator(xxx[] array, int startInclusive, int endExclusive)**

该方法与上一个方法相似，区别是该方法仅转换 startInclusive 到 endExclusive 索引的元素。

**9）XxxStream stream(xxx[] array)**

该方法将数组转换为 Stream，Stream 是 Java 8 新增的流式编程的 API。

**10）XxxStream stream(xxx[] array, int startInclusive, int endExclusive)**

该方法与上一个方法相似，区别是该方法仅将 fromIndex 到 toIndex 索引的元索转换为 Stream。

例如

```java
public class ArraysTest2 {
    public static void main(String[] args) {
        int[] arr1 = new int[] { 3, 4, 25, 16, 30, 18 };
        // 对数组arr1进行并发排序
        Arrays.parallelSort(arr1);
        System.out.println(Arrays.toString(arr1));
        int[] arr2 = new int[] { 13, -4, 25, 16, 30, 18 };
        Arrays.parallelPrefix(arr2, new IntBinaryOperator() {
            // left 代表数组中前一个索引处的元素，计算第一个元素时，left为1
            // right代表数组中当前索引处的元素
            public int applyAsInt(int left, int right) {
                return left * right;
            }
        });
        System.out.println(Arrays.toString(arr2));
        int[] arr3 = new int[5];
        Arrays.parallelSetAll(arr3, new IntUnaryOperator() {
            // operand代表正在计算的元素索引
            public int applyAsInt(int operand) {
                return operand * 5;
            }
        });
        System.out.println(Arrays.toString(arr3));
    }
}
```

上面程序中第一行粗体字代码调用了 parallelSort() 方法对数组执行排序，该方法的功能与传统 sort() 方法大致相似，只是在多 CPU 机器上会有更好的性能。

第二段粗体字代码使用的计算公式为 left * right，其中 left 代表数组中当前一个索引处的元素，right 代表数组中当前索引处的元素。程序使用的数组为：

{3, -4 , 25, 16, 30, 18)

计算新的数组元素的方式为：

{1*3=3, 3*-4—12, -12*25=-300, -300*16=—48000, -48000*30=—144000, -144000*18=-2592000}

因此将会得到如下新的数组元素：

{3, -12, -300, -4800, -144000, -2592000)

第三段粗体字代码使用 operand * 5 公式来设置数组元素，该公式中 operand 代表正在计算的数组元素的索引。因此第三段粗体字代码计算得到的数组为：

{0, 5, 10, 15, 20}

提示：上面两段粗体字代码都可以使用 Lambda 表达式进行简化。

## 5.8数组和字符串相互转换

## 5.9比较数组

**数组相等的条件不仅要求数组元素的个数必须相等，而且要求对应位置的元素也相等。Arrays 类提供了 equals() 方法比较整个数组。**

语法如下：

```java
Arrays.equals(arrayA,arrayB);
```





## 5.10数组填充

Arrays 类提供了一个 fill() 方法，可以在指定位置进行数值填充。fill() 方法虽然可以填充数组，但是它的功能有限制，只能使用同一个数值进行填充。语法如下：

```java
Arrays.fill(array,value);
```

其中，array 表示数组，value 表示填充的值。

#### 例 1

声明一个 int 类型的 number 数组，然后通过 for 语句进行遍历，在该语句中调用 Arrays 类的 fill() 方法来填充数组，并输出数组中元素的值。代码如下：

```java
public static void main(String[] args) {    int[] number = new int[5];    System.out.println("number —共有 " + number.length + " 个元素，它们分别是：");    for (int i = 0; i < number.length; i++) {        Arrays.fill(number, i);        System.out.println("number[" + i + "]=" + i);    }}
```

执行上述代码，输出结果如下所示。

```java
number 一共有 5 个元素，它们分别是：
number[0]=0
number[1]=1
number[2]=2
number[3]=3
number[4]=4
```



## 5.11数组查找指定元素

查找数组是指从数组中查询指定位置的元素，或者查询某元素在指定数组中的位置。使用 Arrays 类的 binarySearch() 方法可以实现数组的查找，该方法可使用二分搜索法来搜索指定数组，以获得指定对象，该方法返回要搜索元素的索引值。

binarySearch() 方法有多种重载形式来满足不同类型数组的查找需要，常用的重载形式有两种。

(1) 第一种形式如下：

```
binarySearch(Object[] a,Object key);
```

其中，a 表示要搜索的数组，key 表示要搜索的值。如果 key 包含在数组中，则返回搜索值的索引；否则返回 -1 或“-插入点”。插入点指搜索键将要插入数组的位置，即第一个大于此键的元素索引。

在进行数组查询之前，必须对数组进行排序（可以使用 sort() 方法）。如果没有对数组进行排序，则结果是不确定的。如果数组包含多个带有指定值的元素，则无法确认找到的是哪一个。

***例1***

声明 double 类型的 score 数组，接着调用 Arrays 类的 sort() 方法对 score 数组排序，排序后分别查找数组中值为 100 和 60 的元素，分别将结果保存到 index1 和 index2 变量中，最后输出变量的值。代码如下：

```java
public static void main(String[] args) {
	double[] score = { 99.5, 100, 98, 97.5, 100, 95, 85.5, 100 };
    Arrays.sort(score);    
    int index1 = Arrays.binarySearch(score, 100);    
    int index2 = Arrays.binarySearch(score, 60);    
    System.out.println("查找到 100 的位置是：" + index1);    
    System.out.println("查找到 60 的位置是：" + index2);
    }
```

执行上述代码，输出结果如下：

```
查找到 100 的位置是：5
查找到 60 的位置是：-1
```

(2) 除了上述形式外，binarySearch() 还有另一种常用的形式，这种形式用于在指定的范围内查找某一元素。语法如下：

```
binarySearch(Object[] a,int fromIndex,int toIndex,Object key);
```

其中，a 表示要进行查找的数组，fromIndex 指定范围的开始处索引（包含开始处），toIndex 指定范围的结束处索引（不包含结束处），key 表示要搜索的元素。

在使用 binarySearch() 方法的上述重载形式时，也需要对数组进行排序，以便获取准确的索引值。如果要查找的元素 key 在指定的范围内，则返回搜索键的索引；否则返回 -1 或 “-插入点”。插入点指要将键插入数组的位置，即范围内第一个大于此键的元素索引。

***例 2***

对例 1 中创建的 score 数组进行查找元素，指定开始位置为 2，结束位置为 6。代码如下:

```java
public static void main(String[] args) {
	double[] score = {99.5,100,98,97.5,100,95,85.5,100};    
	Arrays.sort(score);    
	int index1 = Arrays.binarySearch(score,2,6,100);    
	int index2 = Arrays.binarySearch(score,2,6,60);    
	System.out.println("查找到 100 的位置是："+index1);    
	System.out.println("查找到 60 的位置是："+ index2);
	}
```

执行上述代码，输出结果如下：

```java
查找到 100 的位置是：5
查找到 60 的位置是：-3
```



## 5.12数组复制

### 使用copyOf()方法和copyOfRange()方法

Arrays 类的 copyOf() 方法与 copyOfRange() 方法都可实现对数组的复制。copyOf() 方法是复制数组至指定长度，copyOfRange() 方法则将指定数组的指定长度复制到一个新数组中。

#### 1. 使用 copyOf() 方法对数组进行复制

Arrays 类的 copyOf() 方法的语法格式如下：

```
Arrays.copyOf(dataType[] srcArray,int length);
```

其中，srcArray 表示要进行复制的数组，length 表示复制后的新数组的长度。

使用这种方法复制数组时，默认从原数组的第一个元素（索引值为 0）开始复制，目标数组的长度将为 length。如果 length 大于 srcArray.length，则目标数组中采用默认值填充；如果 length 小于 srcArray.length，则复制到第 length 个元素（索引值为 length-1）即止。

注意：目标数组如果已经存在，将会被重构。

#### 例 1

假设有一个数组中保存了 5 个成绩，现在需要在一个新数组中保存这 5 个成绩，同时留 3 个空余的元素供后期开发使用。

使用 Arrays 类的 CopyOf() 方法完成数组复制的代码如下：

```java
import java.util.Arrays;
public class Test19{
    public static void main(String[] args) {
        // 定义长度为 5 的数组
        int scores[] = new int[]{57,81,68,75,91};
        // 输出原数组
        System.out.println("原数组内容如下：");
        // 循环遍历原数组
        for(int i=0;i<scores.length;i++) {
            // 将数组元素输出
            System.out.print(scores[i]+"\t");
        }
        // 定义一个新的数组，将 scores 数组中的 5 个元素复制过来
        // 同时留 3 个内存空间供以后开发使用
        int[] newScores = (int[])Arrays.copyOf(scores,8);
        System.out.println("\n复制的新数组内容如下：");
        // 循环遍历复制后的新数组
        for(int j=0;j<newScores.length;j++) {
            // 将新数组的元素输出
            System.out.print(newScores[j]+"\t");
        }
    }
}
```

在上述代码中，由于原数组 scores 的长度为 5，而要复制的新数组 newScores 的长度为 8，因此在将原数组中的 5 个元素复制完之后，会采用默认值填充剩余 3 个元素的内容。

因为原数组 scores 的数据类型为 int，而使用 Arrays.copyOf(scores,8) 方法复制数组之后返回的是 Object[] 类型，因此需要将 Object[] 数据类型强制转换为 int[] 类型。同时，也正因为 scores 的数据类型为 int，因此默认值为 0。

运行的结果如下所示。

```
原数组内容如下：
57    81    68    75    91   
复制的新数组内容如下：
57    81    68    75    91    0    0    0
```

#### 2. 使用 CopyOfRange() 方法对数组进行复制

Arrays 类的 CopyOfRange() 方法是另一种复制数组的方法，其语法形式如下：

```
Arrays.copyOfRange(dataType[] srcArray,int startIndex,int endIndex)
```

其中：

- srcArray 表示原数组。
- startIndex 表示开始复制的起始索引，目标数组中将包含起始索引对应的元素，另外，startIndex 必须在 0 到 srcArray.length 之间。
- endIndex 表示终止索引，目标数组中将不包含终止索引对应的元素，endIndex 必须大于等于 startIndex，可以大于 srcArray.length，如果大于 srcArray.length，则目标数组中使用默认值填充。

注意：目标数组如果已经存在，将会被重构。

#### 例 2

假设有一个名称为 scores 的数组其元素为 8 个，现在需要定义一个名称为 newScores 的新数组。新数组的元素为 scores 数组的前 5 个元素，并且顺序不变。

使用 Arrays 类 copyOfRange() 方法完成数组复制的代码如下：

```java
public class Test20 {
    public static void main(String[] args) {
        // 定义长度为8的数组
        int scores[] = new int[] { 57, 81, 68, 75, 91, 66, 75, 84 };
        System.out.println("原数组内容如下：");
        // 循环遍历原数组
        for (int i = 0; i < scores.length; i++) {
            System.out.print(scores[i] + "\t");
        }
        // 复制原数组的前5个元素到newScores数组中
        int newScores[] = (int[]) Arrays.copyOfRange(scores, 0, 5);
        System.out.println("\n复制的新数组内容如下：");
        // 循环遍历目标数组，即复制后的新数组
        for (int j = 0; j < newScores.length; j++) {
            System.out.print(newScores[j] + "\t");
        }
    }
}
```

在上述代码中，原数组 scores 中包含有 8 个元素，使用 Arrays.copyOfRange() 方法可以将该数组复制到长度为 5 的 newScores 数组中，截取 scores 数组的前 5 个元素即可。

该程序运行结果如下所示。

```java
原数组内容如下：
57    81    68    75    91    66    75    84   
复制的新数组内容如下：
57    81    68    75    91
```

### 使用arraycopy()方法

arraycopy() 方法位于 java.lang.System 类中，其语法形式如下：

```
System.arraycopy(dataType[] srcArray,int srcIndex,int destArray,int destIndex,int length)
```

其中，srcArray 表示原数组；srcIndex 表示原数组中的起始索引；destArray 表示目标数组；destIndex 表示目标数组中的起始索引；length 表示要复制的数组长度。

使用此方法复制数组时，length+srcIndex 必须小于等于 srcArray.length，同时 length+destIndex 必须小于等于 destArray.length。

注意：目标数组必须已经存在，且不会被重构，相当于替换目标数组中的部分元素。

#### 例 3

假设在 scores 数组中保存了 8 名学生的成绩信息，现在需要复制该数组从第二个元素开始到结尾的所有元素到一个名称为 newScores 的数组中，长度为 12。scores 数组中的元素在 newScores 数组中从第三个元素开始排列。

使用 System.arraycopy() 方法来完成替换数组元素功能的代码如下：

```java
public class Test21 {
    public static void main(String[] args) {
        // 定义原数组，长度为8
        int scores[] = new int[] { 100, 81, 68, 75, 91, 66, 75, 100 };
        // 定义目标数组
        int newScores[] = new int[] { 80, 82, 71, 92, 68, 71, 87, 88, 81, 79, 90, 77 };
        System.out.println("原数组中的内容如下：");
        // 遍历原数组
        for (int i = 0; i < scores.length; i++) {
            System.out.print(scores[i] + "\t");
        }
        System.out.println("\n目标数组中的内容如下：");
        // 遍历目标数组
        for (int j = 0; j < newScores.length; j++) {
            System.out.print(newScores[j] + "\t");
        }
        System.arraycopy(scores, 0, newScores, 2, 8);
        // 复制原数组中的一部分到目标数组中
        System.out.println("\n替换元素后的目标数组内容如下：");
        // 循环遍历替换后的数组
        for (int k = 0; k < newScores.length; k++) {
            System.out.print(newScores[k] + "\t");
        }
    }
}
```

在该程序中，首先定义了一个包含有 8 个元素的 scores 数组，接着又定义了一个包含有 12 个元素的 newScores 数组，然后使用 for 循环分别遍历这两个数组，输出数组中的元素。最后使用 System.arraycopy() 方法将 newScores 数组中从第三个元素开始往后的 8 个元素替换为 scores 数组中的 8 个元素值。

该程序运行的结果如下所示。

```java
原数组中的内容如下：
100    81    68    75    91    66    75    100   
目标数组中的内容如下：
80    82    71    92    68    71    87    88    81    79    90    77   
替换元素后的目标数组内容如下：
80    82    100    81    68    75    91    66    75    100    90    77  
```

### 使用clone()方法

clone() 方法也可以实现复制数组。该方法是类 Object 中的方法，可以创建一个有单独内存空间的对象。因为数组也是一个 Object 类，因此也可以使用数组对象的 clone() 方法来复制数组。

clone() 方法的返回值是 Object 类型，要使用强制类型转换为适当的类型。其语法形式比较简单：

```
array_name.clone()
```

示例语句如下：

```
int[] targetArray=(int[])sourceArray.clone();
```

注意：目标数组如果已经存在，将会被重构。

#### 例 4

有一个长度为 8 的 scores 数组，因为程序需要，现在要定义一个名称为 newScores 的数组来容纳 scores 数组中的所有元素，可以使用 clone() 方法来将 scores 数组中的元素全部复制到 newScores 数组中。代码如下：

```java
public class Test22 {
    public static void main(String[] args) {
        // 定义原数组，长度为8
        int scores[] = new int[] { 100, 81, 68, 75, 91, 66, 75, 100 };
        System.out.println("原数组中的内容如下：");
        // 遍历原数组
        for (int i = 0; i < scores.length; i++) {
            System.out.print(scores[i] + "\t");
        }
        // 复制数组，将Object类型强制转换为int[]类型
        int newScores[] = (int[]) scores.clone();
        System.out.println("\n目标数组内容如下：");
        // 循环遍历目标数组
        for (int k = 0; k < newScores.length; k++) {
            System.out.print(newScores[k] + "\t");
        }
    }
}
```

注意：以上几种方法都是浅拷贝（浅复制）。浅拷贝只是复制了对象的引用地址，两个对象指向同一个内存地址，所以修改其中任意的值，另一个值都会随之变化。深拷贝是将对象及值复制过来，两个对象修改其中任意的值另一个值不会改变。

## 5.13sort()数组排序

### 升序

使用该方法分为两步：

1. 导入Java.util.Arrays包
2. 使用Arrays.sort(数组名)语法对数组进行排序，排序法规则是从小到大

例如：

```java
public static void main(String[] args) {
    // 定义含有5个元素的数组
    double[] scores = new double[] { 78, 45, 85, 97, 87 };
    System.out.println("排序前数组内容如下：");
    // 对scores数组进行循环遍历
    for (int i = 0; i < scores.length; i++) {
        System.out.print(scores[i] + "\t");
    }
    System.out.println("\n排序后的数组内容如下：");
    // 对数组进行排序
    Arrays.sort(scores);
    // 遍历排序后的数组
    for (int j = 0; j < scores.length; j++) {
        System.out.print(scores[j] + "\t");
    }
}
```

运行后的输出结果

```java
排序前数组内容如下：
78.0    45.0    85.0    97.0    87.0   
排序后的数组内容如下：
45.0    78.0    85.0    87.0    97.0
```

### 降序

**1）利用Collections.reverseOrder()方法**

```java
public static void main(String[] args) {
    Integer[] a = { 9, 8, 7, 2, 3, 4, 1, 0, 6, 5 };    // 数组类型为Integer
    Arrays.sort(a, Collections.reverseOrder());
    for (int arr : a) {
        System.out.print(arr + " ");
    }
}
```

**2）实现Comparator接口的复写compare()方法**

```java
public class Test {
    public static void main(String[] args) {
        /*
         * 注意，要想改变默认的排列顺序，不能使用基本类型（int,double,char）而要使用它们对应的类
         */
        Integer[] a = { 9, 8, 7, 2, 3, 4, 1, 0, 6, 5 };
        // 定义一个自定义类MyComparator的对象
        Comparator cmp = new MyComparator();
        Arrays.sort(a, cmp);
        for (int arr : a) {
            System.out.print(arr + " ");
        }
    }
}
// 实现Comparator接口
class MyComparator implements Comparator<Integer> {
    @Override
    public int compare(Integer o1, Integer o2) {
        /*
         * 如果o1小于o2，我们就返回正值，如果o1大于o2我们就返回负值， 这样颠倒一下，就可以实现降序排序了,反之即可自定义升序排序了
         */
        return o2 - o1;
    }
}
```

输出结果

```java
9 8 7 6 5 4 3 2 1 0
```



## 5.14四个排序

### 冒泡排序

### 快速排序

快速排序（Quicksort）是对冒泡排序的一种改进，是一种排序执行效率很高的排序算法。

快速排序的基本思想是：通过一趟排序，将要排序的数据分隔成独立的两部分，其中一部分的所有数据比另外一部分的所有数据都要小，然后再按此方法对这两部分数据分别进行快速排序，整个排序过程可以递归进行，以此使整个数据变成有序序列。

具体做法是：假设要对某个数组进行排序，首先需要任意选取一个数据（通常选用第一个数据）作为关键数据，然后将所有比它小的数都放到它的前面，所有比它大的数都放到它的后面。这个过程称为一趟快速排序；递归调用此过程，即可实现数据的快速排序。

例如：

(1) 声明静态的 getMiddle() 方法，该方法需要返回一个 int 类型的参数值，在该方法中传入 3 个参数。代码如下：

```java
public static int getMiddle(int[] list, int low, int high) {
    int tmp = list[low]; // 数组的第一个值作为中轴（分界点或关键数据）
    while (low < high) {
        while (low < high && list[high] > tmp) {
            high--;
        }
        list[low] = list[high]; // 比中轴小的记录移到低端
        while (low < high && list[low] < tmp) {
            low++;
        }
        list[high] = list[low]; // 比中轴大的记录移到高端
    }
    list[low] = tmp; // 中轴记录到尾
    return low; // 返回中轴的位置
}
```

(2) 创建静态的 unckSort() 方法，在该方法中判断 low 参数是否小于 high 参数，如果是则调用 getMiddle() 方法，将数组一分为二，并且调用自身的方法进行递归排序。代码如下：

```java
public static void unckSort(int[] list,int low,int high) {
    if(low < high) {
        int middle = getMiddle(list,low,high);    // 将list数组一分为二
        unckSort(list,low,middle-1);    // 对低字表进行递归排序
        unckSort(list,middle+1,high);    // 对高字表进行递归排序
    }
}
```

(3) 声明静态的 quick() 方法，在该方法中判断传入的数组是否为空，如果不为空，则调用 unckSort() 方法进行排序。代码如下：

```java
public static void quick(int[] str) {
    if(str.length > 0) {
        // 查看数组是否为空
        unckSort(str,0,str.length-1);
    }
}
```

(4) 在 main() 方法中声明 int 类型的 number 数组，接着输出该数组中的元素。然后调用自定义的 quick() 方法进行排序，排序后重新输出数组中的元素。代码如下：

```java
int[] number={13,15,24,99,14,11,1,2,3};
System.out.println("排序前：");
for(int val:number) {
    System.out.print(val+" ");
}
quick(number);
System.out.println("\n排序后：");
for(int val:number) {
    System.out.print(val +" ");
}
```

输出结果如下：

```java
排序前：
13 15 24 99 14 11 1 2 3
排序后：
1 2 3 11 13 14 15 24 99 
```



### 选择排序

选择排序是指每一趟从待排序的数据元素中选出最大（或最小）的一个元素，顺序放在已排好序的数列的最后，直到全部待排序的数据元素排完。

```java
int[] number = {13,15,24,99,4,1};
String end = "\n";
int index;
for (int i = 1;i < number.length;i++) {
    index = 0;
    for(int j = 1;j <= number.length-i;j++) {
        if (number[j] > number[index]) {
            index = j;    // 查找最大值
        }
    }
    end = number[index] + " " + end;    // 定位已排好的数组元素
    int temp = number[number.length-i];
    number[number.length-1] = number[index];
    number[index] = temp;
    System.out.print("【");
    for (int j = 0;j < number.length-i;j++) {
        System.out.print(number[j]+" ");
    }
    System.out.print("】"+end);
}
```

执行上述代码，查看每一趟排序后的结果，运行结果如下所示。

```java
【13 15 24 1 4 】99
【13 15 4 1 】24 99
【13 1 4 】15 24 99
【4 1 】13 15 24 99
【1 】4 13 15 24 99 
```

### 直接插入排序

直接插入排序的基本思想是：将 n 个有序数存放在数组 a 中，要插入的数为 x，首先确定 x 插在数组中的位置 p，然后将 p 之后的元素都向后移一个位置，空出 a(p)，将 x 放入 a(p)，这样可实现插入 x 后仍然有序。

例如

```java
public static void main(String[] args) {
    int[] number = { 13, 15, 24, 99, 4, 1 };
    System.out.println("排序前：");
    for (int val : number) { // 遍历数组元素
        System.out.print(val + " "); // 输出数组元素
    }
    int temp, j;
    for (int i = 1; i < number.length; i++) {
        temp = number[i];
        for (j = i - 1; j >= 0 && number[j] > temp; j--) {
            number[j + 1] = number[j];
        }
        number[j + 1] = temp;
    }
    System.out.println("\n排序后：");
    for (int val : number) { // 遍历数组元素
        System.out.print(val + " "); // 输出数组元素
    }
}
```

执行上述代码，最终的输出结果如下：

```java
排序前：
13 15 24 99 4 1
排序后：
1 4 13 15 24 99 
```







# 6.Java类和对象

## 6.1面向对象的概述

面向对象简称 OO（Object Oriented），20 世纪 80 年代以后，有了面向对象分析（OOA）、 面向对象设计（OOD）、面向对象程序设计（OOP）等新的系统开发方式模型的研究。

对 java 语言来说，一切皆是对象。把现实世界中的对象抽象地体现在编程世界中，一个对象代表了某个具体的操作。一个个对象最终组成了完整的程序设计，这些对象可以是独立存在的，也可以是从别的对象继承过来的。对象之间通过相互作用传递信息，实现程序开发。

Java 是面向对象的编程语言，对象就是面向对象程序设计的核心。所谓对象就是真实世界中的实体，对象与实体是一一对应的，也就是说现实世界中每一个实体都是一个对象，它是一种具体的概念。对象有以下特点：

- 对象具有属性和行为。
- 对象具有变化的状态。
- 对象具有唯一性。
- 对象都是某个类别的实例。
-  一切皆为对象，真实世界中的所有事物都可以视为对象。

例如，在真实世界的学校里，会有学生和老师等实体，学生有学号、姓名、所在班级等属性（数据），学生还有学习、提问、吃饭和走路等操作。学生只是抽象的描述，这个抽象的描述称为“类”。在学校里活动的是学生个体，即张同学、李同学等，这些具体的个体称为“对象”，“对象”也称为“实例”。

### 面型对象的三大核心的特性

1. 可重用性：代码重复使用，减少代码量，提高开发效率。下面介绍的面向对象的三大核心特性（继承、封装和多态）都围绕这个核心。
2. 可扩展性：指新的功能可以很容易地加入到系统中来，便于软件的修改。
3. 可管理性：能够将功能与数据结合，方便管理。

该开发模式之所以是程序设计更加完善和强大，主要是因为面向对象具有继承，封装和多态三个核心特性



**继承性**



如同生活中的子女继承父母拥有的所有财产，程序中的继承性是指子类拥有父类的全部特征和行为，这是类之间的一种关系。Java 只支持单继承。

使用这种层次形的分类方式，是为了将多个类的通用属性和方法提取出来，放在它们的父类中，然后只需要在子类中各自定义自己独有的属性和方法，并以继承的形式在父类中获取它们的通用属性和方法即可。

提示：[C++](http://c.biancheng.net/cplus/) 支持多继承，多继承就是一个子类可有多个父类。例如，客轮是轮船也是交通工具，客轮的父类是轮船和交通工具。多继承会引起很多冲突问题，因此现在很多面向对象的语言都不支持多继承。Java 语言是单继承的，即只能有一个父类，但 Java 可以实现多个接口，可防止多继承所引起的冲突问题



**封装性**



封装是将代码及其处理的数据绑定在一起的一种编程机制，该机制保证了程序和数据都不受外部干扰且不被误用。封装的目的在于保护信息，使用它的主要优点如下。

- 保护类中的信息，它可以阻止在外部定义的代码随意访问内部代码和数据。
- 隐藏细节信息，一些不需要程序员修改和使用的信息，比如取款机中的键盘，用户只需要知道按哪个键实现什么操作就可以，至于它内部是如何运行的，用户不需要知道。
- 有助于建立各个系统之间的松耦合关系，提高系统的独立性。当一个系统的实现方式发生变化时，只要它的接口不变，就不会影响其他系统的使用。例如 U 盘，不管里面的存储方式怎么改变，只要 U 盘上的 USB 接口不变，就不会影响用户的正常操作。
- 提高软件的复用率，降低成本。每个系统都是一个相对独立的整体，可以在不同的环境中得到使用。例如，一个 U 盘可以在多台电脑上使用。

*Java 语言的基本封装单位是类。由于类的用途是封装复杂性，所以类的内部有隐藏实现复杂性的机制。Java 提供了私有和公有的访问模式，类的公有接口代表外部的用户应该知道或可以知道的每件东西，私有的方法数据只能通过该类的成员代码来访问，这就可以确保不会发生不希望的事情。*



**多态性**



面向对象的多态性，即“一个接口，多个方法”。多态性体现在父类中定义的属性和方法被子类继承后，可以具有不同的属性或表现方式。多态性允许一个接口被多个同类使用，弥补了单继承的不足。

## 6.2认识类和对象

类是对象的抽象，对象是类的具体

类是概念模型，定义对象的所有特性和所需的操作，对象是真实的模型，是一个具体的体。

由此可见，类是描述了一组有相同特性和行为的一组对象的集合

对象或者实体所拥有的特征在类中表示时称为类的属性

对象所执行的操作叫做类的方法

***类是构造面向对象程序的基本单位，***是抽取了同类对象的共同属性和方法所形成的对象或实体的“模板”。而对象是现实世界中实体的描述，对象要创建才存在，有了对象才能对对象进行操作。类是对象的模板，对象是类的实例。

## 6.3类的定义

***类是java中一种重要的引用数据类型，也是组成Java程序的基本要素，因为所有Java程序都是基于类的***

定义一个类的完整语法如下

```java
[public][abstract|final]class<class_name>[extends<class_name>][implements<interface_name>] {
    // 定义属性部分
    <property_type><property1>;
    <property_type><property2>;
    <property_type><property3>;
    …
    // 定义方法部分
    function1();
    function2();
    function3();
    …
}
```

提示：上述语法中，中括号“[]”中的部分表示可以省略，竖线“|”表示“或关系”，例如 abstract|final，说明可以使用 abstract 或 final 关键字，但是两个关键字不能同时出现。

上述语法中各关键字的描述如下。

- `public`：表示“共有”的意思。如果使用 public 修饰，则可以被其他类和程序访问。每个 Java 程序的主类都必须是 public 类，作为公共工具供其他类和程序使用的类应定义为 public 类。
- `abstract`：如果类被 abstract 修饰，则该类为抽象类，抽象类不能被实例化，但抽象类中可以有抽象方法（使用 abstract 修饰的方法）和具体方法（没有使用 abstract 修饰的方法）。继承该抽象类的所有子类都必须实现该抽象类中的所有抽象方法（除非子类也是抽象类）。
- `final`：如果类被 final 修饰，则不允许被继承。
- `class`：声明类的关键字。
- `class_name`：类的名称。
- `extends`：表示继承其他类。
- `implements`：表示实现某些接口。
- `property_type`：表示成员变量的类型。
- `property`：表示成员变量名称。
- `function()`：表示成员方法名称。

Java 类名的命名规则：

1. 类名应该以下划线（_）或字母开头，最好以字母开头。
2. 第一个字母最好大写，如果类名由多个单词组成，则每个单词的首字母最好都大写。
3. 类名不能为 Java 中的关键字，例如 boolean、this、int 等。
4. 类名不能包含任何嵌入的空格或点号以及除了下划线（_）和美元符号（$）字符之外的特殊字符。



**例一**

创建一个新的类就是创建一个新的数据类型，实例化一个类就是得到类的一个对象。因此类就是一组变量的相关方法的集合，其中变量表明对象的状态和属性，方法表明对象所具有的行为，定义一个列的步骤如下：

(1)声明类。编写类最外面的框架，声明一个名称为Person的类

```java
public class Person{
	//类的主体
}
```

(2)编写类的属性。类中的数据和方法统称为类成员。其中，类的属性就是类的数据成员。

(3) 编写类的方法。类的方法描述了类所具有的行为，是类的方法成员。可以简单地把方法理解为独立完成某个功能的单元模块。

下面简单定义一个person类

```java
public class Person{
	private String name;
	private int age;
	public void tell(){
		//定义说话的方法
		System.out.println(name + "今年" + age + "岁！");
	}
}
```

如上述代码，在 Person 类中首先定义了两个属性，分别为 name 和 age，然后定义了一个名称为 tell() 的方法。

## 6.4类的属性

在java 中类的成员变量定义了类的属性。例如，一个学生类中一般需要有姓名、性别和年龄等属性，这时就需要定义姓名、性别和年龄 3 个属性。声明成员变量的语法如下：

```java
[public|protected|private][static][final]<type><variable_name>
```

各参数的含义如下：

- public、protected、private：用于表示成员变量的访问权限。
- static：表示该成员变量为类变量，也称为静态变量。
- final：表示将该成员变量声明为常量，其值无法更改。
- type：表示变量的类型。
- variable_name：表示变量名称。



可以在声明成员变量的同时对其进行初始化，如果声明成员变量时没有对其初始化，则系统会使用默认的值初始化成员变量

初始化的默认值如下：

- 整数型（byte、short、int 和 long）的基本类型变量的默认值为 0。
- 单精度浮点型（float）的基本类型变量的默认值为 0.0f。
- 双精度浮点型（double）的基本类型变量的默认值为 0.0d。
- 字符型（char）的基本类型变量的默认值为 “\u0000”。
- 布尔型的基本类型变量的默认值为 false。
- 数组引用类型的变量的默认值为 null。如果创建了数组变量的实例，但没有显式地为每个元素赋值，则数组中的元素初始化值采用数组数据类型对应的默认值。

定义类的成员变量示例如下：

```java
public class Student{
	public String name;//姓名
	final int sex = 0;//性别
	private int age;//年龄
}
```

上述示例的 Student 类中定义了 3 个成员变量：String 类型的 name、int 类型的 sex 和 int 类型的 age。其中，name 的访问修饰符为 public，初始化值为 null；sex 的访问修饰符为 friendly（默认），初始化值为 0，表示性别为女，且其值无法更改；age 的访问修饰符为 private，初始化值为 0。

 

例一



举一个简单的例子介绍一下成员变量初始值

```java
public calss Counter{
	static int sum;
	public static void main (String[] args){
		System.out.println(sum);
	}
}
```

这里使用静态的方法修饰变量sum，输出的结果是int类型的初始值，即：0。

## 6.5创建一个学生类

1）首先定义一个名为Student的学生类

```java
public class Student{
	//学生类
}
```

2）在类中定义学生的姓名，性别，年龄等属性

```java
public class Student{
	public String Name;
	public int Age;
	private boolean Sex;
}
```

3）因为sex属性是私有的需要设值set和get方法堆属性值进行获取

```java
public boolean isSex() {
        return Sex;
    }

    public void setSex(boolean sex) {
        this.Sex = sex;
    }
```

4）在Student类中添加main()方法，然后创建两个实例并输出学生信息

```java
public static void main(String[] args) {
        student stu1 = new student();
        stu1.Name = "谢钦";
        //stu1.Age = 20;
        String isMan = stu1.isSex() ? "女" : "男";
        System.out.println("姓名：" + stu1.Name + "性别：" + isMan + "年龄：" + stu1.Age);
        student li = new student(); // 创建第二个实例
        li.Name = "李子文";
        li.Sex = true;
        li.Age = 15;
        String isWoman = li.isSex() ? "女" : "男";
        System.out.println("姓名：" + li.Name + "性别：" + isWoman + "年龄：" + li.Age);
    }
```

5）输出结果是

```java
姓名：谢钦性别：男年龄：0
姓名：李子文性别：女年龄：15
```



由输出结果可以看到，在第一个实例 zhang 中由于仅设置了 Name 属性的值，所以 boolean 类型的 Sex 默认使用值 false，int 类型的 Age 默认使用值 0。第二个实例 li 同时设置了这三个属性的值。

## 6.6成员方法

声明成员方法可以定义类的行为，行为表示一个对象能够做的事情或者能够从一个对象取得的信息。类的各种功能操作都是用方法来实现的，属性只不过提供了相应的数据。***一个完整的方法通常包括方法名称、方法主体、方法参数和方法返回值类型***

成员方法一旦被定义，便可以在程序中多次调用，提高了编程效率。声明成员方法的语法格式如下：

```java
public class Test {
    [public|private|protected][static]<void|return_type><method_name>([paramList]) {
        // 方法体
    }
}
```

注意：上述语法中，中括号“[]”中的部分表示可以省略，竖线“|”表示“或”，例如 public|private，说明可以使用 public 或 private 关键字，但是两个关键字不能同时出现。

上述代码中一个方法包含 4 部分：方法的返回值、方法名称、方法的参数和方法体。其中 retum_type 是方法返回值的数据类型，数据类型可以是原始的数据类型，即常用的 8 种数据类型，也可以是一个引用数据类型，如一个类、接口和数组等。

除了这些，一个方法还可以没有返回值，即返回类型为 void，像 main() 方法。method_name 表示自定义的方法名称，方法的名称首先要遵循标识符的命名约定，除此之外，方法的名称第一个单词的第一个字母是小写，第二单词的第一个字母是大写，依此类推。



paramList 表示参数列表，这些变量都要有自己的数据类型，可以是原始数据类型，也可以是复杂数据类型，一个方法主要依靠参数来传递消息。方法主体是方法中执行功能操作的语句。其他各修饰符的含义如下。

- public、private、protected：表示成员方法的访问权限。
- static：表示限定该成员方法为静态方法。
- final：表示限定该成员方法不能被重写或重载。
- abstract：表示限定该成员方法为抽象方法。抽象方法不提供具体的实现，并且所属类型必须为抽象类。



例一

为学生类添加一个可以返回学生信息字符串的方法：

```java
public class Student {
    public StringBuffer printInfo(Student st) {
        StringBuffer sb = new StringBuffer();
        sb.append("学生姓名："+st.Name+"\n 学生年龄："+st.Age+"\n 学生性别："+st.isSex());
        return sb;
    }
}
```

上述代码创建了一个名称为 printInfo 的方法，其返回值类型为 StringBuffer（引用数据类型）。该方法需要传递一个 Student 类型的参数，最后需要将一个 StringBuffer 类型的数据返回。

**1. 成员方法的返回值**

若方法有返回值，则在方法体中用 return 语句指明要返回的值，其格式如下所示。

```
return 表达式
```

或者

```
return (表达式)
```

其中，表达式可以是常量、变量、对象等。表达式的数据类型必须与声明成员方法时给出的返回值类型一致。

**2. 形参、实参及成员方法的调用**

一般来说，可以通过以下方式来调用成员方法：

```java
methodName({paramList})
```

关于方法的参数，经常会提到形参与实参，*形参是定义方法时参数列表中出现的参数，实参是调用方法时为方法传递的参数*。



例二

下面是returnMin()方法中的m和n是形参，调用returnMin()方法时是实参

```java
public int returnMin(int m,int n) {
    return Math.min(m,n);    // m和n是形参
}
public static void main(String[] args) {
    int x = 50;
    int y = 100;
    Test t = new Test();
    int i = t.returnMin(x,y);    // x和y是实参
    System.out.println(i);
}
```

方法的形参和实参具有以下特点：

- 形参变量只有在被调用时才分配内存单元，在调用结束时，即刻释放所分配的内存单元。因此，形参只有在方法内部有效，方法调用结束返回主调方法后则不能再使用该形参变量。
- 实参可以是常量、变量、表达式、方法等，无论实参是何种类型的量，在进行方法调用时，它们都必须具有确定的值，以便把这些值传送给形参。因此应预先用赋值、输入等办法使实参获得确定值。
- 实参和形参在数量、类型和顺序上应严格一致，否则会发生“类型不匹配” 的错误。
- 方法调用中发生的数据传送是单向的，即只能把实参的值传送绐形参，而不能把形参的值反向地传送给实参。因此在方法调用过程中，形参的值发生改变，而实参中的值不会变化。



例三



下面示例演示了调用add()方法前后形参x的变化

```java
public int add(int x) {
    x += 30;
    System.out.println("形参 x 的值："+x);
    return x;
}
public static void main(String[] args) {
    int x = 150;
    System.out.println("调用 add() 方法之前 x 的值："+x);
    Test t = new Test();
    int i = t.add(x);
    System.out.println("实参 x 的值："+x);
    System.out.println("调用 add() 方法的返回值："+i);
}
```

运行结果

```java
调用 add() 方法之前 x 的值：150
形参 x 的值：180
实参 x 的值：150
调用 add() 方法的返回值：180
```

在调用成员方法时应注意以下 4 点：

1. 对无参成员方法来说，是没有实际参数列表的（即没有 paramList），但方法名后的括号不能省略。
2. 对带参数的成员方法来说，实参的个数、顺序以及它们的数据类型必须与形式参数的个数、顺序以及它们的数据类型保持一致，各个实参间用逗号分隔。实参名与形参名可以相同，也可以不同。
3. 实参也可以是表达式，此时一定要注意使表达式的数据类型与形参的数据类型相同，或者使表达式的类型按java类型转换规则达到形参指明的数据类型。
4. 实参变量对形参变量的数据传递是“值传递”，即只能由实参传递给形参，而不能由形参传递给实参。程序中执行到调用成员方法时，Java 把实参值复制到一个临时的存储区（栈）中，形参的任何修改都在栈中进行，当退出该成员方法时，Java 自动清除栈中的内容。





***方法体中的局部变量***





在方法体内可以定义本方法所使用的变量，这种变量是局部变量。它的生存期与作用域是在本方法内，也就是说，局部变量只能在本方法内有效或可见，离开本方法则这些变量将被自动释放。

在方法体内定义变量时，变量前不能加修饰符。局部变量在使用前必须明确赋值，否则编译时会出错。另外，在一个方法内部，可以在复合语句（把多个语句用括号`{}`括起来组成的一个语句称复合语句）中定义变量，这些变量只在复合语句中有效。

## 6.7this关键字

this 关键字是java常用的关键字，可用于任何实例方法内指向当前对象，也可指向对其调用当前方法的对象，或者在需要当前类型对象引用时使用。

### this.属性名

大部分时候，普通方法访问其他方法、成员变量时无须使用 this 前缀，但如果方法里有个局部变量和成员变量同名，但程序又需要在该方法里访问这个被覆盖的成员变量，则必须使用 this 前缀。

**例一**

定义一个Teacher类

``` java
public class Teacher {
    private String name;    // 教师名称
    private double salary;    // 工资
    private int age;    // 年龄
}
```

在上述代码中 name、salary 和 age 的作用域是 private，因此在类外部无法对它们的值进行设置。为了解决这个问题，可以为 Teacher 类添加一个构造方法，然后在构造方法中传递参数进行修改。代码如下：

```java
// 创建构造方法，为上面的3个属性赋初始值
public Teacher(String name,double salary,int age) {
    this.name = name;    // 设置教师名称
    this.salary = salary;    // 设置教师工资
    this.age = age;    // 设置教师年龄
}
```

在 Teacher 类的构造方法中使用了 this 关键字对属性 name、salary 和 age 赋值，this 表示当前对象。`this.name=name`语句表示一个赋值语句，等号左边的 this.name 是指当前对象具有的变量 name，等号右边的 name 表示参数传递过来的数值。

创建一个 main() 方法对 Teacher 类进行测试，代码如下：

```java
public static void main(String[] args) {
    Teacher teacher = new Teacher("王刚",5000.0,45);
    System.out.println("教师信息如下：");
    System.out.println("教师名称："+teacher.name+"\n教师工资："+teacher.salary+"\n教师年龄："+teacher.age);
}
```

运行结果:

```
教师信息如下：
教师名称：王刚
教师工资：5000.0
教师年龄：45
```

提示：当一个类的属性（成员变量）名与访问该属性的方法参数名相同时，则需要使用 this 关键字来访问类中的属性，以区分类的属性和方法中的参数。

### this.方法名

this 关键字最大的作用就是让类中一个方法，访问该类里的另一个方法或实例变量。

**例二**

假设定义了一个Dog类,这个Dog对象的run()方法需要调用它的jump()方法,Dog类的代码如下:

```java
/**
 * 第一种定义Dog类方法
 **/
public class Dog {
    // 定义一个jump()方法
    public void jump() {
        System.out.println("正在执行jump方法");
    }
    // 定义一个run()方法，run()方法需要借助jump()方法
    public void run() {
        Dog d = new Dog();
        d.jump();
        System.out.println("正在执行 run 方法");
    }
}
```

使用这种方式来定义这个 Dog 类，确实可以实现在 run( ) 方法中调用 jump( ) 方法。下面再提供一个程序来创建 Dog 对象，并调用该对象的 run( ) 方法。

```java
public class DogTest {
    public static void main(String[] args) {
        // 创建Dog对象
        Dog dog = new Dog();
        // 调用Dog对象的run()方法
        dog.run();
    }
}
```

在上面的程序中，一共产生了两个 Dog 对象，在 Dog 类的 run( ) 方法中，程序创建了一个 Dog 对象，并使用名为 d 的引用变量来指向该 Dog 对象。在 DogTest 的 main() 方法中，程序再次创建了一个 Dog 对象，并使用名为 dog 的引用变量来指向该 Dog 对象。

下面我们思考两个问题。

1）在 run( ) 方法中调用 jump( ) 方法时是否一定需要一个 Dog 对象？

答案是肯定的，因为没有使用 static 修饰的成员变量和方法都必须使用对象来调用。

2）是否一定需要重新创建一个 Dog 对象？

不一定，因为当程序调用 run( ) 方法时，一定会提供一个 Dog 对象，这样就可以直接使用这个已经存在的 Dog 对象，而无须重新创建新的 Dog 对象了。因此需要在 run() 方法中获得调用该方法的对象，通过 this 关键字就可以满足这个要求。

this 可以代表任何对象，当 this 出现在某个方法体中时，它所代表的对象是不确定的，但它的类型是确定的，它所代表的只能是当前类的实例。只有当这个方法被调用时，它所代表的对象才被确定下来，谁在调用这个方法，this 就代表谁。

将前面的 Dog 类的 run( ) 方法改为如下形式会更加合适，run( ) 方法代码修改如下，其它代码不变。

```java
/**
 * 第二种定义Dog类方法
 **/
// 定义一个run()方法，run()方法需要借助jump()方法
public void run() {
    // 使用this引用调用run()方法的对象
    this.jump();
    System.out.println("正在执行run方法");
}
```

Java 允许对象的一个成员直接调用另一个成员，可以省略 this 前缀。也就是说，将上面的 run( ) 方法改为如下形式也完全正确。

```java
public void run(){
	jump();
	System.out.println("正在执行run方法");
}
```

注意：对于 static 修饰的方法而言，可以使用类来直接调用该方法，如果在 static 修饰的方法中使用 this 关键字，则这个关键字就无法指向合适的对象。所以，static 修饰的方法中不能使用 this 引用。并且 Java 语法规定，静态成员不能直接访问非静态成员。

省略 this 前缀只是一种假象，虽然程序员省略了调用 jump() 方法之前的 this，但实际上这个 this 依然是存在的。

### this()访问构造方法

**例三**

下面定义一个 Student 类，使用 this( ) 调用构造方法给 name 赋值，Student 类的代码如下所示

```java
public class Student {
    String name;
    // 无参构造方法（没有参数的构造方法）
    public Student() {
        this("张三");
    }
    // 有参构造方法
    public Student(String name) {
        this.name = name;
    }
    // 输出name和age
    public void print() {
        System.out.println("姓名：" + name);
    }
    public static void main(String[] args) {
        Student stu = new Student();
        stu.print();
    }
}
```

输出结果:

```java
姓名:张三
```

注意:

1. this()不能再普通方法中使用,只能写在构造方法中
2. 在构造方法中必须是第一条语句

## 6.8对象的创建

对象是对类的实例化。对象具有状态和行为，变量用来表明对象的状态，方法表明对象所具有的行为。java对象的生命周期包括创建、使用和清除，本文详细介绍对象的创建，在 Java 语言中创建对象分显式创建与隐含创建两种情况。

### 显示创建对象

**1.使用new关键字创建对象**

语法格式如下:

```java
类名 对象名 = new 类名();
```

**2.调用java.long.class或者java.long.reflect.Construct类的newInstance()实例方法**

代码格式如下

```java
 Class类 对象名称 = Class.forName(要实例化的类全称);
类名 对象名 = (类名)Class类对象名称.newInstance();
```

调用 java.lang.Class 类中的 forName() 方法时，需要将要实例化的类的全称（比如 com.mxl.package.Student）作为参数传递过去，然后再调用 java.lang.Class 类对象的 newInstance() 方法创建对象。

**3.调用对象的clone()方法**

不常用,使用该方法创建对象时,要实例化的类必须继承java.lang.Cloneable接口,格式如下:

```java
类对象名 = (类名)已创建好的类对象名,clone();
```

**4.调用java.io.ObjectInputStream对象的readObject()方法**





例一

下面创建一个示例演示前三种对象创建的方法,代码如下

```java
public class Student implements Cloneable {   
    // 实现 Cloneable 接口
    private String Name;    // 学生名字
    private int age;    // 学生年龄
    public Student(String name,int age) {    
        // 构造方法
        this.Name = name;
        this.age = age;
    }
    public Student() {
        this.Name = "name";
        this.age = 0;
    }
    public String toString() {
        return"学生名字："+Name+"，年龄："+age;
    }
    public static void main(String[] args)throws Exception {
        System.out.println("---------使用 new 关键字创建对象---------");
       
        // 使用new关键字创建对象
        Student student1 = new Student("小刘",22);
        System.out.println(student1);
        System.out.println("-----------调用 java.lang.Class 的 newInstance() 方法创建对象-----------");
       
        // 调用 java.lang.Class 的 newInstance() 方法创建对象
        Class c1 = Class.forName("Student");
        Student student2 = (Student)c1.newInstance();
        System.out.println(student2);
        System.out.println("-------------------调用对象的 clone() 方法创建对象----------");
        // 调用对象的 clone() 方法创建对象
        Student student3 = (Student)student2.clone();
        System.out.println(student3);
    }
}
```

对上述示例的说明如下：

- 使用 new 关键字或 Class 对象的 newInstance() 方法创建对象时，都会调用类的构造方法。
- 使用 Class 类的 newInstance() 方法创建对象时，会调用类的默认构造方法，即无参构造方法。
- 使用 Object 类的 clone() 方法创建对象时，不会调用类的构造方法，它会创建一个复制的对象，这个对象和原来的对象具有不同的内存地址，但它们的属性值相同。
- 如果类没有实现 Cloneable 接口，则 clone。方法会抛出 java.lang.CloneNotSupportedException 异常，所以应该让类实现 Cloneable 接口。

程序执行结果如下:

```java
---------使用 new 关键字创建对象---------
学生名字：小刘，年龄：22
-----------调用 java.lang.Class 的 newInstance() 方法创建对象-----------
学生名字：name，年龄：0
-------------------调用对象的done()方法创建对象----------
学生名字：name，年龄：0
```



### 隐式创建对象

1）String strName = "strValue"，其中的“strValue”就是一个 String 对象，由 Java 虚拟机隐含地创建。

2）字符串的“+”运算符运算的结果为一个新的 String 对象，示例如下：

```java
String str1 = "Hello";
String str2 = "Java";
String str3 = str1+str2;    // str3引用一个新的String对象
```

3）当 Java 虚拟机加载一个类时，会隐含地创建描述这个类的 Class 实例。

提示：类的加载是指把类的 .class 文件中的二进制数据读入内存中，把它存放在运行时数据区的方法区内，然后在堆区创建一个 java.lang.Class 对象，用来封装类在方法区内的数据结构

无论釆用哪种方式创建对象，Java 虚拟机在创建一个对象时都包含以下步骤：

- 给对象分配内存。
- 将对象的实例变量自动初始化为其变量类型的默认值。
- 初始化对象，给实例变量赋予正确的初始值。

注意：每个对象都是相互独立的，在内存中占有独立的内存地址，并且每个对象都具有自己的生命周期，当一个对象的生命周期结束时，对象就变成了垃圾，由 Java 虚拟机自带的垃圾回收机制处理。

## 6.9new运算符深入剖析

## 6.10匿名对象

每次 new 都相当于开辟了一个新的对象，并开辟了一个新的物理内存空间。如果一个对象只需要使用唯一的一次，就可以使用匿名对象，匿名对象还可以作为实际参数传递。

匿名对象就是没有明确的给出名字的对象，是对象的一种简写形式。一般匿名对象只使用一次，而且匿名对象只在堆内存中开辟空间，而不存在栈内存的引用。

```java
public class Person {
    public String name; // 姓名
    public int age; // 年龄
    // 定义构造方法，为属性初始化
    public Person(String name, int age) {
        this.name = name;
        this.age = age;
    }
    // 获取信息的方法
    public void tell() {
        System.out.println("姓名：" + name + "，年龄：" + age);
    }
    public static void main(String[] args) {
        new Person("张三", 30).tell(); // 匿名对象
    }
}
```

运行结果:

```
姓名：张三，年龄：30
```

在以上程序的主方法中可以发现，直接使用了“new Person("张三",30)”语句，这实际上就是一个匿名对象，与之前声明的对象不同，此处没有任何栈内存引用它，所以此对象使用一次之后就等待被 GC（垃圾收集机制）回收。

匿名对象在实际开发中基本都是作为其他类实例化对象的参数传递的，在后面的java应用部分的很多地方都可以发现其用法

## 6.11访问对象的属性和行为

每个对象都有自己的属性和行为，这些属性和行为在类中体现为成员变量和成员方法，其中成员变量对应对象的属性，成员方法对应对象的行为。

在java中，要引用对象的属性和行为，需要使用点（.）操作符来访问。对象名在圆点左边，而成员变量或成员方法的名称在圆点的右边。语法格式如下：

```
对象名.属性(成员变量)    // 访问对象的属性
对象名.成员方法名()    // 访问对象的方法
```

例如，定义一个 Student 类，创建该类的对象 stu，再对该对象的属性赋值，代码如下：

```
Student stu = new Student();    // 创建 Student 类的对象 stustu.Name = "李子文";    // 调用stu对象的Name属性并赋值stu.Sex = true;    // 调用stu对象的Sex属性并赋值stu.Age = 15;    // 调用stu对象的Age属性并赋值
```

如果一个对象要被使用，则对象必须被实例化，如果一个对象没有被实例化而直接调用了对象中的属性或方法，如下代码所示：

```
Student stu = null;stu.Name = "李子文";stu.Sex = true;stu.Age = 15;
```

则程序运行时会出现以下异常：

```java
Exception in thread "main" java.lang.NullPointerException
```



## 6.12对象的销毁

对象使用完之后需要对其进行清除。对象的清除是指释放对象占用的内存。在创建对象时，用户必须使用 new 操作符为对象分配内存。不过，在清除对象时，由系统自动进行内存回收，不需要用户额外处理。

一个对象被当作垃圾回收的情况主要如下两种。

1）对象的引用超过其作用范围。

```java
{   
	Object o = new Object();
    }
    // 对象o的作用范围，超过这个范围对象将被视为垃圾}
```

2）对象被赋值为 null。

```java
{
    Object o = new Object();
    o = null;    // 对象被赋值为null将被视为垃圾
}
```

在 Java 的 Object 类中还提供了一个 protected 类型的 finalize() 方法，因此任何 Java 类都可以覆盖这个方法，在这个方法中进行释放对象所占有的相关资源的操作。

在 Java 虚拟机的堆区，每个对象都可能处于以下三种状态之一。

1）可触及状态：当一个对象被创建后，只要程序中还有引用变量引用它，那么它就始终处于可触及状态。

2）可复活状态：当程序不再有任何引用变量引用该对象时，该对象就进入可复活状态。在这个状态下，垃圾回收器会准备释放它所占用的内存，在释放之前，会调用它及其他处于可复活状态的对象的 finalize() 方法，这些 finalize() 方法有可能使该对象重新转到可触及状态。

3）不可触及状态：当 Java 虚拟机执行完所有可复活对象的 finalize() 方法后，如果这些方法都没有使该对象转到可触及状态，垃圾回收器才会真正回收它占用的内存。

注意：调用 System.gc() 或者 Runtime.gc() 方法也不能保证回收操作一定执行，它只是提高了 Java 垃圾回收器尽快回收垃圾的可能性。



## 6.13java中的空对象是怎么回事

## 6.14用户修改密码

## 6.15注释(类，方法和字段)

### 类注释

类注释一般必须放在所有的“import”语句之后，类定义之前，主要声明该类可以做什么，以及创建者、创建日期、版本和包名等一些信息。

例如

```java
/**
 * @projectName（项目名称）: project_name
 * @package（包）: package_name.file_name
 * @className（类名称）: type_name
 * @description（类描述）: 一句话描述该类的功能
 * @author（创建人）: user 
 * @createDate（创建时间）: datetime  
 * @updateUser（修改人）: user 
 * @updateDate（修改时间）: datetime
 * @updateRemark（修改备注）: 说明本次修改内容
 * @version（版本）: v1.0
 */
```

提示：以上以`@`开头的标签为javadoc 标记，由`@`和标记类型组成，缺一不可。`@`和标记类型之间有时可以用空格符分隔，但是不推荐用空格符分隔，这样容易出错。

一个类注释的创建人、创建时间和描述是不可缺少的。

```java
/**
 * @author: zhangsan
 * @createDate: 2018/10/28
 * @description: this is the student class.
 */
public class student{
    .................
}
```

### 方法注释

方法注释必须紧靠在方法定义的前面，主要声明方法参数、返回值、异常等信息。除了可以使用通用标签外，还可以使用下列的以`@`开始的标签。

- @param 变量描述：对当前方法的参数部分添加一个说明，可以占据多行。一个方法的所有 @param 标记必须放在一起。
- @return 返回类型描述：对当前方法添加返回值部分，可以跨越多行。
- @throws 异常类描述：表示这个方法有可能抛出异常。



### 字段注释

```java
/**
	这里面写一些文字类注释
*/
```



## 6.16访问控制修饰符

在 java语言中提供了多个作用域修饰符，其中常用的有 public、private、protected、final、abstract、static、transient 和 volatile，这些修饰符有类修饰符、变量修饰符和方法修饰符。本文将详细介绍访问控制修饰符。

信息隐藏是 OOP 最重要的功能之一，也是使用访问修饰符的原因。在编写程序时，有些核心数据往往不希望被用户调用，需要控制这些数据的访问。

通过使用访问控制修饰符来限制对对象私有属性的访问，可以获得 3 个重要的好处。

- 防止对封装数据的未授权访问。
- 有助于保证数据完整性。
- 当类的私有实现细节必须改变时，可以限制发生在整个应用程序中的“连锁反应”。

访问控制符是一组限定类、属性或方法是否可以被程序里的其他部分访问和调用的修饰符。**类的访问控制符只能是空或者 public**，*方法和属性的访问控制符有 4 个*，分别是 public、 private、protected 和 friendly，其中 friendly 是一种没有定义专门的访问控制符的默认情况。访问控制修饰符的权限如表 1 所示。



| 访问范围         | private  | friendly(默认) | protected | public |
| ---------------- | -------- | -------------- | --------- | ------ |
| 同一个类         | 可访问   | 可访问         | 可访问    | 可访问 |
| 同一包中的其他类 | 不可访问 | 可访问         | 可访问    | 可访问 |
| 不同包中的子类   | 不可访问 | 不可访问       | 可访问    | 可访问 |
| 不同包中的非子类 | 不可访问 | 不可访问       | 不可访问  | 可访问 |

访问控制在面向对象技术中处于很重要的地位，合理地使用访问控制符，可以通过降低类和类之间的耦合性（关联性）来降低整个项目的复杂度，也便于整个项目的开发和维护。在 Java 语言中，访问控制修饰符有 4 种。

#### 1. private

用 private 修饰的类成员，只能被该类自身的方法访问和修改，而不能被任何其他类（包括该类的子类）访问和引用。因此，private 修饰符具有最高的保护级别。例如，设 PhoneCard 是电话卡类，电话卡都有密码，因此该类有一个密码域，可以把该类的密码域声明为私有成员。

#### 2. friendly（默认）

如果一个类没有访问控制符，说明它具有默认的访问控制特性。这种默认的访问控制权规定，该类只能被同一个包中的类访问和引用，而不能被其他包中的类使用，即使其他包中有该类的子类。这种访问特性又称为包访问性（package private）。

同样，类内的成员如果没有访问控制符，也说明它们具有包访问性，或称为友元（friend）。定义在同一个文件夹中的所有类属于一个包，所以前面的程序要把用户自定义的类放在同一个文件夹中（Java 项目默认的包），以便不加修饰符也能运行。

#### 3. protected

用保护访问控制符 protected 修饰的类成员可以被三种类所访问：该类自身、与它在同一个包中的其他类以及在其他包中的该类的子类。使用 protected 修饰符的主要作用，是允许其他包中它的子类来访问父类的特定属性和方法，否则可以使用默认访问控制符。

#### 4. public

当一个类被声明为 public 时，它就具有了被其他包中的类访问的可能性，只要包中的其他类在程序中使用 import 语句引入 public 类，就可以访问和引用这个类。

类中被设定为 public 的方法是这个类对外的接口部分，避免了程序的其他部分直接去操作类内的数据，实际就是数据封装思想的体现。每个 Java 程序的主类都必须是 public 类，也是基于相同的原因。

#### 例 1

下面来创建一个示例，演示 Java 中访问控制修饰符的使用。

(1) 新建 Student.java 文件，在该文件中定义不同修饰符的属性和方法，代码如下：

```java
class Student {
    // 姓名，其访问权限为默认(friendly)
    String name;
    // 定义私有变量，身份证号码
    private String idNumber;
    // 定义受保护变量，学号
    protected String no;
    // 定义共有变量，邮箱
    public String email;
    // 定义共有方法，显示学生信息
    public String info() {
        return"姓名："+name+"，身份证号码："+idNumber+"，学号："+no+"，邮箱："+email;
    }
}
```

(2) 新建 StudentTest.java 文件，在该文件中定义 main() 方法，访问 Student 类中的属性并赋值，打印出用户的信息。代码如下：

```java
public class StudentTest {
    public static void main(String[] args) {
        // 创建Student类对象
        Student stu = new Student();
        // 向Student类对象中的属性赋值
        stu.name = "zhht";
        // stu.idNumber="043765290763137806";
        // 这是不允许的。提示stu.idNumber是不可见的，必须注释掉才可运行
        stu.no = "20lil01637";
        stu.email = "zhht@qq.com";
        System.out.println(stu.info());
    }
}
```

在 StudentTest 类中，“stu.idNumber="043765290763137806";”代码行将提示 “The field User.password is not visible”错误信息。将该代码行注释掉再运行 StudentTest.java 文件，输出的内容如下：

```
姓名：zhht，身份证号码：null，学号：20lil01637，邮箱：zhht@qq.com
```

在源文件中创建了两个类，分别为主类 StudentTest 和辅助类 Student，二者在同一个包中。

在辅助类 Student 中，创建了 4 个属性，其访问控制分别为默认的、私有的、受保护的和共有的，除了私有控制符修饰的变量之外，其他的都可以被主类访问，同时创建了一个共有的方法——info()，用于打印用户信息。

在主类 StudentTest 中，创建类 Student 的实例化对象 stu，通过对象 stu 来访问该对象中的属性并赋值，因为 idNumber 属性的修饰符为 private（私有的），因此，在 StudentTest 类中的 main() 方法中无法访问该属性。

## 6.17static关键字

调用静态成员的语法形式如下：

```
类名.静态成员
```

注意：

- static 修饰的成员变量和方法，从属于类。
- 普通变量和方法从属于对象。
- 静态方法不能调用非静态成员，编译会报错。

### 静态变量

类的成员变量可以分为以下两种：

1. 静态变量（或称为类变量），指被 static 修饰的成员变量。
2. 实例变量，指没有被 static 修饰的成员变量。

静态变量与实例变量的区别如下：

1）静态变量

- 运行时，Java 虚拟机只为静态变量分配一次内存，在加载类的过程中完成静态变量的内存分配。
- 在类的内部，可以在任何方法内直接访问静态变量。
- 在其他类中，可以通过类名访问该类中的静态变量。

2）实例变量

- 每创建一个实例，Java 虚拟机就会为实例变量分配一次内存。
- 在类的内部，可以在非静态方法中直接访问实例变量。
- 在本类的静态方法或其他类中则需要通过类的实例对象进行访问。

静态变量在类中的作用如下：

- 静态变量可以被类的所有实例共享，因此静态变量可以作为实例之间的共享数据，增加实例之间的交互性。
- 如果类的所有实例都包含一个相同的常量属性，则可以把这个属性定义为静态常量类型，从而节省内存空间。例如，在类中定义一个静态常量 PI。

```java
public static double PI = 3.14159256;
```

**例一**

```java
public class StaticVar {
    public static String str1 = "Hello";
    public static void main(String[] args) {
        String str2 = "World!";
        // 直接访问str1
        String accessVar1 = str1+str2;
        System.out.println("第 1 次访问静态变量，结果为："+accessVar1);
        // 通过类名访问str1
        String accessVar2 = StaticVar.str1+str2;
        System.out.println("第 2 次访问静态变量，结果为："+accessVar2);
        // 通过对象svt1访问str1
        StaticVar svt1 = new StaticVar();
        svt1.str1 = svt1.str1+str2;
        String accessVar3 = svt1.str1;
        System.out.println("第3次访向静态变量，结果为："+accessVar3);
        // 通过对象svt2访问str1
        StaticVar svt2 = new StaticVar();
        String accessVar4 = svt2.str1+str2;
        System.out.println("第 4 次访问静态变量，结果为："+accessVar4);
    }
}
```

运行结果如下

```
第 1 次访问静态变量，结果为：HelloWorld!
第 2 次访问静态变量，结果为：HelloWorld!
第 3 次访向静态变量，结果为：HelloWorld!
第 4 次访问静态变量，结果为：HelloWorld!World!
```

从运行结果可以看出，在类中定义静态的属性（成员变量），在 main() 方法中可以直接访问，也可以通过类名访问，还可以通过类的实例对象来访问。

注意：静态变量是被多个实例所共享的。

### 静态方法

与成员变量类似，成员方法也可以分为以下两种：

1. 静态方法（或称为类方法），指被 static 修饰的成员方法。
2. 实例方法，指没有被 static 修饰的成员方法。

静态方法与实例方法的区别如下：

- 静态方法不需要通过它所属的类的任何实例就可以被调用，因此在静态方法中不能使用 this 关键字，也不能直接访问所属类的实例变量和实例方法，但是可以直接访问所属类的静态变量和静态方法。另外，和 this 关键字一样，super 关键字也与类的特定实例相关，所以在静态方法中也不能使用 super 关键字。
- 在实例方法中可以直接访问所属类的静态变量、静态方法、实例变量和实例方法。

#### 例 2

创建一个带静态变量的类，添加几个静态方法对静态变量的值进行修改，然后在 main( ) 方法中调用静态方法并输出结果。

```java
public class StaticMethod {
    public static int count = 1;    // 定义静态变量count
    public int method1() {    
        // 实例方法method1
        count++;    // 访问静态变量count并赋值
        System.out.println("在静态方法 method1()中的 count="+count);    // 打印count
        return count;
    }
    public static int method2() {    
        // 静态方法method2
        count += count;    // 访问静态变量count并赋值
        System.out.println("在静态方法 method2()中的 count="+count);    // 打印count
        return count;
    }
    public static void PrintCount() {    
        // 静态方法PrintCount
        count += 2;
        System.out.println("在静态方法 PrintCount()中的 count="+count);    // 打印count
    }
    public static void main(String[] args) {
        StaticMethod sft = new StaticMethod();
        // 通过实例对象调用实例方法
        System.out.println("method1() 方法返回值 intro1="+sft.method1());
        // 直接调用静态方法
        System.out.println("method2() 方法返回值 intro1="+method2());
        // 通过类名调用静态方法，打印 count
        StaticMethod.PrintCount();
    }
}
```

运行该程序后的结果如下所示。

```java
在静态方法 method1()中的 count=2
method1() 方法返回值 intro1=2
在静态方法 method2()中的 count=4
method2() 方法返回值 intro1=4
在静态方法 PrintCount()中的 count=6
```

在该程序中，静态变量 count 作为实例之间的共享数据，因此在不同的方法中调用 count，值是不一样的。从该程序中可以看出，在静态方法 method1() 和 PrintCount() 中是不可以调用非静态方法 method1() 的，而在 method1() 方法中可以调用静态方法 method2() 和 PrintCount()。

在访问非静态方法时，需要通过实例对象来访问，而在访问静态方法时，可以直接访问，也可以通过类名来访问，还可以通过实例化对象来访问。

### 静态代码块

静态代码块指 Java 类中的 static{ } 代码块，主要用于初始化类，为类的静态变量赋初始值，提升程序性能。

静态代码块的特点如下：

- 静态代码块类似于一个方法，但它不可以存在于任何方法体中。
- 静态代码块可以置于类中的任何地方，类中可以有多个静态初始化块。 
- Java 虚拟机在加载类时执行静态代码块，所以很多时候会将一些只需要进行一次的初始化操作都放在 static 代码块中进行。
- 如果类中包含多个静态代码块，则 Java 虚拟机将按它们在类中出现的顺序依次执行它们，每个静态代码块只会被执行一次。
- 静态代码块与静态方法一样，不能直接访问类的实例变量和实例方法，而需要通过类的实例对象来访问。

#### 例 3

编写一个 Java 类，在类中定义一个静态变量，然后使用静态代码块修改静态变量的值。最后在 main() 方法中进行测试和输出。

```java
public class StaticCode {
    public static int count = 0;
    {
        count++;
        System.out.println("非静态代码块 count=" + count);
    }
    static {
        count++;
        System.out.println("静态代码块1 count=" + count);
    }
    static {
        count++;
        System.out.println("静态代码块2 count=" + count);
    }
    public static void main(String[] args) {
        System.out.println("*************** StaticCode1 执行 ***************");
        StaticCode sct1 = new StaticCode();
        System.out.println("*************** StaticCode2 执行 ***************");
        StaticCode sct2 = new StaticCode();
    }
}
```

如上述示例，为了说明静态代码块只被执行一次，特地添加了非静态代码块作为对比，并在主方法中创建了两个类的实例对象。上述示例的执行结果为：

```java
静态代码块1 count=1
静态代码块2 count=2
*************** StaticCode1 执行 ***************
非静态代码块 count=3
*************** StaticCode2 执行 ***************
非静态代码块 count=4
```

上述代码中 { } 代码块为非静态代码块，非静态代码块是在创建对象时自动执行的代码，不创建对象不执行该类的非静态代码块。代码域中定义的变量都是局部的，只有域中的代码可以调用。 

## 6.18静态导入

在 JDK 1.5 之后增加了一种静态导入的语法，用于导入指定类的某个静态成员变量、方法或全部的静态成员变量、方法。如果一个类中的方法全部是使用 static 声明的静态方法，则在导入时就可以直接使用 import static 的方式导入。

静态导入使用 import static 语句，静态导入也有两种语法，分别用于导入指定类的单个静态成员变量、方法和全部静态成员变量、方法，其中导入指定类的单个静态成员变量、方法的语法格式如下：

```
import static package.ClassName.fieldName|methodName;
```

上面语法导入 package.ClassName 类中名为 fieldName 的静态成员变量或者名为 methodName 的静态方法。例如，可以使用`import static java.lang.System.out;`语句来导入 java.lang.System 类的 out 静态成员变量。

导入指定类的全部静态成员变量、方法的语法格式如下：

```
import static package.ClassName.*;
```

上面语法中的星号只能代表静态成员变量或方法名。

import static 语句也放在 [Java](http://c.biancheng.net/java/) 源文件的 package 语句（如果有的话）之后、类定义之前，即放在与普通 import 语句相同的位置，而且 import 语句和 import static 语句之间没有任何顺序要求。

所谓静态成员变量、静态方法其实就是前面介绍的类变量、类方法，它们都需要使用 static 修饰，而 static 在很多地方都被翻译为静态，因此 import static 也就被翻译成了 “静态导入”。其实完全可以抛开这个翻译，用一句话来归纳 import 和 import static 的作用，使用 import 可以省略写包名，而使用 import static 可以省略类名。

下面程序使用 import static 语句来导入 java.lang.System 类下的全部静态成员变量，从而可以将程序简化成如下形式。

```java
import static java.lang.System.*;
import static java.lang.Math.*;
public class StaticImportTest {
    public static void main(String[] args) {
        // out是java.lang.System类的静态成员变量，代表标准输出
        // PI是java.lang.Math类的静态成员变量，表示π常量
        out.println(PI);
        // 直接调用Math类的sqrt静态方法，返回256的正平方根
        out.println(sqrt(256));
    }
}
```

从上面程序不难看出，import 和 import static 的功能非常相似，只是它们导入的对象不一样而已。import 语句和 import static 语句都是用于减少程序中代码编写量的。

## 6.19static的常见问题和使用误区

## 6.20final修饰符

final 修饰的变量即成为常量，只能赋值一次，但是 final 所修饰局部变量和成员变量有所不同。

1. final 修饰的局部变量必须使用之前被赋值一次才能使用。
2. final 修饰的成员变量在声明时没有赋值的叫“空白 final 变量”。空白 final 变量必须在构造方法或静态代码块中初始化。

```java
public class FinalDemo {
    void doSomething() {
        // 没有在声明的同时赋值
        final int e;
        // 只能赋值一次
        e = 100;
        System.out.print(e);
        // 声明的同时赋值
        final int f = 200;
    }
    // 实例常量
    final int a = 5; // 直接赋值
    final int b; // 空白final变量
    // 静态常量
    final static int c = 12;// 直接赋值
    final static int d; // 空白final变量
    // 静态代码块
    static {
        // 初始化静态变量
        d = 32;
    }
    // 构造方法
    FinalDemo() {
        // 初始化实例变量
        b = 3;
        // 第二次赋值，会发生编译错误
        // b = 4;
    }
}
```

### final 修饰基本类型变量和引用类型变量的区别

当使用 final 修饰基本类型变量时，不能对基本类型变量重新赋值，因此基本类型变量不能被改变。 但对于引用类型变量而言，它保存的仅仅是一个引用，final 只保证这个引用类型变量所引用的地址不会改变，即一直引用同一个对象，但这个对象完全可以发生改变。

```java
import java.util.Arrays;
class Person {
    private int age;
    public Person() {
    }
    // 有参数的构造器
    public Person(int age) {
        this.age = age;
    }
    // 省略age的setter和getter方法
    // age 的 setter 和 getter 方法
}
public class FinalReferenceTest {
    public static void main(String[] args) {
        // final修饰数组变量，iArr是一个引用变量
        final int[] iArr = { 5, 6, 12, 9 };
        System.out.println(Arrays.toString(iArr));
        // 对数组元素进行排序，合法
        Arrays.sort(iArr);
        System.out.println(Arrays.toString(iArr));
        // 对数组元素赋值，合法
        iArr[2] = -8;
        System.out.println(Arrays.toString(iArr));
        // 下面语句对iArr重新赋值,非法
        // iArr = null;
        // final修饰Person变量，p是一个引用变量
        final Person p = new Person(45);
        // 改变Person对象的age实例变量，合法
        p.setAge(23);
        System.out.println(p.getAge());
        // 下面语句对P重新赋值，非法
        // p = null;
    }
}
```

使用final修饰的引用数据类型不能重新赋值，但是可以改变引用类型变量所引用的对象的内容

### final修饰方法

final 修饰的方法不可被重写，如果出于某些原因，不希望子类重写父类的某个方法，则可以使用 final 修饰该方法。

Java 提供的 Object 类里就有一个 final 方法 getClass()，因为 Java 不希望任何类重写这个方法，所以使用 final 把这个方法密封起来。但对于该类提供的 toString() 和 equals() 方法，都允许子类重写，因此没有使用 final 修饰它们。



对于一个 private 方法，因为它仅在当前类中可见，其子类无法访问该方法，所以子类无法重写该方法——如果子类中定义一个与父类 private 方法有相同方法名、相同形参列表、相同返回值类型的方法，也不是方法重写，只是重新定义了一个新方法。因此，即使使用 final 修饰一个 private 访问权限的方法，依然可以在其子类中定义与该方法具有相同方法名、相同形参列表、相同返回值类型的方法。

**例如**

```java
public class PrivateFinalMethodTest {
    private final void test() {
    }
}
class Sub extends PrivateFinalMethodTest {
    // 下面的方法定义不会出现问题
    public void test() {
    }
}
```

final修饰的方法可以重载

### final修饰类

final 修饰的类不能被继承。当子类继承父类时，将可以访问到父类内部数据，并可通过重写父类方法来改变父类方法的实现细节，这可能导致一些不安全的因素。为了保证某个类不可被继承，则可以使用 final 修饰这个类。

下面代码示范了 final 修饰的类不可被继承。

```java
final class SuperClass {
}
class SubClass extends SuperClass {    //编译错误
}
```

因为 SuperClass 类是一个 final 类，而 SubClass 试图继承 SuperClass 类，这将会引起编译错误

## 6.21main()方法

使用 main() 方法时应该注意如下几点：

- 访问控制权限是公有的（public）。
- main() 方法是静态的。如果要在 main() 方法中调用本类中的其他方法，则该方法也必须是静态的，否则需要先创建本类的实例对象，然后再通过对象调用成员方法。
- main() 方法没有返回值，只能使用 void。
- main() 方法具有一个字符串数组参数，用来接收执行 Java 程序的命令行参数。命令行参数作为字符串，按照顺序依次对应字符串数组中的元素。
- 字符串中数组的名字（代码中的 args）可以任意设置，但是根据习惯，这个字符串数组的名字一般和 Java 规范范例中 main() 参数名保持一致，命名为 args，而方法中的其他内容都是固定不变的。
- main() 方法定义必须是“public static void main(String[] 字符串数组参数名)”。
- 一个类只能有一个 main() 方法，这是一个常用于对类进行单元测试（对软件中的最小可测试单元进行检查和验证）的技巧。

演示如何在main()方法中调用本类中的静态和非静态方法

```java
public class Student {
    public void Speak1() {
        System.out.println("你好!");
    }
    public static void Speak2() {
        System.out.println("Java!");
    }
    public static void main(String[] args) {
        // Speak1();    // 错误调用
        Speak2();    // 可以直接调用静态方法Speak2()
        Student t = new Student();
        t.Speak1();    // 调用非静态方法，需要通过类的对象来调用
    }
}
```



## 6.22java中的main方法为什么是固定不变的

## 6.23java方法的可变参数

声明可变参数的语法格式如下：

```java
methodName({paramList},paramType…paramName)
```

其中，methodName 表示方法名称；paramList 表示方法的固定参数列表；paramType 表示可变参数的类型；… 是声明可变参数的标识；paramName 表示可变参数名称。

**注意**：可变参数必须定义在参数列表的最后

例如

```java
public class StudentTestMethod {
    // 定义输出考试学生的人数及姓名的方法
    public void print(String...names) {
        int count = names.length;    // 获取总个数
        System.out.println("本次参加考试的有"+count+"人，名单如下：");
        for(int i = 0;i < names.length;i++) {
            System.out.println(names[i]);
        }
    }
    public static void main(String[] args) {
        // TODO Auto-generated method stub
        StudentTestMethod student = new StudentTestMethod();
        student.print("张强","李成","王勇");    // 传入3个值
        student.print("马丽","陈玲");
    }
}
```

其实在方法内部可变参数被当作一个数组

```java
本次参加考试的有3人，名单如下：
张强
李成
王勇
本次参加考试的有2人，名单如下：
马丽
陈玲
```



## 6.24java的构造方法

是类中的一个热书方法，用来初始化的一个新对象，在创建对象(new运算符)之后自动调用，java中每一个类中都有一个默认的构造方法

Java 构造方法有以下特点：

- 方法名必须与类名相同
- 可以有 0 个、1 个或多个参数
- 没有任何返回值，包括 void
- 默认返回类型就是对象类型本身
- 只能与 new 运算符结合使用



如果构造方法定义了返回类型，这是编译器不会报错但是会把他当作一个普通方法看待



类的构造方法是有返回值的，当使用 new 关键字来调用构造方法时，构造方法返回该类的实例，可以把这个类的实例当成构造器的返回值，因此构造器的返回值类型总是当前类，无须定义返回值类型。但必须注意不要在构造方法里使用 return 来返回当前类的对象，因为构造方法的返回值是隐式的。



注意：构造方法不能被 static、final、synchronized、abstract 和 native（类似于 abstract）修饰。构造方法用于初始化一个新对象，所以用 static 修饰没有意义。构造方法不能被子类继承，所以用 final 和 abstract 修饰没有意义。多个线程不会同时创建内存地址相同的同一个对象，所以用 synchronized 修饰没有必要。



在一个类中，与类名相同的方法就是构造方法。每个类可以具有多个构造方法，但要求它们各自包含不同的方法参数。

构造器主要有无参构造器和有参构造器，示例如下

```java
public class MyClass{
	private int m;
	MyClass(){
	//定义无参的构造方法
	m=0;
	}
	MyClass(int m){
		this.m = m;
	}

}
```

在一个类中定义多个具有不同参数的同名方法，这就是方法的重载。这两个构造方法的名称都与类名相同，均为 MyClass。在实例化该类时可以调用不同的构造方法进行初始化。

注意：类的构造方法不是要求必须定义的。如果在类中没有定义任何一个构造方法，则 Java 会自动为该类生成一个默认的构造方法。默认的构造方法不包含任何参数，并且方法体为空。如果类中显式地定义了一个或多个构造方法，则 Java 不再提供默认构造方法。



例子

演示使用不同的初始化行为创建类的对象

```java
public class Worker {
    public String name;    // 姓名
    private int age;    // 年龄
    // 定义带有一个参数的构造方法
    public Worker(String name) {
        this.name = name;
    }
    // 定义带有两个参数的构造方法
    public Worker(String name,int age) {
        this.name = name;
        this.age = age;
    }
    public String toString() {
        return "大家好！我是新来的员工，我叫"+name+"，今年"+age+"岁。";
    }
}
public class TestWorker {
    public static void main(String[] args) {
        System.out.println("-----------带有一个参数的构造方法-----------");
        // 调用带有一个参数的构造方法
        Worker worker1 = new Worker("张强");
        System.out.println(worker1);
        System.out.println("-----------带有两个参数的构造方法------------");
        // 调用带有两个参数的构造方法
        Worker worker2 = new Worker("李丽",25);
        System.out.println(worker2);
    }
}
```

输出结果

```java
-----------带有一个参数的构造方法-----------
大家好！我是新来的员工，我叫张强，今年0岁。
-----------带有两个参数的构造方法------------
大家好！我是新来的员工，我叫李丽，今年25岁。
```





## 6.25包

三个作用：

1. 区分相同名称的类
2. 能够较好的管理大量的类
3. 控制访问范围

### 包定义

Java 中使用 package 语句定义包，package 语句应该放在源文件的第一行，在每个源文件中只能有一个包定义语句，并且 package 语句适用于所有类型（类、接口、枚举和注释）的文件。定义包语法格式如下：

```
package 包名;
```

Java 包的命名规则如下：

- 包名全部由小写字母（多个单词也全部小写）。
- 如果包名包含多个层次，每个层次用“.”分割。
- 包名一般由倒置的域名开头，比如 com.baidu，不要有 www。
- 自定义包不能 java 开头。

### 包导入

如果使用不同包中的其它类，需要使用该类的全名（包名+类名）。代码如下：

```
example.Test test = new example.Test();
```

其中，example 是包名，Test 是包中的类名，test 是类的对象。





## 6.26 使用自定义包

## 6.27递归算法

自身调用自身称为递归

下面是一个例子

```java
public class Factorial{
	int fact（int n）{
		int result;
		if(n == 1){
			return 1;
			
		}
		result = fact(n - 1) * n;
		return result;
	}
}
class Recursion {
    public static void main(String args[]) {
        Factorial f = new Factorial();
        System.out.println("3的阶乘是 " + f.fact(3));
        System.out.println("4的阶乘是 " + f.fact(4));
        System.out.println("5的阶乘是 " + f.fact(5));
    }
}
```

输出结果是

```java
3的阶乘是 6
4的阶乘是 24
5的阶乘是 120
```





# 7.Java继承和多态

## 7.1封装

封装将类的某些信息隐藏在类内部，不允许外部程序直接访问，只能通过该类提供的方法来实现对隐藏信息的操作和访问。

封装的特点：

- 只能通过规定的方法访问数据
- 隐藏类的实例细节，方便修改和实现



实现封装的具体步骤如下：

1. 修改属性的可见性来限制对属性的访问，一般设为 private。
2. 为每个属性创建一对赋值（setter）方法和取值（getter）方法，一般设为 public，用于属性的读写。
3. 在赋值和取值方法中，加入属性控制语句（对属性值的合法性进行判断）。

**示例：下面是一个员工类的封装过程**

```java
public class Employee {
    private String name; // 姓名
    private int age; // 年龄
    private String phone; // 联系电话
    private String address; // 家庭住址
    public String getName() {
        return name;
    }
    public void setName(String name) {
        this.name = name;
    }
    public int getAge() {
        return age;
    }
    public void setAge(int age) {
        // 对年龄进行限制
        if (age < 18 || age > 40) {
            System.out.println("年龄必须在18到40之间！");
            this.age = 20; // 默认年龄
        } else {
            this.age = age;
        }
    }
    public String getPhone() {
        return phone;
    }
    public void setPhone(String phone) {
        this.phone = phone;
    }
    public String getAddress() {
        return address;
    }
    public void setAddress(String address) {
        this.address = address;
    }
}
```

编写测试类 EmployeeTest，在该类的 main() 方法中调用 Employee 属性的 setXxx() 方法对其相应的属性进行赋值，并调用 getXxx() 方法访问属性，代码如下：

```java
public class EmployeeTest {
    public static void main(String[] args) {
        Employee people = new Employee();
        people.setName("王丽丽");
        people.setAge(35);
        people.setPhone("13653835964");
        people.setAddress("河北省石家庄市");
        System.out.println("姓名：" + people.getName());
        System.out.println("年龄：" + people.getAge());
        System.out.println("电话：" + people.getPhone());
        System.out.println("家庭住址：" + people.getAddress());
    }
}
```



## 7.2继承

java中的继承就是在已有的类上进行扩展，从而产生新的类，已存在的类称为父类，基类或者超类；而新产生的叫子类或者派生类，子类中不仅包含父类中的属性和方法还可以增加新的属性和方法



java中继承的语法格式

```java
修饰符 class class_name extends extend_class{
	//类的主体
}
```







**java中遵循单继承规则**

Java不支持多继承，只允许一个子类直接继承另一个类，即一个子类只能有一个直接父类，extends关键字后面只能有一个类名

但是一个子类可以间接有多个父类

如果定义一个java类时并没有显式的指出这个类的父类，那这个类继承java.lang.Object类

使用继承的注意点：

1. 子类一般比父类包含更多的属性和方法。
2. 父类中的 private 成员在子类中是不可见的，因此在子类中不能直接使用它们。
3. 父类和其子类间必须存在“是一个”即“is-a”的关系，否则不能用继承。但也并不是所有符合“is-a”关系的都应该用继承。例如，正方形是一个矩形，但不能让正方形类来继承矩形类，因为正方形不能从矩形扩展得到任何东西。正确的继承关系是正方形类继承图形类。
4. Java 只允许单一继承（即一个子类只能有一个直接父类），C++ 可以多重继承（即一个子类有多个直接父类）。

#### 继承的优缺点

在面向对象语言中，继承是必不可少的、非常优秀的语言机制，它有如下优点：

1. 实现代码共享，减少创建类的工作量，使子类可以拥有父类的方法和属性。
2. 提高代码维护性和可重用性。
3. 提高代码的可扩展性，更好的实现父类的方法。

自然界的所有事物都是优点和缺点并存的，继承的缺点如下：

1. 继承是侵入性的。只要继承，就必须拥有父类的属性和方法。
2. 降低代码灵活性。子类拥有父类的属性和方法后多了些约束。
3. 增强代码耦合性（开发项目的原则为高内聚低耦合）。当父类的常量、变量和方法被修改时，需要考虑子类的修改，有可能会导致大段的代码需要重构。

## 7.3super关键字

super关键字的功能

- 在子类的构造方法中显式的调用父类构造方法
- 访问父类的成员方法和变量

### super访问父类构造方法

基本格式如下

```
super(parameter-list);
```

super( ) 必须是在子类构造方法的方法体的第一行。

**例一**

声明父类Person类中定义两个构造方法

```java
public class Person {
    public Person(String name, int age) {
    }
    public Person(String name, int age, String sex) {
    }
}
```

子类 Student 继承了 Person 类，使用 super 语句来定义 Student 类的构造方法。示例代码如下：

```java
public class Student extends Person {
    public Student(String name, int age, String birth) {
        super(name, age); // 调用父类中含有2个参数的构造方法
    }
    public Student(String name, int age, String sex, String birth) {
        super(name, age, sex); // 调用父类中含有3个参数的构造方法
    }
}
```

### super访问父类成员

语法格式如下

```java
super.member
```

member是父类中的属性和方法，使用super访问弗雷德属性和方法不用位于第一行



**super调用成员属性**

```java
class Person {
    int age = 12;
}
class Student extends Person {
    int age = 18;
    void display() {
        System.out.println("学生年龄：" + super.age);
    }
}
class Test {
    public static void main(String[] args) {
        Student stu = new Student();
        stu.display();
    }
}
```

输出结果是

```java
学生年龄：12
```





**super调用成员方法**

当父类和子类具有相同的方法时可以用super调用

```java
class Person {
    void message() {
        System.out.println("This is person class");
    }
}
class Student extends Person {
    void message() {
        System.out.println("This is student class");
    }
    void display() {
        message();
        super.message();
    }
}
class Test {
    public static void main(String args[]) {
        Student s = new Student();
        s.display();
    }
}
```

输出结果是：

```java
This is student class
This is person class
```

### super和this的区别

this指的是当前对象的引用，super是当前对象的父对象引用

super 关键字的用法：

- super.父类属性名：调用父类中的属性
- super.父类方法名：调用父类中的方法
- super()：调用父类的无参构造方法
- super(参数)：调用父类的有参构造方法


如果构造方法的第一行代码不是 this() 和 super()，则系统会默认添加 super()。

this 关键字的用法：

- this.属性名：表示当前对象的属性
- this.方法名(参数)：表示调用当前对象的方法

## 7.4对象的类型转换

对象类型转换是指存在继承关系的对象，不是任意类型的对象，否则抛出强制类型转换异常

### 向上转型

父类引用子类对象为向上转型

```java
fatherClass obj = new sonClass();
```

其中，fatherClass 是父类名称或接口名称，obj 是创建的对象，sonClass 是子类名称。

向上转型就是把子类对象直接赋给父类引用，不用强制转换。使用向上转型可以调用父类类型中的所有成员，不能调用子类类型中特有成员，最终运行效果看子类的具体实现。

### 向下转型

子类对象指向父类引用为向下转型，格式如下

```java
sonClass obj = (sonClass)fatherClass;
```

其中，fatherClass 是父类名称，obj 是创建的对象，sonClass 是子类名称。

向下转型可以调用子类类型中所有的成员，不过需要注意的是如果父类引用对象指向的是子类对象，那么在向下转型的过程中是安全的，也就是编译是不会出错误。但是如果父类引用对象是父类本身，那么在向下转型的过程中是不安全的，编译不会出错，但是运行时会出现我们开始提到的 Java 强制类型转换异常，一般使用 instanceof 运算符来避免出此类错误。

**例一**

父类 Animal 和子类 Cat 中都定义了实例变量 name、静态变量 staticName、实例方法 eat() 和静态方法 staticEat()。此外，子类 Cat 中还定义了实例变量 str 和实例方法 eatMethod()。

父类 Animal 的代码如下：

```java
public class Animal {
    public String name = "Animal：动物";
    public static String staticName = "Animal：可爱的动物";
    public void eat() {
        System.out.println("Animal：吃饭");
    }
    public static void staticEat() {
        System.out.println("Animal：动物在吃饭");
    }
}
```



子类Cat的代码如下

```java
public class Cat extends Animal {
    public String name = "Cat：猫";
    public String str = "Cat：可爱的小猫";
    public static String staticName = "Dog：我是喵星人";
    public void eat() {
        System.out.println("Cat：吃饭");
    }
    public static void staticEat() {
        System.out.println("Cat：猫在吃饭");
    }
    public void eatMethod() {
        System.out.println("Cat：猫喜欢吃鱼");
    }
    public static void main(String[] args) {
        Animal animal = new Cat();
        Cat cat = (Cat) animal; // 向下转型
        System.out.println(animal.name); // 输出Animal类的name变量
        System.out.println(animal.staticName); // 输出Animal类的staticName变量
        animal.eat(); // 输出Cat类的eat()方法
        animal.staticEat(); // 输出Animal类的staticEat()方法
        System.out.println(cat.str); // 调用Cat类的str变量
        cat.eatMethod(); // 调用Cat类的eatMethod()方法
    }
}
```

通过引用类型变量来访问所引用对象的属性和方法时，Java 虚拟机将采用以下绑定规则：

- 实例方法与引用变量实际引用的对象的方法进行绑定，这种绑定属于动态绑定，因为是在运行时由 Java 虚拟机动态决定的。例如，animal.eat() 是将 eat() 方法与 Cat 类绑定。
- 静态方法与引用变量所声明的类型的方法绑定，这种绑定属于静态绑定，因为是在编译阶段已经做了绑定。例如，animal.staticEat() 是将 staticEat() 方法与 Animal 类进行绑定。
- 成员变量（包括静态变量和实例变量）与引用变量所声明的类型的成员变量绑定，这种绑定属于静态绑定，因为在编译阶段已经做了绑定。例如，animal.name 和 animal.staticName 都是与 Animal 类进行绑定。

对于 Cat 类，运行时将会输出如下结果：

```java
Animal：动物
Animal：可爱的动物
Cat：吃饭
Animal：动物在吃饭
Cat：可爱的小猫
Cat：猫喜欢吃鱼
```







### 强制类型转换

对于向下转型必须使用强制类型转换；对于向上转型不必使用强制转换

类型强制转换时想运行成功就必须保证父类引用指向的对象一定是该子类对象，最好使用 instanceof 运算符判断后，再强转，例如：

```java
Animal animal = new Cat();
if (animal instanceof Cat) {
    Cat cat = (Cat) animal; // 向下转型
    ...
}
```



## 7.5方法重载

**如果同一个类中包含了两个或两个以上方法名相同的方法，但形参列表不同，这种情况被称为方法重载（overload）。**

·



方法重载的要求是两同一不同：即同一个类中的方法名相同，参数列表不同，至于方法返回值，修饰符等等与方法重载没有任何关系



## 7.6方法重写

在子类中如果创建了一个与父类中相同名称、相同返回值类型、相同参数列表的方法，只是方法体中的实现不同，以实现不同于父类的功能，这种方式被称为方法重写（override），又称为方法覆盖。当父类中的方法无法满足子类需求或子类具有特有功能的时候，需要方法重写。



在重写方法时，需要遵循下面的规则：

- 参数列表必须完全与被重写的方法参数列表相同。
- 返回的类型必须与被重写的方法的返回类型相同  java1.5 版本之前返回值类型必须一样，之后的 Java 版本放宽了限制，返回值类型必须小于或者等于父类方法的返回值类型）。
- 访问权限不能比父类中被重写方法的访问权限更低（public>protected>default>private）。
- 重写方法一定不能抛出新的检査异常或者比被重写方法声明更加宽泛的检査型异常。

另外还要注意以下几条：

- 重写的方法可以使用 @Override 注解来标识。
- 父类的成员方法只能被它的子类重写。
- 声明为 final 的方法不能被重写。
- 声明为 static 的方法不能被重写，但是能够再次声明。
- 构造方法不能被重写。
- 子类和父类在同一个包中时，子类可以重写父类的所有方法，除了声明为 private 和 final 的方法。
- 子类和父类不在同一个包中时，子类只能重写父类的声明为 public 和 protected 的非 final 方法。
- 如果不能继承一个方法，则不能重写这个方法。



## 7.7多态性

**指的是在父类中定义的属性和方法在被子类继承后，可以具有不同的数据类型或表现出不同的行为**



对面向对象来说，多态分为编译时多态 和运行时多态



实现多态有 3 个必要条件：继承、重写和向上转型



**例一**

1）创建 Figure 类，在该类中首先定义存储二维对象的尺寸，然后定义有两个参数的构造方法，最后添加 area() 方法，该方法计算对象的面积。代码如下：

```java
public class Figure {
    double dim1;
    double dim2;
    Figure(double d1, double d2) {
        // 有参的构造方法
        this.dim1 = d1;
        this.dim2 = d2;
    }
    double area() {
        // 用于计算对象的面积
        System.out.println("父类中计算对象面积的方法，没有实际意义，需要在子类中重写。");
        return 0;
    }
}
```

2）创建继承自 Figure 类的 Rectangle 子类，该类调用父类的构造方法，并且重写父类中的 area() 方法。代码如下：

```java
public class Rectangle extends Figure {
    Rectangle(double d1, double d2) {
        super(d1, d2);
    }
    double area() {
        System.out.println("长方形的面积：");
        return super.dim1 * super.dim2;
    }
}
```

3）创建继承自 Figure 类的 Triangle 子类，该类与 Rectangle 相似。代码如下：

```java
public class Triangle extends Figure {
    Triangle(double d1, double d2) {
        super(d1, d2);
    }
    double area() {
        System.out.println("三角形的面积：");
        return super.dim1 * super.dim2 / 2;
    }
}
```

4）创建 Test 测试类，在该类的 main() 方法中首先声明 Figure 类的变量 figure，然后分别为 figure 变量指定不同的对象，并调用这些对象的 area() 方法。代码如下：

```java
public class Test {
    public static void main(String[] args) {
        Figure figure; // 声明Figure类的变量
        figure = new Rectangle(9, 9);
        System.out.println(figure.area());
        System.out.println("===============================");
        figure = new Triangle(6, 8);
        System.out.println(figure.area());
        System.out.println("===============================");
        figure = new Figure(10, 10);
        System.out.println(figure.area());
    }
}
```

5）执行上述代码，输出结果如下：

```java
长方形的面积：
81.0
===============================
三角形的面积：
24.0
===============================
父类中计算对象面积的方法，没有实际意义，需要在子类中重写。
0.0
```

## 7.8instanceof关键字

严格来说是一个双目运算符，由于是由字母组成也是Java的关键字，可以用来判断一个对象是否为一个类或是接口或是抽象类或是父类，

语法格式如下

```java
boolean result = obj instanceof Class
```

其中，obj 是一个对象，Class 表示一个类或接口。obj 是 class 类（或接口）的实例或者子类实例时，结果 result 返回 true，否则返回 false。

下面介绍 Java instanceof 关键字的几种用法。

#### 1）声明一个 class 类的对象，判断 obj 是否为 class 类的实例对象（很普遍的一种用法），如以下代码：

```java
Integer integer = new Integer(1);
System.out.println(integer instanceof Integer);  // true
```



#### 2）声明一个 class 接口实现类的对象 obj，判断 obj 是否为 class 接口实现类的实例对象，如以下代码：

Java 集合中的 List 接口有个典型实现类 ArrayList。

```java
public class ArrayList<E> extends AbstractList<E>
    implements List<E>, RandomAccess, Cloneable, java.io.Serializable
```

所以我们可以用 instanceof 运算符判断 ArrayList 类的对象是否属于 List 接口的实例，如果是返回 true，否则返回 false。

```java
ArrayList arrayList = new ArrayList();
System.out.println(arrayList instanceof List);  // true
```

或者反过来也是返回 true

```java
List list = new ArrayList();
System.out.println(list instanceof ArrayList);  // true
```

#### 3）obj 是 class 类的直接或间接子类

我们新建一个父类 Person.class，代码如下：

```java
public class Person {
}
```

创建 Person 的子类 Man，代码如下：

```java
public class Man extends Person {
}
```

测试代码如下：

```java
Person p1 = new Person();
Person p2 = new Man();
Man m1 = new Man();
System.out.println(p1 instanceof Man);    // false
System.out.println(p2 instanceof Man);    // true
System.out.println(m1 instanceof Man);    // true
```

**注意：**

obj只能是引用数据类型不能是基本数据类型



当obj为null时直接返回false因为null没有引用任何对象



当class为null时会发生编译错误，所以class只能是类或者接口



## 7.9抽象类( abstract)

Java有两种类：具体类和抽象类

语法格式如下

```java
<abstract>class<class_name> {
    <abstract><type><method_name>(parameter-iist);
}
```

其中，abstract 表示该类或该方法是抽象的；class_name 表示抽象类的名称；method_name 表示抽象方法名称，parameter-list 表示方法参数列表。

如果一个方法使用 abstract 来修饰，则说明该方法是抽象方法，抽象方法只有声明没有实现。需要注意的是 abstract 关键字只能用于普通方法，不能用于 static 方法或者构造方法中。



抽象方法的 3 个特征如下：

1. 抽象方法没有方法体
2. 抽象方法必须存在于抽象类中
3. 子类重写父类时，必须重写父类所有的抽象方法



注意：在使用 abstract 关键字修饰抽象方法时不能使用 private 修饰，因为抽象方法必须被子类重写，而如果使用了 private 声明，则子类是无法重写的。

抽象类的定义和使用规则如下：

1. 抽象类和抽象方法都要使用 abstract 关键字声明。
2. 如果一个方法被声明为抽象的，那么这个类也必须声明为抽象的。而一个抽象类中，可以有 0~n 个抽象方法，以及 0~n 个具体方法。
3. 抽象类不能实例化，也就是不能使用 new 关键字创建对象。



#### 例 1

不同几何图形的面积计算公式是不同的，但是它们具有的特性是相同的，都具有长和宽这两个属性，也都具有面积计算的方法。那么可以定义一个抽象类，在该抽象类中含有两个属性（width 和 height）和一个抽象方法 area( )，具体步骤如下。

1）首先创建一个表示图形的抽象类 Shape，代码如下所示。

```java
public abstract class Shape {
    public int width; // 几何图形的长
    public int height; // 几何图形的宽
    public Shape(int width, int height) {
        this.width = width;
        this.height = height;
    }
    public abstract double area(); // 定义抽象方法，计算面积
}
```

2）定义一个正方形类，该类继承自形状类Shape，并重写了area()抽象方法。代码如下：

```java
public class Square extends Shape {
    public Square(int width, int height) {
        super(width, height);
    }
    // 重写父类中的抽象方法，实现计算正方形面积的功能
    @Override
    public double area() {
        return width * height;
    }
}
```

3)定义一个三角形类，该类与正方形类一样，需要继承形状类 Shape，并重写父类中的抽象方法 area()。三角形类的代码实现如下：

```java
public class Triangle extends Shape {
    public Triangle(int width, int height) {
        super(width, height);
    }
    // 重写父类中的抽象方法，实现计算三角形面积的功能
    @Override
    public double area() {
        return 0.5 * width * height;
    }
}
```

4）最后创建一个测试类，分别创建正方形类和三角形类的对象，并调用各类中的 area() 方法，打印出不同形状的几何图形的面积。测试类的代码如下：

```java
public class ShapeTest {
    public static void main(String[] args) {
        Square square = new Square(5, 4); // 创建正方形类对象
        System.out.println("正方形的面积为：" + square.area());
        Triangle triangle = new Triangle(2, 5); // 创建三角形类对象
        System.out.println("三角形的面积为：" + triangle.area());
    }
}
```

5）运行该程序，输出的结果如下：

```java
正方形的面积为：20.0
三角形的面积为：5.0
```



## 7.10接口的定义与实现(Interface)

抽象类是从多个类中抽象出来的模板，如果将这种抽象进行的更彻底，则可以提炼出一种更加特殊的“抽象类”——接口（Interface）。接口是java中最重要的概念之一，它可以被理解为一种特殊的类，不同的是接口的成员没有执行体，是由全局常量和公共的抽象方法所组成。

### 定义接口

Java 接口的定义方式与类基本相同，不过接口定义使用的关键字是 interface，接口定义的语法格式如下：、

```java
[public] interface interface_name [extends interface1_name[, interface2_name,…]] {
    // 接口体，其中可以包含定义常量和声明方法
    [public] [static] [final] type constant_name = value;    // 定义常量
    [public] [abstract] returnType method_name(parameter_list);    // 声明方法
}
```

对以上语法的说明如下：

- public 表示接口的修饰符，当没有修饰符时，则使用默认的修饰符，此时该接口的访问权限仅局限于所属的包；
- interface_name 表示接口的名称。接口名应与类名采用相同的命名规则，即如果仅从语法角度来看，接口名只要是合法的标识符即可。如果要遵守 Java 可读性规范，则接口名应由多个有意义的单词连缀而成，每个单词首字母大写，单词与单词之间无需任何分隔符。
- extends 表示接口的继承关系；
- interface1_name 表示要继承的接口名称；
- constant_name 表示变量名称，一般是 static 和 final 型的；
- returnType 表示方法的返回值类型；
- parameter_list 表示参数列表，在接口中的方法是没有方法体的。

```java
注意：一个接口可以有多个直接父接口，但接口只能继承接口，不能继承类。
```

接口对于其声明、变量和方法都做了许多限制，这些限制作为接口的特征归纳如下：

- 具有 public 访问控制符的接口，允许任何类使用；没有指定 public 的接口，其访问将局限于所属的包。

- **方法的声明不需要其他修饰符，在接口中声明的方法，将隐式地声明为公有的（public）和抽象的（abstract）。**

- **在 Java 接口中声明的变量其实都是常量，接口中的变量声明，将隐式地声明为 public、static 和 final，即常量，所以接口中定义的变量必须初始化。**

- 接口没有构造方法，不能被实例化。例如：

  ```java
  public interface A {
      public A(){…}    // 编译出错，接口不允许定义构造方法
  }
  ```

一个接口不能够实现另一个接口，但它可以继承多个其他接口。子接口可以对父接口的方法和常量进行重写。例如：

```java
public interface StudentInterface extends PeopleInterface {
    // 接口 StudentInterface 继承 PeopleInterface
    int age = 25;    // 常量age重写父接口中的age常量
    void getInfo();    // 方法getInfo()重写父接口中的getInfo()方法
}
```

例如，定义一个接口 MyInterface，并在该接口中声明常量和方法，如下：

```java
public interface MyInterface {    // 接口myInterface
    String name;    // 不合法，变量name必须初始化
    int age = 20;    // 合法，等同于 public static final int age = 20;
    void getInfo();    // 方法声明，等同于 public abstract void getInfo();
}
```

### 实现接口

接口的主要用途就是被实现类实现，一个类可以实现一个或多个接口，继承使用 extends 关键字，实现则使用 implements 关键字。因为一个类可以实现多个接口，这也是 Java 为单继承灵活性不足所作的补充。类实现接口的语法格式如下：

```java
<public> class <class_name> [extends superclass_name] [implements interface1_name[, interface2_name…]] {
    // 主体
}
```

对以上语法的说明如下：

- public：类的修饰符；
- superclass_name：需要继承的父类名称；
- interface1_name：要实现的接口名称。

实现接口需要注意以下几点：

- 实现接口与继承父类相似，一样可以获得所实现接口里定义的常量和方法。如果一个类需要实现多个接口，则多个接口之间以逗号分隔。
- 一个类可以继承一个父类，并同时实现多个接口，implements 部分必须放在 extends 部分之后。
- **一个类实现了一个或多个接口之后，这个类必须完全实现这些接口里所定义的全部抽象方法**（也就是重写这些抽象方法）；否则，该类将保留从父接口那里继承到的抽象方法，该类也必须定义成抽象类。



**例一**

1）创建一个名称为 IMath 的接口，代码如下：

```java
public interface IMath {
    public int sum();    // 完成两个数的相加
    public int maxNum(int a,int b);    // 获取较大的数
}
```

2）定义一个 MathClass 类并实现 IMath 接口，MathClass 类实现代码如下：

```java
public class MathClass implements IMath {
    private int num1;    // 第 1 个操作数
    private int num2;    // 第 2 个操作数
    public MathClass(int num1,int num2) {
        // 构造方法
        this.num1 = num1;
        this.num2 = num2;
    }
    // 实现接口中的求和方法
    public int sum() {
        return num1 + num2;
    }
    // 实现接口中的获取较大数的方法
    public int maxNum(int a,int b) {
        if(a >= b) {
            return a;
        } else {
            return b;
        }
    }
}
```

在实现类中，所有的方法都使用了 public 访问修饰符声明。无论何时实现一个由接口定义的方法，它都必须实现为 public，因为接口中的所有成员都显式声明为 public。

3）最后创建测试类 NumTest，实例化接口的实现类 MathClass，调用该类中的方法并输出结果。该类内容如下：

```java
public class NumTest {
    public static void main(String[] args) {
        // 创建实现类的对象
        MathClass calc = new MathClass(100, 300);
        System.out.println("100 和 300 相加结果是：" + calc.sum());
        System.out.println("100 比较 300，哪个大：" + calc.maxNum(100, 300));
    }
}
```

程序运行结果如下所示。

```java
100 和 300 相加结果是：400
100 比较 300，哪个大：300
```

## 7.11接口和抽象类的区别和联系

接口和抽象类的区别

接口（interface）可以说成是抽象类的一种特例，接口中的所有方法都必须是抽象的。接口中的方法定义默认为public abstract类型，接口中的成员变量类型默认为public static final。另外，接口和抽象类在方法上有区别：

> - 抽象类可以有构造方法，接口中不能有构造方法。
> - 抽象类中可以包含非抽象的普通方法，接口中的所有方法必须都是抽象的，不能有非抽象的普通方法。
> - 抽象类中可以有普通成员变量，接口中没有普通成员变量
> - 抽象类中的抽象方法的访问类型可以是public，protected和默认类型
> - 抽象类中可以包含静态方法，接口中不能包含静态方法
> - 抽象类和接口中都可以包含静态成员变量，抽象类中的静态成员变量的访问类型可以任意，但接口中定义的变量只能是public static final类型，并且默认即为public static final类型
> - 一个类可以实现多个接口，但只能继承一个抽象类。二者在应用方面也有一定的区别：接口更多的是在系统架构设计方法发挥作用，主要用于定义模块之间的通信契约。而抽象类在代码实现方面发挥作用，可以实现代码的重用，例如，模板方法设计模式是抽象类的一个典型应用，假设某个项目的所有Servlet类都要用相同的方式进行权限判断、记录访问日志和处理异常，那么就可以定义一个抽象的基类，让所有的Servlet都继承这个抽象基类，在抽象基类的service方法中完成权限判断、记录访问日志和处理异常的代码，在各个子类中只是完成各自的业务逻辑代码。

## 7.12内部类简介

在类内部可定义成员变量和方法，且在类内部也可以定义另一个类。如果在类 Outer 的内部再定义一个类 Inner，此时类 Inner 就称为内部类（或称为嵌套类），而类 Outer 则称为外部类（或称为宿主类）。

内部类可以很好地实现隐藏，一般的非内部类是不允许有 private 与 protected 权限的，但内部类可以。内部类拥有外部类的所有元素的访问权限。

**内部类可以分为：实例内部类、静态内部类和成员内部类**

内部类的特点如下：

1. 内部类仍然是一个独立的类，在编译之后内部类会被编译成独立的`.class`文件，但是前面冠以外部类的类名和`$`符号。
2. 内部类不能用普通的方式访问。内部类是外部类的一个成员，因此内部类可以自由地访问外部类的成员变量，无论是否为 private 的。
3. 内部类声明成静态的，就不能随便访问外部类的成员变量，仍然是只能访问外部类的静态成员变量。

**例一**

内部类的简单应用

```java
public class Test {
    public class InnerClass {
        public int getSum(int x,int y) {
            return x + y;
        }
    }
    public static void main(String[] args) {
        Test.InnerClass ti = new Test().new InnerClass();
        int i = ti.getSum(2,3);
        System.out.println(i);    // 输出5
    }
}
```

有关内部类的说明有如下几点。

- 外部类只有两种访问级别：public 和默认；内部类则有 4 种访问级别：public、protected、 private 和默认。
- 在外部类中可以直接通过内部类的类名访问内部类。

```
InnerClass ic = new InnerClass();    // InnerClass为内部类的类名
```

- 在外部类以外的其他类中则需要通过内部类的完整类名访问内部类。

```
Test.InnerClass ti = newTest().new InnerClass();    // Test.innerClass是内部类的完整类名
```

- 内部类与外部类不能重名。



## 7.13实例内部类

## 7.14静态内部类

## 7.15局部内部类

局部内部类就是在方法中定义的类



特点：

1. 与局部变量一样不能使用访问控制修饰符和static修饰符

2. 只在当前方法生效

3. 不能在类中定义static成员

4. 还可以包含内部类，到那时这些内部类也不能使用访问控制修饰符和static修饰符

5. 局部内内部类可以访问外部类的所有成员

6. 在局部内部类中只可以访问当前方法中的final类型的参数与变量，如果方法中的成员与外部类中的成员同名，则可以使用 <OuterClassName>.this.<MemberName> 的形式访问外部类中的成员。

   ```java
   public class Test {
       int a = 0;
       int d = 0;
       public void method() {
           int b = 0;
           final int c = 0;
           final int d = 10;
           class Inner {
               int a2 = a;    // 访问外部类中的成员
               // int b2 = b;    // 编译出错
               int c2 = c;    // 访问方法中的成员
               int d2 = d;    // 访问方法中的成员
               int d3 = Test.this.d;    //访问外部类中的成员
           }
           Inner i = new Inner();
           System.out.println(i.d2);    // 输出10
           System.out.println(i.d3);    // 输出0
       }
       public static void main(String[] args) {
           Test t = new Test();
           t.method();
       }
   }
   ```



## 7.16匿名内部类

## 7.17Lanbda表达式

Lambda 表达式（Lambda expression）是一个匿名函数，基于数学中的λ演算得名，也可称为闭包（Closure）。现在很多语言都支持 Lambda 表达式，如 C++、C#、Java、Python 和 JavaScript 等。

Lambda 表达式是推动 Java 8 发布的重要新特性，它允许把函数作为一个方法的参数（函数作为参数传递进方法中），下面通过例 1 来理解 Lambda 表达式的概念。

Lambda 表达式标准语法形式如下：

(参数列表) -> {
  // Lambda表达式体
}

`->`被称为箭头操作符或 Lambda 操作符，箭头操作符将 Lambda 表达式拆分成两部分：

- 左侧：Lambda 表达式的参数列表。
- 右侧：Lambda 表达式中所需执行的功能，用`{ }`包起来，即 Lambda 体。

#### Java Lambda 表达式的优缺点

优点：

1. 代码简洁，开发迅速
2. 方便函数式编程
3. 非常容易进行并行计算
4. Java 引入 Lambda，改善了集合操作（引入 Stream API）

缺点：

1. 代码可读性变差
2. 在非并行计算中，很多计算未必有传统的 for 性能要高
3. 不容易进行调试



### 函数式接口

Lambda 表达式实现的接口不是普通的接口，而是函数式接口。如果一个接口中，有且只有一个抽象的方法（Object 类中的方法不包括在内），那这个接口就可以被看做是函数式接口。这种接口只能有一个方法。如果接口中声明多个抽象方法，那么 Lambda 表达式会发生编译错误：

```java
The target type of this expression must be a functional interface
```

这说明该接口不是函数式接口，为了防止在函数式接口中声明多个抽象方法，Java 8 提供了一个声明函数式接口注解 @FunctionalInterface，示例代码如下。

```java
// 可计算接口
@FunctionalInterface
public interface Calculable {
    // 计算两个int数值
    int calculateInt(int a, int b);
}
```

在接口之前使用 @FunctionalInterface 注解修饰，那么试图增加一个抽象方法时会发生编译错误。但可以添加默认方法和静态方法。



@FunctionalInterface 注解与 @Override 注解的作用类似。Java 8 中专门为函数式接口引入了一个新的注解 @FunctionalInterface。该注解可用于一个接口的定义上，一旦使用该注解来定义接口，编译器将会强制检查该接口是否确实有且仅有一个抽象方法，否则将会报错。需要注意的是，即使不使用该注解，只要满足函数式接口的定义，这仍然是一个函数式接口，使用起来都一样。


提示：Lambda 表达式是一个匿名方法代码，Java 中的方法必须声明在类或接口中，那么 Lambda 表达式所实现的匿名方法是在函数式接口中声明的。

# 8.Java异常处理

## 8.1异常处理及常见异常

**异常是在运行程序时产生的一种异常情况**

### 异常简介

Java中的异常又称为例外，是一个程序执行期间发生的事件，它中断在执行的正常指令流

在 Java 中一个异常的产生，主要有如下三种原因：

1. Java 内部错误发生异常，Java 虚拟机产生的异常。
2. 编写的程序代码中的错误所产生的异常，例如空指针异常、数组越界异常等。
3. 通过 throw 语句手动生成的异常，一般用来告知该方法的调用者一些必要信息。



Java 通过面向对象的方法来处理异常。在一个方法的运行过程中，如果发生了异常，则这个方法会产生代表该异常的一个对象，并把它交给运行时的系统，运行时系统寻找相应的代码来处理这一异常。

我们把生成异常对象，并把它提交给运行时系统的过程称为拋出（throw）异常。运行时系统在方法的调用栈中查找，直到找到能够处理该类型异常的对象，这一个过程称为捕获（catch）异常。

### 异常类型

为了能够及时有效的处理程序中的运行的错误，Java中引进了异常类。其都是java.lang.Throwable类的子类，即Throwable位于异常类层次结构的顶层

Throwable 类下有两个异常分支 Exception 和 Error，如图 1 所示。



![img](https://c.biancheng.net/uploads/allimg/181023/3-1Q0231H424V1.jpg)

图 1 异常结构图



由图 2 可以知道，Throwable 类是所有异常和错误的超类，下面有 Error 和 Exception 两个子类分别表示错误和异常。其中异常类 Exception 又分为运行时异常和非运行时异常，这两种异常有很大的区别，也称为不检查异常（Unchecked Exception）和检查异常（Checked Exception）。

- Exception 类用于用户程序可能出现的异常情况，它也是用来创建自定义异常类型类的类。
- Error 定义了在通常环境下不希望被程序捕获的异常。一般指的是 JVM 错误，如堆栈溢出。



运行时异常都是 RuntimeException 类及其子类异常，如 NullPointerException、IndexOutOfBoundsException 等，这些异常是不检查异常，程序中可以选择捕获处理，也可以不处理。这些异常一般由程序逻辑错误引起，程序应该从逻辑角度尽可能避免这类异常的发生。

非运行时异常是指 RuntimeException 以外的异常，类型上都属于 Exception 类及其子类。从程序语法角度讲是必须进行处理的异常，如果不处理，程序就不能编译通过。如 IOException、ClassNotFoundException 等以及用户自定义的 Exception 异常（一般情况下不自定义检查异常）。

表 1 和表 2 分别列出了 java.lang 中定义的运行时异常和非运行时异常的类型及作用。

**运行时异常**

| 异常类型                      | 说明                                                  |
| ----------------------------- | ----------------------------------------------------- |
| ArithmeticException           | 算术错误异常，如以零做除数                            |
| ArraylndexOutOfBoundException | 数组索引越界                                          |
| ArrayStoreException           | 向类型不兼容的数组元素赋值                            |
| ClassCastException            | 类型转换异常                                          |
| IllegalArgumentException      | 使用非法实参调用方法                                  |
| lIIegalStateException         | 环境或应用程序处于不正确的状态                        |
| lIIegalThreadStateException   | 被请求的操作与当前线程状态不兼容                      |
| IndexOutOfBoundsException     | 某种类型的索引越界                                    |
| NullPointerException          | 尝试访问 null 对象成员，空指针异常                    |
| NegativeArraySizeException    | 再负数范围内创建的数组                                |
| NumberFormatException         | 数字转化格式异常，比如字符串到 float 型数字的转换无效 |
| TypeNotPresentException       | 类型未找到                                            |

**非运行时异常**

| 异常类型                     | 说明                       |
| ---------------------------- | -------------------------- |
| ClassNotFoundException       | 没有找到类                 |
| IllegalAccessException       | 访问类被拒绝               |
| InstantiationException       | 试图创建抽象类或接口的对象 |
| InterruptedException         | 线程被另一个线程中断       |
| NoSuchFieldException         | 请求的域不存在             |
| NoSuchMethodException        | 请求的方法不存在           |
| ReflectiveOperationException | 与反射有关的异常的超类     |

## 8.2Error和Exception的异同

Error（错误）和 Exception（异常）都是 java.lang.Throwable 类的子类，在java 代码中只有继承了 Throwable 类的实例才能被 throw 或者 catch。

Exception 和 Error 体现了 Java 平台设计者对不同异常情况的分类，Exception 是程序正常运行过程中可以预料到的意外情况，并且应该被开发者捕获，进行相应的处理。Error 是指正常情况下不大可能出现的情况，绝大部分的 Error 都会导致程序处于非正常、不可恢复状态。所以不需要被开发者捕获。

Error 错误是任何处理技术都无法恢复的情况，肯定会导致程序非正常终止。并且 Error 错误属于未检查类型，大多数发生在运行时。Exception 又分为可检查（checked）异常和不检查（unchecked）异常，可检查异常在源码里必须显示的进行捕获处理，这里是编译期检查的一部分。不检查异常就是所谓的运行时异常，通常是可以编码避免的逻辑错误，具体根据需要来判断是否需要捕获，并不会在编译器强制要求。

如下是常见的 Error 和 Exception：

1）运行时异常（RuntimeException）：

- NullPropagation：空指针异常；
- ClassCastException：类型强制转换异常
- IllegalArgumentException：传递非法参数异常
- IndexOutOfBoundsException：下标越界异常
- NumberFormatException：数字格式异常

2）非运行时异常：

- ClassNotFoundException：找不到指定 class 的异常
- IOException：IO 操作异常

3）错误（Error）：

- NoClassDefFoundError：找不到 class 定义异常
- StackOverflowError：深递归导致栈被耗尽而抛出的异常
- OutOfMemoryError：内存溢出异常

**例 1**

下面代码会导致 Java 堆栈溢出错误。

```java
//通过无限递归演示占堆溢出错误
class StackOverflow{
	public static void test(int i){
		if(i == 0){
			return;
			
		}else{
			test(i++);
		}
	}
}
public class ErrorEg{
    public static void main(String[] args){
        //执行StackOverflow方法
        StackOverflow.test(5);
    }
}
```

运行输出为：

```
Exception in thread "main" java.lang.StackOverflowError
  at ch11.StackOverflow.test(ErrorEg.java:9)
  at ch11.StackOverflow.test(ErrorEg.java:9)
  at ch11.StackOverflow.test(ErrorEg.java:9)
  at ch11.StackOverflow.test(ErrorEg.java:9)
```

## 8.3异常处理机制及异常处理的基本结构

异常处理通过五个关键字实现：try，catch，throw，throws，finally



try catch 语句用于捕获并处理异常，finally 语句用于在任何情况下（除特殊情况外）都必须执行的代码，throw 语句用于拋出异常，throws 语句用于声明可能会出现的异常。



java中提供了一种结构性和控制性的方式来处理程序执行期间发生的事件，异常处理机制如下：

- 在方法中使用try...catch语句捕获并处理异常，catch语句可以有多个用来匹配多个异常
- 对于处理不了的异常或是要转换的异常，在方法声明处通过throws语句抛出异常

以下是异常处理程序的基本结构

```
try{
	逻辑程序块
}catch{
	处理代码块1
}catch{
	处理代码块2
	throw(e);//抛出这个异常
}finally{
	释放资源代码块
}
```

## 8.4try...catch语句详解

语法格式如下：

```java
try{
	//可能发生异常的语句
}catch（Exception e）{
	//处理异常语句
}
```

在以上语法中，把可能引发异常的语句封装在 try 语句块中，用以捕获可能发生的异常。catch 后的`( )`里放匹配的异常类，指明 catch 语句可以处理的异常类型，发生异常时产生异常类的实例化对象。

如果 try 语句块中发生异常，那么一个相应的异常对象就会被拋出，然后 catch 语句就会依据所拋出异常对象的类型进行捕获，并处理。处理之后，程序会跳过 try 语句块中剩余的语句，转到 catch 语句块后面的第一条语句开始执行。

如果 try 语句块中没有异常发生，那么 try 块正常结束，后面的 catch 语句块被跳过，程序将从 catch 语句块后的第一条语句开始执行。



注意：try...catch 与 if...else 不一样，try 后面的花括号`{ }`不可以省略，即使 try 块里只有一行代码，也不可省略这个花括号。与之类似的是，catch 块后的花括号`{ }`也不可以省略。另外，try 块里声明的变量只是代码块内的局部变量，它只在 try 块内有效，其它地方不能访问该变量。



在上面语法的处理代码块 1 中，可以使用以下 3 个方法输出相应的异常信息。

- printStackTrace() 方法：指出异常的类型、性质、栈层次及出现在程序中的位置
- getMessage() 方法：输出错误的性质。
- toString() 方法：给出异常的类型与性质。



**例一**

```java
import java.util.Scanner;
public class Test02 {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        System.out.println("---------学生信息录入---------------");
        String name = ""; // 获取学生姓名
        int age = 0; // 获取学生年龄
        String sex = ""; // 获取学生性别
        try {
            System.out.println("请输入学生姓名：");
            name = scanner.next();
            System.out.println("请输入学生年龄：");
            age = scanner.nextInt();
            System.out.println("请输入学生性别：");
            sex = scanner.next();
        } catch (Exception e) {
            e.printStackTrace();
            System.out.println("输入有误！");
        }
        System.out.println("姓名：" + name);
        System.out.println("年龄：" + age);
    }
}
```

上述代码在 main() 方法中使用 try catch 语句来捕获异常，将可能发生异常的`age = scanner.nextlnt();`代码放在了 try 块中，在 catch 语句中指定捕获的异常类型为 Exception，并调用异常对象的 printStackTrace() 方法输出异常信息。运行结果如下所示。

```java
---------学生信息录入---------------
请输入学生姓名：
徐白
请输入学生年龄：
110a
java.util.InputMismatchException
    at java.util.Scanner.throwFor(Unknown Source)
    at java.util.Scanner.next(Unknown Source)
    at java.util.Scanner.nextInt(Unknown Source)
    at java.util.Scanner.nextInt(Unknown Source)
输入有误！
姓名：徐白
年龄：0
    at text.text.main(text.java:19)
```

### 多重catch语句

如果try代码中有很多语句会发生异常，而且异常的种类很多。那么可以在try后面跟多个catch代码块，代码格式如下：

```java
try {
    // 可能会发生异常的语句
} catch(ExceptionType e) {
    // 处理异常语句
} catch(ExceptionType e) {
    // 处理异常语句
} catch(ExceptionType e) {
    // 处理异常语句
...
}
```

在多个 catch 代码块的情况下，当一个 catch 代码块捕获到一个异常时，其它的 catch 代码块就不再进行匹配。

注意：当捕获的多个异常类之间存在父子关系时，捕获异常时一般先捕获子类，再捕获父类。所以子类异常必须在父类异常的前面，否则子类捕获不到。

**例二**

```java
public class Test03 {
    public static void main(String[] args) {
        Date date = readDate();
        System.out.println("读取的日期 = " + date);
    }
    public static Date readDate() {
        FileInputStream readfile = null;
        InputStreamReader ir = null;
        BufferedReader in = null;
        try {
            readfile = new FileInputStream("readme.txt");
            ir = new InputStreamReader(readfile);
            in = new BufferedReader(ir);
            // 读取文件中的一行数据
            String str = in.readLine();
            if (str == null) {
                return null;
            }
            DateFormat df = new SimpleDateFormat("yyyy-MM-dd");
            Date date = df.parse(str);
            return date;
        } catch (FileNotFoundException e) {
            System.out.println("处理FileNotFoundException...");
            e.printStackTrace();
        } catch (IOException e) {
            System.out.println("处理IOException...");
            e.printStackTrace();
        } catch (ParseException e) {
            System.out.println("处理ParseException...");
            e.printStackTrace();
        }
        return null;
    }
}
```

在 try 代码块中第 12 行代码调用 FileInputStream 构造方法可能会发生 FileNotFoundException 异常。第 16 行代码调用 BufferedReader 输入流的 readLine() 方法可能会发生 IOException 异常。FileNotFoundException 异常是 IOException 异常的子类，应该先捕获 FileNotFoundException 异常，见代码第 23 行；后捕获 IOException 异常，见代码第 26 行。

如果将 FileNotFoundException 和 IOException 捕获顺序调换，那么捕获 FileNotFoundException 异常代码块将永远不会进入，FileNotFoundException 异常处理永远不会执行。 上述代码第 29 行 ParseException 异常与 IOException 和 FileNotFoundException 异常没有父子关系，所以捕获 ParseException 异常位置可以随意放置。

## 8.5try...catch...finally语句

实际中try  catch语句执行时语句块不能完全被执行，而有些处理的代码块要求必须被执行。如打开的一些物理资源必须显式回收

**Java中的垃圾回收机制不会回收任何物理资源，只回收堆内存中对象占用的内存**

finally 语句可以与前面介绍的 [try catch](http://c-local.biancheng.net/view/6732.html) 语句块匹配使用，语法格式如下：

```java
try {
    // 可能会发生异常的语句
} catch(ExceptionType e) {
    // 处理异常语句
} finally {
    // 清理代码块
}
```

对于以上格式，无论是否发生异常（除特殊情况外），finally 语句块中的代码都会被执行。此外，finally 语句也可以和 try 语句匹配使用，其语法格式如下：

```java
try {
    // 逻辑代码块
} finally {
    // 清理代码块
}
```

使用try-catch-finally语句需要注意以下几点：

1. 异常处理语法中只有try块是必须的，也就是说没有try后面的catch和finally也不能有
2. catch块和finally块都是可选的，但是必须出现其中之一，或者同时出现
3. 可以有多个catch块捕获父类异常，但是父类异常必须放在子类异常后面
4. 三个出现顺序必须是先try再catch在finally

try catch finally 语句块的执行情况可以细分为以下 3 种情况：

1. 如果 try 代码块中没有拋出异常，则执行完 try 代码块之后直接执行 finally 代码块，然后执行 try catch finally 语句块之后的语句。
2. 如果 try 代码块中拋出异常，并被 catch 子句捕捉，那么在拋出异常的地方终止 try 代码块的执行，转而执行相匹配的 catch 代码块，之后执行 finally 代码块。如果 finally 代码块中没有拋出异常，则继续执行 try catch finally 语句块之后的语句；如果 finally 代码块中拋出异常，则把该异常传递给该方法的调用者。
3. 如果 try 代码块中拋出的异常没有被任何 catch 子句捕捉到，那么将直接执行 finally 代码块中的语句，并把该异常传递给该方法的调用者。



**例一**

当Windows系统启动之后，不做任何操作，在关机时都会显示“谢谢使用”，下面展示这个过程

```java
import java.util.Scanner;
public class Test04 {
    public static void main(String[] args) {
        Scanner input = new Scanner(System.in);
        System.out.println("Windows 系统已启动！");
        String[] pros = { "记事本", "计算器", "浏览器" };
        try {
            // 循环输出pros数组中的元素
            for (int i = 0; i < pros.length; i++) {
                System.out.println(i + 1 + "：" + pros[i]);
            }
            System.out.println("是否运行程序：");
            String answer = input.next();
            if (answer.equals("y")) {
                System.out.println("请输入程序编号：");
                int no = input.nextInt();
                System.out.println("正在运行程序[" + pros[no - 1] + "]");
            }
        } catch (Exception e) {
            e.printStackTrace();
        } finally {
            System.out.println("谢谢使用!");
        }
    }
}
```

上述代码在 main() 方法中使用 try catch finally 语句模拟了系统的使用过程。当系统启动之后显示提示语，无论是否运行了程序，或者在运行程序时出现了意外，程序都将执行 finally 块中的语句，即显示“谢谢使用！”。输出时的结果如下所示。

```java
Windows 系统已启动！
1：记事本
2：计算器
3：浏览器
是否运行程序：
y
请输入程序编号：
5
谢谢使用!
java.lang.ArrayIndexOutOfBoundsException: 4
    at text.text.main(text.java:23)
```

## 8.6finally和return的执行顺序

### 第一种情况

try语句块中有return语句，catch和finally语句块里面都没有return

示例代码

```java
public class Main {
    public static void main(String[] args) {
        System.out.println(test1());
    }
    public static int test1() {
        int i =10;
        try {
            System.out.println("try语句");
            return --i;
        }
        catch (Exception e) {
            System.out.println("catch语句");
        }
        finally {
            System.out.println("finally语句");
        }
    return 0;
    }
}
```

运行结果

```
try语句
finally语句
9
```

执行顺序：

1. 先执行try块中的语句，包括return语句中的运算表达式，但是不返回
2. 执行finally语句块中的全部代码
3. 最有执行try块中的return返回



### 第二种情况

try语句块和finally语句块里面有return语句，catch语句块里面没有return

示例代码如下

```java
public class Main {
    public static void main(String[] args) {
        System.out.println(test2());
    }
    public static int test2() {
        int i =10;
        try {
            System.out.println("try语句");
            return --i;
        }
        catch (Exception e) {
            System.out.println("catch语句");
        }
        finally {
            System.out.println("finally语句");
            return --i;
        }
    }
}
```

运行结果如下

```
try语句
finally语句
8
```

执行顺序：

1. 先执行try块中的语句，包括return，但是不返回
2. 执行finally语句块中的全部代码
3. 最后发现finally语句块中有return语句，从这里返回



### 第三种情况

try和catch语句块中有return语句，finally语句块里面没有return语句，存在异常

示例代码如下

```java
public class Main {
    public static void main(String[] args) {
        System.out.println(test3());
    }
    public static int test3() {
        int i =10;
        try {
            System.out.println("try语句");
            int j = 10 / 0;
            return --i;
        }
        catch (Exception e) {
            System.out.println("catch语句");
            return --i;
        }
        finally {
            System.out.println("finally语句");
        }
    }
}
```

运行结果如下：

```
try语句
catch语句
finally语句
9
```

执行顺序：

1. 先执行try块中的语句，出现异常，catch捕获异常
2. 执行catch块中的语句，包括return语句中的表达式运算，但是不返回
3. 执行finally语句块中的全部代码
4. 最后执行catch块中的return返回

### 第四种情况

try语句块，catch语句块和finally语句块里面都有return语句，存在异常

示例代码如下

```java
public class Main {
    public static void main(String[] args) {
        System.out.println(test4());
    }
    public static int test4() {
        int i =10;
        try {
            System.out.println("try语句");
            int j = 10 / 0;
            return --i;
        }
        catch (Exception e) {
            System.out.println("catch语句");
            return --i;
        }
        finally {
            System.out.println("finally语句");
            return --i;
        }
    }
}
```

运行结果

```
try语句
catch语句
finally语句
8
```

执行顺序：

1.先执行try块中语句，出现异常，catch捕获到异常。

2.执行catch块中语句，包括return语句中的表达式运算，但不返回。

3.执行finally语句块中的全部代码。

4.最后发现finally语句块中有return语句，从这里返回。



### 总结

1. finally语句在return语句执行之后return语句返回之前执行
2. finally块中的return语句会覆盖try块中的return返回
3. 如果fianlly语句块中没有return语句覆盖返回值，那么原来的返回值可能因俄日finally里的修改而改变也可能不变
4. try块里的return语句在存在异常的情况下不会执行，具体返回哪个值看情况
5. 当异常发生后，catch中的return执行情况与未发生异常的try中的return的执行情况完全一样





## 8.7Java9 增强的自动资源管理器

当程序使用finally块关闭资源时，程序会显得特别臃肿，如下：

```java
public static void main(String[] args) {
    FileInputStream fis = null;
    try {
        fis = new FileInputStream("a.txt");
    } catch (FileNotFoundException e) {
        e.printStackTrace();
    } finally {
        // 关闭磁盘文件，回收资源
        if (fis != null) {
            try {
                fis.close();
            } catch (IOException e) {
                e.printStackTrace();
            }
        }
    }
}
```



为了解决这个问题Java在后续的更新中添加的 **自动资源管理**，该特性是在太try的基础上扩展，主动释放不再需要的文件或是其他资源



自动资源管理替代了finally代码块，并优化了代码结构和可读性，语法如下

```java
try (声明或初始化资源语句) {
    // 可能会生成异常语句
} catch(Throwable e1){
    // 处理异常e1
} catch(Throwable e2){
    // 处理异常e1
} catch(Throwable eN){
    // 处理异常eN
}
```

**注意：**

1. try语句中的声明的资源被隐式的声明为final，资源的作用局限与这个try语句
2. 可以在一条try语句中声明或是初始化多个资源，每个资源以 `;`隔开即可
3. 需要关闭的资源必须实现了AutoCloseable或Closeable接口



Closeable 是 AutoCloseable 的子接口，Closeable 接口里的 close() 方法声明抛出了 IOException，因此它的实现类在实现 close() 方法时只能声明抛出 IOException 或其子类；AutoCloseable 接口里的 close() 方法声明抛出了 Exception，因此它的实现类在实现 close() 方法时可以声明抛出任何异常。



下面示范如何使用自动关闭资源的 try 语句。

```java
public class AutoCloseTest {
    public static void main(String[] args) throws IOException {
        try (
                // 声明、初始化两个可关闭的资源
                // try语句会自动关闭这两个资源
                BufferedReader br = new BufferedReader(new FileReader("AutoCloseTest.java"));
                PrintStream ps = new PrintStream(new FileOutputStream("a.txt"))) {
            // 使用两个资源
            System.out.println(br.readLine());
            ps.println("日向雏田");
        }
    }
}
```

上面程序中粗体字代码分别声明、初始化了两个 IO 流，BufferedReader 和 PrintStream 都实现了 Closeable 接口，并在 try 语句中进行了声明和初始化，所以 try 语句会自动关闭它们。

自动关闭资源的 try 语句相当于包含了隐式的 finally 块（这个 finally 块用于关闭资源），因此这个 try 语句可以既没有 catch 块，也没有 finally 块。

> Java 7 几乎把所有的“资源类”（包括文件 IO 的各种类、JDBC 编程的 Connection 和 Statement 等接口）进行了改写，改写后的资源类都实现了 AutoCloseable 或 Closeable 接口。

如果程序需要，自动关闭资源的 try 语句后也可以带多个 catch 块和一个 finally 块。

Java 9 再次增强了这种 try 语句。Java 9 不要求在 try 后的圆括号内声明并创建资源，只需要自动关闭的资源有 final 修饰或者是有效的 final (effectively final)，Java 9 允许将资源变量放在 try 后的圆括号内。上面程序在 Java 9 中可改写为如下形式。

```java
public class AutoCloseTest {
    public static void main(String[] args) throws IOException {
        // 有final修饰的资源
        final BufferedReader br = new BufferedReader(new FileReader("AutoCloseTest.java"));
        // 没有显式使用final修饰，但只要不对该变量重新赋值，该变量就是有效的
        final PrintStream ps = new PrintStream(new FileOutputStream("a. txt"));
        // 只要将两个资源放在try后的圆括号内即可
        try (br; ps) {
            // 使用两个资源
            System.out.println(br.readLine());
            ps.println("漩涡鸣人");
        }
    }
}
```

## 8.8声明和抛出异常

可以通过throws在方法上生命该方法要抛出的异常，然后再方法内部通过throw抛出异常对象

### throws声明异常

使用throws声明的方法表示该方法不处理异常。具体格式如下

```java
returnType method_name(paramList) throws Exception 1,Exception2,…{…}
```

其中，returnType 表示返回值类型；method_name 表示方法名；paramList 表示参数列表；Exception 1，Exception2，… 表示异常类。



如果有多个异常类使用逗号隔开

使用 throws 声明抛出异常的思路是，当前方法不知道如何处理这种类型的异常，该异常应该由向上一级的调用者处理；如果 main 方法也不知道如何处理这种类型的异常，也可以使用 throws 声明抛出异常，该异常将交给 JVM 处理。JVM 对异常的处理方法是，打印异常的跟踪栈信息，并中止程序运行，这就是前面程序在遇到异常后自动结束的原因。

**例一**

创建一个 readFile() 方法，该方法用于读取文件内容，在读取的过程中可能会产生 IOException 异常，但是在该方法中不做任何的处理，而将可能发生的异常交给调用者处理。在 main() 方法中使用 try catch 捕获异常，并输出异常信息。代码如下：

```java
import java.io.FileInputStream;
import java.io.IOException;
public class Test04 {
    public void readFile() throws IOException {
        // 定义方法时声明异常
        FileInputStream file = new FileInputStream("read.txt"); // 创建 FileInputStream 实例对象
        int f;
        while ((f = file.read()) != -1) {
            System.out.println((char) f);
            f = file.read();
        }
        file.close();
    }
    public static void main(String[] args) {
        Throws t = new Test04();
        try {
            t.readFile(); // 调用 readFHe()方法
        } catch (IOException e) {
            // 捕获异常
            System.out.println(e);
        }
    }
}
```

以上代码，首先在定义 readFile() 方法时用 throws 关键字声明在该方法中可能产生的异常，然后在 main() 方法中调用 readFile() 方法，并使用 catch 语句捕获产生的异常。



**方法重写时抛出异常的限制**

*子类方法声明抛出的异常类型应该是父类方法声明抛出的异常类型的子类或相同，子类方法声明抛出的异常不允许比父类方法声明抛出的异常多*

```java
public class OverrideThrows {
    public void test() throws IOException {
        FileInputStream fis = new FileInputStream("a.txt");
    }
}
class Sub extends OverrideThrows {
    // 子类方法声明抛出了比父类方法更大的异常
    // 所以下面方法出错
    public void test() throws Exception {
    }
}
```

上面程序中 Sub 子类中的 test() 方法声明抛出 Exception，该 Exception 是其父类声明抛出异常 IOException 类的父类，这将导致程序无法通过编译。

所以在编写类继承代码时要注意，子类在重写父类带 throws 子句的方法时，子类方法声明中的 throws 子句不能出现父类对应方法的 throws 子句中没有的异常类型，因此 throws 子句可以限制子类的行为。也就是说，子类方法拋出的异常不能超过父类定义的范围。

### throw抛出异常

throw 语句用来直接拋出一个异常，后接一个可拋出的异常类对象，其语法格式如下：

```
throw ExceptionObject;
```

其中，ExceptionObject 必须是 Throwable 类或其子类的对象。如果是自定义异常类，也必须是 Throwable 的直接或间接子类。例如，以下语句在编译时将会产生语法错误：

```java
throw new String("拋出异常");    // String类不是Throwable类的子类
```



## 8.9多异常捕获

多 catch 代码块虽然客观上提高了程序的健壮性，但是也导致了程序代码量大大增加。如果有些异常种类不同，但捕获之后的处理是相同的，例如以下代码。

```java
try{
    // 可能会发生异常的语句
} catch (FileNotFoundException e) {
    // 调用方法methodA处理
} catch (IOException e) {
    // 调用方法methodA处理
} catch (ParseException e) {
    // 调用方法methodA处理
}
```



为了解决这种问题，java7推出了多异常捕获技术，结合修改后代码如下

```java
try{
    // 可能会发生异常的语句
} catch (IOException | ParseException e) {
    // 调用方法methodA处理
}
```

注意：由于 FileNotFoundException 属于 IOException 异常，IOException 异常可以捕获它的所有子类异常。所以不能写成 `FileNotFoundException | IOException | ParseException` 。



使用一个 catch 块捕获多种类型的异常时需要注意如下两个地方。

- 捕获多种类型的异常时，多种异常类型之间用竖线`|`隔开。
- 捕获多种类型的异常时，异常变量有隐式的 final 修饰，因此程序不能对异常变量重新赋值。



下面示例多异常捕获

```java
public class ExceptionTest {
    public static void main(String[] args) {
        try {
            int a = Integer.parseInt(args[0]);
            int b = Integer.parseInt(args[1]);
            int c = a / b;
            System.out.println("您输入的两个数相除的结果是：" + c);
        } catch (IndexOutOfBoundsException | NumberFormatException | ArithmeticException e) {
            System.out.println("程序发生了数组越界、数字格式异常、算术异常之一");
            // 捕获多异常时，异常变量默认有final修饰
            // 所以下面代码有错
            e = new ArithmeticException("test");
        } catch (Exception e) {
            System.out.println("未知异常");
            // 捕获一种类型的异常时，异常变量没有final修饰
            // 所以下面代码完全正确
            e = new RuntimeException("test");
        }
    }
}
```

上面程序中第一行粗体字代码使用了`IndexOutOfBoundsException|NumberFormatException|ArithmeticException`来定义异常类型，这就表明该 catch 块可以同时捕获这 3 种类型的异常。捕获多种类型的异常时，异常变量使用隐式的 final 修饰，因此上面程序的第 12 行代码将产生编译错误；捕获一种类型的异常时，异常变量没有 final 修饰，因此上面程序的第 17 行代码完全正确。



## 8.10自定义异常

如果Java提供的异常类型不能满足使用，可以自定义异常类型，这时异常需要继承Exception类或其他子类，如果自定义运行时异常需要继承RunException类或其子类

自定义异常语法形式如下

```java
<class><自定义异常名><extends><Exception>
```

在编码规范上，一般将自定义异常类的类名命名为XXXException，其中XXX表示异常作用

**自定义异常一般含有两个构造方法：一个是无参默认的构造方法，另一个是构造方法以字符串形式接收一个定制的异常消息，并将该消息传递给超类的构造方法**

例如，以下代码创建一个名称为 IntegerRangeException 的自定义异常类：

```java
class IntegerRangeException extends Exception {
    public IntegerRangeException() {
        super();
    }
    public IntegerRangeException(String s) {
        super(s);
    }
}

```

以上代码创建的自定义异常类 IntegerRangeException 类继承自 Exception 类，在该类中包含两个构造方法。

**例一**

编写一个程序，对会员注册时的年龄进行验证，检测是否在一到一百之间

1）这里创建了一个异常类 MyException，并提供两个构造方法。MyException 类的实现代码如下：

```java
public class MyException extends Exception {
    public MyException() {
        super();
    }
    public MyException(String str) {
        super(str);
    }
}
```

2）接着创建测试类，调用自定义异常类。代码实现如下：

```java
import java.util.InputMismatchException;
import java.util.Scanner;
public class Test07 {
    public static void main(String[] args) {
        int age;
        Scanner input = new Scanner(System.in);
        System.out.println("请输入您的年龄：");
        try {
            age = input.nextInt();    // 获取年龄
            if(age < 0) {
                throw new MyException("您输入的年龄为负数！输入有误！");
            } else if(age > 100) {
                throw new MyException("您输入的年龄大于100！输入有误！");
            } else {
                System.out.println("您的年龄为："+age);
            }
        } catch(InputMismatchException e1) {
            System.out.println("输入的年龄不是数字！");
        } catch(MyException e2) {
            System.out.println(e2.getMessage());
        }
    }
}
```

3）运行该程序，当用户输入的年龄为负数时，则拋出 MyException 自定义异常，执行第二个 catch 语句块中的代码，打印出异常信息。程序的运行结果如下所示。

```
请输入您的年龄：
-2
您输入的年龄为负数！输入有误！
```

当用户输入的年龄大于 100 时，也会拋出 MyException 自定义异常，同样会执行第二个 catch 语句块中的代码，打印出异常信息，如下所示。

```java
请输入您的年龄：
110
您输入的年龄大于100！输入有误！
```

在该程序的主方法中，使用了 if…else if…else 语句结构判断用户输入的年龄是否为负数和大于 100 的数，如果是，则拋出自定义异常 MyException，调用自定义异常类 MyException 中的含有一个 String 类型的构造方法。在 catch 语句块中捕获该异常，并调用 getMessage() 方法输出异常信息。

提示：因为自定义异常继承自 Exception 类，因此自定义异常类中包含父类所有的属性和方法。

# 9.Java集合，泛型和枚举

## 9.1集合

在编程时，可以使用数组来保存多个对象，但数组长度不可变化，一旦在初始化数组时指定了数组长度，这个数组长度就是不可变的。如果需要保存数量变化的数据，数组就有点无能为力了。而且数组无法保存具有映射关系的数据，如成绩表为语文——79，数学——80，这种数据看上去像两个数组，但这两个数组的元素之间有一定的关联关系。

为了保存数量不确定的数据，以及保存具有映射关系的数据（也被称为关联数组），java提供了集合类。***集合类主要负责保存、盛装其他数据，因此集合类也被称为容器类*。**Java 所有的集合类都位于 java.util 包下，提供了一个表示和操作对象集合的统一构架，包含大量集合接口，以及这些接口的实现类和操作它们的算法。

集合类和数组不一样，数组元素既可以是基本类型的值，也可以是对象（实际上保存的是对象的引用变量），而集合里只能保存对象（实际上只是保存对象的引用变量，但通常习惯上认为集合里保存的是对象）。

***Java 集合类型分为 Collection 和 Map***，它们是 Java 集合的根接口，这两个接口又包含了一些子接口或实现类



java集合接口

| 接口名称        | 作  用                                                       |
| --------------- | ------------------------------------------------------------ |
| Iterator 接口   | 集合的输出接口，主要用于遍历输出（即迭代访问）Collection 集合中的元素，Iterator 对象被称之为迭代器。迭代器接口是集合接口的父接口，实现类实现 Collection 时就必须实现 Iterator 接口。 |
| Collection 接口 | 是 List、Set 和 Queue 的父接口，是存放一组单值的最大接口。所谓的单值是指集合中的每个元素都是一个对象。一般很少直接使用此接口直接操作。 |
| Queue 接口      | Queue 是 Java 提供的队列实现，有点类似于 List。              |
| Dueue 接口      | 是 Queue 的一个子接口，为双向队列。                          |
| List 接口       | 是最常用的接口。是有序集合，允许有相同的元素。使用 List 能够精确地控制每个元素插入的位置，用户能够使用索引（元素在 List 中的位置，类似于数组下标）来访问 List 中的元素，与数组类似。 |
| Set 接口        | 不能包含重复的元素。                                         |
| Map 接口        | 是存放一对值的最大接口，即接口中的每个元素都是一对，以 key➡value 的形式保存。 |

java集合实现的类

| 类名称     | 作用                                                         |
| ---------- | ------------------------------------------------------------ |
| HashSet    | 为优化査询速度而设计的 Set。它是基于 HashMap 实现的，HashSet 底层使用 HashMap 来保存所有元素，实现比较简单 |
| TreeSet    | 实现了 Set 接口，是一个有序的 Set，这样就能从 Set 里面提取一个有序序列 |
| ArrayList  | 一个用数组实现的 List，能进行快速的随机访问，效率高而且实现了可变大小的数组 |
| ArrayDueue | 是一个基于数组实现的双端队列，按“先进先出”的方式操作集合元素 |
| LinkedList | 对顺序访问进行了优化，但随机访问的速度相对较慢。此外它还有 addFirst()、addLast()、getFirst()、getLast()、removeFirst() 和 removeLast() 等方法，能把它当成栈（Stack）或队列（Queue）来用 |
| HsahMap    | 按哈希算法来存取键对象                                       |
| TreeMap    | 可以对键对象进行排序                                         |

## 9.2Collection接口

Collection接口是List，Set，Queue接口的父接口，通常不直接使用



Collection接口中的常用方法

| 方法名称                          | 说明                                                         |
| --------------------------------- | ------------------------------------------------------------ |
| boolean add(E e)                  | 向集合中添加一个元素，如果集合对象被添加操作改变了，则返回 true。E 是元素的数据类型 |
| boolean addAll(Collection c)      | 向集合中添加集合 c 中的所有元素，如果集合对象被添加操作改变了，则返回 true。 |
| void clear()                      | 清除集合中的所有元素，将集合长度变为 0。                     |
| boolean contains(Object o)        | 判断集合中是否存在指定元素                                   |
| boolean containsAll(Collection c) | 判断集合中是否包含集合 c 中的所有元素                        |
| boolean isEmpty()                 | 判断集合是否为空                                             |
| Iterator<E>iterator()             | 返回一个 Iterator 对象，用于遍历集合中的元素                 |
| boolean remove(Object o)          | 从集合中删除一个指定元素，当集合中包含了一个或多个元素 o 时，该方法只删除第一个符合条件的元素，该方法将返回 true。 |
| boolean removeAll(Collection c)   | 从集合中删除所有在集合 c 中出现的元素（相当于把调用该方法的集合减去集合 c）。如果该操作改变了调用该方法的集合，则该方法返回 true。 |
| boolean retainAll(Collection c)   | 从集合中删除集合 c 里不包含的元素（相当于把调用该方法的集合变成该集合和集合 c 的交集），如果该操作改变了调用该方法的集合，则该方法返回 true。 |
| int size()                        | 返回集合中元素的个数                                         |
| Object[] toArray()                | 把集合转换为一个数组，所有的集合元素变成对应的数组元素。     |



## 9.3List集合

LIst是一个有序，可以重复的集合，集合中每个元素都有其对应的顺序索引。List集合允许使用重复元素，可以通过索引访问指定位置的集合元素，

List实现类Collection接口，它主要有两个常用类：ArrayList类和LinkedList类

### ArrayList类

ArrayList 类实现了可变数组的大小，存储在内的数据称为元素。它还提供了快速基于索引访问元素的方式，对尾部成员的增加和删除支持较好。使用 ArrayList 创建的集合，允许对集合中的元素进行快速的随机访问，不过，向 ArrayList 中插入与删除元素的速度相对较慢。



ArrayList类的常用方法：

| 方法名称                                    | 说明                                                         |
| ------------------------------------------- | ------------------------------------------------------------ |
| E get(int index)                            | 获取此集合中指定索引位置的元素，E 为集合中元素的数据类型     |
| int index(Object o)                         | 返回此集合中第一次出现指定元素的索引，如果此集合不包含该元 素，则返回 -1 |
| int lastIndexOf(Object o)                   | 返回此集合中最后一次出现指定元素的索引，如果此集合不包含该 元素，则返回 -1 |
| E set(int index, Eelement)                  | 将此集合中指定索引位置的元素修改为 element 参数指定的对象。 此方法返回此集合中指定索引位置的原元素 |
| List<E> subList(int fromlndex, int tolndex) | 返回一个新的集合，新集合中包含 fromlndex 和 tolndex 索引之间 的所有元素。包含 fromlndex 处的元素，不包含 tolndex 索引处的 元素 |

**注意：**

当调用 List 的 set(int index, Object element) 方法来改变 List 集合指定索引处的元素时，指定的索引必须是 List 集合的有效索引。例如集合长度为 4，就不能指定替换索引为 4 处的元素，也就是说这个方法不会改变 List 集合的长度。



在使用 List 集合时需要注意区分 indexOf() 方法和 lastIndexOf() 方法。前者是获得指定对象的最小索引位置，而后者是获得指定对象的最大索引位置。前提条件是指定的对象在 List 集合中有重复的对象，否则这两个方法获取的索引值相同。



使用 subList() 方法截取 List 集合中部分元素时要注意，新的集合中包含起始索引位置的元素，但是不包含结束索引位置的元素。例如，subList(1,4) 方法实际截取的是索引 1 到索引 3 的元素，并组成新的 List 集合。



### LinkedList类

该类采用链表结构保存对象，有点事便于向集合中插入或者删除元素，但是LinkedList类随机访问元素的速度先对较慢

除了Collection和List接口中的方法之外，还提供了一些常用方法

| 方法名称           | 说明                         |
| ------------------ | ---------------------------- |
| void addFirst(E e) | 将指定元素添加到此集合的开头 |
| void addLast(E e)  | 将指定元素添加到此集合的末尾 |
| E getFirst()       | 返回此集合的第一个元素       |
| E getLast()        | 返回此集合的最后一个元素     |
| E removeFirst()    | 删除此集合中的第一个元素     |
| E removeLast()     | 删除此集合中的最后一个元素   |



### ArrayList类和LinkedLIst类的区别

都是List接口的实现类因此都实现了List的所有未实现的方法，只是实现方法不一样



ArrayList是基于动态数组数据结构的实现，访问元素速度优于LinkedList。LinkedList是基于链表数据结构的实现，占用的内存空间比较大，但是再批量插入或删除时好于ArrayList

对于快速访问对象的需求，使用 ArrayList 实现执行效率上会比较好。需要频繁向集合中插入和删除元素时，使用 LinkedList 类比 ArrayList 类效果高。

## 9.4Set集合

Set集合中的对象不按照特定的方式排序

Set集合中不能包含重复的对象

Set集合中只能有一个null元素

Set实现了Collection接口，主要有两个常用实现类：HashSet和TreeSet类

### HashSet类

HashSet 是 Set 接口的典型实现，大多数时候使用 Set 集合时就是使用这个实现类。HashSet 是按照 Hash 算法来存储集合中的元素。因此具有很好的存取和查找性能。

HashSet 具有以下特点：

- 不能保证元素的排列顺序，顺序可能与添加顺序不同，顺序也有可能发生变化。
- HashSet 不是同步的，如果多个线程同时访问或修改一个 HashSet，则必须通过代码来保证其同步。
- 集合元素值可以是 null。

在 HashSet 类中实现了 Collection 接口中的所有方法。HashSet 类的常用构造方法重载形式如下。

- HashSet()：构造一个新的空的 Set 集合。
- HashSet(Collection<? extends E>c)：构造一个包含指定 Collection 集合元素的新 Set 集合。其中，“< >”中的 extends 表示 HashSet 的父类，即指明该 Set 集合中存放的集合元素类型。c 表示其中的元素将被存放在此 Set 集合中。

**示例**

```java
HashSet hs = new HashSet();//带用无参的构造函数创建
HashSet<String> hss = new HashSet<String>();//创建反省的HashSet集合对象
```



**注意**

如果向Set集合中添加相同的元素，则后面添加的元素会覆盖前面添加的元素，即Set集合中不会出现相同的元素

### TreeSet类

TreeSet 类同时实现了 Set 接口和 SortedSet 接口。SortedSet 接口是 Set 接口的子接口，可以实现对集合进行自然排序，因此使用 TreeSet 类实现的 Set 接口默认情况下是自然排序的，这里的自然排序指的是升序排序。



TreeSet 只能对实现了 Comparable 接口的类对象进行排序，因为 Comparable 接口中有一个 compareTo(Object o) 方法用于比较两个对象的大小。例如 a.compareTo(b)，如果 a 和 b 相等，则该方法返回 0；如果 a 大于 b，则该方法返回大于 0 的值；如果 a 小于 b，则该方法返回小于 0 的值。x

下面是类库中实现了Comparable接口的类和比较方式

| 类                                                           | 比较方式                                  |
| ------------------------------------------------------------ | ----------------------------------------- |
| 包装类（BigDecimal、Biglnteger、 Byte、Double、 Float、Integer、Long 及 Short) | 按数字大小比较                            |
| Character                                                    | 按字符的 Unicode 值的数字大小比较         |
| String                                                       | 按字符串中字符的 Unicode 值的数字大小比较 |

TreeSet除了实现Collection接口的所有方法之外还提供了一些其他的方法

| 方法名称                                       | 说明                                                         |
| ---------------------------------------------- | ------------------------------------------------------------ |
| E first()                                      | 返回此集合中的第一个元素。其中，E 表示集合中元素的数据类型   |
| E last()                                       | 返回此集合中的最后一个元素                                   |
| E poolFirst()                                  | 获取并移除此集合中的第一个元素                               |
| E poolLast()                                   | 获取并移除此集合中的最后一个元素                             |
| SortedSet<E> subSet(E fromElement,E toElement) | 返回一个新的集合，新集合包含原集合中 fromElement 对象与 toElement 对象之间的所有对象。包含 fromElement 对象，不包含 toElement 对象 |
| SortedSet<E> headSet<E toElement〉             | 返回一个新的集合，新集合包含原集合中 toElement 对象之前的所有对象。 不包含 toElement 对象 |
| SortedSet<E> tailSet(E fromElement)            | 返回一个新的集合，新集合包含原集合中 fromElement 对象之后的所有对 象。包含 fromElement 对象 |

**例二**

本次有 5 名学生参加考试，当老师录入每名学生的成绩后，程序将按照从低到高的排列顺序显示学生成绩。此外，老师可以查询本次考试是否有满分的学生存在，不及格的成绩有哪些，90 分以上成绩的学生有几名。

下面使用 TreeSet 类来创建 Set 集合，完成学生成绩查询功能。具体的代码如下：

```java
public class Test08 {
    public static void main(String[] args) {
        TreeSet<Double> scores = new TreeSet<Double>(); // 创建 TreeSet 集合
        Scanner input = new Scanner(System.in);
        System.out.println("------------学生成绩管理系统-------------");
        for (int i = 0; i < 5; i++) {
            System.out.println("第" + (i + 1) + "个学生成绩：");
            double score = input.nextDouble();
            // 将学生成绩转换为Double类型，添加到TreeSet集合中
            scores.add(Double.valueOf(score));
        }
        Iterator<Double> it = scores.iterator(); // 创建 Iterator 对象
        System.out.println("学生成绩从低到高的排序为：");
        while (it.hasNext()) {
            System.out.print(it.next() + "\t");
        }
        System.out.println("\n请输入要查询的成绩：");
        double searchScore = input.nextDouble();
        if (scores.contains(searchScore)) {
            System.out.println("成绩为： " + searchScore + " 的学生存在！");
        } else {
            System.out.println("成绩为： " + searchScore + " 的学生不存在！");
        }
        // 查询不及格的学生成绩
        SortedSet<Double> score1 = scores.headSet(60.0);
        System.out.println("\n不及格的成绩有：");
        for (int i = 0; i < score1.toArray().length; i++) {
            System.out.print(score1.toArray()[i] + "\t");
        }
        // 查询90分以上的学生成绩
        SortedSet<Double> score2 = scores.tailSet(90.0);
        System.out.println("\n90 分以上的成绩有：");
        for (int i = 0; i < score2.toArray().length; i++) {
            System.out.print(score2.toArray()[i] + "\t");
        }
    }
}
```

 运行结果如下

```java
------------学生成绩管理系统-------------
第1个学生成绩：
53
第2个学生成绩：
48
第3个学生成绩：
85
第4个学生成绩：
98
第5个学生成绩：
68
学生成绩从低到高的排序为：
48.0    53.0    68.0    85.0    98.0   
请输入要查询的成绩：
90
成绩为： 90.0 的学生不存在！

不及格的成绩有：
48.0    53.0   
90 分以上的成绩有：
98.0   
```

在使用自然排序时只能向TreeSet集合中添加相同数据类型的对象，否则抛出异常



## 9.5Map集合

Map 是一种键-值对（key-value）集合，Map 集合中的每一个元素都包含一个键（key）对象和一个值（value）对象。用于保存具有映射关系的数据。

Map 集合里保存着两组值，一组值用于保存 Map 里的 key，另外一组值用于保存 Map 里的 value，key 和 value 都可以是任何引用类型的数据。Map 的 key 不允许重复，value 可以重复，即同一个 Map 对象的任何两个 key 通过 equals 方法比较总是返回 false。

Map 中的 key 和 value 之间存在单向一对一关系，即通过指定的 key，总能找到唯一的、确定的 value。从 Map 中取出数据时，只要给出指定的 key，就可以取出对应的 value。

Map 接口主要有两个实现类：HashMap 类和 TreeMap 类。其中，HashMap 类按哈希算法来存取键对象，而 TreeMap 类可以对键对象进行排序。



Map接口中常用的方法

| 方法名称                                 | 说明                                                         |
| ---------------------------------------- | ------------------------------------------------------------ |
| void clear()                             | 删除该 Map 对象中的所有 key-value 对。                       |
| boolean containsKey(Object key)          | 查询 Map 中是否包含指定的 key，如果包含则返回 true。         |
| boolean containsValue(Object value)      | 查询 Map 中是否包含一个或多个 value，如果包含则返回 true。   |
| V get(Object key)                        | 返回 Map 集合中指定键对象所对应的值。V 表示值的数据类型      |
| V put(K key, V value)                    | 向 Map 集合中添加键-值对，如果当前 Map 中已有一个与该 key 相等的 key-value 对，则新的 key-value 对会覆盖原来的 key-value 对。 |
| void putAll(Map m)                       | 将指定 Map 中的 key-value 对复制到本 Map 中。                |
| V remove(Object key)                     | 从 Map 集合中删除 key 对应的键-值对，返回 key 对应的 value，如果该 key 不存在，则返回 null |
| boolean remove(Object key, Object value) | 这是 [Java](http://c.biancheng.net/java/) 8 新增的方法，删除指定 key、value 所对应的 key-value 对。如果从该 Map 中成功地删除该 key-value 对，该方法返回 true，否则返回 false。 |
| Set entrySet()                           | 返回 Map 集合中所有键-值对的 Set 集合，此 Set 集合中元素的数据类型为 Map.Entry |
| Set keySet()                             | 返回 Map 集合中所有键对象的 Set 集合                         |
| boolean isEmpty()                        | 查询该 Map 是否为空（即不包含任何 key-value 对），如果为空则返回 true。 |
| int size()                               | 返回该 Map 里 key-value 对的个数                             |
| Collection values()                      | 返回该 Map 里所有 value 组成的 Collection                    |

**例一**

每名学生都有属于自己的唯一编号，即学号。在毕业时需要将该学生的信息从系统中移除。

下面编写 Java 程序，使用 HashMap 来存储学生信息，其键为学生学号，值为姓名。毕业时，需要用户输入学生的学号，并根据学号进行删除操作。具体的实现代码如下：

```java
public class Test09 {
    public static void main(String[] args) {
        HashMap users = new HashMap();
        users.put("11", "张浩太"); // 将学生信息键值对存储到Map中
        users.put("22", "刘思诚");
        users.put("33", "王强文");
        users.put("44", "李国量");
        users.put("55", "王路路");
        System.out.println("******** 学生列表 ********");
        Iterator it = users.keySet().iterator();
        while (it.hasNext()) {
            // 遍历 Map
            Object key = it.next();
            Object val = users.get(key);
            System.out.println("学号：" + key + "，姓名:" + val);
        }
        Scanner input = new Scanner(System.in);
        System.out.println("请输入要删除的学号：");
        int num = input.nextInt();
        if (users.containsKey(String.valueOf(num))) { // 判断是否包含指定键
            users.remove(String.valueOf(num)); // 如果包含就删除
        } else {
            System.out.println("该学生不存在！");
        }
        System.out.println("******** 学生列表 ********");
        it = users.keySet().iterator();
        while (it.hasNext()) {
            Object key = it.next();
            Object val = users.get(key);
            System.out.println("学号：" + key + "，姓名：" + val);
        }
    }
}
```

在该程序中，两次使用 while 循环遍历 HashMap 集合。当有学生毕业时，用户需要输入该学生的学号，根据学号使用 HashMap 类的 remove() 方法将对应的元素删除。程序运行结果如下所示。

```
******** 学生列表 ********
学号：44，姓名:李国量
学号：55，姓名:王路路
学号：22，姓名:刘思诚
学号：33，姓名:王强文
学号：11，姓名:张浩太
请输入要删除的学号：
22
******** 学生列表 ********
学号：44，姓名：李国量
学号：55，姓名：王路路
学号：33，姓名：王强文
学号：11，姓名：张浩太
```

```java
******** 学生列表 ********
学号：44，姓名:李国量
学号：55，姓名:王路路
学号：22，姓名:刘思诚
学号：33，姓名:王强文
学号：11，姓名:张浩太
请输入要删除的学号：
44
******** 学生列表 ********
学号：55，姓名：王路路
学号：22，姓名：刘思诚
学号：33，姓名：王强文
学号：11，姓名：张浩太
```

treeMap类的使用方法与HashMap类相同，不同的是TreeMap类可以对键对象进行排序

## 9.6遍历Map集合

Map 集合的遍历与 List 和 Set 集合不同。Map 有两组值，因此遍历时可以只遍历值的集合，也可以只遍历键的集合，也可以同时遍历。Map 以及实现 Map 的接口类（如 HashMap、TreeMap、LinkedHashMap、Hashtable 等）都可以用以下几种方式遍历。

1）在for循环中使用entries实现Map的遍历

```java
public static void main(String[] args) {
    Map<String, String> map = new HashMap<String, String>();
    map.put("谢钦", "河南人");
    map.put("战地五", "好玩");
    for (Map.Entry<String, String> entry : map.entrySet()) {
        String mapKey = entry.getKey();
        String mapValue = entry.getValue();
        System.out.println(mapKey + "：" + mapValue);
    }
}
```

2)使用foreach循环遍历key和values，一般适用于只需要Map中的key或者value时使用。性能比entryset好

```java
Map<String, String> map = new HashMap<String, String>();
map.put("谢钦", "河南人");
    map.put("战地五", "好玩");
// 打印键集合
for (String key : map.keySet()) {
    System.out.println(key);
}
// 打印值集合
for (String value : map.values()) {
    System.out.println(value);
}
```

3)使用迭代器（Iterator）遍历

```java
Map<String, String> map = new HashMap<String, String>();
map.put("谢钦", "河南人");
map.put("战地五", "好玩");
Iterator<Entry<String, String>> entries = map.entrySet().iterator();
while (entries.hasNext()) {
    Entry<String, String> entry = entries.next();
    String key = entry.getKey();
    String value = entry.getValue();
    System.out.println(key + ":" + value);
}
```

4)通过键值遍历，这种方式的效率比较低，因为本身从键取值就是耗时操作

```
for(String key : map.keySet()){
    String value = map.get(key);
    System.out.println(key+":"+value);
}
```



## 9.7java8中新增的方法

## 9.8Collection类

Collections 类是 java  提供的一个操作 Set、List 和 Map 等集合的工具类。Collections 类提供了许多操作集合的静态方法，借助这些静态方法可以实现集合元素的排序、查找替换和复制等操作

### 排序(正向和逆向)

Collections 提供了如下方法用于对 List 集合元素进行排序。

- void reverse(List list)：对指定 List 集合元素进行逆向排序。
- void shuffle(List list)：对 List 集合元素进行随机排序（shuffle 方法模拟了“洗牌”动作）。
- void sort(List list)：根据元素的自然顺序对指定 List 集合的元素按升序进行排序。
- void sort(List list, Comparator c)：根据指定 Comparator 产生的顺序对 List 集合元素进行排序。
- void swap(List list, int i, int j)：将指定 List 集合中的 i 处元素和 j 处元素进行交换。
- void rotate(List list, int distance)：当 distance 为正数时，将 list 集合的后 distance 个元素“整体”移到前面；当 distance 为负数时，将 list 集合的前 distance 个元素“整体”移到后面。该方法不会改变集合的长度。



下面程序简单示范了利用 Collections 工具类来操作 List 集合。

**例一**

```java
public class Test1 {
    public static void main(String[] args) {
        Scanner input = new Scanner(System.in);
        List prices = new ArrayList();
        for (int i = 0; i < 5; i++) {
            System.out.println("请输入第 " + (i + 1) + " 个商品的价格：");
            int p = input.nextInt();
            prices.add(Integer.valueOf(p)); // 将录入的价格保存到List集合中
        }
        Collections.sort(prices); // 调用sort()方法对集合进行排序
        System.out.println("价格从低到高的排列为：");
        for (int i = 0; i < prices.size(); i++) {
            System.out.print(prices.get(i) + "\t");
        }
    }
}
```

输入后执行结果如下：

```java
请输入第 1 个商品的价格：
85
请输入第 2 个商品的价格：
48
请输入第 3 个商品的价格：
66
请输入第 4 个商品的价格：
80
请输入第 5 个商品的价格：
18
价格从低到高的排列为：
18    48    66    80    85
```

**例二**

循环录入 5 个商品的名称，并按录入时间的先后顺序进行降序排序，即后录入的先输出。

下面编写程序，使用 Collections 类的 reverse() 方法对保存到 List 集合中的 5 个商品名称进行反转排序，并输出排序后的商品信息。具体的实现代码如下：

```java
public class Test2 {
    public static void main(String[] args) {
        Scanner input = new Scanner(System.in);
        List students = new ArrayList();
        System.out.println("******** 商品信息 ********");
        for (int i = 0; i < 5; i++) {
            System.out.println("请输入第 " + (i + 1) + " 个商品的名称：");
            String name = input.next();
            students.add(name); // 将录入的商品名称存到List集合中
        }
        Collections.reverse(students); // 调用reverse()方法对集合元素进行反转排序
        System.out.println("按录入时间的先后顺序进行降序排列为：");
        for (int i = 0; i < 5; i++) {
            System.out.print(students.get(i) + "\t");
        }
    }
}
```

执行后输出结果如下

```java
******** 商品信息 ********
请输入第 1 个商品的名称：
果粒橙
请输入第 2 个商品的名称：
冰红茶
请输入第 3 个商品的名称：
矿泉水
请输入第 4 个商品的名称：
软面包
请输入第 5 个商品的名称：
巧克力
按录入时间的先后顺序进行降序排列为：
巧克力    软面包    矿泉水    冰红茶    果粒橙   
```



### 查找替换操作

Collections 还提供了如下常用的用于查找、替换集合元素的方法。

- int binarySearch(List list, Object key)：使用二分搜索法搜索指定的 List 集合，以获得指定对象在 List 集合中的索引。如果要使该方法可以正常工作，则必须保证 List 中的元素已经处于有序状态。
- Object max(Collection coll)：根据元素的自然顺序，返回给定集合中的最大元素。
- Object max(Collection coll, Comparator comp)：根据 Comparator 指定的顺序，返回给定集合中的最大元素。
- Object min(Collection coll)：根据元素的自然顺序，返回给定集合中的最小元素。
- Object min(Collection coll, Comparator comp)：根据 Comparator 指定的顺序，返回给定集合中的最小元素。
- void fill(List list, Object obj)：使用指定元素 obj 替换指定 List 集合中的所有元素。
- int frequency(Collection c, Object o)：返回指定集合中指定元素的出现次数。
- int indexOfSubList(List source, List target)：返回子 List 对象在父 List 对象中第一次出现的位置索引；如果父 List 中没有出现这样的子 List，则返回 -1。
- int lastIndexOfSubList(List source, List target)：返回子 List 对象在父 List 对象中最后一次出现的位置索引；如果父 List 中没有岀现这样的子 List，则返回 -1。
- boolean replaceAll(List list, Object oldVal, Object newVal)：使用一个新值 newVal 替换 List 对象的所有旧值 oldVal。

下面的代码展示了Collection工具类的用法

**例三**

```java
public class Test3 {
    public static void main(String[] args) {
        Scanner input = new Scanner(System.in);
        List products = new ArrayList();
        System.out.println("******** 商品信息 ********");
        for (int i = 0; i < 3; i++) {
            System.out.println("请输入第 " + (i + 1) + " 个商品的名称：");
            String name = input.next();
            products.add(name); // 将用户录入的商品名称保存到List集合中
        }
        System.out.println("重置商品信息，将所有名称都更改为'未填写'");
        Collections.fill(products, "未填写");
        System.out.println("重置后的商品信息为：");
        for (int i = 0; i < products.size(); i++) {
            System.out.print(products.get(i) + "\t");
        }
    }
}
```

运行后结果如下

```java
******** 商品信息 ********
请输入第 1 个商品的名称：
苏打水
请输入第 2 个商品的名称：
矿泉水
请输入第 3 个商品的名称：
冰红茶
重置商品信息，将所有名称都更改为'未填写'
重置后的商品信息为：
未填写    未填写    未填写    
```



**例四**

在一个集合中保存 4 个数据，分别输出最大最小元素和指定数据在集合中出现的次数。

```java
public class Test4 {
    public static void main(String[] args) {
        ArrayList nums = new ArrayList();
        nums.add(2);
        nums.add(-5);
        nums.add(3);
        nums.add(0);
        System.out.println(nums); // 输出：[2, -5, 3, 0]
        System.out.println(Collections.max(nums)); // 输出最大元素，将输出 3
        System.out.println(Collections.min(nums)); // 输出最小元素，将输出-5
        Collections.replaceAll(nums, 0, 1);// 将 nums中的 0 使用 1 来代替
        System.out.println(nums); // 输出：[2, -5, 3, 1]
        // 判断-5在List集合中出现的次数，返回1
        System.out.println(Collections.frequency(nums, -5));
        Collections.sort(nums); // 对 nums集合排序
        System.out.println(nums); // 输出：[-5, 1, 2, 3]
        // 只有排序后的List集合才可用二分法查询，输出3
        System.out.println(Collections.binarySearch(nums, 3));
    }
}
```

运行后执行结果如下

```java
[2, -5, 3, 0]
3
-5
[2, -5, 3, 1]
1
[-5, 1, 2, 3]
3
```

### 复制

Collections 类的 copy() 静态方法用于将指定集合中的所有元素复制到另一个集合中。执行 copy() 方法后，目标集合中每个已复制元素的索引将等同于源集合中该元素的索引。

copy() 方法的语法格式如下：

```java
void copy(List <? super T> dest,List<? extends T> src)
```

其中dest表示目标集合对象，src表示原集合对象

注意：目标集合的长度至少和源集合的长度相同，如果目标集合的长度更长，则不影响目标集合中的其余元素。如果目标集合长度不够而无法包含整个源集合元素，程序将抛出 IndexOutOfBoundsException 异常。

**例五**

```java
public class Test5 {
    public static void main(String[] args) {
        Scanner input = new Scanner(System.in);
        List srcList = new ArrayList();
        List destList = new ArrayList();
        destList.add("苏打水");
        destList.add("木糖醇");
        destList.add("方便面");
        destList.add("火腿肠");
        destList.add("冰红茶");
        System.out.println("原有商品如下：");
        for (int i = 0; i < destList.size(); i++) {
            System.out.println(destList.get(i));
        }
        System.out.println("输入替换的商品名称：");
        for (int i = 0; i < 3; i++) {
            System.out.println("第 " + (i + 1) + " 个商品：");
            String name = input.next();
            srcList.add(name);
        }
        // 调用copy()方法将当前商品信息复制到原有商品信息集合中
        Collections.copy(destList, srcList);
        System.out.println("当前商品有：");
        for (int i = 0; i < destList.size(); i++) {
            System.out.print(destList.get(i) + "\t");
        }
    }
}
```

结果如下

```java
原有商品如下：
苏打水
木糖醇
方便面
火腿肠
冰红茶
输入替换的商品名称：
第 1 个商品：
燕麦片
第 2 个商品：
八宝粥
第 3 个商品：
软面包
当前商品有：
燕麦片    八宝粥    软面包    火腿肠    冰红茶
```



## 9.9Lambda表达式遍历迭代器

java8 为 Iterable 接口新增了一个 forEach(Consumer action) 默认方法，该方法所需参数的类型是一个函数式接口，而 Iterable 接口是 Collection 接口的父接口，因此 Collection 集合也可直接调用该方法。

当程序调用 Iterable 的 forEach(Consumer action) 遍历集合元素时，程序会依次将集合元素传给 Consumer 的 accept(T t) 方法（该接口中唯一的抽象方法）。正因为 Consumer 是函数式接口，因此可以使用 Lambda 表达式来遍历集合元素。

如下程序示范了使用 Lambda 表达式来遍历集合元素。

```java
public class CollectionEach {
    public static void main(String[] args) {
        // 创建一个集合
        Collection objs = new HashSet();
        objs.add("C语言中文网Java教程");
        objs.add("C语言中文网C语言教程");
        objs.add("C语言中文网C++教程");
        // 调用forEach()方法遍历集合
        objs.forEach(obj -> System.out.println("迭代集合元素：" + obj));
    }
}
```

输出结果

```java
迭代集合元素：C语言中文网C++教程
迭代集合元素：C语言中文网C语言教程
迭代集合元素：C语言中文网Java教程
```

上面程序中粗体字代码调用了 Iterable 的 forEach() 默认方法来遍历集合元素，传给该方法的参数是一个 Lambda 表达式，该 Lambda 表达式的目标类型是 Comsumer。forEach() 方法会自动将集合元素逐个地传给 Lambda 表达式的形参，这样 Lambda 表达式的代码体即可遍历到集合元素了。

## 9.10使用迭代器遍历集合元素

Iterator（迭代器）是一个接口，它的作用就是遍历容器的所有元素，也是 java 集合框架的成员，但它与 Collection 和 Map 系列的集合不一样，Collection 和 Map 系列集合主要用于盛装其他对象，而 Iterator 则主要用于遍历（即迭代访问）Collection 集合中的元素。



Iterator 接口隐藏了各种 Collection 实现类的底层细节，向应用程序提供了遍历 Collection 集合元素的统一编程接口。Iterator 接口里定义了如下 4 个方法。

- boolean hasNext()：如果被迭代的集合元素还没有被遍历完，则返回 true。
- Object next()：返回集合里的下一个元素。
- void remove()：删除集合里上一次 next 方法返回的元素。
- void forEachRemaining(Consumer action)：这是 Java 8 为 Iterator 新增的默认方法，该方法可使用 Lambda 表达式来遍历集合元素。



下面程序示范了通过 Iterator 接口来遍历集合元素。

```java
import java.util.Collection;
import java.util.HashSet;
import java.util.Iterator;
public class IteratorTest {
    public static void main(String[] args) {
        // 创建一个集合
        Collection objs = new HashSet();
        objs.add("甘");
        objs.add("文");
        objs.add("崔");
        // 调用forEach()方法遍历集合
        // 获取books集合对应的迭代器
        Iterator it = objs.iterator();
        while (it.hasNext()) {
            // it.next()方法返回的数据类型是Object类型，因此需要强制类型转换
            String obj = (String) it.next();
            System.out.println(obj);
            if (obj.equals("甘")) {
                // 从集合中删除上一次next()方法返回的元素
                it.remove();
            }
            // 对book变量赋值，不会改变集合元素本身
            obj = "文";
        }
        System.out.println(objs);
    }
}
```

从上面代码中可以看出，Iterator 仅用于遍历集合，如果需要创建 Iterator 对象，则必须有一个被迭代的集合。没有集合的 Iterator 没有存在的价值。

注意：Iterator 必须依附于 Collection 对象，若有一个 Iterator 对象，则必然有一个与之关联的 Collection 对象。Iterator 提供了两个方法来迭代访问 Collection 集合里的元素，并可通过 remove() 方法来删除集合中上一次 next() 方法返回的集合元素。

上面程序中第 24 行代码对迭代变量 obj 进行赋值，但当再次输岀 objs 集合时，会看到集合里的元素没有任何改变。所以当使用 Iterator 对集合元素进行迭代时，Iterator 并不是把集合元素本身传给了迭代变量，而是把集合元素的值传给了迭代变量，所以修改迭代变量的值对集合元素本身没有任何影响。

当使用 Iterator 迭代访问 Collection 集合元素时，Collection 集合里的元素不能被改变，只有通过 Iterator 的 remove() 方法删除上一次 next() 方法返回的集合元素才可以，否则将会引发“java.util.ConcurrentModificationException”异常。下面程序示范了这一点。

```java
public class IteratorErrorTest {
    public static void main(String[] args) {
        // 创建一个集合
        Collection objs = new HashSet();
        objs.add("甘");
        objs.add("文");
        objs.add("崔");
        // 获取books集合对应的迭代器
        Iterator it = objs.iterator();
        while (it.hasNext()) {
            String obj = (String) it.next();
            System.out.println(obj);
            if (obj.equals("甘")) {
                // 使用Iterator迭代过程中，不可修改集合元素，下面代码引发异常
                objs.remove(obj);
            }
        }
    }
}
```

输出结果

```java
甘
Exception in thread "main" java.util.ConcurrentModificationException
        at java.util.HashMap$HashIterator.nextNode(Unknown Source)
        at java.util.HashMap$KeyIterator.next(Unknown Source)
        at IteratorErrorTest.main(IteratorErrorTest.java:15)
```

上面程序中第 15 行代码位于 Iterator 迭代块内，也就是在 Iterator 迭代 Collection 集合过程中修改了 Collection 集合，所以程序将在运行时引发异常。

Iterator 迭代器采用的是快速失败（fail-fast）机制，一旦在迭代过程中检测到该集合已经被修改（通常是程序中的其他线程修改），程序立即引发 ConcurrentModificationException 异常，而不是显示修改后的结果，这样可以避免共享资源而引发的潜在问题。

> 快速失败（fail-fast）机制，是 Java Collection 集合中的一种错误检测机制。

## 9.11Lambda表达式遍历迭代器



## 9.12foreach遍历Collection集合

## 9.13Predicate操作Collection集合

## 9.14Stream操作Collection集合

## 9.15java9中新增的不可变集合

## 9.16Java9中新增的菱形语法

## 9.17泛型

集合被设计成可以存放任何类型的对象，但是存放之后集合会忘记存放的对象类型，因此导致了两个问题：

1. 集合对元素类型没有任何限制，这样可能引发一些问题。例如，想创建一个只能保存 Dog 对象的集合，但程序也可以轻易地将 Cat 对象“丢”进去，所以可能引发异常。
2. 由于把对象“丢进”集合时，集合丢失了对象的状态信息，集合只知道它盛装的是 Object，因此取出集合元素后通常还需要进行强制类型转换。这种强制类型转换既增加了编程的复杂度，也可能引发 ClassCastException 异常。



所以为了解决上述问题，从 Java 1.5 开始提供了泛型。泛型可以在编译的时候检查类型安全，并且所有的强制转换都是自动和隐式的，提高了代码的重用率。



### 泛型集合

泛型本质上是提供类型的”类型参数“，也就是参数化类型。我们可以为类，接口，方法指定一个类型参数，通过这个参数显示操作的数据类型，从而保证类型转换的绝对安全

**例一**

下面将结合泛型与集合编写一个案例实现图书信息输出。

1）首先需要创建一个表示图书的实体类 Book，其中包括的图书信息有图书编号、图书名称和价格。Book 类的具体代码如下：

```java
public class Book {
    private int Id; // 图书编号
    private String Name; // 图书名称
    private int Price; // 图书价格
    public Book(int id, String name, int price) { // 构造方法
        this.Id = id;
        this.Name = name;
        this.Price = price;
    }
    public String toString() { // 重写 toString()方法
        return this.Id + ", " + this.Name + "，" + this.Price;
    }
}
```

2）使用Book作为类型的创建Map和List两个泛型集合，然后象集合中添加图书元素，最后输出集合中的元素，代码如下

```java
public class Test14 {
    public static void main(String[] args) {
        // 创建3个Book对象
        Book book1 = new Book(1, "唐诗三百首", 8);
        Book book2 = new Book(2, "小星星", 12);
        Book book3 = new Book(3, "成语大全", 22);
        Map<Integer, Book> books = new HashMap<Integer, Book>(); // 定义泛型 Map 集合
        books.put(1001, book1); // 将第一个 Book 对象存储到 Map 中
        books.put(1002, book2); // 将第二个 Book 对象存储到 Map 中
        books.put(1003, book3); // 将第三个 Book 对象存储到 Map 中
        System.out.println("泛型Map存储的图书信息如下：");
        for (Integer id : books.keySet()) {
            // 遍历键
            System.out.print(id + "——");
            System.out.println(books.get(id)); // 不需要类型转换
        }
        List<Book> bookList = new ArrayList<Book>(); // 定义泛型的 List 集合
        bookList.add(book1);
        bookList.add(book2);
        bookList.add(book3);
        System.out.println("泛型List存储的图书信息如下：");
        for (int i = 0; i < bookList.size(); i++) {
            System.out.println(bookList.get(i)); // 这里不需要类型转换
        }
    }
}
```

在该示例中，第 7 行代码创建了一个键类型为 Integer、值类型为 Book 的泛型集合，即指明了该 Map 集合中存放的键必须是 Integer 类型、值必须为 Book 类型，否则编译出错。在获取 Map 集合中的元素时，不需要将`books.get(id);`获取的值强制转换为 Book 类型，程序会隐式转换。在创建 List 集合时，同样使用了泛型，因此在获取集合中的元素时也不需要将`bookList.get(i)`代码强制转换为 Book 类型，程序会隐式转换。

执行结果如下：

```java
泛型Map存储的图书信息如下：
1001——1, 唐诗三百首，8
1003——3, 成语大全，22
1002——2, 小星星，12
泛型List存储的图书信息如下：
1, 唐诗三百首，8
2, 小星星，12
3, 成语大全，22
```

### 泛型类

除了可以定义泛型集合之外，还可以直接限定泛型类的类型参数，语法格式如下

```java
public class class_name <data_typel,data_type2,...>{}
```

其中，class_name 表示类的名称，data_ type1 等表示类型参数。Java 泛型支持声明一个以上的类型参数，只需要将类型用逗号隔开即可。

泛型类一般用于类中的属性类型不确定的情况下。在声明属性时，使用下面的语句：

```java
private data_type1 property_name1;
private data_type2 property_name2;
```

该语句中的 data_type1 与类声明中的 data_type1 表示的是同一种数据类型。

**例2** 

在实例化泛型类时，需要指明泛型类中的类型参数，并赋予泛型类属性相应类型的值。例如，下面的示例代码创建了一个表示学生的泛型类，该类中包括 3 个属性，分别是姓名、年龄和性别。

```java
public class Stu<N, A, S> {
    private N name; // 姓名
    private A age; // 年龄
    private S sex; // 性别
    // 创建类的构造函数
    public Stu(N name, A age, S sex) {
        this.name = name;
        this.age = age;
        this.sex = sex;
    }
    // 下面是上面3个属性的setter/getter方法
    public N getName() {
        return name;
    }
    public void setName(N name) {
        this.name = name;
    }
    public A getAge() {
        return age;
    }
    public void setAge(A age) {
        this.age = age;
    }
    public S getSex() {
        return sex;
    }
    public void setSex(S sex) {
        this.sex = sex;
    }
}
```

创建测试类

```java
public class Test14 {
    public static void main(String[] args) {
        Stu<String, Integer, Character> stu = new Stu<String, Integer, Character>("张晓玲", 28, '女');
        String name = stu.getName();
        Integer age = stu.getAge();
        Character sex = stu.getSex();
        System.out.println("学生信息如下：");
        System.out.println("学生姓名：" + name + "，年龄：" + age + "，性别：" + sex);
    }
}
```

结果如下

```java
学生信息如下：
学生姓名：张晓玲，年龄：28，性别：女
```

### 泛型方法

泛型可以在类中包含参数化的方法，而方法所在的类可以是泛型类，也可以不是。也就是说，是否拥有泛型方法，于其所在类是不是泛型没有关系



泛型方法是的该方法能够独立于类而产生变化。如果泛型方法可以取代类泛型化，那么就应该只使用泛型方法。



对于一个static方法而言，无法访问泛型类的类型参数，因此如果static方法需要使用泛型能力，就必须使其成为泛型方法



**定义泛型方法的语法格式如下：**

```java
[访问权限修饰符] [static] [final] <类型参数列表> 返回值类型 方法名([形式参数列表])
```

例如

```java
public static <T> List find (Class<T> cs,int userId){}
```

一般来说编写 Java 泛型方法，其返回值类型至少有一个参数类型应该是泛型，而且类型应该是一致的，如果只有返回值类型或参数类型之一使用了泛型，那么这个泛型方法的使用就被限制了。下面就来定义一个泛型方法，具体介绍泛型方法的创建和使用。

**例三**

使用泛型方法打印图书信息。定义泛型方法，参数类型使用“T”来代替。在方法的主体中打印出图书信息。代码的实现如下

```java
public class Test16 {
    public static <T> void List(T book) { // 定义泛型方法
        if (book != null) {
            System.out.println(book);
        }
    }
    public static void main(String[] args) {
        Book stu = new Book(1, "细学 Java 编程", 28);
        List(stu); // 调用泛型方法
    }
}
```

该程序中的 Book 类为前面示例中使用到的 Book 类。在该程序中定义了一个名称为 List 的方法，该方法的返回值类型为 void，类型参数使用“T”来代替。在调用该泛型方法时，将一个 Book 对象作为参数传递到该方法中，相当于指明了该泛型方法的参数类型为 Book。

该程序的运行结果如下：

```java
1, 细学 Java 编程，28
```

### 泛型的高级用法

#### 限制泛型可用类型

在Java中默认可以使用任何类型来实例化一个泛型类对象，当然也可以对泛型类实例的类型进行限制，语法格式如下：

```java
calss 类名称 <T extends anyClass> 
```

其中，anyClass 指某个接口或类。使用泛型限制后，泛型类的类型必须实现或继承 anyClass 这个接口或类。无论 anyClass 是接口还是类，在进行泛型限制时都必须使用 extends 关键字。

例如，在下面的示例代码中创建了一个 ListClass 类，并对该类的类型限制为只能是实现 List 接口的类。

```java
// 限制ListClass的泛型类型必须实现List接口
public class ListClass<T extends List> {
    public static void main(String[] args) {
        // 实例化使用ArrayList的泛型类ListClass，正确
        ListClass<ArrayList> lc1 = new ListClass<ArrayList>();
        // 实例化使用LinkedList的泛型类LlstClass，正确
        ListClass<LinkedList> lc2 = new ListClass<LinkedList>();
        // 实例化使用HashMap的泛型类ListClass，错误，因为HasMap没有实现List接口
        // ListClass<HashMap> lc3=new ListClass<HashMap>();
    }
}
```

在上述代码中，定义 ListClass 类时设置泛型类型必须实现 List 接口。例如，ArrayList 和 LinkedList 都实现了 List 接口，所以可以实例化 ListClass 类。而 HashMap 没有实现 List 接口，所以在实例化 ListClass 类时会报错。

当没有使用 extends 关键字限制泛型类型时，其实是默认使用 Object 类作为泛型类型。因此，Object 类下的所有子类都可以实例化泛型类对象，如图 1 所示的这两种情况。



![img](https://c.biancheng.net/uploads/allimg/181026/3-1Q026102419131.jpg)
图1 两个等价的泛型类

#### 适用类型通配符

作用是创建一个泛型类对象时限制这个泛型类的而理性必须实现或是继承某个接口或类

使用泛型类型通配符的语法格式如下：

```java
泛型类名称<? extends List>a = null;
```

其中<? extends List>作为一个整体表示类型未知，当需要泛型时单独实例化

下面演示使用

```jva
A <? extends List>a = null;
a = new A<ArrayList> ();    // 正确
b = new A<LinkedList> ();    // 正确
c = new A<HashMap> ();    // 错误
```

在上述代码中，同样由于 HashMap 类没有实现 List 接口，所以在编译时会报错。

####  继承泛型类和实现泛型接口

定义为泛型的类和接口也可以被继承和实现。例如下面的示例代码演示了如何继承泛型类。

```java
public class FatherClass<T1>{}
public class SonClass<T1,T2,T3> extents FatherClass<T1>{}
```

如果要在 SonClass 类继承 FatherClass 类时保留父类的泛型类型，需要在继承时指定，否则直接使用 extends FatherClass 语句进行继承操作，此时 T1、T2 和 T3 都会自动变为 Object，所以一般情况下都将父类的泛型类型保留。

下面的示例代码演示了如何在泛型中实现接口。

```java

interface interface1<T1>{}
interface SubClass<T1,T2,T3> implements
Interface1<T2>{}
```





## 9.18枚举

枚举是一个被命名的整数常数集合，用于声明一组带标识符的常数。枚举在曰常生活中很常见，例如一个人的性别只能是“男”或者“女”，一周的星期只能是 7 天中的一个等。类似这种当一个变量有几种固定可能的取值时，就可以将它定义为枚举类型。



### 声明枚举

声明枚举时必须使用 enum 关键字，然后定义枚举的名称、可访问性、基础类型和成员等。枚举声明的语法如下：

```java
enum-modifiers enum enumname:enum-base {
    enum-body,
}
```

其中，enum-modifiers 表示枚举的修饰符主要包括 public、private 和 internal；enumname 表示声明的枚举名称；enum-base 表示基础类型；enum-body 表示枚举的成员，它是枚举类型的命名常数。

**提示：如果没有显示的声明基础类型的枚举，那么意味着它所对应的基础类型时int**

**例一**

下面定义了一个表示性别的枚举类型SexEnum和一个表示颜色的枚举类型

```java
public enum SexEnum {
    male,female;
}
public enum Color {
    RED,BLUE,GREEN,BLACK;
}
```

之后便可以通过枚举类型名直接引用常量，如：SexEnum.male

使用枚举还可以使switch语句的可读性更强

```java
enum Signal {
    // 定义一个枚举类型
    GREEN,YELLOW,RED
}
public class TrafficLight {
    Signal color = Signal.RED;
    public void change() {
        switch(color) {
            case RED:
                color = Signal.GREEN;
                break;
            case YELLOW:
                color = Signal.RED;
                break;
            case GREEN:
                color = Signal.YELLOW;
                break;
        }
    }
}
```



### 枚举类

Java中所有的枚举都继承自java.lang.Enum类当定义一个枚举类型时，每一个枚举类型成员都可以看做是Enum类的实例，这些枚举成员默认都被final，public，static修饰，当使用枚举类型成员时，直接使用枚举名称调用成员即可



所有枚举实例都可以调用Enum类的实例方法，常用方法如下

| 方法名称    | 描述                               |
| ----------- | ---------------------------------- |
| values()    | 以数组的形式返回枚举类型的所有成员 |
| valueOf()   | 将普通字符串转换为枚举实例         |
| compareTo() | 比较两个枚举成员在定义时的顺序     |
| ordinal（） | 获取枚举成员的索引位置             |

**例二**

通过调用枚举类型实例的 `values( ) 方法`可以将枚举的所有成员以数组形式返回，也可以通过该方法获取枚举类型的成员。

下面的示例创建一个包含 3 个成员的枚举类型 Signal，然后调用 values() 方法输出这些成员。

```java
enum Signal{
	GREEN,YELLOW,RED;
}
public static void main(String[] args) {
    for(int i = 0;i < Signal.values().length;i++) {
        System.out.println("枚举成员："+Signal.values()[i]);
    }
}
```

输出结果如下：

```java
枚举成员：GREEN
枚举成员：YELLOW
枚举成员：RED
```

**例三**

```java
public class TestEnum {
    public enum Sex {
        // 定义一个枚举
        male,female;
    }
    public static void main(String[] args) {
        compare(Sex.valueOf("male"));    // 比较
    }
    public static void compare(Sex s) {
        for(int i = 0;i < Sex.values().length;i++) {
            System.out.println(s + "与" + Sex.values()[i] + "的比较结果是：" + s.compareTo(Sex.values()[i]));
        }
    }
}
```

上述代码中使用 Sex.valueOf("male") 取出枚举成员 male 对应的值，再将该值与其他枚举成员进行比较。最终输出结果如下：

```java
male与male的比较结果是：0
male与female的比较结果是：-1
```

**例四**

通过调用枚举类型实例的`ordinal() 方法`可以获取一个成员在枚举中的索引位置。下面的示例创建一个包含 3 个成员的枚举类型 Signal，然后调用 ordinal() 方法输出成员及对应索引位置。

具体实现代码如下：

```java
public class TestEnum1 {
    enum Signal {
        // 定义一个枚举类型
        GREEN,YELLOW,RED;
    }
    public static void main(String[] args) {
        for(int i = 0;i < Signal.values().length;i++) {
            System.out.println("索引" + Signal.values()[i].ordinal()+"，值：" + Signal.values()[i]);
        }
    }
}
```

输出结果如下：

```java
索引0，值：GREEN
索引1，值：YELLOW
索引2，值：RED
```

### 为枚举添加方法

Java 为枚举类型提供了一些内置的方法，同时枚举常量也可以有自己的方法。此时要注意必须在枚举实例的最后一个成员后添加分号，而且必须先定义枚举实例。

**例5** 

下面的代码创建了一个枚举类型 WeekDay，而且在该类型中添加了自定义的方法。

```java
enum WeekDay {
    Mon("Monday"),Tue("Tuesday"),Wed("Wednesday"),Thu("Thursday"),Fri("Friday"),Sat("Saturday"),Sun("Sunday");
    // 以上是枚举的成员，必须先定义，而且使用分号结束
    private final String day;
    private WeekDay(String day) {
        this.day = day;
    }
    public static void printDay(int i) {
        switch(i) {
            case 1:
                System.out.println(WeekDay.Mon);
                break;
            case 2:
                System.out.println(WeekDay.Tue);
                break;
            case 3:
                System.out.println(WeekDay.Wed);
                break;
            case 4:
                System.out.println(WeekDay.Thu);
                break;
            case 5:
                System.out.println(WeekDay.Fri);
                break;
            case 6:
                System.out.println(WeekDay.Sat);
                break;
            case 7:
                System.out.println(WeekDay.Sun);
                break;
            default:
                System.out.println("wrong number!");
        }
    }
    public String getDay() {
        return day;
    }
}
```



上面代码创建了 WeekDay 枚举类型，下面遍历该枚举中的所有成员，并调用 printDay() 方法。示例代码如下

```java
public static void main(String[] args) {
    for(WeekDay day : WeekDay.values()) {
        System.out.println(day+"====>" + day.getDay());
    }
    WeekDay.printDay(5);
}

```

输出结果如下：

```java
Mon====>Monday
Tue====>Tuesday
Wed====>Wednesday
Thu====>Thursday
Fri====>Friday
Sat====>Saturday
Sun====>Sunday
Fri
```

Java 中的 enum 还可以跟 Class 类一样覆盖基类的方法。下面示例代码创建的 Color 枚举类型覆盖了 toString() 方法。

```java
public class Test {
    public enum Color {
        RED("红色",1),GREEN("绿色",2),WHITE("白色",3),YELLOW("黄色",4);
        // 成员变量
        private String name;
        private int index;
        // 构造方法
        private Color(String name,int index) {
            this.name = name;
            this.index = index;
        }
        // 覆盖方法
        @Override
        public String toString() {
            return this.index + "-" + this.name;
        }
    }
    public static void main(String[] args) {
        System.out.println(Color.RED.toString());    // 输出：1-红色
    }
}
```

### EunmMap和EnumSet

#### EnumMap类

EnumMap 是专门为枚举类型量身定做的 Map 实现。虽然使用其他的 Map（如 [HashMap](http://c-local.biancheng.net/view/1067.html)）实现也能完成枚举类型实例到值的映射，但是使用 EnumMap 会更加高效。

*HashMap 只能接收同一枚举类型的实例作为键值*，并且由于枚举类型实例的数量相对固定并且有限，所以 EnumMap 使用数组来存放与枚举类型对应的值，使得 EnumMap 的效率非常高。

**例六**

```java
// 定义数据库类型枚举
public enum DataBaseType {
    MYSQUORACLE,DB2,SQLSERVER
}
// 某类中定义的获取数据库URL的方法以及EnumMap的声明
private EnumMap<DataBaseType,String>urls = new EnumMap<DataBaseType,String>(DataBaseType.class);
public DataBaseInfo() {
    urls.put(DataBaseType.DB2,"jdbc:db2://localhost:5000/sample");
    urls.put(DataBaseType.MYSQL,"jdbc:mysql://localhost/mydb");
    urls.put(DataBaseType.ORACLE,"jdbc:oracle:thin:@localhost:1521:sample");
    urls.put(DataBaseType.SQLSERVER,"jdbc:microsoft:sqlserver://sql:1433;Database=mydb");
}
//根据不同的数据库类型，返回对应的URL
// @param type DataBaseType 枚举类新实例
// @return
public String getURL(DataBaseType type) {
    return this.urls.get(type);
}
```

#### EnumSet类

EnumSet是枚举类型的高性能Set实现，**它要求放入它的枚举常量必须属于同一枚举类型**。EnumSet 提供了许多工厂方法以便于初始化，如表 2 所示。

| 方法名称                      | 描述                                                         |
| ----------------------------- | ------------------------------------------------------------ |
| allOf(Class<E> element type)  | 创建一个包含指定枚举类型中所有枚举成员的 EnumSet 对象        |
| complementOf(EnumSet<E> s)    | 创建一个与指定 EnumSet 对象 s 相同的枚举类型 EnumSet 对象， 并包含所有 s 中未包含的枚举成员 |
| copyOf(EnumSet<E> s)          | 创建一个与指定 EnumSet 对象 s 相同的枚举类型 EnumSet 对象， 并与 s 包含相同的枚举成员 |
| noneOf(<Class<E> elementType) | 创建指定枚举类型的空 EnumSet 对象                            |
| of(E first,e...rest)          | 创建包含指定枚举成员的 EnumSet 对象                          |
| range(E from ,E to)           | 创建一个 EnumSet 对象，该对象包含了 from 到 to 之间的所有枚 举成员 |

EnumSet 作为 Set 接口实现，它支持对包含的枚举常量的遍历。

```java
for(Operation op:EnumSet.range(Operation.PLUS,Operation.MULTIPLY)) {
    doSomeThing(op);
}
```

[java](www.baidu.com)

# 10.反射机制

## 10.1反射基本概念

Java 反射机制是在运行状态中，对于任意一个类，都能够知道这个类的所有属性和方法；对于任意一个对象，都能够调用它的任意方法和属性；这种动态获取信息以及动态调用对象方法的功能称为 Java 语言的反射机制。简单来说，反射机制指的是程序在运行时能够获取自身的信息。在 Java 中，只要给定类的名字，就可以通过反射机制来获得类的所有信息。

Java 反射机制在服务器程序和中间件程序中得到了广泛运用。在服务器端，往往需要根据客户的请求，动态调用某一个对象的特定方法。此外，在 ORM 中间件的实现中，运用 Java 反射机制可以读取任意一个 JavaBean 的所有属性，或者给这些属性赋值。



Java 反射机制主要提供了以下功能，这些功能都位于java.lang.reflect包。
在运行时判断任意一个对象所属的类。
在运行时构造任意一个类的对象。
在运行时判断任意一个类所具有的成员变量和方法。
在运行时调用任意一个对象的方法。
生成动态代理。

要想知道一个类的属性和方法，必须先获取到该类的字节码文件对象。获取类的信息时，使用的就是 Class 类中的方法。所以先要获取到每一个字节码文件（.class）对应的 Class 类型的对象.

众所周知，所有 Java 类均继承了 Object 类，在 Object 类中定义了一个 getClass() 方法，该方法返回同一个类型为 Class 的对象。例如，下面的示例代码：

```java
Class labelCls = label1.getClass();    // label1为 JLabel 类的对象
```

**反射的优缺点**

优点

- 能够运行时获取类的实例，大大提高系统的灵活性和扩展性
- 与 Java 动态编译相结合，可以实现无比强大的功能。
- 对于 Java 这种先编译再运行的语言，能够让我们很方便的创建灵活的代码，这些代码可以在运行时装配，无需在组件之间进行源代码的链接，更加容易实现面向对象。


缺点：

- 反射会消耗一定的系统资源，因此，如果不需要动态地创建一个对象，那么就不需要用反射；
- 反射调用方法时可以忽略权限检查，获取这个类的私有方法和属性，因此可能会破坏类的封装性而导致安全问题。

## 10.2反射API

实现java反射机制的类都位于java.lang.reflect包中，java.lang.Class是API中的核心类

### java.lang.Class类

java.lang.Class 类是实现反射的关键所在，Class 类的一个实例表示 Java 的一种数据类型，包括类、接口、枚举、注解（Annotation）、数组、基本数据类型和 void。Class 没有公有的构造方法，Class 实例是由 JVM 在类加载时自动创建的。

在程序代码中获得 Class 实例可以通过如下代码实现：

```java
// 1. 通过类型class静态变量
Class clz1 = String.class;
String str = "Hello";
// 2. 通过对象的getClass()方法
Class clz2 = str.getClass();
```

每一种类型包括类和接口等，都有一个 class 静态变量可以获得 Class 实例。另外，每一个对象都有 getClass() 方法可以获得 Class 实例，该方法是由 Object 类提供的实例方法。

```java
public class ReflectionTest01 {
    public static void main(String[] args) {
        // 获得Class实例
        // 1.通过类型class静态变量
        Class clz1 = String.class;
        String str = "Hello";
        // 2.通过对象的getClass()方法
        Class clz2 = str.getClass();
        // 获得int类型Class实例
        Class clz3 = int.class;
        // 获得Integer类型Class实例
        Class clz4 = Integer.class;
        System.out.println("clz2类名称：" + clz2.getName());
        System.out.println("clz2是否为接口：" + clz2.isInterface());
        System.out.println("clz2是否为数组对象：" + clz2.isArray());
        System.out.println("clz2父类名称：" + clz2.getSuperclass().getName());
        System.out.println("clz2是否为基本类型：" + clz2.isPrimitive());
        System.out.println("clz3是否为基本类型：" + clz3.isPrimitive());
        System.out.println("clz4是否为基本类型：" + clz4.isPrimitive());
    }
}
```

运行结果如下

```
clz2类名称：java.lang.String
clz2是否为接口：false
clz2是否为数组对象：false
clz2父类名称：java.lang.Object
clz2是否为基本类型：false
clz3是否为基本类型：true
clz4是否为基本类型：false
```

### java.lang.reflectbao

java.lang.reflect 包提供了反射中用到类，主要的类说明如下：

- Constructor 类：提供类的构造方法信息。

- Field 类：提供类或接口中成员变量信息。

- Method 类：提供类或接口成员方法信息。

- Array 类：提供了动态创建和访问 Java 数组的方法。

- Modifier 类：提供类和成员访问修饰符信息。

  ```java
  public class ReflectionTest02 {
      public static void main(String[] args) {
          try {
              // 动态加载xx类的运行时对象
              Class c = Class.forName("java.lang.String");
              // 获取成员方法集合
              Method[] methods = c.getDeclaredMethods();
              // 遍历成员方法集合
              for (Method method : methods) {
                  // 打印权限修饰符，如public、protected、private
                  System.out.print(Modifier.toString(method.getModifiers()));
                  // 打印返回值类型名称
                  System.out.print(" " + method.getReturnType().getName() + " ");
                  // 打印方法名称
                  System.out.println(method.getName() + "();");
              }
          } catch (ClassNotFoundException e) {
              System.out.println("找不到指定类");
          }
      }
  }
  ```

  上述代码第 5 行是通过 Class 的静态方法`forName(String)`创建某个类的运行时对象，其中的参数是类全名字符串，如果在类路径中找不到这个类则抛出 ClassNotFoundException 异常，见代码第 17 行。

  代码第 7 行是通过 Class 的实例方法 getDeclaredMethods() 返回某个类的成员方法对象数组。代码第 9 行是遍历成员方法集合，其中的元素是 Method 类型。

  代码第 11 行的`method.getModifiers()`方法返回访问权限修饰符常量代码，是 int 类型，例如 1 代表 public，这些数字代表的含义可以通过`Modifier.toString(int)`方法转换为字符串。代码第 13 行通过 Method 的 getReturnType() 方法获得方法返回值类型，然后再调用 getName() 方法返回该类型的名称。代码第 15 行`method.getName()`返回方法名称。

# 11.输入输出流

## 11.1流的概念

在java 中所有数据都是使用流读写的。流是一组有序的数据序列，将数据从一个地方带到另一个地方。根据数据流向的不同，可以分为输入（Input）流和输出（Output）流两种。

### 什么是输入/输出流

输入就是将数据从各种输入设备（包括文件、键盘等）中读取到内存中，输出则正好相反，是将数据写入到各种输出设备（比如文件、显示器、磁盘等）。例如键盘就是一个标准的输入设备，而显示器就是一个标准的输出设备，但是文件既可以作为输入设备，又可以作为输出设备。

数据流是 Java 进行 I/O 操作的对象，它按照不同的标准可以分为不同的类别。

- 按照流的方向主要分为输入流和输出流两大类。
- 数据流按照数据单位的不同分为字节流和字符流。
- 按照功能可以划分为节点流和处理流。



数据流的处理只能按照数据序列的顺序来进行，即前一个数据处理完之后才能处理后一个数据。数据流以输入流的形式被程序获取，再以输出流的形式将数据输出到其它设备。图 1 为输入流模式，图 2 为输出流模式。

![输入流模式](https://c.biancheng.net/uploads/allimg/200115/5-200115142HWK.png)
图 1 输入流模式

![输出流模式](https://c.biancheng.net/uploads/allimg/200115/5-200115142K1644.png)
图 2 输出流模式



### 输入流

Java 流相关的类都封装在 java.io 包中，而且每个数据流都是一个对象。所有输入流类都是 InputStream 抽象类（字节输入流）和 Reader 抽象类（字符输入流）的子类。其中 InputStream 类是字节输入流的抽象类，是所有字节输入流的父类，其层次结构如图 3 所示。



![InputStream类的层次结构图](https://c.biancheng.net/uploads/allimg/200115/5-200115145253550.png)
														图 3 InputStream类的层次结构图

InputStream 类中所有方法遇到错误时都会引发 IOException 异常。如下是该类中包含的常用方法。

| 名称                               | 作用                                                         |
| ---------------------------------- | ------------------------------------------------------------ |
| int read()                         | 从输入流读入一个 8 字节的数据，将它转换成一个 0~ 255 的整数，返回一个整数，如果遇到输入流的结尾返回 -1 |
| int read(byte[] b)                 | 从输入流读取若干字节的数据保存到参数 b 指定的字节数组中，返回的字节数表示读取的字节数，如果遇到输入流的结尾返回 -1 |
| int read(byte[] b,int off,int len) | 从输入流读取若干字节的数据保存到参数 b 指定的字节数组中，其中 off 是指在数组中开始保存数据位置的起始下标，len 是指读取字节的位数。返回的是实际读取的字节数，如果遇到输入流的结尾则返回 -1 |
| void close()                       | 关闭数据流，当完成对数据流的操作之后需要关闭数据流           |
| int available()                    | 返回可以从数据源读取的数据流的位数。                         |
| skip(long n)                       | 从输入流跳过参数 n 指定的字节数目                            |
| boolean markSupported()            | 判断输入流是否可以重复读取，如果可以就返回 true              |
| void mark(int readLimit)           | 如果输入流可以被重复读取，从流的当前位置开始设置标记，readLimit 指定可以设置标记的字节数 |
| void reset()                       | 使输入流重新定位到刚才被标记的位置，这样可以重新读取标记过的数据 |

上述最后 3 个方法一般会结合在一起使用，首先使用 markSupported() 判断，如果可以重复读取，则使用 mark(int readLimit) 方法进行标记，标记完成之后可以使用 read() 方法读取标记范围内的字节数，最后使用 reset() 方法使输入流重新定位到标记的位置，继而完成重复读取操作。



Java 中的字符是 Unicode 编码，即双字节的，而 InputerStream 是用来处理单字节的，在处理字符文本时不是很方便。这时可以使用 Java 的文本输入流 Reader 类，该类是字符输入流的抽象类，即所有字符输入流的实现都是它的子类，该类的方法与 InputerSteam 类的方法类似



### 输出流

在 Java 中所有输出流类都是 OutputStream 抽象类（字节输出流）和 Writer 抽象类（字符输出流）的子类。其中 OutputStream 类是字节输出流的抽象类，是所有字节输出流的父类，其层次结构如图 4 所示。

![OutputStream类的层次结构图](https://c.biancheng.net/uploads/allimg/200115/5-200115151G3J0.png)
													图 4 OutputStream 类的层次结构图



OutputStream 类是所有字节输出流的超类，用于以二进制的形式将数据写入目标设备，该类是抽象类，不能被实例化。OutputStream 类提供了一系列跟数据输出有关的方法，如下所示。

| 名称                                 | 作用                                                     |
| ------------------------------------ | -------------------------------------------------------- |
| int write(b)                         | 将指定字节的数据写入到输出流                             |
| int write (byte[] b)                 | 将指定字节数组的内容写入输出流                           |
| int write (byte[] b,int off,int len) | 将指定字节数组从 off 位置开始的 len 字节的内容写入输出流 |
| close()                              | 关闭数据流，当完成对数据流的操作之后需要关闭数据流       |
| flush()                              | 刷新输出流，强行将缓冲区的内容写入输出流                 |



## 11.2java系统流

每个 java 程序运行时都带有一个系统流，系统流对应的类为 java.lang.System。Sytem 类封装了 Java 程序运行时的 3 个系统流，分别通过 in、out 和 err 变量来引用。这 3 个系统流如下所示：

- System.in：标准输入流，默认设备是键盘。
- System.out：标准输出流，默认设备是控制台。
- System.err：标准错误流，默认设备是控制台。

以上变量为public和static，因此在程序的任何部分，都不需要引用System对象就可以使用

**例一**

演示如何使用System.in读取字节数组，使用System.out输出字节数组

```java
public class Test01 {
    public static void main(String[] args) {
        byte[] byteData = new byte[100]; // 声明一个字节数组
        System.out.println("请输入英文：");
        try {
            System.in.read(byteData);
        } catch (IOException e) {
            e.printStackTrace();
        }
        System.out.println("您输入的内容如下：");
        for (int i = 0; i < byteData.length; i++) {
            System.out.print((char) byteData[i]);
        }
    }
}
```

结果如下

```java
请输入英文：
abcdefg hijklmn opqrst uvwxyz
您输入的内容如下：
abcdefg hijklmn opqrst uvwxyz
```

System.in 是 InputStream 类的一个对象，因此上述代码的 System.in.read() 方法实际是访问 InputStream 类定义的 read() 方法。该方法可以从键盘读取一个或多个字符。对于 System.out 输出流主要用于将指定内容输出到控制台。

System.out 和 System.error 是 PrintStream 类的对象。因为 PrintStream 是一个从 OutputStream 派生的输出流，所以它还执行低级别的 write() 方法。因此，除了 print() 和 println() 方法可以完成控制台输出以外，System.out 还可以调用 write() 方法实现控制台输出。



write() 方法的简单形式如下：

```java
void write(int byteval) throws IOException
```

该方法通过 byteval 参数向文件写入指定的字节。在实际操作中，print() 方法和 println() 方法比 write() 方法更常用。

注意：尽管它们通常用于对控制台进行读取和写入字符，但是这些都是字节流。因为预定义流是没有引入字符流的 Java 原始规范的一部分，所以它们不是字符流而是字节流，但是在 Java 中可以将它们打包到基于字符的流中使用。

## 11.3字符编码介绍

常见编码说明如下：

- ISO8859-1：属于单字节编码，最多只能表示 0~255 的字符范围。
- GBK/GB2312：中文的国标编码，用来表示汉字，属于双字节编码。GBK 可以表示简体中文和繁体中文，而 GB2312 只能表示简体中文。GBK 兼容 GB2312。
- Unicode：是一种编码规范，是为解决全球字符通用编码而设计的。UTF-8 和 UTF-16 是这种规范的一种实现，此编码不兼容 ISO8859-1 编码。Java 内部采用此编码。
- UTF：UTF 编码兼容了 ISO8859-1 编码，同时也可以用来表示所有的语言字符，不过 UTF 编码是不定长编码，每一个字符的长度为 1~6 个字节不等。一般在中文网页中使用此编码，可以节省空间。

本地的默认编码可以使用 System 类查看。Java 中 System 类可以取得与系统有关的信息，所以直接使用此类可以找到系统的默认编码。方法如下所示：

```java
public static Properties getProperty()
```

使用上述方法可以查看 JVM 的默认编码，代码如下：

```java
public static void main(String[] args){
	//获取当前系统编码
	System.out.println("系统默认编码：" + System.getProperty("file.encoding"));
}
```



运行结果如下

```java
系统默认编码：GBK
```

可以看出，现在操作系统的默认编码是 GBK。

下面通过一个示例讲解乱码的产生。现在本地的默认编码是 GBK，下面通过 ISO8859-1 编码对文字进行编码转换。如果要实现编码的转换可以使用 String 类中的 getBytes(String charset) 方法，此方法可以设置指定的编码，该方法的格式如下：

```java
public byte[] getBytes(String charset);
```

示例如下

```java
public class Test {
    public static void main(String[] args) throws Exception {
        File f = new File("D:" + File.separator + "test.txt");
        // 实例化输出流
        OutputStream out = new FileOutputStream(f);
        // 指定ISO8859-1编码
        byte b[] = "你好世界！".getBytes("ISO8859-1");
        // 保存转码之后的数据
        out.write(b);
        // 关闭输出流
        out.close();
    }
}
```

结果是文件乱码

## 11.4File类

在Java中file类是唯一代表磁盘文件本身的对象，也就是说如果希望在程序中操作文件和目录，都可以通过File来完成



File类不能访问文件本身，如果需要访问文件本身，则需要使用输入输出流



File 类提供了如下三种形式构造方法。

1. File(String path)：如果 path 是实际存在的路径，则该 File 对象表示的是目录；如果 path 是文件名，则该 File 对象表示的是文件。
2. File(String path, String name)：path 是路径名，name 是文件名。
3. File(File dir, String name)：dir 是路径对象，name 是文件名

使用任意一个构造方法都可以创建一个 File 对象，然后调用其提供的方法对文件进行操作。在表 1 中列出了 File 类的常用方法及说明。

| 方法名称                      | 说明                                                         |
| ----------------------------- | ------------------------------------------------------------ |
| boolean canRead()             | 测试应用程序是否能从指定的文件中进行读取                     |
| boolean canWrite()            | 测试应用程序是否能写当前文件                                 |
| boolean delete()              | 删除当前对象指定的文件                                       |
| boolean exists()              | 测试当前 File 是否存在                                       |
| String getAbsolutePath()      | 返回由该对象表示的文件的绝对路径名                           |
| String getName()              | 返回表示当前对象的文件名或路径名（如果是路径，则返回最后一级子路径名） |
| String getParent()            | 返回当前 File 对象所对应目录（最后一级子目录）的父目录名     |
| boolean isAbsolute()          | 测试当前 File 对象表示的文件是否为一个绝对路径名。该方法消除了不同平台的差异，可以直接判断 file 对象是否为绝对路径。在 UNIX/Linux/BSD 等系统上，如果路径名开头是一条斜线`/`，则表明该 File 对象对应一个绝对路径；在 Windows 等系统上，如果路径开头是盘符，则说明它是一个绝对路径。 |
| boolean isDirectory()         | 测试当前 File 对象表示的文件是否为一个路径                   |
| boolean isFile()              | 测试当前 File 对象表示的文件是否为一个“普通”文件             |
| long lastModified()           | 返回当前 File 对象表示的文件最后修改的时间                   |
| long length()                 | 返回当前 File 对象表示的文件长度                             |
| String[] list()               | 返回当前 File 对象指定的路径文件列表                         |
| String[] list(FilenameFilter) | 返回当前 File 对象指定的目录中满足指定过滤器的文件列表       |
| boolean mkdir()               | 创建一个目录，它的路径名由当前 File 对象指定                 |
| boolean mkdirs()              | 创建一个目录，它的路径名由当前 File 对象指定                 |
| boolean renameTo(File)        | 将当前 File 对象指定的文件更名为给定参数 File 指定的路径名   |

File 类中有以下两个常用常量：

- public static final String pathSeparator：指的是分隔连续多个路径字符串的分隔符，Windows 下指`;`。例如 `java -cp test.jar;abc.jar HelloWorld`。
- public static final String separator：用来分隔同一个路径字符串中的目录的，Windows 下指`/`。例如 `C:/Program Files/Common Files`。

注意：可以看到 File 类的常量定义的命名规则不符合标准命名规则，常量名没有全部大写，这是因为 Java 的发展经过了一段相当长的时间，而命名规范也是逐步形成的，File 类出现较早，所以当时并没有对命名规范有严格的要求，这些都属于 Java 的历史遗留问题。

> Windows 的路径分隔符使用反斜线“\”，而 Java 程序中的反斜线表示转义字符，所以如果需要在 Windows 的路径下包括反斜线，则应该使用两条反斜线或直接使用斜线“/”也可以。Java 程序支持将斜线当成平台无关的路径分隔符。

假设在 Windows 操作系统中有一文件 `D:\javaspace\hello.java`，在 Java 中使用的时候，其路径的写法应该为 `D:/javaspace/hello.java` 或者 `D:\\javaspace\\hello.java`。



### 获取文件属性

获取文件属性的第一步是先创建一个File对象并指向那个已经存在的文件，然后调用表一的方法进行操作

**例1** 

假设有一个文件位于 `C:\windows\notepad.exe`。编写 Java 程序获取并显示该文件的长度、是否可写、最后修改日期以及文件路径等属性信息。实现代码如下：

```java
public class Test02 {
    public static void main(String[] args) {
        String path = "C:/windows/"; // 指定文件所在的目录
        File f = new File(path, "notepad.exe"); // 建立File变量,并设定由f变量引用
        System.out.println("C:\\windows\\notepad.exe文件信息如下：");
        System.out.println("============================================");
        System.out.println("文件长度：" + f.length() + "字节");
        System.out.println("文件或者目录：" + (f.isFile() ? "是文件" : "不是文件"));
        System.out.println("文件或者目录：" + (f.isDirectory() ? "是目录" : "不是目录"));
        System.out.println("是否可读：" + (f.canRead() ? "可读取" : "不可读取"));
        System.out.println("是否可写：" + (f.canWrite() ? "可写入" : "不可写入"));
        System.out.println("是否隐藏：" + (f.isHidden() ? "是隐藏文件" : "不是隐藏文件"));
        System.out.println("最后修改日期：" + new Date(f.lastModified()));
        System.out.println("文件名称：" + f.getName());
        System.out.println("文件路径：" + f.getPath());
        System.out.println("绝对路径：" + f.getAbsolutePath());
    }
}
```

### 删除和创建文件

File不仅可以获取已知文件的属性和信息，还能指定路径创建文件，创建文件的同时需要使用createNewFile（）方法，删除文件需要调用create（）方法，无论是创建还是删除都要先调用exists（）方法判断文件是否存在

**例二**

假设要在C盘上创建一个test.txt文件，程序启动时回自动检测该文件是否存在，不过不存在就创建，如果存在就删除在创建

```java
public class Test03 {
    public static void main(String[] args) throws IOException {
        File f = new File("C:\\test.txt"); // 创建指向文件的File对象
        if (f.exists()) // 判断文件是否存在
        {
            f.delete(); // 存在则先删除
        }
        f.createNewFile(); // 再创建
    }
}
```

运行程序之后可以发现，在 C 盘中已经创建好了 test.txt 文件。但是如果在不同的操作系统中，路径的分隔符是不一样的，例如：

- Windows 中使用反斜杠`\`表示目录的分隔符。
- Linux 中使用正斜杠`/`表示目录的分隔符。

那么既然 Java 程序本身具有可移植性的特点，则在编写路径时最好可以根据程序所在的操作系统自动使用符合本地操作系统要求的分隔符，这样才能达到可移植性的目的。要实现这样的功能，则就需要使用 File 类中提供的两个常量。

代码修改如下：

```java
public static void main(String[] args) throws IOException {
    String path = "C:" + File.separator + "test.txt"; // 拼凑出可以适应操作系统的路径
    File f = new File(path);
    if (f.exists()) // 判断文件是否存在
    {
        f.delete(); // 存在则先删除
    }
    f.createNewFile(); // 再创建
}
```

程序的运行结果和前面程序一样，但是此时的程序可以在任意的操作系统中使用。

注意：在操作文件时一定要使用 File.separator 表示分隔符。在程序的开发中，往往会使用 Windows 开发环境，因为在 Windows 操作系统中支持的开发工具较多，使用方便，而在程序发布时往往是直接在 Linux 或其它操作系统上部署，所以这时如果不使用 File.separator，则程序运行就有可能存在问题。关于这一点我们在以后的开发中一定要有所警惕。

### 创建和删除目录

File 类除了对文件的创建和删除外，还可以创建和删除目录。创建目录需要调用 mkdir() 方法，删除目录需要调用 delete() 方法。无论是创建还是删除目录都可以调用 exists() 方法判断目录是否存在。

**例三**

编写一个程序判断 C 盘根目录下是否存在 config 目录，如果存在则先删除再创建。实现代码如下：

```java
public class Test04 {
    public static void main(String[] args) {
        String path = "C:/config/"; // 指定目录位置
        File f = new File(path); // 创建File对象
        if (f.exists()) {
            f.delete();
        }
        f.mkdir(); // 创建目录
    }
}
```

### 遍历目录

通过遍历目录可以在指定的目录中查找文件，或者显示所有的文件列表。File 类的 list() 方法提供了遍历目录功能，该方法有如下两种重载形式。

#### 1. String[] list()

该方法表示返回由 File 对象表示目录中所有文件和子目录名称组成的字符串数组，如果调用的 File 对象不是目录，则返回 null。

提示：list() 方法返回的数组中仅包含文件名称，而不包含路径。但不保证所得数组中的相同字符串将以特定顺序出现，特别是不保证它们按字母顺序出现。

#### 2. String[] list(FilenameFilter filter)

该方法的作用与 list() 方法相同，不同的是返回数组中仅包含符合 filter 过滤器的文件和目录，如果 filter 为 null，则接受所有名称。

**例四**

遍历C盘下的所有文件和目录，并显示文件或者目录名，类型以及大小

```java
public class Test05 {
    public static void main(String[] args) {
        File f = new File("C:/"); // 建立File变量,并设定由f变量变数引用
        System.out.println("文件名称\t\t文件类型\t\t文件大小");
        System.out.println("===================================================");
        String fileList[] = f.list(); // 调用不带参数的list()方法
        for (int i = 0; i < fileList.length; i++) { // 遍历返回的字符数组
            System.out.print(fileList[i] + "\t\t");
            System.out.print((new File("C:/", fileList[i])).isFile() ? "文件" + "\t\t" : "文件夹" + "\t\t");
            System.out.println((new File("C:/", fileList[i])).length() + "字节");
        }
    }
}
```

由于 list() 方法返回的字符数组中仅包含文件名称，因此为了获取文件类型和大小，必须先转换为 File 对象再调用其方法。如下所示的是实例的运行效果

```java
$Recycle.Bin		文件夹		4096字节
$WinREAgent		文件夹		0字节
appverifUI.dll		文件		112080字节
Documents and Settings		文件夹		4096字节
DumpStack.log		文件		12288字节
DumpStack.log.tmp		文件		12288字节
hiberfil.sys		文件		6548586496字节
jetbrains-agent.jar		文件		2248607字节
JetBrainsCrack		文件夹		0字节
KuGou		文件夹		0字节
OneDriveTemp		文件夹		0字节
pagefile.sys		文件		8321499136字节
PerfLogs		文件夹		0字节
Program Files		文件夹		8192字节
Program Files (x86)		文件夹		8192字节
ProgramData		文件夹		8192字节
Recovery		文件夹		0字节
SteamLibrary		文件夹		4096字节
swapfile.sys		文件		16777216字节
System Volume Information		文件夹		8192字节
Users		文件夹		4096字节
vfcompat.dll		文件		66160字节
Windows		文件夹		16384字节

```

**例五**

假设希望只列出目录下的某些文件，这就需要调用带过滤器参数的 list() 方法。首先需要创建文件过滤器，该过滤器必须实现 `java.io.FilenameFilter` 接口，并在 accept() 方法中指定允许的文件类型。

如下所示为允许 SYS、TXT 和 BAK 格式文件的过滤器实现代码：

```java
public class ImageFilter implements FilenameFilter {
    // 实现 FilenameFilter 接口
    @Override
    public boolean accept(File dir, String name) {
        // 指定允许的文件类型
        return name.endsWith(".sys") || name.endsWith(".txt") || name.endsWith(".bak");
    }
}
```

上述代码创建的过滤器名称为 ImageFilter，接下来只需要将该名称传递给 list() 方法即可实现筛选文件。如下所示为修改后的 list() 方法，其他代码与例 4 相同，这里不再重复。

```java
String fileList[] = f.list(new ImageFilter());
```

再次运行程序，遍历结果如下所示：

```java
文件名称        文件类型        文件大小
===================================================
offline_FtnInfo.txt        文件        296字节
pagefile.sys        文件        8436592640字节
```

## 11.5字节流的使用

 InputStream 是 java所有字节输入流类的父类，OutputStream 是 Java 所有字节输出流类的父类，它们都是一个抽象类，因此继承它们的子类要重新定义父类中的抽象方法。

### 字节输入流

InputStream 类及其子类的对象表示字节输入流，InputStream 类的常用子类如下。

- ByteArrayInputStream 类：将字节数组转换为字节输入流，从中读取字节。
- FileInputStream 类：从文件中读取数据。
- PipedInputStream 类：连接到一个 PipedOutputStream（管道输出流）。
- SequenceInputStream 类：将多个字节输入流串联成一个字节输入流。
- ObjectInputStream 类：将对象反序列化。

使用 InputStream 类的方法可以从流中读取一个或一批字节。表 1 列出了 InputStream 类的常用方法。

| 方法名及返回值类型                   | 说明                                                         |
| ------------------------------------ | ------------------------------------------------------------ |
| int read()                           | 从输入流中读取一个 8 位的字节，并把它转换为 0~255 的整数，最后返回整数。 如果返回 -1，则表示已经到了输入流的末尾。为了提高 I/O 操作的效率，建议尽量 使用 read() 方法的另外两种形式 |
| int read(byte[] b)                   | 从输入流中读取若干字节，并把它们保存到参数 b 指定的字节数组中。 该方法返回 读取的字节数。如果返回 -1，则表示已经到了输入流的末尾 |
| int read(byte[] b, int off, int len) | 从输入流中读取若干字节，并把它们保存到参数 b 指定的字节数组中。其中，off 指 定在字节数组中开始保存数据的起始下标；len 指定读取的字节数。该方法返回实际 读取的字节数。如果返回 -1，则表示已经到了输入流的末尾 |
| void close()                         | 关闭输入流。在读操作完成后，应该关闭输入流，系统将会释放与这个输入流相关 的资源。注意，InputStream 类本身的 close() 方法不执行任何操作，但是它的许多 子类重写了 close() 方法 |
| int available()                      | 返回可以从输入流中读取的字节数                               |
| long skip(long n)                    | 从输入流中跳过参数 n 指定数目的字节。该方法返回跳过的字节数  |
| void mark(int readLimit)             | 在输入流的当前位置开始设置标记，参数 readLimit 则指定了最多被设置标记的字 节数 |
| boolean markSupported()              | 判断当前输入流是否允许设置标记，是则返回 true，否则返回 false |
| void reset()                         | 将输入流的指针返回到设置标记的起始处                         |

注意：在使用 mark() 方法和 reset() 方法之前，需要判断该文件系统是否支持这两个方法，以避免对程序造成影响。

### 字节输出流

OutputStream 类及其子类的对象表示一个字节输出流。OutputStream 类的常用子类如下。

- ByteArrayOutputStream 类：向内存缓冲区的字节数组中写数据。
- FileOutputStream 类：向文件中写数据。
- PipedOutputStream 类：连接到一个 PipedlntputStream（管道输入流）。
- ObjectOutputStream 类：将对象序列化

| 方法名及返回值类型                   | 说明                                                         |
| ------------------------------------ | ------------------------------------------------------------ |
| void write(int b)                    | 向输出流写入一个字节。这里的参数是 int 类型，但是它允许使用表达式， 而不用强制转换成 byte 类型。为了提高 I/O 操作的效率，建议尽量使用 write() 方法的另外两种形式 |
| void write(byte[] b)                 | 把参数 b 指定的字节数组中的所有字节写到输出流中              |
| void write(byte[] b,int off,int len) | 把参数 b 指定的字节数组中的若干字节写到输出流中。其中，off 指定字节 数组中的起始下标，len 表示元素个数 |
| void close()                         | 关闭输出流。写操作完成后，应该关闭输出流。系统将会释放与这个输出 流相关的资源。注意，OutputStream 类本身的 close() 方法不执行任何操 作，但是它的许多子类重写了 close() 方法 |
| void flush()                         | 为了提高效率，在向输出流中写入数据时，数据一般会先保存到内存缓冲 区中，只有当缓冲区中的数据达到一定程度时，缓冲区中的数据才会被写 入输出流中。使用 flush() 方法则可以强制将缓冲区中的数据写入输出流， 并清空缓冲区 |

### 字节组输入流

ByteArrayInputStream 类可以从内存的字节数组中读取数据，该类有如下两种构造方法重载形式。

1. ByteArrayInputStream(byte[] buf)：创建一个字节数组输入流，字节数组类型的数据源由参数 buf 指定。
2. ByteArrayInputStream(byte[] buf,int offse,int length)：创建一个字节数组输入流，其中，参数 buf 指定字节数组类型的数据源，offset 指定在数组中开始读取数据的起始下标位置，length 指定读取的元素个数。

**例一**

```java
public class test08 {
    public static void main(String[] args) {
        byte[] b = new byte[] { 1, -1, 25, -22, -5, 23 }; // 创建数组
        ByteArrayInputStream bais = new ByteArrayInputStream(b, 0, 6); // 创建字节数组输入流
        int i = bais.read(); // 从输入流中读取下一个字节，并转换成int型数据
        while (i != -1) { // 如果不返回-1，则表示没有到输入流的末尾
            System.out.println("原值=" + (byte) i + "\t\t\t转换为int类型=" + i);
            i = bais.read(); // 读取下一个
        }
    }
}
```

在该示例中，字节输入流 bais 从字节数组 b 的第一个元素开始读取 4 字节元素，并将这 4 字节转换为 int 类型数据，最后返回。

提示：上述示例中除了打印 i 的值外，还打印出了 (byte)i 的值，由于 i 的值是从 byte 类型的数据转换过来的，所以使用 (byte)i 可以获取原来的 byte 数据。

该程序的运行结果如下

```java
原值=1   转换为int类型=1
原值=-1   转换为int类型=255
原值=25   转换为int类型=25
原值=-22   转换为int类型=234
原值=-5   转换为int类型=251
原值=23   转换为int类型=23
```

从上述的运行结果可以看出，字节类型的数据 -1 和 -22 转换成 int 类型的数据后变成了 255 和 234，对这种结果的解释如下：

- 字节类型的 1，二进制形式为 00000001，转换为 int 类型后的二进制形式为 00000000 00000000 0000000000000001，对应的十进制数为 1。
- 字节类型的 -1，二进制形式为 11111111，转换为 int 类型后的二进制形式为 00000000 00000000 0000000011111111，对应的十进制数为 255。

可见，从字节类型的数转换成 int 类型的数时，如果是正数，则数值不变；如果是负数，则由于转换后，二进制形式前面直接补了 24 个 0，这样就改变了原来表示负数的二进制补码形式，所以数值发生了变化，即变成了正数。

提示：负数的二进制形式以补码形式存在，例如 -1，其二进制形式是这样得来的：首先获取 1 的原码 00000001，然后进行反码操作，1 变成 0，0 变成 1，这样就得到 11111110，最后进行补码操作，就是在反码的末尾位加 1，这样就变成了 11111111。

### 字节组输出流

ByteArrayOutputStream 类可以向内存的字节数组中写入数据，该类的构造方法有如下两种重载形式。

1. ByteArrayOutputStream()：创建一个字节数组输出流，输出流缓冲区的初始容量大小为 32 字节。
2. ByteArrayOutputStream(int size)：创建一个字节数组输出流，输出流缓冲区的初始容量大小由参数 size 指定。

ByteArrayOutputStream 类中除了有前面介绍的字节输出流中的常用方法以外，还有如下两个方法。

1. intsize()：返回缓冲区中的当前字节数。
2. byte[] toByteArray()：以字节数组的形式返回输出流中的当前内容。

**例二**

使用 ByteArrayOutputStream 类编写一个案例，实现将字节数组中的数据输出，代码如下所示。

```java
public class Test09 {
    public static void main(String[] args) {
        ByteArrayOutputStream baos = new ByteArrayOutputStream();
        byte[] b = new byte[] { 1, -1, 25, -22, -5, 23 }; // 创建数组
        baos.write(b, 0, 6); // 将字节数组b中的前4个字节元素写到输出流中
        System.out.println("数组中一共包含：" + baos.size() + "字节"); // 输出缓冲区中的字节数
        byte[] newByteArray = baos.toByteArray(); // 将输出流中的当前内容转换成字节数组
        System.out.println(Arrays.toString(newByteArray)); // 输出数组中的内容
    }
}
```



该程序的输出结果如下：

```java
数组中一共包含：6字节
[1, -1, 25, -22, -5, 23]
```

### 文件输入流

FileInputStream 是 Java 流中比较常用的一种，它表示从文件系统的某个文件中获取输入字节。通过使用 FileInputStream 可以访问文件中的一个字节、一批字节或整个文件。

在创建 FileInputStream 类的对象时，如果找不到指定的文件将拋出 FileNotFoundException 异常，该异常必须捕获或声明拋出。

FileInputStream 常用的构造方法主要有如下两种重载形式。

1. FileInputStream(File file)：通过打开一个到实际文件的连接来创建一个 FileInputStream，该文件通过文件系统中的 File 对象 file 指定。
2. FileInputStream(String name)：通过打开一个到实际文件的链接来创建一个 FileInputStream，该文件通过文件系统中的路径名 name 指定。

下面的示例演示了 FileInputStream() 两个构造方法的使用。

```java
try {
    // 以File对象作为参数创建FileInputStream对象
    FileInputStream fis1 = new FileInputStream(new File("F:/mxl.txt"));
    // 以字符串值作为参数创建FilelnputStream对象
    FileInputStream fis2 = new FileInputStream("F:/mxl.txt");
} catch(FileNotFoundException e) {
    System.out.println("指定的文件找不到!");
}
```

**例 3**

假设有一个 `D:\myJava\HelloJava.java` 文件，下面使用 FileInputStream 类读取并输出该文件的内容。具体代码如下：

```java
public class Test10 {
    public static void main(String[] args) {
        File f = new File("D:/myJava/HelloJava.java");
        FileInputStream fis = null;
        try {
            // 因为File没有读写的能力,所以需要有个InputStream
            fis = new FileInputStream(f);
            // 定义一个字节数组
            byte[] bytes = new byte[1024];
            int n = 0; // 得到实际读取到的字节数
            System.out.println("D:\\myJava\\HelloJava.java文件内容如下：");
            // 循环读取
            while ((n = fis.read(bytes)) != -1) {
                String s = new String(bytes, 0, n); // 将数组中从下标0到n的内容给s
                System.out.println(s);
            }
        } catch (Exception e) {
            e.printStackTrace();
        } finally {
            try {
                fis.close();
            } catch (IOException e) {
                e.printStackTrace();
            }
        }
    }
}
```

如上述代码，在 FileInputDemo 类的 main() 方法中首先创建了一个 File 对象 f，该对象指向 D:\myJava\HelloJava.java 文件。接着使用 FileInputStream 类的构造方法创建了一个 FileInputStream 对象 fis，并声明一个长度为 1024 的 byte 类型的数组，然后使用 FileInputStream 类中的 read() 方法将 HelloJava.java 文件中的数据读取到字节数组 bytes 中，并输出该数据。最后在 finally 语句中关闭 FileInputStream 输入流。

图 1 所示为 HelloJava.java 文件的原始内容，如下所示的是运行程序后的输出内容。

```java
D:\myJava\HelloJava.java文件内容如下：
/*
*第一个java程序
*/
public class HelloJava {
    // 这里是程序入口
    public static void main(String[] args) {
        // 输出字符串
        System.out.println("你好 Java");
    }
}
```

![HelloJava.java文件内容](https://c.biancheng.net/uploads/allimg/191218/5-19121Q25Z21J.png)

注意：FileInputStream 类重写了父类 InputStream 中的 read() 方法、skip() 方法、available() 方法和 close() 方法，不支持 mark() 方法和 reset() 方法。

### 文件输出流

FileOutputStream 类继承自 OutputStream 类，重写和实现了父类中的所有方法。FileOutputStream 类的对象表示一个文件字节输出流，可以向流中写入一个字节或一批字节。在创建 FileOutputStream 类的对象时，如果指定的文件不存在，则创建一个新文件；如果文件已存在，则清除原文件的内容重新写入。

FileOutputStream 类的构造方法主要有如下 4 种重载形式。

1. FileOutputStream(File file)：创建一个文件输出流，参数 file 指定目标文件。
2. FileOutputStream(File file,boolean append)：创建一个文件输出流，参数 file 指定目标文件，append 指定是否将数据添加到目标文件的内容末尾，如果为 true，则在末尾添加；如果为 false，则覆盖原有内容；其默认值为 false。
3. FileOutputStream(String name)：创建一个文件输出流，参数 name 指定目标文件的文件路径信息。
4. FileOutputStream(String name,boolean append)：创建一个文件输出流，参数 name 和 append 的含义同上。

注意：使用构造方法 FileOutputStream(String name,boolean append) 创建一个文件输出流对象，它将数据附加在现有文件的末尾。该字符串 name 指明了原文件，如果只是为了附加数据而不是重写任何已有的数据，布尔类型参数 append 的值应为 true。

对文件输出流有如下四点说明：

1. 在 FileOutputStream 类的构造方法中指定目标文件时，目标文件可以不存在。
2. 目标文件的名称可以是任意的，例如 D:\\abc、D:\\abc.de 和 D:\\abc.de.fg 等都可以，可以使用记事本等工具打开并浏览这些文件中的内容。
3. 目标文件所在目录必须存在，否则会拋出 java.io.FileNotFoundException 异常。
4. 目标文件的名称不能是已存在的目录。例如 D 盘下已存在 Java 文件夹，那么就不能使用 Java 作为文件名，即不能使用 D:\\Java，否则抛出 java.io.FileNotFoundException 异常。

**例 4**

同样是读取 D:\myJava\HelloJava.java 文件的内容，在这里使用 FileInputStream 类实现，然后再将内容写入新的文件 D:\myJava\HelloJava.txt 中。具体的代码如下：

```java
public class Test11 {
    public static void main(String[] args) {
        FileInputStream fis = null; // 声明FileInputStream对象fis
        FileOutputStream fos = null; // 声明FileOutputStream对象fos
        try {
            File srcFile = new File("D:/myJava/HelloJava.java");
            fis = new FileInputStream(srcFile); // 实例化FileInputStream对象
            File targetFile = new File("D:/myJava/HelloJava.txt"); // 创建目标文件对象，该文件不存在
            fos = new FileOutputStream(targetFile); // 实例化FileOutputStream对象
            byte[] bytes = new byte[1024]; // 每次读取1024字节
            int i = fis.read(bytes);
            while (i != -1) {
                fos.write(bytes, 0, i); // 向D:\HelloJava.txt文件中写入内容
                i = fis.read(bytes);
            }
            System.out.println("写入结束！");
        } catch (Exception e) {
            e.printStackTrace();
        } finally {
            try {
                fis.close(); // 关闭FileInputStream对象
                fos.close(); // 关闭FileOutputStream对象
            } catch (IOException e) {
                e.printStackTrace();
            }
        }
    }
}
```

如上述代码，将 D:\myJava\HelloJava.java 文件中的内容通过文件输入/输出流写入到了 D:\myJava\HelloJava.txt 文件中。由于 HelloJava.txt 文件并不存在，所以在执行程序时将新建此文件，并写入相应内容。

运行程序，成功后会在控制台输出“写入结束！”。此时，打开 D:\myJava\HelloJava.txt 文件会发现，其内容与 HelloJava.java 文件的内容相同，如图 2 所示。



![img](https://c.biancheng.net/uploads/allimg/191219/5-1912191A322507.png)
图 2



# 12.注解

## 12.1注解的概念及其作用

在Java源代码中添加的补充信息叫注解

注解并不能改变程序的运行结果，也不会影响程序运行的性能。有些注解可以在编译时给用户提示或警告，有的注解可以在运行时读写字节码文件信息。

注解可以元数据这个词来描述，即一种描述数据的数据。所以可以说注解就是源代码的元数据。例如以下代码：

```java
@Override
public String toString(){
	return "我是你爹"

}
```

