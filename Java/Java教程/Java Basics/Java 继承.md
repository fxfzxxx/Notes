# Java 继承

## 为什么需要继承

代码存在重复了，导致后果就是代码量大且臃肿，而且维护性不高(维护性主要是后期需要修改的时候，就需要修改很多的代码，容易出错)，所以要从根本上解决代码的问题，就需要继承. 

## 继承的特性

- 子类拥有父类非 **private** 的属性、方法。
- 子类可以拥有自己的属性和方法，即子类可以对父类进行扩展。
- 子类可以用自己的方式实现父类的方法。
- Java 的继承是单继承，但是可以多重继承，单继承就是一个子类只能继承一个父类，多重继承就是，例如 B 类继承 A 类，C 类继承 B 类，所以按照关系就是 B 类是 C 类的父类，A 类是 B 类的父类，这是 Java 继承区别于 C++ 继承的一个特性。
- 提高了类之间的耦合性（继承的缺点，耦合度高就会造成代码之间的联系越紧密，代码**独立性越差**）。

## **继承关键字**

继承可以使用 `extends` 和 `implements` 这两个关键字来实现继承，而且所有的类都是继承于 `java.lang.Object`，当一个类没有继承的两个关键字，则默认继承`object`（这个类在 `java.lang` 包中，所以不需要 `import`）祖先类。

### extends关键字

在 Java 中，类的继承是单一继承，也就是说，**一个子类只能拥有一个父类**，所以 extends 只能继承一个类。

```java
public class A{
    ...
}

public class B extends A{
    ...
}
```

### implements关键字

使用 implements 关键字可以变相的使java具有多继承的特性，使用范围为类继承接口的情况，**可以同时继承多个接口**（接口跟接口之间采用逗号分隔）。

```java
public interface A {
    ...
}
 
public interface B {
    ...
}
 
public class C implements A,B {
}
```

### super 与 this 关键字

super关键字：我们可以通过super关键字来实现**对父类成员的访问**，用来引用当前对象的父类。

this关键字：指向**自己**的引用。

#### super与this比较 的例子

```java
class Animal {
    
    void name() {
        System.out.println("Animal");
    }
}

class Fish extends Animal{
    void name() {
        System.out.println("Fish");
    }

    void nameTest() {
        this.name(); //调用类内函数 输出 Fish
        super.name(); //调用父函数 输出 Animal
    }
}

public class InheritTest {
    public static void main(String[] args) {
        Animal animal = new Animal();
        animal.name();
        Fish fish = new Fish();
        fish.name();
        fish.nameTest();
    }
    
}
```

输出：

```java
Animal
Fish
Fish
Animal
```

### final关键字

final 关键字声明类可以把类定义为**不能继承**的，即最终类；或者用于修饰方法，该方法**不能**被子类**重写**.

## 构造器

子类是**不继承**父类的**构造器**（构造方法或者构造函数）的，它**只是调用**（隐式或显式）。如果父类的构造器带**有参数**，则必须在子类的构造器中显式地通过 **super** 关键字**调用**父类的构造器并配以适当的参数列表。

如果父类构造器**没有参数**，则在子类的构造器中**不需要**使用 **super** 关键字**调用**父类构造器，系统会自动调用父类的无参构造器。

### 构造器继承 的例子

```java
class SuperClass {
    private int n;
    SuperClass(){
      System.out.println("SuperClass()");
    }
    SuperClass(int n) {
      System.out.println("SuperClass(int n):" + n);
      this.n = n;
    }
  }
  // SubClass 类继承
  class SubClass extends SuperClass{
    private int n;
    
    SubClass(){ // 自动调用父类的无参数构造器
      System.out.println("SubClass()");
    }  
    
    public SubClass(int n){ 
      super(300);  // 调用父类中带有参数的构造器
      System.out.println("SubClass(int n):"+n);
      this.n = n;
    }
  }
  // SubClass2 类继承
  class SubClass2 extends SuperClass{
    private int n;
    
    SubClass2(){
      super(300);  // 调用父类中带有参数的构造器
      System.out.println("SubClass2()");
    }  
    
    public SubClass2(int n){ // 自动调用父类的无参数构造器
      System.out.println("SubClass2(int n):"+n);
      this.n = n;
    }
  }
  public class InheritConstructor {
    public static void main (String args[]){
      System.out.println("------SubClass 类继承------");
      SubClass sc1 = new SubClass();
      SubClass sc2 = new SubClass(100); 
      System.out.println("------SubClass2 类继承------");
      SubClass2 sc3 = new SubClass2();
      SubClass2 sc4 = new SubClass2(200); 
    }
  }
```

其实这里仍然不明白 `super(300)` 的意思.

输出:

```java
------SubClass 类继承------
SuperClass()
SubClass()
SuperClass(int n):300
SubClass(int n):100
------SubClass2 类继承------
SuperClass(int n):300
SubClass2()
SuperClass()
SubClass2(int n):200
```



### super 关键字

- 子类的所有构造方法内部， 第一行会（隐式）自动先调用父类的无参构造函数 **super()**；
- 如果子类构造方法第一行显式调用了父类构造方法，系统就不再调用无参的 **super()** 了。

**在编写代码要注意：**

- 如果父类中**不含** 默认构造函数（就是 类名() ），那么子类中的super()语句就会执行失败，系统就会报错。一般 默认构造函数 编译时会自动添加，但如果类中已经有一个构造函数时，就不会添加。
- 执行父类构造函数的语句只能放在**函数内语句的首句**，不然会报错。

在继承关系中，在调用函数（方法）或者类中的成员变量时，JVM（JAVA虚拟机）会先检测当前的类（也就是子类）是否含有该函数或者成员变量，**如果有，就执行子类中的，如果没有才会执行父类中的**。

#### super 关键字的例子

```java
class Base {
    public Base() {
        System.out.println("Base--默认构造方法");
    }
    
    public Base(int c){
        System.out.println("Base--有参构造方法--" + c);
    }
}

public class Derived extends Base {
    public Derived() {
        // super(); //系统会自动隐式先调用父类的无参构造函数 super(); //必须是第一行，否则不能编译 
        System.out.println("Derived--默认构造方法");
    }
    
    public Derived(int c) {
        // super(); //系统会自动隐式先调用父类的无参构造函数 super(); //必须是第一行，否则不能编译
        System.out.println("Derived--有参构造方法" + c);
    }
    
    public Derived(int a, int b) {
        super(a); //如果子类构造方法第一行显式调用了父类构造方法，系统就不再调用无参的super()了。
        System.out.println("Derived--有参构造方法--" + b);
    }
    
    public static void main(String[] args) {
        System.out.println("============子类无参============");
        Derived no = new Derived();
        System.out.println("============子类有参============");
        Derived have = new Derived(33);
        System.out.println("============子类有参============");
        Derived have2 = new Derived(33, 55);
    }
}
```

输出:

```shell
============子类无参============
Base--默认构造方法
Derived--默认构造方法
============子类有参============
Base--默认构造方法
Derived--有参构造方法33
============子类有参============
Base--有参构造方法--33
Derived--有参构造方法--55
```

### 如何继承父类中的 private 属性和方法

```java

/**建立一个公共动物父类*/
class Animals {
    private String name;
    private int id;
    /*由于name和id都是私有的，所以子类不能直接继承，
    需要通过有参构造函数进行继承*/
    Animals(String myname,int myid) {
        name = myname;
        id = myid;
    }
    void eat() {
        System.out.println(name+"正在吃");
    }
    void sleep() {
        System.out.println(name+"正在睡");
    }
    void introduction() {
        System.out.println("大家好！我是"  +id+"号"+name +".");
    }

}

//子类 Penguin 需要通过关键字 super 进行声明

public class InheritConstructorPrivate extends Animals {
    public InheritConstructorPrivate(String myname,int myid) {
        super(myname,myid); // 声明继承父类中的两个属性
    }

    public static void main(String[] args) {
        InheritConstructorPrivate a = new InheritConstructorPrivate("Sam",12345);
        a.eat();
        a.introduction();

    }
}
```

输出:

```java
Sam正在吃
大家好！我是12345号Sam.
```





