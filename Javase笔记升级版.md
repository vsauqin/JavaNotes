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





# 8.Java异常处理

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



## 9.6遍历Map集合

## 9.7java8中新增的方法

## 9.8Collection类

## 9.9Lambda表达式遍历迭代器

## 9.10使用迭代器遍历集合元素

## 9.11Lambda表达式遍历迭代器

## 9.12foreach遍历Collection集合

## 9.13Predicate操作Collection集合

## 9.14Stream操作Collection集合

## 9.15java9中新增的不可变集合

## 9.16Java9中新增的菱形语法

## 9.17泛型



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

# 12.注解

