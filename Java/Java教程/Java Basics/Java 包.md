# Java 包 package

通常，一个公司使用它互联网域名的颠倒形式来作为它的包名.例如：互联网域名是 runoob.com，所有的包名都以 com.runoob 开头。包名中的每一个部分对应一个子目录。

例如：有一个 **com.runoob.test** 的包，这个包包含一个叫做 Runoob.java 的源文件，那么相应的，应该有如下面的一连串子目录：

```java
....\com\runoob\test\Runoob.java
```

编译的时候，编译器为包中定义的每个类、接口等类型各创建一个不同的输出文件，输出文件的名字就是这个类型的名字，并加上 .class 作为扩展后缀。 例如：

```java
// 文件名: Runoob.java
 
package com.runoob.test;
public class Runoob {
      
}
class Google {
      
}
```

```shell
$javac -d . Runoob.java
```

输出:

```shell
.\com\runoob\test\Runoob.class
.\com\runoob\test\Google.class
```

