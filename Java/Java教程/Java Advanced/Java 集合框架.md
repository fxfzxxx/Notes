# Java 集合框架

<img src="https://www.runoob.com/wp-content/uploads/2014/01/2243690-9cd9c896e0d512ed.gif" alt="img"  />S

从上面的集合框架图可以看到，Java 集合框架主要包括两种类型的容器，一种是集合（Collection），存储一个元素集合，另一种是图（Map），存储键/值对映射。Collection 接口又有 3 种子类型，List、Set 和 Queue，再下面是一些抽象类，最后是具体实现类，常用的有 [ArrayList](https://www.runoob.com/java/java-arraylist.html)、[LinkedList](https://www.runoob.com/java/java-linkedlist.html)、[HashSet](https://www.runoob.com/java/java-hashset.html)、LinkedHashSet、[HashMap](https://www.runoob.com/java/java-hashmap.html)、LinkedHashMap 等等。

集合框架是一个用来代表和操纵集合的统一架构。所有的集合框架都包含如下内容：

- 

  **接口：**是代表集合的抽象数据类型。例如 Collection、List、Set、Map 等。之所以定义多个接口，是为了以不同的方式操作集合对象

- **实现（类）：**是集合接口的具体实现。从本质上讲，它们是可重复使用的数据结构，例如：ArrayList、LinkedList、HashSet、HashMap。

- **算法：**是实现集合接口的对象里的方法执行的一些有用的计算，例如：搜索和排序。这些算法被称为多态，那是因为相同的方法可以在相似的接口上有着不同的实现。

除了集合，该框架也定义了几个 Map 接口和类。Map 里存储的是键/值对。尽管 Map 不是集合，但是它们完全整合在集合中。

<img src="https://www.runoob.com/wp-content/uploads/2014/01/java-coll-2020-11-16.png" alt="img" style="zoom:80%;" />

Java 集合框架提供了一套性能优良，使用方便的接口和类，java集合框架位于 java.util 包中， 所以当使用集合框架的时候需要进行导包。

---

## 集合接口

| 接口        | 接口描述                                                     |
| :---------- | :----------------------------------------------------------- |
| Collection  | Collection 是最基本的集合接口，一个 Collection 代表一组 Object，即 Collection 的元素, Java不提供直接继承自Collection的类，只提供继承于的子接口(如List和set)。Collection 接口存储一组不唯一，无序的对象。 |
| List        | List接口是一个有序的 Collection，使用此接口能够精确的控制每个元素插入的位置，能够通过索引(元素在List中位置，类似于数组的下标)来访问List中的元素，第一个元素的索引为 0，而且允许有相同的元素。List 接口存储一组不唯一，有序（插入顺序）的对象。 |
| Set         | Set具有与 Collection 完全一样的接口，只是行为上不同，Set 不保存重复的元素。Set 接口存储一组唯一，无序的对象。 |
| SortedSet   | SortedSet 继承于Set保存有序的集合。                          |
| Map         | Map 接口存储一组键值对象，提供key（键）到value（值）的映射。 |
| Map.Entry   | Map.Entry 描述在一个Map中的一个元素（键/值对）。是一个 Map 的内部接口。 |
| SortedMap   | SortedMap 继承于 Map，使 Key 保持在升序排列。                |
| Enumeration | Enumeration 这是一个传统的接口和定义的方法，通过它可以枚举（一次获得一个）对象集合中的元素。这个传统接口已被迭代器取代。 |

### Set和List的区别

- Set 接口实例存储的是无序的，不重复的数据。List 接口实例存储的是有序的，可以重复的元素。
- Set检索效率低下，删除和插入效率高，插入和删除不会引起元素位置改变 **<实现类有HashSet,TreeSet>**。
- List和数组类似，可以动态增长，根据实际存储的数据的长度自动增长List的长度。查找元素效率高，插入删除效率低，因为会引起其他元素位置改变 **<实现类有ArrayList,LinkedList,Vector>** 。

## 如何使用迭代器

#### 例子: 遍历AarryLisit

```java
package traverse;

import java.util.ArrayList;
import java.util.Iterator;
import java.util.List;

public class ArrayListTraverse {
    public static void main(String[] args) {
        List<String> list = new  ArrayList<String>();
        list.add("hello");
        list.add("World");
        list.add("lol");

        //for-each
        for(String str : list) {
            System.out.println(str);
        }
        //ArrayList to array
        String[] str = new String[list.size()];
        list.toArray(str);
        for (String string : str) {
            System.out.println(string);            
        }
        //Iterator
        Iterator<String> ite = list.iterator();
        while (ite.hasNext()) {
            System.out.println(ite.next());
            
        }
    }
}
```

#### 例子: 遍历map

```java
package traverse;

import java.util.*;

public class MapTraverse {
    public static void main(String[] args) {
        Map<String, String> map = new HashMap<String, String>();
        map.put("1", "one");
        map.put("2", "two");
        map.put("3", "three");

        // keySet()
        for (String key : map.keySet()) {
            System.out.println(key + " " + map.get(key));
        }

        // iterator and entrySet()
        Iterator<Map.Entry<String, String>> it = map.entrySet().iterator();
        while (it.hasNext()) {
            Map.Entry<String, String> entry = it.next();
            System.out.println("key= " + entry.getKey() + " and value= " + entry.getValue());
        }

        //values()
        for (String v : map.values()) {
            System.out.println(v);
            
        }
    }
}

```

