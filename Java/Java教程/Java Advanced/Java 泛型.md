# Java 泛型

Java 泛型（generics）是 JDK 5 中引入的一个新特性, 泛型提供了编译时类型安全检测机制，该机制允许程序员在编译时检测到非法的类型。

泛型的本质是参数化类型，也就是说所操作的数据类型被指定为一个参数。

## 泛型方法

你可以写一个泛型方法，该方法在调用时可以接收 **不同类型的参数**。根据传递给泛型方法的参数类型，编译器适当地处理每一个方法调用。

下面是定义泛型方法的规则：

- 所有泛型方法声明都有一个类型参数声明部分（由尖括号分隔），该类型参数声明部分在方法返回类型之前（在下面例子中的<E>）。
- 每一个类型参数声明部分包含一个或多个类型参数，参数间用逗号隔开。一个泛型参数，也被称为一个类型变量，是用于指定一个泛型类型名称的标识符。
- 类型参数能被用来声明返回值类型，并且能作为泛型方法得到的实际参数类型的**占位符**。
- 泛型方法体的声明和其他方法一样。注意类型参数只能代表**引用型类型**，不能是原始类型（像int,double,char的等）。

#### 例子: 泛型方法 输出不同数组元素

```java
package GenericsTest;

public class GenericsMethodTest {
    //Generic method
    public static <E> void printArray(E[] inputArray) {
        for (E e : inputArray) {
            System.out.printf("%s",e + " ");
        }
    }

    public static void main(String[] args) {
        // Different arrays
        Integer[] intArray = {1,2,3,4,5};
        Double[] doubleArray = {1.1,2.2,3.3};
        String[] charArray = {"Hello","World!"};
        // invoke with generic method
        printArray(intArray);
        printArray(doubleArray);
        printArray(charArray);
    }
}

```

输出:

```java
1 2 3 4 5 1.1 2.2 3.3 Hello World! 
```

**有界的类型参数:**

可能有时候，你会想限制那些被允许传递到一个类型参数的类型种类范围。例如，一个操作数字的方法可能只希望接受Number或者Number子类的实例。这就是有界类型参数的目的。

要声明一个有界的类型参数，首先列出类型参数的名称，后跟**extends**关键字，最后紧跟它的上界。

#### 例子: 有界泛型方法

```java
public class MaximumTest
{
   // 比较三个值并返回最大值
   public static <T extends Comparable<T>> T maximum(T x, T y, T z)
   {                     
      T max = x; // 假设x是初始最大值
      if ( y.compareTo( max ) > 0 ){
         max = y; //y 更大
      }
      if ( z.compareTo( max ) > 0 ){
         max = z; // 现在 z 更大           
      }
      return max; // 返回最大对象
   }
   public static void main( String args[] )
   {
      System.out.printf( "%d, %d 和 %d 中最大的数为 %d\n\n",
                   3, 4, 5, maximum( 3, 4, 5 ) );
 
      System.out.printf( "%.1f, %.1f 和 %.1f 中最大的数为 %.1f\n\n",
                   6.6, 8.8, 7.7, maximum( 6.6, 8.8, 7.7 ) );
 
      System.out.printf( "%s, %s 和 %s 中最大的数为 %s\n","pear",
         "apple", "orange", maximum( "pear", "apple", "orange" ) );
   }
}
```

输出:

```java
3, 4 和 5 中最大的数为 5

6.6, 8.8 和 7.7 中最大的数为 8.8

pear, apple 和 orange 中最大的数为 pear
```

## 泛型类

泛型类的声明和非泛型类的声明类似，除了在类名后面添加了**类型参数**声明部分。

和泛型方法一样，泛型类的类型参数声明部分也包含**一个或多个**类型参数，参数间用逗号隔开。一个泛型参数，也被称为一个类型变量，是用于指定一个泛型类型名称的标识符。因为他们接受一个或多个参数，这些类被称为**参数化的类或参数化的类型**。

#### 例子: 泛型类

```java
package GenericsTest;

public class GenericClassTest <T>{
    private T t;

    public void add(T t){
        this.t = t;
    }
    
    public T get(){
        return t;
    }

    public static void main(String[] args) {
        GenericClassTest<Integer> integerBox = new GenericClassTest<Integer>();
        GenericClassTest<String> stringBox = new GenericClassTest<String>();
        integerBox.add(22); // (new Integer(22))
        stringBox.add("Twenty-two");// (new String("Twenty-twi")) 

        System.out.printf("Integer value is :%d\n\n", integerBox.get());
        System.out.printf("String value is :%s\n", stringBox.get());
    }
}

```

输出:

```java
Integer value is :22

String value is :Twenty-two
```



## 类型通配符

类型通配符一般是使用?代替具体的类型参数。例如 **List<?>** 在逻辑上是**List<String>,List<Integer>** 等所有List<具体类型实参>的父类。

```java
import java.util.*;
 
public class GenericTest {
     
    public static void main(String[] args) {
        List<String> name = new ArrayList<String>();
        List<Integer> age = new ArrayList<Integer>();
        List<Number> number = new ArrayList<Number>();
        
        name.add("icon");
        age.add(18);
        number.add(314);
 
        getData(name);
        getData(age);
        getData(number);
       
   }
 
   public static void getData(List<?> data) {
      System.out.println("data :" + data.get(0));
   }
}
```

输出:

```java
data :icon
data :18
data :314
```

**解析：** 因为 **getData()** 方法的参数是List类型的，所以name，age，number都可以作为这个方法的实参，这就是通配符的作用

2、类型通配符上限通过形如List来定义，如此定义就是通配符泛型值接受Number及其下层子类类型。

```java
import java.util.*;
 
public class GenericTest {
     
    public static void main(String[] args) {
        List<String> name = new ArrayList<String>();
        List<Integer> age = new ArrayList<Integer>();
        List<Number> number = new ArrayList<Number>();
        
        name.add("icon");
        age.add(18);
        number.add(314);
 
        //getUperNumber(name);//1
        getUperNumber(age);//2
        getUperNumber(number);//3
       
   }
 
   public static void getData(List<?> data) {
      System.out.println("data :" + data.get(0));
   }
   
   public static void getUperNumber(List<? extends Number> data) {
          System.out.println("data :" + data.get(0));
       }
}
```

输出:

```java
data :18
data :314
```

**解析：** 在(//1)处会出现错误，因为getUperNumber()方法中的参数已经限定了参数泛型上限为Number，所以泛型为String是不在这个范围之内，所以会报错

3、类型通配符下限通过形如 **List<? super Number>**来定义，表示类型只能接受Number及其三层父类类型，如 Object 类型的实例。