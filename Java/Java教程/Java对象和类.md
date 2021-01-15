# 对象和类

一个类可以包含以下类型变量：

- **局部变量**：在方法、构造方法或者语句块中定义的变量被称为局部变量。变量声明和初始化都是在方法中，
  方法结束后，变量就会自动销毁。
- **成员变量**：成员变量是定义在类中，方法体之外的变量。这种变量在创建对象的时候实例化。成员变量
  可以被类中方法、构造方法和特定类的语句块访问。
- **类变量**：类变量也声明在类中，方法体之外，但必须声明为 static 类型。



## 构造方法

每个类都有构造方法。如果没有显式地为类定义构造方法，Java 编译器将会为该类提供一个**默认构造方法**。

在创建一个对象的时候，至少要调用一个构造方法。构造方法的名称必须与类同名，一个类可以有多个构造方法。

下面是一个构造方法示例：

```java
public class Cat{
	public Cat(){
	
	}
	
	public Cat(String name){
	// 构造器有一个参数 name
	}
}
```

## 创建对象

对象是根据类创建的。在Java中，使用关键字 new 来创建一个新的对象。创建对象需要以下三步：

- **声明**：声明一个对象，包括对象名称和对象类型。
- **实例化**：使用关键字 new 来创建一个对象。
- **初始化**：使用 new 创建对象时，会调用 *构造方法* 初始化对象。

```java
public class Cat{
    public Cat(String name){
        // Constructor parameter: name
        System.Out.println("The name of cat is" + name);
    }
    public static void main(String[] args){
        // Create an object of Class Cat
        Cat myCat = new Cat("Sam");
    }
}
```

> 编译运行以上程序结果:
>
> ```shell
> The name of cat is Sam
> ```



***

一个例子:

```java
public class Cat {
    int catAge;
    public Cat(String name){
        // 构造器
        System.out.println("The cat name is " + name);
    }

    public void setAge(int age){
        catAge = age;
    }

    public int getAge(){
        System.out.println("The cat age is" + catAge);
        return catAge;
    }

    public static void main(String[] args){
        Cat myCat = new Cat("Sam"); // 创建对象
        myCat.setAge(2); // 方法设定年龄
        myCat.getAge();// 方法调用年龄
        System.out.println("The cat age is " + myCat.catAge);
    }
}

```

输出:

```shell
PS D:\Java\JavaBaiscs> java Cat.java
The cat name is Sam
The cat age is2 
The cat age is 2
```

## 源文件声明规则

当在一个源文件中定义多个类，并且还有import语句和package语句时，要特别注意这些规则:

- **一个源文件中只能有一个 public 类**。

- 一个源文件可以有多个非 public 类。

- 源文件的名称应该和 public 类的类名保持一致。

- 如果一个类定义在某个包中，那么 package 语句应该在源文件的首行。

- 如果源文件包含 import 语句，那么应该放在 package 语句和类定义之间。如果没有 package 语句，那么 import 语句应该在源文件中最前面。

- import 语句和 package 语句对源文件中定义的所有类都有效。

***

## 一个简单的例子

### 创建一个类

```java
import java.io.*;

public class Employee{
    // 变量
    String name;
    int age;
    double wage;
    String title;
    // 构造器
    public Employee(String name){
        this.name = name; // 类变量name赋值
    }

    public void setAge(int age){
        this.age = age;
    }

    public void setTitle(String title){
        this.title = title;
    }

    public void setWage(double wage){
        this.wage = wage;
    }

    public void printEmployee(){
        System.out.println("Name:" + name);
        System.out.println("Age:" + age);
        System.out.println("Title:" + title);
        System.out.println("Wage:" + wage);
    }
}
```

### 创建类的实例对象, 写入main方法.

java因强制要求类名（唯一的public类）和文件名统一，因此在引用其它类时无需显式声明。在编译时，编译器会根据类名去寻找同名文件。

```java
import java.io.*;

public class EmployeeTest {
    // Creat Object
    public static void main(String[] args) {
        Employee empAlex = new Employee("Alex");
        // Employee empSam = new Employee("Sam");
    
        empAlex.setAge(26);
        empAlex.name = "Alex ";
        empAlex.title = "Engineer"; //直接定义变量
        empAlex.setTitle("Engineer");//通过方法赋值
        empAlex.setWage(26.44);
        empAlex.printEmployee();
    }
}

```

> 运行结果:
>
> ```shell
> Name:Alex 
> Age:26
> Title:Engineer
> Wage:26.44
> ```

