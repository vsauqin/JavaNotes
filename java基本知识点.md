**javaSE笔记**

# java基本知识点

## 1.程序控制结构

### 1.1顺序结构

* 介绍：程序从上到下逐行执行，中间无间断和跳转。

### 1.2分支结构

#### 1.2.1 switch...case结构

1.switch(表达式){

​				case 常量1：

​				执行语句1;

​				break；

​				case 常量2：

​				执行语句2；

​				break；

​				......

​				default:

​				执行语句n；

}

* *break表示结束当前循环，如果没有break则执行下一条执行语句！*

* *表达式数据类型应和后面常量类型一致*

* *switch结构中的表达式只能是：byte，short，char，int，枚举类型（enum），string类型*

* *case之后只能声明常量或常量表达式，不能声明范围,变量*

* *break关键字可选，default相当于else，default结构可选并且位置灵活，当没有匹配条件的执行语句又没有default时什么都不输出！*

  

#### 1.2.2  if结构

1.if（条件表达式）{

​					执行表达式：*可以有多条执行语句*

}

如果执行语句只有一个大括号可省略（*建议不省略*）

```java
import java.util.scanner;
public class if{
    public static void main(String[] args){
        Scanner myScanner = new Scanner(System.in);
        System.out.println("请输入年龄")；
            int age = Myscanner.nextInt();
        if(age > 18){
            System.out.println("送进监狱！");            
        }
        System.out.println("程序继续执行!");
    }
}
```

**2**.if（条件表达式）{

​				执行表达式1

​	}

​	else{

​			执行表达式2

​	}

```java
import java.util.scanner;
public class if02{
    public static void main(String[] args){
        Scanner myScanner = new Scanner(System.in);
        System.out.println("请输入年龄")；
            int age = myscanner.nextInt();
        if(age > 18){
            System.out.println("送进监狱！");            
        }else{
            System.out.println("年龄不满十八岁暂缓入狱！");
        }
    }
}
```

**3**.if（条件表达式）{

执行表达式1

}else if（条件表达式）{

执行表达式2

}else if（条件表达式）{

执行表达式3

}

....

else{执行表达式n

}

* 多分支可以没有else，如果所有条件表达式都不成立，则一个执行入口都没有；如果有else所有条件表达式都不成立，则默认执行最后一个执行表达式！

* 嵌套分支：在一个分支结构中又完整的嵌入一个完整的分支结构。**里面的的分支结构成为内层分支，外面的称为外层分支（不建议超过三层否则可读性变差！）**

  ---

  总结：如果判断条件具体数值不多且符合byte，short，char，int，枚举类型（enum），string类型则使用switch；如果对于区间的判断或对布尔类型的判断则使用if

  

### 1.3循环结构

四个组成部分：1初始化部分，2循环条件部分，3循环体部分，4迭代部分

#### 1.3.1 for循环结构

1.for循环结构：for（初始化条件;循环条件；迭代条件）{

循环体

}

执行过程：1-2-3-4-2-3-4-...-2

---

2.死循环：for( ; ; ){

}

---

3.示例：打印一到一百九的倍数，并输出个数，计算总和

```java
public class fortest{
    public static void main(String[] args){
        int count = 0;int sum = 0;
        for(int i = 0;i < = 100;i++){
            if(i % 9 == 0){
                System.out.println("i+" + i);
                count++;
                sum += i;
            }
        }
        System.out.println("count=" + count + "sum=" + sum);
    }
}
```



#### 1.3.2 while循环结构

1.while循环的结构：

初始化条件;

while（循环条件）{

​			循环体；

​			迭代条件;

}

执行过程：1-2-3-4-2-3-4-...-2

#### 1.3.3 do while循环结构

3.do-while循环结构：

初始化条件

do{

​			循环体；

​			迭代条件；

}while（循环条件);

执行顺序：1——3——4——2*至少执行一次循环体！*先执行后循环

---

示例：

```java
import java.util.Scanner
    public class doWhile01{
        public static void main(String[] args){
            Scanner myScanner = new Scanner(System.in);
            char answer = ' ';
            de{
                System.out.println("马保国使出闪电五连鞭");
                System.out.println("你还不还钱？ Y/N");
                answer = myScanner.next().chatAt(0);
                System.put.prinitln("他的回答是" + answer);
            }while(answer != 'Y');
        }
    }
```

#### 1.3.4循环嵌套使用

1.嵌套循环：将一个循环结构与A声明在另一个循环结构B中

2.外层循环控制行数，内层循环控制列数

3.设外层执行m次内层执行n次，则一共执行m*n次

```java

```



### 1.4break，continue，return

#### 1.4.1跳转控制语句break

* 结束本次循环且下面循环不在执行，循环外的语句不受影响

每次结束默认结束最近的一个循环。如果想要结束指定循环，在循环前面和break后添加相同的标签即可！*实际开发中尽量不要使用*如果没有标签默认终止最近的循环语句！

#### 1.4.2  continue

* 结束当前循环且继续执行后面的循环

  continue也可添加标签指定结束循环！

#### 1.4.3 return

表示跳出所在方法，如果return使用在main方法中则表示退出程序！（所有语句都不再执行！）

# 2.数组，排序与查找

## 2.1数组（Array）

### 2.1.1关于数组的通用知识点

定义：多个*相同类型的数据（元素）*按一定顺序排列的集合，并使用一个名字命名，并通过编号的方式对数据进行统一管理

* 数组的反转：

  ```java
  //方法一
  int[]arr = {11,22,33,44,55,66,77,88}
  for(int i = 1;i < arr.length/2;i++){
  String temp = arr[i];
  arr[i] = arr[arr.length-i-1];
  arr[arr.length-i-1] = temp;
  }
  //方法二
  for(int i = 0,j < arr.length - 1;i < j;i++,j--){
  String temp = arr[i];
  arr[i] = arr[j];
  arr[j] = temp;
  }
  ```

* 数组中的元素可以是任何数据类型

* **数组扩容：**

  ```
  in[] arr = {1,2,3,4}
  int[] arrNew = new int[arr.length+1];
  for(int i = 0;i < arr.length;i++){
  arrNew[i] = arr[i];
  }
  arrNew[arrnew.length - 1] = 5;
  arr = arrNew;
  ```

  

* 获取数组长度：System.out.println(names.length)

* 数组的缩减：

  ```java
   int[] arr = {1,2,3,4,5};
   int[] arr1 = new int[]{arr1.length-1};
   for(int i = 0;i < arr.length-1;i++){
       arr1[1] = arr[i];
   }
        arr = arr1;
  ```

  

* 数组的下标必须在有效范围内使用，否则运行时报下标越界异常

* 数组的下标从零开始

* 数组的复制(拷贝)：

  ```java
  String[] arr = new String[]{"8","9","19"};
  String[] arr1 = new String[arr.length];
  for(int i = 0;i < arr1.length;i++){
    	arr1[i] = arr[i];
  }
  ```

  此时arr1变化不会对arr有影响！

* 数组元素的默认初始化值

  - 数组元素是整形：0
  - 数组元素是浮点型：0.0
  - 数组元素是char型：0但不是数字0
  - 数组元素是boolean型：false

  

  - 数据元素是引用数据类型：null

###  2.1.2一维数组：

* 静态初始化①：数据类型 数组名[] = new 数据类型 [] {元素值，元素值...}	

  ​							数据类型 数组名 [] = { 元素值，元素值，元素值.....}		

* 引用（使用访问获取数组元素）：数组名[下标/索引/index]

* 动态初始化：数据类型 数组名[] /数据类型[] 数组名= new 数据类型[数组长度]

​						数组可先声明再创建

如果元素已知且数量不多使用静态初始化，如果元素数量较多且不明确则使用动态初始化

### 2.1.3二维数组

1.一维数组内嵌一个一维数组叫二维数组！即数组套数组。

2.二维数组的使用

①：动态初始化

int arr [][] = new int [2] [3];

int arr [][] [] [];

arr = new int[2] [3];

列数不确定时

```java
int arr = new int [3][];
for(int i = 0;i < arr.length;i++){
    arr[i] = new int[i + 1];
    for(int j = 0;j < arr[i].length;j++){
        arr[i][j] = i+ 1;
    }
}
for(int i = 0;i < arr.length;i++){
    for(int j = 0;j < arr[i].length;j++){
        System.out.println(arr[i][j]);
    }
}
```

②静态初始化： int [] []arr = {{},{},{}};

## 2.2排序

将多个数据按指定顺序进行排列的过程有内部排序和外部排序

###  2.2.1冒泡排序

```java
class BubbleTest{
    public static void main(String[] args){
        int[] arr1 = {21,31,12,22,41,15,5,61,33};
        for(int i = 0;i < arr1.length;i++){
            for(int j = 0;j < arr1.length-i;j++){
            if(arr[j] > arr[j + 1]){
                int temp = arr[j];
                arr[j] = arr[j + 1];
                arr[j + 1] = temp;
            }
        }
            for(int j = 0;j< arr1.length;j++){
                System.out.println("输出数组arr1" + arr1);
            }
    }
        
    }
}
```





## 2.3查找

### 2.3.1顺序查找

```java
int[] ssr = {2,41,3,44,23,52,1,17,77};
int dest = 23;
for(i = 0;i < ssr.length;i++){
    if(ssr[i] = dest){
        System.out.println("目标数字的下标为：" + i);
        break;
    }
}
```



### 2.3.2二分查找

```java
int[] arr = {1,2,3,4,5,6,7,8,9,10}
int target = 7;
int head = 0;
int end = arr.length;
while(head < end){
    int mid = (head + end)/2;
    if(arr[mid] = target){
        return mid;
    }else if(arr[mid] < targert){
        head = arr[mid];
    }else{
        end = arr[mid];
    }
    return -1;
}
    
```



# 3.面向对象的编程（初级）

## 3.1类与对象

①类：一种自定义的数据类型

②对象：对类的描述（一个具体的实例）

③属性/成员变量：类的组成部分，一般是基本数据类型，也可以使用引用类型

​							*访问修饰符：`public protected `，默认，private*（控制方法使用的范围）

④如何创建对象：数据类型 数据名 = new 数据名（）



## 3.2成员方法

### 3.2.1方法使用细节

①方法声明：**权限修饰符 返回值类型 方法名（形参列表）{**

​									**方法体**

​									**return 返回值**

**}**

​                         return 语句不是必须的

​						方法主体是为了实现某一功能的代码块！**方法体里不能再次定义方法**

②返回数据类型：类型可以是任意数据类型，包含基本数据类型和引用数据类型。如果方法要求有返回数据类型，则方法中最后的执行语句一定是return，且返回值类型和return必须一致

③形参列表：一个方法中可以有零个参数，当有多个时，中间用逗号隔开。参数可以是任意数据类型。调用参数时，一定对应参数列表传入对应的数据类型或兼容类型。方法定义时参数称为形参，方法调用时传入的参数叫实参！两种参数必须类型相同或互相兼容，个数和顺序也必须一致！

形式参数可以理解为实参的统称 

### 3.2.2方法调用细节

①同一个类中的方法可直接调用

②跨类中的方法a类调用b类方法需要通过对象名调用

③跨类方法的调用和方法修饰符有关

## 3.3成员方法传参机制

①基本数据类型：传递的是值（拷贝），形参的任何改变不影响实参

②引用数据类型：引用类型传递的是地址（传递的也是值，但是地址值），可以通过形参影响实参！

③递归的重要规则：

​								执行一个方法时，就创建一个新的受保护的独立空间

​								方法的局部变量是独立的，不会相互影响

​								如果是引用类型的变量，则会共享该类型数据

​								递归必须向推出递归条件逼近否则无限递归

​								当一个方法执行完毕，或者遇到return，就会返回，遵守谁调用就将结果返回给谁。同时当方法中执行完毕或者返回时，该方法也就执行完毕

## 3.4重载

基本介绍：**java中允许同一个类中，多个同名方法的存在，但要求形参列表不一致**

 注意点：	①方法名要相同

​					②*形参列表必须不同，个数也不同*

​					③参数名没有要求，返回类型没有要求

​					

## 3.5可变参数

基本概念：java中允许将同一个类中的多个同名同功能但参与个数不同地方法，封装成同一个方法就可通过可变参数实现！

基本语法：**访问修饰符  返回类型  方法名（数据类型...形参名）{**

**}** 

 例如：

```
Public int sum(int...num){
//System.out.println("接收参数");
		int res = 0;
for(int i = 0;i < nums.length;i++){
		res += num[i];
	}
		return res;
}
```

注意事项：①可变参数可以是零也可以是多个

​					② 可变参数本质就是数组

​					③一个形参列表内只能有一个可变参数

​					④可变参数可以和普通类型的参数放在一起，但是可变参数必须在普通类型参数的后面，其前面也可以没有其他参数

```Java
public class Varargs {				//可变参数调用举例

    public static void test(String... args) {
        for(String arg : args) {
            System.out.println(arg);
        }
    }

    public static void main(String[] args) {
        test();//0个参数
        test("a");//1个参数
        test("a","b");//多个参数
        test(new String[] {"a", "b", "c"});//直接传递数组
    }
}
```



## 3.6作用域

注意事项：①属性和局部变量可以重名，访问遵循就近原则

​					②在一个作用域中，比如在一个成员方法中，两个局部变量不能重名

作用域的范围不一样：

- 全局变量可以被本类调用或其它类调用
- 局部变量只能在本类对应方法中使用

修饰符不同

​					全局变量可以加修饰符

​					局部变量不可以加修饰符

## 3.7构造器 == 构造方法（对新对象进行初始化）

### 3.7.1基本语法:

**[修饰符]   方法名(形参列表){**

​			**方法体；**

**}**

* 说明：构造器的修饰符可以是默认的

  构造器没有返回值，**不能写void**

  **方法名和类名必须一致**

  参数列表和成员方法一样的规则

  构造器的调用系统完成

​		如果程序员没有定义构造器，系统会自动给类生成一个默认构造器

* 构造方法是不能被继承的，但是可以使用super来调用，且super必须声明在在子类构造方法中的首行

### 3.7.2this关键字

* **this关键字可以用来访问本类属性，方法，构造器等**
* 用于区分当前类的属性和局部变量
* 访问成员的语法：this.方法名（形参列表）；
* 访问构造器语法：this（参数列表）；**注意只能在构造器中使用**，**必须放在第一条语句**
* this不能在类的定义外部使用，只能在类定义的方法中使用
* 当this查找到方法或者对象时就会停止查找

# 4.面向对象（中级）

## 4.1包

创建不同的文件夹或者目录来保存类文件

package的作用是声明当前类所在的包，需要放在类的最上面，一个类中最多只能有一个package

import指令位置放在package的下面，在类的定义前面，可以有多句且没有顺序要求

### 4.1.1常用的包

java.lang  //lang包是基本包，默认引入，不需要再引入

java.util    //util包，系统提供的工具包，工具类

java.net    //网络包，网络开发

java.aet    //做java的页面开发，GUI

### 4.1.2包的命名和规范

* 只能包含数字，字母，下划线，小圆点，但不能用数字开头，不能是关键字或者保留字 
* 一般是小写字母 + 小圆点

### 4.1.3包的基本语法

**package com.hspedu;**

说明

* package关键字表示打包
* com.hspedu表示包名

### 4.1.4包的三大作用

* 区分相同名字的类

* 类多时，可以很好的管理类

* 控制访问范围

  

## 4.2访问修饰符

用于控制方法和属性的访问权限

### 4.2.1访问范围和注意事项

* 公开级别：用public修饰，对外公开

* 受保护级别：用proteed修饰，对子类和同一个包中的类展开

* 默认级别：没有修饰符，向同一个包的类公开

* 私有级别：用private修饰，只有类本身可以访问，不对外公开

  ![](C:\Users\86188\Pictures\Screenshots\屏幕截图 2023-05-26 093529.png)

  **使用注意事项**

  * 修饰符可以用来修饰类中的属性，成员方法以及类
  * **只有默认和public才能修饰类！**。并遵循上述访问权限的特点
  * 成员方法的访问规则和属性完全一样

  

  

## 4.3面向对象的三大特征		

### 4.3.1封装(encapsulation)

封装就是把抽象出的数据（属性）和对数据的操作封装在一起，数据被保护在内部，程序的其他部分只有通过被授权的操作才能对数据进行操作

#### 4.3.1.1好处

1.隐藏实现细节    2.可以对数据进行验证，保证安全合理

#### 4.3.1.2封装实现步骤

* **将属性进行私有化**

* **提供一个公共的set方法，用于对属性判断并赋值**

  **public void setXxx（类型  参数名）{**

  **属性 = 参数名；**

  **}**

* **提供一个get方法，用于获取属性值** 

  **public 数据类型 getXxx（）{**

  **return xx；**

  **}**
  
  ```java
  //封装代码示例
  public class Person{
      private String name;
      private int age;
  
      public int getAge(){
        return age;
      }
  
      public String getName(){
        return name;
      }
  
      public void setAge(int age){
        this.age = age;
      }
  
      public void setName(String name){
        this.name = name;
      }
  }
  ```
  
  

### 4.3.2继承

解决代码复用性

#### 4.3.2.1super关键字

* super代表父类的引用，用于访问父类的属性，方法，构造器（私有方法，属性，构造器不能访问）

* super的访问不限于直接父类，如果上级类中有同名成员，也可以使用super去访问上级类，如果多个基类中都有同名成员使用super访问遵循就近原则

* **好处**：分工明确，父类属性由父类初始化，子类属性由子类初始化

  当子类中有和父类中的成员重名时，为了访问父类成员，必须通过super，如果没有重名，使用super，this直接访问是一样的效果
  
  ```java
  //基本语法
  super(arguments);  // 调用父构造函数
    super.parentMethod(arguments);  // 调用父方法
    
  ```
  
  

#### 4.3.2.2继承的基本语法

```java
class 子类 extends 父类{
    
}
```

子类会自动拥有父类定义的属性和方法

父类又叫超类，基类

子类又叫派生类

#### 4.3.2.3细节

* 子类继承了所有的属性和方法，但是私有属性不能在子类 直接访问，要通过公共方法访问
* 子类必须调用父类的构造器，完成父类的初始化
* 当创建子类对象时，不管使用子类的哪个构造器默认情况下总会去调用父类的无参构造器，如果父类没有提供无参构造器，则必须在子类的构造器中用super去指定使用父类的哪个构造器完成对父类的初始化工作，否则编译不通过
* 如果希望指定去调用父类的某个构造器，则显式调用一下
* super在使用时，需要放在构造器第一行
* super（）和this（）都只能放在构造器的第一行，因此这两种方法不能共存在同一个构造器中
* java中所有的类都是object的子类
* 父类构造器的调用不限于直接父类！将一直往上追溯直到Object类（顶级父类）
* 子类最多只能继承一个父类-----单继承机制
* 不能滥用继承，子类和父类之间必须满足逻辑关系

### 4.3.3override

**介绍**：子类中有一个方法，和父类的某个方法的名称，返回类型，参数一样，那我们就说子类的方法覆盖了父类的方法

**注意事项和使用细节**:

1.子类的方法的参数，方法名称，要和父类的参数，方法名称完全一致

2.子类方法的返回类型和父类方法的返回类型一样，或者时父亲返回类型的子类

3.子类方法不能缩小父类方法的权限

![](C:\Users\86188\Pictures\Screenshots\屏幕截图 2023-05-27 195550.png)



## 4.6多态

### 4.6.1对象的多态(重点中的重点)

多态的前提是：两个**对象存在继承**关系

注意事项：

属性没有重写之说，属性的值直接看编译类型

**instanceOf比较符，用于判断对象的运行类型是否为XX型或XX型的子类型**

* **一个对象的编译类型和运行类型可以不一致**
* **编译类型在定义对象时就确定了不能改变**
* **运行类型是可以变化的**
* **编译类型看定义时 = 号的左边，运行类型看 = 号的右边**

---

**java的动态绑定机制**  ***重点***

1.当调用对象方法的时候，该方法会和对象的内存地址/运行类型绑定

*即优先从运行类型中调用方法*

2.当调用对象属性时，没有动态绑定机制，哪里声明哪里使用



---



多态的向上转型

**本质**：父类的应用指向了子类的对象

**语法**：父类类型	引用名 = new 子类类型（）；

**特点**：编译类型看左边，运行类型看右边

​			可以调用父类中的所有成员（须遵守访问权限）

​			不能调用子类中特有成员

​			最终运行效果看子类的具体实现！（若子类中，没有就去父类中查找并调用）

---

多态的向下转型

**语法**：子类类型	引用名 = （ 子类类型）父类引用；

只能强转父类引用，不能强转父类对象

要求父类的引用必须指向的是当前目标类型的对象

可以调用子类类型中的所有成员

```java
public class Test {
    public static void main(String[] args) {
      show(new Cat());  // 以 Cat 对象调用 show 方法
      show(new Dog());  // 以 Dog 对象调用 show 方法
                
      Animal a = new Cat();  // 向上转型  
      a.eat();               // 调用的是 Cat 的 eat
      Cat c = (Cat)a;        // 向下转型  
      c.work();        // 调用的是 Cat 的 work
  }  
            
    public static void show(Animal a)  {
      a.eat();  
        // 类型判断
        if (a instanceof Cat)  {  // 猫做的事情 
            Cat c = (Cat)a;  
            c.work();  
        } else if (a instanceof Dog) { // 狗做的事情 
            Dog c = (Dog)a;  
            c.work();  
        }  
    }  
}
 
abstract class Animal {  
    abstract void eat();  
}  
  
class Cat extends Animal {  
    public void eat() {  
        System.out.println("吃鱼");  
    }  
    public void work() {  
        System.out.println("抓老鼠");  
    }  
}  
  
class Dog extends Animal {  
    public void eat() {  
        System.out.println("吃骨头");  
    }  
    public void work() {  
        System.out.println("看家");  
    }  
}
```



*** ***

### 4.6.2多态的应用

**多态数组**：数组的定义类型为父类类型，里面保存的实际元素类型为子类元素

```java
package com.education.encap.polyarr_;

public class polyArray {
    public static void main(String[] args){
     Person[] person = new Person[5];
     person[0] = new Person("谢钦",20);
     person[1] = new Student("谢钦",20,100);
     person[2] = new Student("谢钦",20,101);
     person[3] = new Teacher("谢钦",20,5000);
     person[4] = new Teacher("谢钦",20,6000);
     for(int i = 0;i <= 4;i++){
         System.out.println("输出信息为：" + person[i].say());
//         System.out.println("输出信息为：" + ((Student)person[i]).study());
//         System.out.println("输出信息为：" + ((Teacher)person[i]).teach());
         if(person[i] instanceof Student){
             System.out.println("输出信息为：" + ((Student)person[i]).study());
         }else if(person[i] instanceof Teacher){
             System.out.println("输出信息为：" + ((Teacher)person[i]).teach());
         }else{
             
         	}
     	}
    }
}

```

---

**多态参数**





## 4.7Object类详解

### 4.7.1equals方法

==和equals的对比

1.==既可以判断基本类型，又可以判断引用类型

2.==如果判断基本类型，判断的是值是否相等

3.==如果判断引用类型，判断的是地址是否相等，即判定是不是同一个对象

```java
A a = new A();
A b = a;
A c = b;
System.out.println(a == b);//true
System.out.println(b == c);//true
```

1.equals是Object类中的方法，只能判断引用类型

2.默认判断的是地址是否相等，子类中往往重写该方法，用于判断内容是否相等

```java
//源代码：String类的equals方法
public boolean equals(Object anObject) {
        if (this == anObject) {
            return true;
        }
        if (anObject instanceof String) {
            String anotherString = (String)anObject;
            int n = value.length;
            if (n == anotherString.value.length) {
                char v1[] = value;
                char v2[] = anotherString.value;
                int i = 0;
                while (n-- != 0) {
                    if (v1[i] != v2[i])
                        return false;
                    i++;
                }
                return true;
            }
        }
        return false;
    }
```

### 4.7.2hashCode方法

1.提高具有哈希结果的容器的效率

2.两个引用，如果指向是同一个对象，则哈希值肯定一样，相反如果是不同对象则哈希值不一样

3.哈希值主要根据地址号来的，不能完全将哈希值等价于地址

### 4.7.3toString方法

**基本介绍**：默认返回：全类名 + @ + 哈希值的十六进制【查看Object的toStriing方法】子类往往重写toString方法，用于返回对象信息

重写toString方法，打印对象或拼接对象时，都会自动调用

当直接输出一个对象时，toString方法会被默认调用

```

```

### 4.7.4finalize方法

1.当对象被收回时，系统自动调用对象的finalize方法，子类可以重写该方法，做一些释放资源的操作

2.当某个对象没有任何引用时，jvm就认为这个对象是垃圾对象，就会回收，在这之前会先调用finalize方法

3.垃圾回收机制的调用是由系统决定也可以通过System.gc()主动触发

## 4.8断点调试

纯勾八

# 5.面向对象（高级）

## 5.1类变量类方法

### 5.1.1类变量

**什么是类变量？**

类变量也叫静变量或者静态属性，是该类的所有对象共享的变量，任何一个该类的对象去访问它时，取到的都是相同的值，同样任何一个该类的对象去修改他时，修改的也是同一个变量

**如何定义变量**

\/\/\/访问修饰符  static  数据类型  变量名；（推荐）

static  访问修饰符  数据类型  变量名；

**如何访问变量**

\/\/\/类名.类变量名（推荐）

或者  对象名.类变量名

静态变量的访问修饰符和普通变量的访问修饰符的权限和范围一样

**类变量使用细节**

*1.什么时候需要使用类变量*

某个类的所有对象都共享一个变量时

*2.类变量与实例变量的区别*

类变量所有对象共享，实例变量是每个对象独享

3.加上static称为类变量或静态变量否则为实例变量/普通变量/非静态变量

4.类变量在类加载时就初始化了，也就是说，即使你没有创建对象，只要类加载了，就可以使用类变量了

7.类变量的生命周期就是随类的加载而开始，随类的消亡而销毁

### 5.1.2类方法

**注意事项**

类方法中不允许使用和对象有关的关键字，比如super和this

*类方法中只能访问静态变量或静态方法*

*普通成员方法既可以访问普通变量，也可以访问静态变量*

类方法中没有this

**类方法基本介绍**

类方法也叫静态方法，形式如下：

访问修饰符  static  数据返回类型  方法名（）{  }（推荐）

static  访问修饰符  数据返回类型  方法名（）{  }

**类方法调用**

类名.类方法名    或者    对象名.类方法名



## 5.2理解main方法语法

解释为什么main方法的形式时public static void main（String[] args){}

1.java虚拟机需要调用类的main方法，所以该方法的访问权限必须是public

2.java虚拟机在执行main（）方法时不必创建对象，所以该方法必须是static

3.该方法接收String类型的数组参数，该数组中保存执行Java命令时所传递给所运行类的参数

---

**特别提醒**

1.在main方法中，我们可以直接调用main方法所在类的静态方法或静态属性

2.不能访问该类的非静态成员，必须创建一个类的实例对象后才能访问类类的非静态成员变量

```Java
package com.test02;

public class calme {
    private static String name = "谢钦";//静态变量
    public int n1 = 33;
    //静态方法
    public static void Hi(){
        System.out.println("谢钦在学Java");
    }

    public static void main(String[] args) {
       System.out.println(name);
       calme.Hi();
       System.out.println(n1);//报错！！！
        System.out.println(new calme().n1);//不报错
    }
}

```



## 5.3代码块

### 5.3.1基本介绍

代码块也叫初始化块，属于类中的成员(类中的一部分)，类似于方法，讲逻辑语句封装在方法体中，通过{}包围起来

但是和方法不同，没有方法名，没有返回，没有参数，只有方法体，而且不用通过对象或类显式调用，而是加载类时，或创建对象时隐式调用

### 5.3.2基本语法

修饰符{

​		代码；

}

**注意**

1.修饰符可选，要写的话也只能写static

2.代码块分为两类，使用static的叫静态代码块，没有static修饰的叫普通代码块

3.逻辑语句可以为任何逻辑语句（输入，输出，方法调用，循环，判断等）

4.；可以写上也可以省

### 5.3.3代码块细节

1.static代码块也叫静态代码块，作用就是对类进行初始化，而且*它随着类的加载而执行，并且只执行一次。*如果是普通代码块，每创建一个对象就会执行一次，如果只使用类的静态成员，普通代码块不会被执行

---



**2.类什么时候被加载？**

**①创建对象实例时**

**②创建子对象实例，父类也会被加载(父类先被加载，子类后被加载)**

**③使用类的静态成员时（静态属性，静态方法）**

---



3.创建一个对象时，代码块的调用顺序

①**调用静态代码块和静态属性初始化**（注意：静态代码块和静态属性初始化调用的优先级一致，如果有多个静态代码块和多个静态变量初始化，则按他们的定义顺序调用）

**②调用普通代码块和普通属性的初始化**（注意：优先级一样，如果普通代码块和多个普通属性初始化，则按定义顺序调用）

**③调用构造方法**

---



4.构造器前面其实隐含了super（）和调用普通代码块

---



5.创建一个子类，他们的静态代码块，静态属性初始化，普通代码块，普通属性初始化，构造方法的调用顺序如下：

①父类的静态代码块和静态属性（优先级一样按顺序执行）

②子类的静态代码块和静态属性（优先级一样按顺序执行）

③父类的普通代码块和普通属性初始化（优先级一样按顺序执行）

④父类的构造方法

⑤子类的普通代码块和普通属性初始化（优先级一样按顺序执行）

⑥子类构造方法

6.静态代码块可以直接调用非静态的成员变量

## 5.4单例设计模式

### 5.4.1饿汉式

**实现步骤**

1）构造器私有化

2）在类的内部创建对象

3）向外暴露一个静态的公共方法

4）代码实现

```java
class Girlfriend{
    private static String name;
    private static Girlfriend gf = new Girlfriend("小红");
    private instance(String name){
        this.name = name;
    }
    public static instence(){
        return gf;
    }
}

```



## 5.5final关键字

### 5.5.1final使用注意事项和细节

* final修饰的属性又叫常量，一般用XX XX XX来命名

* final修饰的属性在定义时，必须赋初值，并且以后不能再修改，赋值可以在以下位置之一（选择一个位置赋初值即可）

  一，定义时：如public  final  double  TAX_RATE = 0.08

  二，在构造器中

  三，在代码块中

* 如果final修饰的属性是静态的则初始化的位置只能是

  一，定义时

  二，在静态代码块，不能在构造器中赋值

* **final类不能继承，但是可以实现实例化对象**

* 如果类不是final类，但是含有final方法，则该方法虽然不能重写，但是可以被继承

* 一般来说如果 一个类已经是final类了，就没有必要再将方法修饰称final方法了。因为final类无法被继承final方法根本无法被重写

* fianl不能修饰构造器方法（即构造器）

* 包装类（Integer,Double,Float,Boolean等都是final）String 也是final类

* final和static往往搭配使用效率更高，不会导致类加载，底层编译器做了优化处理

  ```
  class Demo{
  		public static final int i = 16;
  		static{
  		System.out.println("谢钦一定他妈得学好Java")
  		}
  }
  ```

  

### 5.5.2基本介绍

可以修饰类，属性，方法和局部变量   以下需求可能用到Final

### 5.5.3使用场景

* 当不希望类被继承时使用final修饰

* 当不希望父类的某个方法被子类覆盖或者重写时，可以用final关键字修饰

* 当不希望类的，某个属性的值被修改可以用final修饰

* 当不希望某个局部变量被修改可以用final修饰

  

## 5.6抽象类

当父类的某些方法，需要声明，但是又不确定如何实现时，可以将其声明为抽象方法，那么这个类就是抽象类（**没有方法体**）

例如

```java
abstract class Animal{
    orivate String name;
    public Animal(String name){
        this.name = name;
    }
    public abstract void eat();
}
//当一个类中有抽象方法时，需要把这个类声明为抽象方法
```

### 5.6.1抽象类的介绍

* 用abstract关键字来修饰一个类时，这个类就叫抽象类

  访问修饰符  abstract  类名{

  }

* 用abstract关键字来修饰一个方法时，这个方法就是抽象方法

  **访问修饰符  abstract  返回类型  方法名（参数列表）；//没有方法主体**

* 抽象类的价值更多作用是在于设计，是设计者设计好后，让子类继承并实现的抽象类（）

* 在框架和设计模式使用较多

### 5.6.2抽象类使用注意事项和细节讨论

* 抽象类不能被实例化
* 抽象类不一定包含abstract方法，也就是说，抽象类可以没有abstract方法
* 一旦类包含了abstract方法，则这个类必须声明为abstract
* abstract只能修饰类和方法，不能修饰属性和其他的
* 抽象类可以有任意成员【因为抽象类还是类】，比如：非抽象方法，构造器，静态属性等等
* 抽象方法不能有主体，即不能实现
* 如果一个类继承了抽象类，则它必须实现抽象类的所有抽象方法，除非她自己也声明为abstract类

### 



## 5.7接口

**基本介绍：**接口就是给出一些没有实现的方法，封装到一起，到某个类要使用的时候，再根据具体情况把这些方法写出来

### 5.7.1接口的使用细节和注意事项

* 接口不能实例化
* 接口中所有方法都是public方法，接口中的抽象方法可以不用abstract修饰
* **一个普通类实现接口，就必须将该接口的所有方法都实现**
* 抽象类实现接口，可以不用实现接口的方法
* **一个类可以实现多个接口**
* 接口中的属性只能是final的，而且是public  static  final  修饰符；比如int  a  = 1；实际上是public  static  final  int  a  =  1；
* **接口中属性的访问形式：接口名.属性名**
* 一个接口不能继承其他的类，但是可以继承多个别的接口
* 接口的修饰符只能是public和默认，这点和类的修饰符一样

### 5.7.2接口和继承类

* 实现是对单继承的一种补充 
* 继承：当子类继承了父类就自动有了父类的功能，如果需要扩展功能，可以通过接口实现
* 解决问题不同

​		继承的价值在于解决代码复用性的问题

​		接口主要是设计好各种规范，让其它类去实现它

* 接口比继承更加灵活
* 接口在一定程度上实现代码解耦

### 5.7.3接口的多态

也有向上转型和向下转型

* **接口的动态传递：** 接口与接口之间可以继承，若此时有一个类实现了子类接口，那么相当于实现了父类接口中的所有方法

* ```java
  interface IH{
  	void hi();
  }
  interface IG extends IH{
  
  }
  class Teacher implements IG{
  	public void hi(){
  	
  	}
  }
  ```

  

## 5.8内部类

### 5.8.1内部类基本点

* 基本介绍：一个类的内部又完整的嵌套了另一个类结构，被嵌套的类称为内部类，嵌套其他类的类成为外部类，是我们类的第五大成员，内部类的最大特点就是***可以直接访问私有属性，并且可以体现类与类之间的包含关系***
* 基本语法：   

class Outer{//外部类

​		class Inner{//内部类

​		}

}

class Other{//外部其他类

}

* 分类：定义在外部类局部上（比如方法内）：
  * 局部内部类(有类名)
  * 匿名内部类（没有类名）
* 定义在外部类的成员位置上：
  * 成员内部类（没用static修饰）
  * 静态内部类（使用static修饰）

### 5.8.2局部内部类

* 可以直接访问外部类的所有成员，比如方法中并且有类名
* 不能使用访问修饰符，因为他的地位就是一个局部变量，局部变量不能使用修饰符，但是可以使用final修饰，因为局部变量也可以使用final
* 作用域仅仅在定义它的方法或者代码块中
* 局部内部类可以直接访问外部类成员
* 外部类成员访问内部类成员需要创建内部类对象然后调用方法即可 
* 外部其他类不能访问内部类
* **如果外部类和局部内部类的成员重名时，默认遵循就近原则，如果想访问外部类的成员，可以使用(外部类类名.this.成员)去访问**



### 5.8.3匿名内部类(重点)

* 匿名内部类基本语法：

new **类**或**接口**（参数列表）{

​					类体

}；

* 匿名内部类使用一次就不能再使用了，但是对象可以一直调用
* 如果是基于类的匿名内部类，形参列表里的参数会传回

---

**匿名内部类的细节**

* 调用匿名内部类的方法：
* 可以访问外部类所有成员，包含私有的；外部其他类不能访问匿名内部类
* 不能添加访问修饰符，因为他的地位相当于一个局部变量
* 作用于仅仅在定义它的方法或者代码块中
* 如果外部类成员和匿名内部类成员重名时，，匿名内部类访问的话默认遵循就近原则，如果想访问外部类成员，则可以使用（外部类.this.成员）去访问

---

```JAVA
public class AnonymouClass {
    public static void main(String[] args){
        CellPhone cellPhone = new CellPhone();
        cellPhone.alarmClock(new Bell() {
            @Override
            public void ring() {
                System.out.println("懒猪起床了！！！");
                }
            });
        cellPhone.alarmClock(new Bell() {
            @Override
            public void ring() {
                System.out.println("起床上课了");
            }
        });
    }
}
interface Bell{
    void ring();
}
class CellPhone{
    public void alarmClock(Bell bell){
        bell.ring();
    }
}
```

### 5.8.4成员内部类

定义在外部类的成员位置，并且没有static修饰

---

* 可以直接访问外部类所有成员，包含私有的
* 可以添加任意访问修饰符，因为他就是一个成员

```JAVA
package com.education.innerclass;

public class Memberberiber {
    public static void main(String[] args){
        Outer08 outer08 = new Outer08();
        outer08.t1();
        //外部类访问成员内部类第一种方法
        Outer08.Inner inner = outer.new Inner08();
        inner.say();
        //第二种编写一个方法返回一个实例
        Outer08.Inner getInner = outer08.getInnerInstance();
        innerInstance.say();
    }
}
class Outer08{
    private int n1 = 10;
    private String name = "张三";
    //成员内部类,既没写在方法中也没在代码块中
    class Inner{
        public void asy(){
            System.out.println(n1 + name);
        }
    }
    public Inner getInnerInstance(){
        return new Inner();
    }
    public void t1(){
        Inner inner = new Inner();
        inner.asy();
    }
}
```

* 作用域和外部类其他成员一样为整个类体，**若是想调用需要在外部类成员方法中创建成员内部类对象**
* 内部类访问外部类成员直接访问，方法也是直接访问
* 外部类访问成员内部类先创建内部类对象
* 外部其他类也可以访问成员内部类
* 成员重名和上面一样遵循就近原则；外部类名.this.属性

### 5.8.5静态内部类

定义在外部类的成员位置，并且**有static修饰**

---

* 可以直接访问外部类所有静态成员，包含私有，但是不能直接访问非静态成员

*  可以添加任访问修饰符

* 作用域和其他成员一样为整个类体

* 静态内部类要访问外部类时可以访问外部类所有静态成员

* 外部类访问内部类先创建对象再访问

* 外部其他类访问静态内部类 

  * 通过类名直接访问并且需要满足访问权限

  * ```JAVA
    Outer.Inner inner = new Outer.Inner();
    inner.say();
    ```

  * 编写一个方法可以返回内部类对象实例,如果是静态方法不需要再创建对象

  * ```java
    //调用格式
    Outer.Inner inner = outer.getInner();
    inner.say();
    //编写的方法
    public Inner getInner(){
        return new Inner();
    }
    ```

* 重名问题依然遵循就近原则，若是想优先访问外部类属性格式为（外部类名.成员）



# 6.枚举和注解

## 6.1自定义实现枚举

* 不需要提供set方法，枚举对象值通常为只读
* 对枚举对象或者属性使用final + static共同修饰实现底层优化
* 枚举对象名通常使用全部大写，常量的命名规范
* 枚举对象根据需要也可以有多个属性

```java
package com.xqxuejava.enum_;

public class Enumeration01 {
    public static void main(String[] args) {
		System.out.println(Season.SPRING);
    }
}
class Season{
    private String name;
    private String deac;
    //对象固定
    public static final Season SPRING = new Season("春天","温暖");
    public static final Season SUMMER = new Season("夏天","炎热");
    public static final Season AUTUMN = new Season("秋天","凉爽");
    public static final Season WINTER = new Season("冬天","寒冷");
    //1,将构造器私有化，防止直接new对象
    //2，去掉set方法防止属性被修改
    //3，在Season内部直接创建固定对象
    private Season(String name,String deac){
        this.deac = deac;
        this.name = name;
    }

    public String getName() {
        return name;
    }

    public String getDeac() {
        return deac;
    }

    @Override
    public String toString() {
        return "Season{" +
                "name='" + name + '\'' +
                ", deac='" + deac + '\'' +
                '}';
    }
}
```



## 6.2enum关键字实现枚举

* 使用enum关键字代替class
* 将public static final Season WINTER = new Season("冬天","寒冷");变为WINTER("春天"，"温暖")
* 如果有多个常量使用逗号隔开
* **如果使用enum来实现枚举要求将定义常量对象写在前面**

```
public class Enumeration01 {
    public static void main(String[] args) {
		System.out.println(Season.SPRING);
		
		
    }
}
enum Season{
	SPRING(),SUMMER(),AUTUMN(),WINTER();
    private String name;
    private String deac;
    
    //1,将构造器私有化，防止直接new对象
    //2，去掉set方法防止属性被修改
    //3，在Season内部直接创建固定对象
    private Season(String name,String deac){
        this.deac = deac;
        this.name = name;
    }

    public String getName() {
        return name;
    }

    public String getDeac() {
        return deac;
    }

    @Override
    public String toString() {
        return "Season{" +
                "name='" + name + '\'' +
                ", deac='" + deac + '\'' +
                '}';
    }
}
```

---

* enum关键字使用注意事项
  * 当我们使用enum关键字开发一个枚举类时，默认会继承Enum类
  * 如果使用无参构造器创建枚举对象，则实参列表和小括号都可以省略‘
  * 当有多个枚举对象时，使用逗号间隔，最后使用分号结尾
  * 枚举对象必须放在枚举类的首行
* enum常用方法实例
  * name：返回当前对象名，子类中不能重写’
  * ordinal：返回当前对象位置号，默认从零开始
  * values：返回当前枚举类中所用的常量
  * valueOf：将字符串转换成枚举对象，要求字符串必须为已有的常量名，否则异常
  * compareTo：比较两个枚举常量，比较的就是编号
* 使用enum关键字后不能再继承其他类，但是可以实现接口

## 6.3jdk内置基本注解类型Annotation

### 6.3.1注解的理解

* 也被称为元数据，用于修饰解释包，类，方法，属性，构造器，局部变量等数据信息
* 和注释一样注解不影响程序逻辑，但是可以被编译和运行，相当于嵌入代码的补充信息
* 再javaee中用来配置应用程序的任何切面

---

### 6.3.2**三个基本注解：**

* @Override只能在方法中判断重写是否成功
* @Deprecated表示用于某个程序元素(类，方法等)已过时，但是仍然可以使用
* @SuppressWarnings：可以抑制编译器警告；格式为@SuppressWarnings{("")};可以在方法上也可以在类上

## 6.4元注解：对注解进行注解

* 元注解的种类
  * Retention指定注解的作用范围，三种SOURCE，CLASS，RUNTIME
  * Target指定注解可以作用在那些地方
  * Documented指定该注解是否会在Javadoc中出现
  * Inherited子类会继承父类的注解

勾八玩意！！！！

# 7.异常

## 7.1异常的概念

### 7.1.1基本概念

* 将执行程序中发生的不正常情况称为异常（语法错误和逻辑错误不是异常）

### 7.1.2两大类异常

* Error异常：Java虚拟机无法解决的严重问题。比如内部资源耗尽，栈溢出等等
* Exception编译时异常：其他因编程错误或偶然外在因素导致的一般性问题，可以使用针对性的代码进行处理。
* RuntimeException运行时异常

## 7.2异常体系图

![](C:\Users\86188\Pictures\Screenshots\屏幕截图 2023-07-03 200511.png)

## 7.3常见的异常

### 7.3.1常见运行时异常

* Null Pointer Exception空指针异常

当应用程序在需要对象的地方使用null时，抛出该异常

```java
String name = null；
System.out.println(name.length);
```

* ArithmeticException数学运算异常

当出现异常的运算条件时，抛出该异常

```java
int n1 = 10;
int n2 = 0
int num = n1/n2;
```

* ArrayIndexOutOfBoundsException数组下标越界异常

用非法索引访问数组时抛出的异常

```java
int[] arr = {1,2,3,4};
System.out.println(arr[5]);
```

* ClassCastException类型转换异常

当试图将对象强制转换为不是实例的子类时，抛出该异常

```java
A b = new B();
B b2 = (B)b;
C c2 = (C)b;
class A{}
class B extend A{}
class C extend A{}
```

* NumberFormatException数字格式不正确异常

当以用程序试图将字符串转换成一种数值类型，但该字符不能转换为适当格式时，抛出该异常

### 7.3.2常见的编译异常

* 介绍：指在编译期间就必须处理的异常，否则代码不能通过

![](C:\Users\86188\Pictures\Screenshots\屏幕截图 2023-07-03 150851.png)

## 7.4异常处理概念和处理分类

* 基本介绍：

异常处理就是当异常发生时，对异常的处理方式

* 处理方式：ctrl + alt + t

  * try-catch-finally

    ```Java
    try{
    代码可能异常
    }catch(Exception e){
    //当捕获到异常时
    系统将异常封装成Exception对象e传递给catch
    }finally{
    不论是否有异常finally都执行
    }
    //可以有多个catch语句，捕获不同的异常，要求父类异常在后，子类异常在前。如果发生异常，只会匹配一个catch
    ```

  * 多重捕获

  ```Java
  try{
     // 程序代码
  }catch(异常类型1 异常的变量名1){
    // 程序代码
  }catch(异常类型2 异常的变量名2){
    // 程序代码
  }catch(异常类型3 异常的变量名3){
    // 程序代码
  }
  ```
  
  
  
  * throws
  
  **介绍：**如果一个方法可能生成某种异常，但是并不能确定如何处理这种异常，则可以显示的抛出异常，表明该方法将不对这些一场进行处理，而由该方法的调用者负责处理，可能同时抛出多个异常，之间用逗号隔开
  
  ```java
  import java.io.;
  public class className
  {
     public void withdraw(double amount) throws RemoteException,InsufficientFundsException
     {
         // Method implementation
     }
     //Remainder of class definition
  }
  ```
  
  
  
  * throw关键字用于在当前方法中抛出一个异常。
  
  通常情况下，当代码执行到某个条件下无法继续正常执行时，可以使用 **throw** 关键字抛出异常，以告知调用者当前代码的执行状态。
  
  例如，下面的代码中，在方法中判断 num 是否小于 0，如果是，则抛出一个 IllegalArgumentException 异常。
  
  ```Java
  public void checkNumber(int num) {
    if (num < 0) {
    throw new IllegalArgumentException("Number must be positive");
   }
  }
  ```
  
  

## 7.5自定义异常

* 步骤
  * 定义类：自定义异常类名继承Exception或者RuntimeException
  * 如果继承Exception属于编译异常
  * 如果继承Runtime Exception属于运行异常

## 7.6throw和throws的对比

**throw** 关键字用于在代码中抛出异常，而 **throws** 关键字用于在方法声明中指定可能会抛出的异常类型。

![](C:\Users\86188\Pictures\Screenshots\屏幕截图 2023-07-03 164800.png)

# 8.常用类

## 8.1包装类(Wrapper)-----针对八种基本定义相应的引用类型

![](C:\Users\86188\Pictures\Screenshots\屏幕截图 2023-07-03 203901.png)

![](C:\Users\86188\Pictures\Screenshots\屏幕截图 2023-07-03 203917.png)

![](C:\Users\86188\Pictures\Screenshots\屏幕截图 2023-07-03 203933.png)

## 8.2包装类和基本数据类型的转换（装箱与拆箱）

```java
public class IntegerTest05 {
    public static void main(String[] args) {
        // 900是基本数据类型
        // x是包装类型
        // 基本数据类型 --(自动转换)--> 包装类型：自动装箱
        Integer x = 900; // 等同于：Integer z = new Integer(900);
        System.out.println(x);

        // x是包装类型
        // y是基本数据类型
        // 包装类型 --(自动转换)--> 基本数据类型：自动拆箱
        int y = x;
        System.out.println(y);
    }
}

```



```JAVA
//以int和Integer为例子其他的一样
//自动装箱
int n2 = 200；
//int->Integer
Integer integer = n2;
//拆箱
int n3 = integer2;
```

* Integer 和 String之间相互转换

```java
//包装类Integer转为String
Integer i = 100;
String str1 = i + "";
String str2 = i.toString();
String str3 = String.valueOf(i);
//以上是三种方法
//String 转成 Integer
String str4 = "12345";
Integer i2 = Integer.parseInt(str4);
Integer i3 = new Integer(str4); 

```

* 整数型常量池(Integer)

```java
public class IntegerTest06 {
    public static void main(String[] args) {
        Integer a = 128;
        Integer b = 128;
        System.out.println(a == b); //false

        //原理：x变量中保存的对象的内存地址和y变量中保存的对象的内存地址是一样的。
        Integer x = 127;
        Integer y = 127;
        // == 永远判断的都是两个对象的内存地址是否相同。
        System.out.println(x == y); //true
    }
}

```

java中为了提高程序的执行效率，将 **`[-128 ~ 127]`** 之间所有的包装对象**提前创建**好， 放到了一个方法区的“**`整数型常量池`**”当中了。

目的是：只要用这个区间的数据不需要再new了，直接从整数型常量池当中取出来。

* Integer方法
  方法名	                                                                              作用
  static Integer decode(String nm)	                                将String转成Integer
  static int compare(int x, int y)	                                      比较两个数是否相等；相等返回0；前大后小返回1；后大前小返回-1
  static int signum(int i)													   符号函数；负数返回-1；正数返回1；0返回0
  static String toBinaryString(int i)									 将i转成二进制
  static String toHexString(int i)										  将i转成十六进制
  static String toOctalString(int i )	                                  将i转成八进制
  常用方法	
  static int parseInt(String s)	                                           字符串转int
  static Integer valueOf(String s)	                                    字符串转Integer
  String toString()	                                                              Integer转String
  boolean equals(Object obj)	                                          判断两个Integer是否相等

  ```java
  class IntegerTest{
      public static void main(String[] args) {
          Integer d = Integer.decode("123");
          System.out.println(d);//自动拆箱 123
  
          Integer a = 100;
          Integer b = 100;
  
          int res1 = Integer.compare(a, b);
          System.out.println(res1);//0
          res1 = Integer.compare(-a, b);
          System.out.println(res1);//-1
          res1 = Integer.compare(a, -b);
          System.out.println(res1);//1
  
          System.out.println(a.equals(b));//true
  
          int i = Integer.parseInt("123");
          System.out.println(i);//123
  
          System.out.println(Integer.signum(-123));//-1
          System.out.println(Integer.signum(123));//1
          System.out.println(Integer.signum(0));//0
  
          System.out.println(Integer.toBinaryString(10));//1010
          System.out.println(Integer.toOctalString(10));//12
          System.out.println(Integer.toHexString(10));//a
  
          String s = Integer.toString(123);
          System.out.println(s);//123
  
          Integer int1 = Integer.valueOf("123");
          System.out.println(int1);//123
      }
  }
  
  ```

  

## 8.3  String

### 8.3.1String特点

String：字符串，使用一对“”引起来表示

* String声明为final的，不可被继承
* String实现了Serializable接口，表是字符串是支持序列化的，实现了Comparable接口表示String可以比较大小
* String内部定义了final   char[]  value用于存储字符串数据
* String代表不可变的字符序列
  * 当对字符串重新赋值时，需要重写指定内存区域赋值，不适用于有的value赋值
  * 当对现有的字符串进行连接操作时，需要重新制定区域赋值，不能在原有的value上赋值
  * 当调用String的replace方法时修改字符或者字符串时也得重新指定区域赋值
* 通过字面量的方式给一个字符串赋值，此时字符串值在字符串常量池中，且池中不会存在相同内容的字符串

### 8.3.2 String的创建方式和细节

* 方式一：直接赋值String s  = “xq”；
  * 先从常量池中查看是否有xq的数据空间，如果有就直接指向，如果没有则重新创建然后指向，s最终指向的是常量池的空间地址
* 方式二：调用构造器String  s2 = new String(“xq”）；
  * 现在堆中创建空间，里面维护了value属性，指向常量池和xq空间，如果常量池没有xq，重新创建，如果有直接通过value指向，最终指向堆中的空间地址

## 8.4 StringBuffer类

### 8.4.1基本介绍

* 代表可变序列，可以对字符串进行删减
* StringBuffer可变长度
* 是一个容器
* final类不能被继承
* 其字符内容存放在char [] value,不用每次开新地址

### 8.4.2 构造器

* StringBuffer（）

构造一个其中不带字符的缓冲区，起初是容量为十六个字符

* StringBuffer（CharSequence seq）

构造一个字符缓冲区，它包含与指定的CharSequence相同的字符

* StringBuffer（int  capacity）

构造一个不带字符，但是具有指定初始容量的字符缓冲区，即对char[]大小进行指定

* StringBuffer（String str）

构造一个字符缓冲区，并将其内用初始化为指定字符串内容

### 8.4.3 StringBuffer 常见方法

* **添加字符串**																																					**重点**

**StringBuffer append（T t）
含义：将参数 t 的字符串表示附加到此序列的末尾。T可以是boolean、char
、char[] 、double、float、int、long、Object、String、StringBuffer。
只有字符数组可以，其他类型的数组不可以。
也可以指定字符数组开始和结尾的索引值，取其中一部分**

```Java
StringBuffer s1=new StringBuffer();
boolean b=true;
s1.append(b);
char[] c={'a','p','p','l','e','s','l','o'};
s1.append(c);
int i=7777;
s1.append(i);
System.out.println(s1); //输出：trueappleslo



char[] c={'a','p','p','l','e','s','l','o'};
StringBuffer s2=new StringBuffer();
s2.append(c,0,5);
System.out.println(s2);  //输出：apple


```

* **返回指定索引的char字符
  char charAt（int index）**

```Java
StringBuffer s3=new StringBuffer("Java");
System.out.println(s3.charAt(1));  //输出：a

```

* **删除		 	
  StringBuffer delete(int start ，int end)
  含义：删除此序列的子字符串中的字符。**																																																													**重点**																																								

```java
StringBuffer s3=new StringBuffer("Java Hello");
System.out.println(s3.delete(0,5)); //输出：Hello

```

**StringBuffer delectCharAt(int index)
含义：删除此序列指定位置的字符。**

```java
StringBuffer s3=new StringBuffer("Java Hello");
System.out.println(s3.deleteCharAt(0)); //输出：ava Hello

```

* **返回字符索引值
  int indexOf(String str)
  含义：返回指定子字符串第一次出现的字符串内的索引。**

```java
StringBuffer s3=new StringBuffer("Java Hello");
System.out.println(s3.indexOf("Hello")); //输出；5

```

* **int indexOf(String str，int fromIndex)
  含义：从指定索引开始，返回指定返回指定子字符串第一次出现的字符串内的索引。**																		**重点**

```java
StringBuffer s3=new StringBuffer("Java Hello");
System.out.println(s3.indexOf("a",2)); //输出：3

```

* **int lastIndexOf(String str)
  含义：返回指定子字符串最后一次出现的字符串中的索引**

```java
StringBuffer s3=new StringBuffer("Java Hello");
System.out.println(s3.lastIndexOf("a"));//输出：3

```

* **int lastIndexOf(String str，int fromIndex)
  含义：从参数索引值往左看，返回指定子字符串最后一次出现的字符串中的索引**

```java
StringBuffer s3=new StringBuffer("Java Hello");
System.out.println(s3.lastIndexOf("a",2));//输出：1

```

* **插入	
  StringBuffer insert（int offset，T t）
  含义：在指定的offset索引位置，插入参数t字符串表示形式。
  T可以是：boolean、char、char[] 、double、float、int、long、Object、String、StringBuffer**														**重点**

```java
StringBuffer s3=new StringBuffer("Java Hello");
int i=555;
char[] c={'a','p','p','l','e','s','l','o'};
StringBuffer stb=new StringBuffer("MySql");
System.out.println(s3.insert(5,i)); //输出：Java 555Hello
System.out.println(s3.insert(5,stb)); //输出：Java MySql555Hello
System.out.println(s3.insert(0,c,0,5)); //输出：appleJava MySql555Hello

```

* **替换	
  StringBuffer replace（int start，int end，String str）
  含义：用指定的String字符串替换此序列中start索引至end索引范围的内容。**																				**重点**

```java
StringBuffer s3=new StringBuffer("Java Hello");
System.out.println(s3.replace(0,4,"MySql"));  //输出：MySql Hello

```

**void setCharAt(int index，char ch)
含义：指定索引处的字符设置为ch。**

```java
StringBuffer s3=new StringBuffer("Java Hello");
s3.setCharAt(4,'&');
System.out.println(s3);  //输出：Java&Hello

```

* **反向
  StringBuffer reverse();
  含义：使该序列被相反的代替。**

```java
StringBuffer s3=new StringBuffer("Java Hello");
System.out.println(s3.reverse()); //输出：olleH avaJ

```

* **返回子串
  String substring（int start）
  含义：返回一个新的String，从此序列的索引start开始
  String substring（int start，int end）
  含义：返回一个新的String，从此序列的索引start开始至索引end结束**

```java
StringBuffer s3=new StringBuffer("Java Hello");
String s=s3.substring(5);
String s2=s3.substring(0,4);
System.out.println(s); //输出：Hello
System.out.println(s2); //输出：Java

```

## 8.5 StringBuilder类

### 8.5.1 基本介绍 

* 一个可变的字符序列。此类提供一个与StringBuffer兼容的API，但是不保证同步(StringBulider不是安全线程)。该类被设计用作StringBuffer的一个简易替换，**用在字符串缓冲区被*单个线程*使用的时候**，如果可以的话建议优先使用该类，因为大多数现实中他比StringBuffer更快
* 在StringBuilder上主要的操作是append和insert方法，可重载这些方法，已接受任意类型的数据

### 8.5.2 常用方法

* 和stringbuffer一样均代表可变字符序列，方法是一样的。

## 8.6 Math类

### 8.6.1概述

- 类包含用于执行基本数学运算的方法
- Math 类包含用于执行基本数学运算的方法，如初等指数、对数、平方根和三角函数。
- Math所有类都是静态的。可以直接类名。调用。
- 由于Math类在java.lang包下，所以不需要导包。
- 因为它的成员全部是静态的,所以私有了构造方法

### 8.6.2 常见方法及应用

```java
public class MathMethod{
    public static void main(String[] args){
        //静态方法
        //abs 取绝对值
        int abs = Math.abs(9);
        System.out.println(abs);
        //pow 求幂
        double pow = Math.pow(-3.5,4);
        System.out.println(pow);
        //ceil 向上取整，返回>=该参数的最小整数
        double ceil = Math.ceil(-3.000001);
        System.out.println(ceil);
        //floor 向下取整，返回<=该参数的最大整数
        double floor = Math.floor(-4.9999);
        System.out.println(floor);
        //round 四舍五入
        long round = Math.round(-5.0001);
        System.out.println(round);
        //sqrt 求开方
        double sqrt = Math.sqrt(-9.0);
        System.out.println(sqrt);
        //random 返回[0,1)之间的一个随机小数
        for (int i = 0; i < 10; i++){
            System.out.println(Math.random());
        }
        //随机获得一个区间（a，b）的整数比如（2，7）
        for (int i = 0; i < 10; i++){
            System.out.println((int)2 * Math.random() * (7 - 2 + 1));
        }
        //max , min 返回最大值和最小值
        int min = Math.min(1,9);
        int max = Math.max(45,90);
        System.out.println(min);
        System.out.println(max);
    }
}
```

## 8.7 Arrays类

* toString 返回数组的字符串形式

Arrays.toString(arr)

```java
    int[] arr = {3,2,1,5,4};
    System.out.print(arr);//直接将数组打印输出
    //输出：[I@7852e922 (数组的地址)

	String str = Arrays.toString(arr); // Arrays类的toString()方法能将数组中的内容全部打印出来
	//System.out.print(str);
	//输出：[3, 2, 1, 5, 4]

```



* sort 排序（自然排序和定制排序）

```java
Integer arr[] = {1, -1, 7, 0, 89};
Arrays.sort(arr);
```

sort是重载的，可以通过传入一个接口Comparator实现定制排序，

```java
Arrays.sort(arr, new Comparator(){
		public int compare(Object o1, Object o2){
			Integer i1 = (Integer) o1;
			Integer i2 = (Integer) o2;
			return i1 - i2;
		}
})
System.out.println(Arrays.toString(arr));
```

* binarySearch 通过二分搜索法查找，**要求必须排好序**

int index = Arrays.binarySearch(arr, 3);

* copyOf 数组元素的复制

```JAVA
Integer[] newArr = Arrays.copyOf(arr, arr.length);

```

* fill 数组元素填充

```Java
    int[] arr = new int[5];//新建一个大小为5的数组
	Arrays.fill(arr,4);//给所有值赋值4
	String str = Arrays.toString(arr); // Arrays类的toString()方法能将数组中的内容全部打印出来
	System.out.print(str);
	//输出：[4, 4, 4, 4, 4]



	int[] arr = new int[5];//新建一个大小为5的数组
	Arrays.fill(arr, 2,4,6);//给第2位（0开始）到第4位（不包括）赋值6
	String str = Arrays.toString(arr); // Arrays类的toString()方法能将数组中的内容全部打印出来
	System.out.print(str);
	//输出：[0, 0, 6, 6, 0]
```

* equal 比较两个数组元素是否一致

```java
	int[] arr1 = {1,2,3};
	int[] arr2 = {1,2,3};
	System.out.println(Arrays.equals(arr1,arr2));
	//输出：true
	//如果是arr1.equals(arr2),则返回false，因为equals比较的是两个对象的地址，不是里面的数，而Arrays.equals重写了equals，所以，这里能比较元素是否相等。
```

* asList  将一组值转换成list

```java 
List asList = Arrays.asList(1, 3, 4, 5, 64, 91);
```

## 8.8 System类

* exit 退出当前程序

```java
System.out.println("ok1");
System.exit(0);
System.out.println("ok2");
//只输出ok1，ok2不会输出
```



* arraycopy： 复制数组元素，比较适合底层调用，一般使用Arrays.copyOf复制数组

```java
int[] src = {1, 2, 3};
int[] dest = new int[3];//现在数组是{0，0，0}
//src 表示从原数组的哪个索引开始拷贝
//dest 表示把原数组的数据拷贝到哪个数组
System.out.println(src, 0, dest, 0, 3);
System.out.println(Arrays.toString(dest));//输出结果是{1，2，3}
```



* currentTimeMillens：返回当前时间距离1970-1-1的毫秒数

```java
System.out.println(System.currentTimeMillis);
```



* gc：运行垃圾回收机制 System.gc();

## 8.9 BigInteger和BigDecimal类

* 在编程中需要处理很大的数，long不够用时，使用BigInteger,  进行运算时不能直接用运算符，需要调用相应的方法

```java
BigInteger bigInteger = new BigInteger("54653464135643655864");
System.out.println(bigInteger);
BigInteger add = bigInteger.add(100);
System.out.println(add);
```

* 当我们需要保存一个精度很高的数时 ，double不够用; 同样不能使用运算符

  ```java
  BigDecimal bigDecimal = new BigDecimal("9.92347687239456298356239865");
  //当调用divide方法时可能会抛出异常，此时指定精度即可
  //即使用BigDecimal.ROUND_CEILING保留分子的精度
  System.out.println(bigDecimal.divide(3, BigDecimal.ROUND_CEILING));
  ```

## 8.10 Date类

### 8.10.1第一代日期类

* **getTime() 获取从1970年1月1日 0时0分0秒到此刻毫秒值**

```Java
System.out.println(date.getTime());
```

* **SimpleDateFormat对象，可以指定相应的时期**

```java
	  Date dNow = new Date( );
      SimpleDateFormat ft = new SimpleDateFormat ("yyyy-MM-dd hh:mm:ss");
 
      System.out.println("当前时间为: " + ft.format(dNow));
```

*  把一个格式化的String转成对应的Date

```
String s = "1996年01月01日 10：20：30 星期一";
Date parse = sdf.parse(s);
System.out.println(sdf.parse);
```

### 8.10.2 第二代日期类

* Calender是一个抽象类，并且构造器是私有的，可以通过个体Instance（）获取实例

```java
Calendar c = Calendar.getInstance();
//获取日历对象的某个日历字段
System.out.println("年" + c.get(Calendar.YEAR));
//返回月时从零开始所以加一
System.out.println("月" + (c.get(Calendar.MONTH) + 1));
//没有专门的格式化方法，需要自己组合

```

### 8.10.3 第三代日期类

* LocalDate只包含日期，可以获取日期字段
* LocalTime只包含时间，可以获取时间字段
* LocalDateTime包含日期和时间都可以获取

```java 
LocalDateTime ldt = LocalDateTime.now();
System.out.println(ldt);
System.out.println("年" + ldt.getYear());
```

* DateTimeFormat

```
DateTimeFormat dateTimeFormat = DateTimeFormat.ofpattern("yyyy年MM月dd日 HH小时mm分钟ss秒");
String format = dateTimeFormat.format（ldt）；
System.out.println();
```

* 时间戳

```java
//通过静态方法 now()获取表示当前时间戳的对象
Instant now = Instant.now();
System.out.println(now);
//通过from可以把Instance转成Date
Date date = Date.from(now);
//通过date的同Instant()可以把date转成Instant对象
```

# 9.集合

 

## 9.1集合框架体系

* 集合主要分为两组（单例集合，双例集合）
* Collection接口有两个重要的子接口 List和Set，他们实现的子类都是单例集合
* Map接口实现的子类都是双列集合，存放的K-V

![](C:\Users\86188\Pictures\Screenshots\屏幕截图 2023-07-05 162632.png)

![](C:\Users\86188\Pictures\Screenshots\屏幕截图 2023-07-05 162655.png)

## 9.2Collection



### 9.2.1常用方法

* add：添加单个元素

```java
List list = new ArrayList();
list.add("jack");
list.add(19);
list.add(true);
System.out.println(list);
//输出结果是[jack, 10, true]
```

* remove 删除

```java
list.remove(0);
list.remove(10);
System.out.println(list);
//输出结果是[true]
```

* contains ：查找元素是否存在

```
System.out.println(list.contains(true));
//输出结果是true
```

* size： 返回元素个数

```java
System.out.println(list.size());
//输出结果是1
```

* clear： 清空

```java
System.out.println(list.clear());
//输出结果是[]
```

* addAll:传入多个元素

```java
List list2 = new ArrayList();
list2.add("红楼梦");
list2.add("三国演义");
list.addAll(list2);
System.out.println(list);
//输出结果是[红楼梦, 三国演义]
```

* removeAll:删除多个元素

### 9.2.2Collection接口遍历元素方式

#### 9.2.2.1Iterator遍历

* 执行原理：

  * ```java
    Iterator iterator = coll.iterator();//得到一个集合迭代器
    //hasNext()判断是否还有下一个元素
    while(iterator.hasNext()){
        //Next()作用1.下移2.将下移后集合位置上的元素返回
        Object obj = iterator.next();
        System.out.println(inerator.next());
    }
    //如果想再次遍历需要重置迭代器
    iterator = coll.iterator();
    ```

    //快捷键itit

* 主要用于遍历Collection集合中的元素，所有实现了Collection接口的集合类都有一个iterator（）方法，用以返回一个实现了Iterator接口的对象，既可以返回一个迭代器。其本身不存放任何对象。

* 使用iterator(迭代器)接口方法
  * **next()** - 返回迭代器的下一个元素，并将迭代器的指针移到下一个位置。
  * **hasNext()** - 用于判断集合中是否还有下一个元素可以访问。**调用next方法前必须先调用hasNext方法进行检查，如果不调用且下一条记录无效会出现异常**
  * **remove()** - 从集合中删除迭代器最后访问的元素（可选操作）。

#### 9.2.2.2for增强循环

* 基本语法：

```Java
for(元素类型 元素名 ： 集合名或数组名){
			访问元素
}
```

* 底层仍然是迭代器

### 9.2.3 list接口方法

* 是Collection接口的子接口
  * list集合类中的元素有序即添加和取出顺序一致且可重复
  * list集合中每个元素都有其对应的顺序索引，即支持索引
  * list肉其中的元素都对应一个整数型的序号记载在容器中的位置，可以根据序号存取容器中的元素
  * **api常用的实现类有ArrayList，LinkList，Vector**

* 常用方法

void add(int index, Object ele):在index位置插入ele元素
boolean addAll(int index, Collection eles):从index位置开始将eles中 的所有元素添加进来
Object get(int index):获取指定index位置的元素
int indexOf(Object obj):返回obj在集合中首次出现的位置
int lastIndexOf(Object obj):返回obj在当前集合中末次出现的位置
Object remove(int index):移除指定index位置的元素，并返回此元素
Object set(int index, Object ele):设置指定index位置的元素为ele
List subList(int fromIndex, int toIndex):返回从fromIndex到toIndex 位置的子集合(前闭后开)

### 9.2.4 Array List底层结构

* 底层机制
  * Array List中维护了一个Object类型的数组elementData.transient Object[] elementData;
  * 当创建ArrayList对象时，如果使用的是无参构造器，则初始elementData容量为0，第一次添加扩容为10，再次扩容编程一点五倍
  * 如果使用指定大小的构造器，则初始elementData容纳量为指定大小，下次扩容直接变1.5倍
  * 当添加元素时：先判度是否需要扩容，如果需要扩容，则调用grow方法，否则直接添加元素到合适位置

### 9.2.5 Vector底层结构

* 底层也是一个对象数组，protected Object[] elementDate;
* Vector是线程同步的，操作方法带有synchronized
* 开发中如果需要考虑线程安全，需要考虑使用Vector
* Vector和ArrayList比较

![](C:\Users\86188\Pictures\Screenshots\屏幕截图 2023-07-06 103739.png)

### 9.2.6 LinkedList底层结构

* 底层实现了双向链表和和双段队列特点
* 可以添加任意元素包括null
* 线程不安全，没实现同步

## 9.2.7hashset

### 9.2.7.1概念

HashSet是基于HashMap来实现的，实现了Set接口，同时还实现了序列化和可克隆化。而集合（Set）是不允许重复值的。

所以HashSet是一个没有重复元素的集合，但不保证集合的迭代顺序，所以随着时间元素的顺序可能会改变。

由于HashSet是基于HashMap来实现的，所以允许空值，不是线程安全的。
### 9.2.7.2Java文档中HashSet的实现

HashSet是基于HashMap实现的，区别就在于在HashMap中输入一个键值对，而在HashSet中只输入一个值。

```Java
private transient HashMap map;

// Constructor - 1
// All the constructors are internally creating HashMap Object.
public HashSet()
{
    // Creating internally backing HashMap object
    map = new HashMap();
}

// Constructor - 2
public HashSet(int initialCapacity)
{
    // Creating internally backing HashMap object
    map = new HashMap(initialCapacity);
}

// Dummy value to associate with an Object in Map
private static final Object PRESENT = new Object();

```

### 9.2.7.3常见方法

* 添加元素add()

```Java
hs.add("谢钦");
```

* 删除元素remove()

```Java
hs.remove("B");
```

* 判断是否包含某个元素contains（）

```java
boolean c = hs.contains("fs");
```

* 判断是否为空

```java
boolean c = hs.isEmpty();
```

* 获得大小size()

```java
int size = hs.size();
```



## 9.4Map

```java 
//Map六大遍历方式
Map map = new HashMap();
//第一组先取出所有Key，通过Key取出对应的Value
//1
Set keyset = map.keySet();
for(Object key : keyset){
    System.out.println(key + map.get(key));
}
//2
Iterator iterator = Keyset.iterator();
while(iterator.hasNext()){
    Object key = inerator.next();
    System.out.ptintln(key + map.get(key));
}
//把所有value取出
//1
Collection values = map.values();
for(Object value : values){
    System.out.println(value);
}

//2
Iterator iterator = values.iterator();
while(iterator2.hasNext()){
    Object value = iterator2.next();
    System.out.println(value);
}
//通过EntrySet获取k-v
//1
Set entrySet = map.entrySet();
for(Object entry : entrySet){
    Map.Entry m = (Map.Entry)entry:
    System.out.println(m.getKey() + m.getValue());
}
//2
Iterator iterator3 = entrySe.iterator();
 while(iterator3.hasNext()){
     Object entry = iterator3.next();
     Map.Entry m = (Map.Entry) entry;
     System.out.println(m.getKey() + m.getValue());
 }
```



### 9.4.1hashMap

* 接口实现类的特点
  * Map用于保存具有映射关系的数据：key-value
  * k和v可以是任何引用数据类型的数据，会封装到Hash Map$Node中
  * key不允许重复
  * value可以重复
  * k和v都可以为null，key为空只能有一个，value可以有多个
  * 常用String作为map的key
  * k和v是一对一单向关系
  * **一对k-y是放在一个Node中的，Node实现了Entry接口**
    * 
* 常用方法
  * put添加
  * remove删除
  * get获取值
  * size获取k-v数
  * isEmpty判断个数是否为零
  * clear清空
  * containsKey查找键是否存在
* Map接口遍历方法heshangmianchabud

### 9.4.2Hashtable



## 9.5Collections工具类



### 9.5.1介绍

* 是一个操作set，List，Map等集合的工具类
* 提供了一系列的静态方法对集合元素进行排序，查询和修改等操作

### 9.5.2排序操作

* reveser(List):反转List中的元素顺序
* shuffle(List)：对List集合元素进行随机排序
* sort(List):根据元素的自然顺序对指定List集合元素按升序排序
* sort(List，Comparator):根据Comparator产生的顺序对List集合元素进行排序
* swap(List,int,int):将指定list集合中的i元素和j元素进行交换
* int frequency(Collection, Object)返回指定集合中元素出现的次数
* void copy(List dest, List src)将src中的内容复制到dest中
* boolean replaceAll (List list, Object oldVal, Object newVal)



# 10.泛型

泛型的好处

* 编译时，检查添加元素的类型，提高了安全性
* 减少了类型转换次数
* 不再提示编译警告

泛型的介绍

* 泛型又称参数化类型，用于解决数据类型的安全性问题
* 在声明或者实例化时只要指定好具体的类型即可
* Java泛型可以保证如果程序在编译时没有发出警告，运行时就不会产生ClassCastException异常，同时使代码更简洁和健壮
* 泛型的作用是可以在声明时通过一个表示类中的某个属性的类型，或是某个方法的返回值类型，或是参数类型

## 10.1泛型语法

* 泛型的声明  **interface 接口<T>{}和class 类<K,V>{}**
  * T,K,V不代表值，而是表示类型
  * 任意字母都可以
* 泛型的实例化
  * 需要在类名后面指定参数类型比如：
    * list<String> strList = new ArrayList<String>();简写形式为：list<String> strList = new ArrayList<>();
    * Iterator<Customer>iterator = customers.iterator();
* 泛型使用细节
  * 给泛型指向数据类型时必须是引用数据类型，不能是基本数据类型
  * 在给泛型指定具体类型后，可以传入该类型或其子类类型
  * 不指定泛型默认为Object

## 10.2 自定义泛型

### 10.2.1自定义泛型类

* 基本语法

class 类名 <T,R....>{

​		成员

}

* 注意细节

  * 普通成员可以使用泛型（属性方法）

  * 使用泛型的数组不能初始化

  * 静态方法中不能使用类的泛型

  * 泛型类的类型，是在创建指定对象时确定的(因为创建对象时，需要制定确定的类型)

  * 如果在创建对象时，没有指定类型，默认为Object

  * ```java
    //Tiger后面泛型，所以把Tiger称为自定义泛型
    //T，R，M，泛型标识符，一般是单个大写字母
    //泛型标识符可以有多个
    //
    class Tiger<T,R,M>{
        String name;
        R r;//属性使用到泛型
        T t;
        M m;
        T[] ts = new T[];//报错
    
        public Tiger(String name, R r, T t, M m) {//构造器使用泛型
            this.name = name;
            this.r = r;
            this.t = t;
            this.m = m;
        }
        public static void m1(M m){//报错，静态方法不能使用泛型，因为静态和类相关，类加载时，对象还没创建
    
        }
    }
    ```

### 10.2.3 自定义泛型接口

* 基本语法

inteface 接口名<T,R...>{

}

* 注意细节
  * 接口中静态成员也不能使用泛型
  * 泛型接口的类型，在**继承接口**或者**实现接口**时确定
  * 没有指定时依旧默认是Object

### 10.2.4 自定义泛型方法

* 基本语法

修饰符 <T,R...>返回类型 方法名(参数列表){

}

* 注意细节
  * 泛型方法可以定义在普通类中，也可以定义在泛型类中
  * 当泛型方法被调用时，类型会确定
  * publib void eat(E e){},修饰符后没有<T,R...>eat方法不是泛型方法，而是使用了泛型

## 10.3 泛型继承和通配符

* 泛型的继承和通配符说明
  * 泛型不具备继承性
  * <?>支持任意类型泛型
  * <? extends A>：支持A类和A类的子类，规定了泛型的上限
  * <? super A>:支持A类和A类的父类，不限于直接父类，规定了泛型的下限



# 11.线程基础

## 11.1线程相关概念

* 程序：是为完成特定任务，用某种语言编写的一组指令集和
* 进程：是运行中的程序、
  * 进程是程序的一次执行过程，是动态过程，有产生存在消亡的过程
* 线程：是由进程创建的，是线程的一个实体，进程可以拥有多个线程
  * 单线程：同一个时刻只允许执行一个线程
  * 多线程：同一时刻可以执行多个线程
* 其他概念：
  * 并发：同一时刻多个任务交替执行
  * 并行：同一个时刻，多个任务同时执行

## 11.2线程的使用

### 11.2.1继承Thread类

* 定义 Thread 类的⼦类，并重写该类的 run() ⽅法，该 run() ⽅法的⽅法体就代表了线程需要完成的任务，因此把 run() ⽅法称为线程执⾏体。

  创建 Thread ⼦类的实例，即创建了线程对象

  调⽤线程对象的 start() ⽅法来启动该线程

* ```java
  public class Demo01 {
   public static void main(String[] args) {
   // 创建⾃定义线程对象
   MyThread mt = new MyThread("新的线程！");
   // 开启新线程
   mt.start();
   // 在主⽅法中执⾏for循环
   for (int i = 0; i < 10; i++) {
   System.out.println("main线程！" + i);
   		}
   	} 
  }
  public class MyThread extends Thread {
   // 定义指定线程名称的构造⽅法
   public MyThread(String name) {
   // 调⽤⽗类的String参数的构造⽅法，指定线程的名称
   super(name);
   }
   /**
   * 重写run⽅法，完成该线程执⾏的逻辑
   */
   @Override
   public void run() {
   for (int i = 0; i < 10; i++) {
   System.out.println(getName() + "：正在执⾏！" + i);
   		}
   	}
  }
  ```

  

### 11.2.2 实现Runnable接口

* 定义 Runnable 接⼝的实现类，并重写该接⼝的 run() ⽅法，该 run() ⽅法的⽅法体同样是该线程的线程执⾏体。

  创建 Runnable 实现类的实例，并以此实例作为 Thread 的 target 来创建 Thread 对象，该 Thread 对象才是 真正的线程对象。

  调⽤线程对象的 start() ⽅法来启动线程。

* ```java
  public class MyRunnable implements Runnable {
   @Override
   public void run() {
   for (int i = 0; i < 20; i++) {
   System.out.println(Thread.currentThread().getName() + " " + i);
   		}
   	} 
  }
  public class Demo {
   public static void main(String[] args) {
   // 创建⾃定义类对象 线程任务对象
   MyRunnable mr = new MyRunnable();
   // 创建线程对象
   Thread t = new Thread(mr, "⼩强");
   t.start();
   for (int i = 0; i < 20; i++) {
   System.out.println("旺财 " + i);
   		}
   	}
  }
  ```

  

* Thread和Runnable的区别

  * 适合多个相同的程序代码的线程去共享同⼀个资源。

    可以避免 java 中的单继承的局限性。

    增加程序的健壮性，实现解耦操作，代码可以被多个线程共享，代码和线程独⽴。

    线程池只能放⼊实现 Runable 或 Callable 类线程，不能直接放⼊继承 Thread 的类。
    

### 11.2.3线程常用方法(一)

* public String getName() ：获取当前线程名称。
* public void start() ：导致此线程开始执⾏；Java虚拟机调⽤此线程的run⽅法。
* public void run() ：此线程要执⾏的任务在此处定义代码。
* public static void sleep(long millis) ：使当前正在执⾏的线程以指定的毫秒数暂停（暂时停⽌执⾏）。
* public static Thread currentThread() ：返回对当前正在执⾏的线程对象的引⽤。
* setName():设置线程名称
* setPriority：更改线程的优先级
* initerrupt：中断线程
* getPriority：获取线程的优先级

* yield：线程的礼让，让出CPU，让其他线程执行，但时间不确定不一定礼让成功
* join：线程插队。插队一旦成功，则肯定先执行完插入的线程所有的任务

 用户线程和守护线程

* 用户线程：也叫做工作线程，当线程的任务执行完或通知方式结束
* 守护线程：一般是为工作线程服务的，当所有的用户线程结束时，守护线程自动结束
* 常见的守护线程有垃圾回收机制



## 11.3 线程的生命周期

![](C:\Users\86188\Pictures\Screenshots\427c9cba8c5c40868d7ee42ef77f945c.png)

## 11.4 Synchronize

* 线程同步机制

  * 在多线程编程，一些敏感数据不允许被多个线程同时访问，此时就是用同步访问技术，保证数据在任何时刻，最多有一个线程访问，以保证数据的完整性
  * 可以理解为当有一个线程在对内存进行操作时，其他线程不可以对这个内存地址进行操作，知道该线程完成操作，其他线程才能对该地址内存地址进行操作

* 具体方法

  *  同步代码块。

  ```java
  synchronized(同步锁) {
   需要同步操作的代码
  }
  ```

  

  * 同步⽅法。

  ```java
  public synchronized void method() {
   可能会产⽣线程安全问题的代码
  }
  ```

  

  * 锁机制。

## 11.5 锁

### 11.5.1 互斥锁

* 基本介绍
  * 在Java语言中，引入了对象互斥锁的概念，来保证共享数据的完整性
  * 每个对象都对应一个可称为“互斥锁 ”的标记，这个标记用来保证任意时刻只能有一个线程访问该对象
  * 关键字synchronized来与对象的互斥锁联系，某个对象用该关键字修饰时表明该对象在任意时间只能由一个线程访问
  * 局限性：导致程序执行效率降低
  * 非静态同步方法的锁可以是this，也可以是其他对象（要求是同一个对象）
  * 静态的同步方法的锁是当前类的本身
* 注意事项和细节
  * 同步方法如果没有使用static修饰：默认锁对象是this
  * 如果方法使用static修饰，默认对象是：当前类.class

### 11.5.2 死锁

* 基本介绍：多个线程都占用了对方的锁资源

```java
public class DeadLockDemo {
    private static Object resource1 = new Object();//资源 1
    private static Object resource2 = new Object();//资源 2

    public static void main(String[] args) {
        new Thread(() -> {
            synchronized (resource1) {
                System.out.println(Thread.currentThread() + "get resource1");
                try {
                    Thread.sleep(1000);
                } catch (InterruptedException e) {
                    e.printStackTrace();
                }
                System.out.println(Thread.currentThread() + "waiting get resource2");
                synchronized (resource2) {
                    System.out.println(Thread.currentThread() + "get resource2");
                }
            }
        }, "线程 1").start();
        new Thread(() -> {
            synchronized (resource2) {
                System.out.println(Thread.currentThread() + "get resource2");
                try {
                    Thread.sleep(1000);
                } catch (InterruptedException e) {
                    e.printStackTrace();
                }
                System.out.println(Thread.currentThread() + "waiting get resource1");
                synchronized (resource1) {
                    System.out.println(Thread.currentThread() + "get resource1");
                }
            }
        }, "线程 2").start();
    }
}
```

```java
Thread[线程 1,5,main]get resource1
Thread[线程 2,5,main]get resource2
Thread[线程 1,5,main]waiting get resource2
Thread[线程 2,5,main]waiting get resource1
```



### 11.5.3 释放锁

* 释放锁的操作
  * 当线程的同步方法，同步代码块执行结束
  * 当线程在同步代码块，同步方法中遇到break，return
  * 当线程在同步代码块，同步方法中出现了未处理的Error和Exception，导致异常结束
  * 当线程在同步代码块，同步方法中执行了线程对象的wait（）方法，当前线程暂停，并释放锁
* 不会释放锁
  * 调用sleep方法，Thread方法不会释放锁
  * 执行同步代码块时，其他线程调用了该线程的suspend()方法将该线程挂起

# 12. IO流

流：数据在数据源文件和程序内存之间的路径

## 12.1 文件

* 文件流：文件在程序中是以流的形式来操作的

* 概念：保存数据的地方

* 创建文件常用操作

  * new File(String pathname)//根据路径创建一个File对象

  ```java
  String filePath = "e:\\news2.txt";
  File file = new File(filePath);
  file.creatNewFile();
  ```

  

  * new File(File patent,String child)//根据父目录文件+子路径构建

  ```java
  File parentFile = new File("e:\\");
  String fileName = "news2.txt";
  File file = new File(parentFile, fileName);
  file.creatNewFile();
  ```

  

  * new File(String patent,String child)//根据父目录+子路径构建

  ```java
  String parentPath = "e:\\";
  String fileName = "news.txt";
  File file = new File(parentPath, fileName);
  file.creatNewFile();
  
  ```

* 文件常用方法
  * 获得文件名：getName（）;
  * 获得绝对路径：getAbsoulutePath（）；
  * 获得父级目录：getParent（）；
  * 获得文件大小(按字节来算)：length（）；
  * 判断文件是否存在：exists（）；
  * 是不是一个目录：isDirectory（）；
  * 是不是一个文件：isFile();
  * 删除文件：delect();
  * 创建多级目录：madirs();

## 12.2 IO流原理及流的分类

* 流的分类
  * 按照流的方向： 输入流和输出流
  * 按照数据单位不同分为：字节流和字符流
  * 按照角色不同分为：节点流 ，处理流/包装流

## 12.3 节点流和处理流

## 12.4 输入流

**读取外部数据到程序中**

### 12.4.1inputStream

* FileInputStream：文件输入流
* BufferedInputStream：缓冲字节输入流
* ObjectInputStream：对象字节输入流

### 12.4.2 Reader

## 12.5 输出流

**将程序数据输出到磁盘，光盘等存储设备中**

### 12.5.1 OutputStream

### 12.5.2 Writer

## 12.6 properties类

