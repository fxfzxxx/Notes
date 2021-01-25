# Java HashSet

HashSet 基于 HashMap 来实现的，是一个不允许有**重复**元素的集合。

HashSet 允许有 null 值。

HashSet 是**无序**的，即不会记录插入的顺序。

HashSet 不是**线程安全**的， 如果多个线程尝试同时修改 HashSet，则最终结果是不确定的。 您必须在多线程访问时显式同步对 HashSet 的并发访问。

HashSet 实现了 Set 接口。

<img src="https://www.runoob.com/wp-content/uploads/2020/07/java-hashset-hierarchy.png" alt="img" style="zoom:80%;" />

### 添加元素

HashSet 类提供类很多有用的方法，添加元素可以使用 add() 方法:

## 实例

```java
*// 引入 HashSet 类*    
**import** java.util.HashSet;

**public** **class** RunoobTest {
  **public** **static** **void** main(String[] args) {
  HashSet<String> sites = **new** HashSet<String>();
    sites.add("Google");
    sites.add("Runoob");
    sites.add("Taobao");
    sites.add("Zhihu");
    sites.add("Runoob"); *// 重复的元素不会被添加*
    System.out.println(sites);
  }
}
```

执行以上代码，输出结果如下：

```
[Google, Runoob, Zhihu, Taobao]
```



在上面的实例中，Runoob 被添加了两次，它在集合中也只会出现一次，因为集合中的每个元素都必须是唯一的。



### 判断元素是否存在

我们可以使用 contains() 方法来判断元素是否存在于集合当中:

## 实例

```java

// 引入 HashSet 类   
import java.util.HashSet;

public class RunoobTest {
  public static void main(String[] args) {
  HashSet<String> sites = new HashSet<String>();
    sites.add("Google");
    sites.add("Runoob");
    sites.add("Taobao");
    sites.add("Zhihu");
    sites.add("Runoob"); // 重复的元素不会被添加
    System.out.println(sites.contains("Taobao"));
  }
}
```

执行以上代码，输出结果如下：

```
true
```

### 删除元素

我们可以使用 remove() 方法来删除集合中的元素:

## 实例

```java
// 引入 HashSet 类
import java.util.HashSet;

public class RunoobTest {
  public static void main(String[] args) {
  HashSet<String> sites = new HashSet<String>();
    sites.add("Google");
    sites.add("Runoob");
    sites.add("Taobao");
    sites.add("Zhihu");
    sites.add("Runoob");   // 重复的元素不会被添加
    sites.remove("Taobao"); // 删除元素，删除成功返回 true，否则为 false
    System.out.println(sites);
  }
}
```

执行以上代码，输出结果如下：

```
[Google, Runoob, Zhihu]
```

删除集合中所有元素可以使用 clear 方法：

## 实例

```java
// 引入 HashSet 类*    
import java.util.HashSet;

public class RunoobTest {
  public static void main(String[] args) {
  HashSet<String> sites = new HashSet<String>();
    sites.add("Google");
    sites.add("Runoob");
    sites.add("Taobao");
    sites.add("Zhihu");
    sites.add("Runoob");   // 重复的元素不会被添加*
    sites.clear(); 
    System.out.println(sites);
  }
}
```

执行以上代码，输出结果如下：

```
[]
```

### 计算大小

如果要计算 HashSet 中的元素数量可以使用 size() 方法：

## 实例

```java
// 引入 HashSet 类*    
import java.util.HashSet;

public class RunoobTest {
  public static void main(String[] args) {
  HashSet<String> sites = new HashSet<String>();
    sites.add("Google");
    sites.add("Runoob");
    sites.add("Taobao");
    sites.add("Zhihu");
    sites.add("Runoob");   // 重复的元素不会被添加*
    System.out.println(sites.size()); 
  }
}
```

执行以上代码，输出结果如下：

```
4
```

### 迭代 HashSet

可以使用 for-each 来迭代 HashSet 中的元素。

## 实例

```java
// 引入 HashSet 类 
import java.util.HashSet;

public class RunoobTest {
  public static voi* main(String[] args) {
  HashSet<String> sites = **new** HashSet<String>();
    sites.add("Google");
    sites.add("Runoob");
    sites.add("Taobao");
    sites.add("Zhihu");
    sites.add("Runoob");   // 重复的元素不会被添加*
    for (String i : sites) {
      System.out.println(i);
    }
  }
}
```

执行以上代码，输出结果如下：

```
Google
Runoob
Zhihu
Taobao
```