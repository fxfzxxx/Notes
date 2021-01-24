# Java 修饰符

Java 修饰符主要分两类:

- 访问修饰符(Access Modifiers)
- 非访问修饰符(Non-Access Modifiers)

## 访问修饰符

- **default** (即默认，什么也不写）: 在同一 **包内** *可见*，不使用任何修饰符。使用对象：类、接口、变量、方法。
- **private** : 在 **同一类** 内可见。使用对象：变量、方法。 **注意：不能修饰类（外部类）**
- **public** : 对所有类可见。使用对象：类、接口、变量、方法
- **protected** : 对同一包内的类和所有子类可见。使用对象：变量、方法。 **注意：不能修饰类（外部类）**。

> 可见就是 Accessible
>
> **Public**: It is basically as simple as you can access from any class whether that is in same package or not. ... **Default**: It is accessible **in the** same package from any of the class of package. To access you can create an object of the class. But you can not access this variable outside of the package.

### 私有访问修饰符-private

私有访问修饰符是最严格的访问级别，所以被声明为 **private** 的方法、变量和构造方法只能被所属类访问，并且类和接口不能声明为 **private**。

声明为私有访问类型的变量只能通过类中公共的 getter 方法被外部类访问。

**Private 访问修饰符的使用主要用来隐藏类的实现细节和保护类的数据。**

下面的类使用了私有访问修饰符：

```java 
public class Logger {
   private String format;
    
   public String getFormat() {
      return this.format;
   }
   public void setFormat(String format) {
      this.format = format;
   }
}
```



实例中，Logger 类中的 format 变量为私有变量，所以其他类不能直接得到和设置该变量的值。为了使其他类能够操作该变量，定义了两个 public 方法：`getFormat() `（返回 format的值）和 `setFormat(String)`（设置 format 的值）.

### 受保护的访问修饰符-protected

protected 需要从以下两个点来分析说明：

- **子类与基类在同一包中**：被声明为 protected 的变量、方法和构造器能被同一个包中的任何其他类访问；
- **子类与基类不在同一包中**：那么在子类中，子类实例可以访问其从基类继承而来的 protected 方法，而不能访问基类实例的protected方法。

protected 可以修饰数据成员，构造方法，方法成员，**不能修饰类（内部类除外）**。

> 如果把 **父类** 方法 声明为 `private`，那么除了 **父类** 之外的类将不能访问该方法。

> 如果把 **父类** 方法 声明为 `public`，那么所有的类都能够访问该方法。

> 如果我们只想让该方法对其所在类的子类可见，则将该方法声明为 `protected`。

### 访问控制和继承

请注意以下方法继承的规则：

- 父类中声明为 public 的方法在子类中也必须为 public。
- 父类中声明为 protected 的方法在子类中要么声明为 protected，要么声明为 public，不能声明为 private。
- 父类中声明为 private 的方法，不能够被继承。

---





## 非访问修饰符

static 修饰符，用来修饰类方法和类变量。

final 修饰符，用来修饰类、方法和变量，final 修饰的类不能够被继承，修饰的方法不能被继承类重新定义，修饰的变量为常量，是不可修改的。

abstract 修饰符，用来创建抽象类和抽象方法。

synchronized 和 volatile 修饰符，主要用于线程的编程。

### static 修饰符

- **静态变量：**

  static 关键字用来声明独立于对象的静态变量，无论一个类实例化多少对象，它的静态变量只有一份拷贝。 静态变量也被称为类变量。局部变量不能被声明为 static 变量。

- **静态方法：**

  static 关键字用来声明独立于对象的静态方法。**静态方法不能使用类的非静态变量**。静态方法从参数列表得到数据，然后计算这些数据。

#### 一个例子

```java
public class InstanceCounter{
    // 私有类变量
    private static int numInstances = 0;
    // get 类方法访问类变量
    protected static int getCount(){
        return numInstances;
    }
    // 私有类方法 
    private static void addInstances(){
        numInstances++;
    }
    // 构造器
    InstanceCounter(){
        InstanceCounter.addInstances();
    }

    public static void main(String[] args) {
        System.out.println("Starting with " + InstanceCounter.getCount() + " instances.");

        // 500个实例, 每个实例创建的时候 构造器 会调用 get类方法 改变 类变量的值.
        for (int i = 0;i<500;i++){
            new InstanceCounter();
        }

        System.out.println("Created " + InstanceCounter.getCount() + " instances.");

    }
}
```

### final 修饰符

#### **final 变量:**

final 表示"最后的、最终的"含义，变量一旦赋值后，不能被重新赋值。被 final 修饰的实例变量必须**显式指定初始值**。

final 修饰符通常和 static 修饰符一起使用来创建类常量。

#### final 方法:

父类中的 final 方法可以被子类继承，但是**不能被子类重写**。

声明 final 方法的主要目的是防止该方法的内容被修改。

#### final 类:

final 类**不能被继承**，没有类能够继承 final 类的任何特性。

### abstract 修饰符

**抽象类：**

抽象类不能用来**实例化对象**，声明抽象类的唯一目的是为了将来对该类进行扩充。

一个类不能同时被 abstract 和 final 修饰。如果一个类包含**抽象方法**，那么该类一定要声明为抽象类，否则将出现编译错误。

抽象类可以包*含抽象方法*和*非抽象方法*。

```java
abstract class Car{
   private double price;
   private String model;
   private String year;
   public abstract void moveForward(); //抽象方法
   public abstract void moveBackward();
}
```

**抽象方法**

抽象方法是一种**没有任何实现**的方法，该方法的的具体实现由**子类提供**。

抽象方法不能被声明成 final 和 static。

**任何继承抽象类的子类必须实现父类的所有抽象方法，除非该子类也是抽象类。**

如果一个类包含若干个抽象方法，那么该类必须声明为抽象类。抽象类可以不包含抽象方法。

抽象方法的声明以分号结尾，例如：`public abstract sample();`。

```java
public abstract class SuperClass{
    abstract void m(); //抽象方法
}
// 继承抽象方法
class SubClass extends SuperClass{
     //实现抽象方法
      void m(){
          .........
      }
}
```

### synchronized 修饰符

synchronized 关键字声明的方法同一时间只能被**一个线程**访问。synchronized 修饰符可以应用于四个访问修饰符。

### volatile 修饰符

volatile 修饰的成员变量在**每次被线程访问时**，都强制从共享内存中**重新读取**该成员变量的值。而且，当成员变量发生变化时，会强制线程将**变化值回写到共享内存**。这样在任何时刻，两个**不同的线程**总是看到某个成员变量的**同一个值**。

一个 volatile 对象引用可能是 null。

```java
public class MyRunnable implements Runnable
{
    private volatile boolean active;
    public void run()
    {
        active = true;
        while (active) // 第一行
        {
            // 代码
        }
    }
    public void stop()
    {
        active = false; // 第二行
    }
}
```

通常情况下，在一个线程调用 run() 方法（在 Runnable 开启的线程），在另一个线程调用 stop() 方法。 如果 ***第一行\*** 中缓冲区的 active 值被使用，那么在 ***第二行\*** 的 active 值为 false 时循环不会停止。

但是以上代码中我们使用了 volatile 修饰 active，所以该循环**会停止**。