# 命名及注释标准

### **命名规范**

1、 项目名全部小写

2、 包名全部小写

3、 类名首字母大写，如果类名由多个单词组成，每个单词的首字母都要大写。如：**public class MyFirstClass{}**

4、 变量名、方法名首字母小写，如果名称由多个单词组成，每个单词的首字母都要大写。如：

```java
int index=0;
public void toString(){}
```

5、 常量名全部大写

如：

```java
public static final String GAME_COLOR="RED";
```

6、所有命名规则必须遵循以下规则：

-  1)、名称只能由字母、数字、下划线、$符号组成
-  2)、不能以数字开头
-  3)、名称不能使用JAVA中的关键字。
-  4)、坚决不允许出现中文及拼音命名。

### **注释规范**

1、类注释

在每个类前面必须加上类注释，注释模板如下：

```java
/**
* Copyright (C), 2006-2010, ChengDu Lovo info. Co., Ltd.
* FileName: Test.java
* 类的详细说明
*
* @author 类创建者姓名
* @Date    创建日期
* @version 1.00
*/
```

2、属性注释

在每个属性前面必须加上属性注释，注释模板如下：

```java
/** 提示信息 */
private String strMsg = null;
```

3、方法注释

在每个方法前面必须加上方法注释，注释模板如下：

```java
/**
* 类方法的详细使用说明
*
* @param 参数1 参数1的使用说明
* @return 返回结果的说明
* @throws 异常类型.错误代码 注明从此类方法中抛出异常的说明
*/
```

4、构造方法注释

在每个构造方法前面必须加上注释，注释模板如下：

```java
/**
* 构造方法的详细使用说明
*
* @param 参数1 参数1的使用说明
* @throws 异常类型.错误代码 注明从此类方法中抛出异常的说明
*/
```

5、方法内部注释

在方法内部使用单行或者多行注释，该注释根据实际情况添加。

如：

```java
//背景颜色
Color bgColor = Color.RED
```

***



### **一个完整的 .Java 源程序应该包括下列部分：**

-  `package` 语句，该部分 *至多* 只有一句，必须放在源程序的第一句。
-  `import` 语句，该部分可以有若干import语句或者没有，必须放在所有的类定义之前。
-  `public classDefinition`，公共类定义部分，至多只有一个公共类的定义，Java语言规定该Java源程序的文件名必须与该公共类名完全一致。
-  `classDefinition`，类定义部分，可以有0个或者多个类定义。
- `interfaceDefinition`，接口定义部分，可以有0个或者多个接口定义。

例如：

```java
package javawork.helloworld;
/*把编译生成的所有．class文件放到包javawork.helloworld中*/
import java awt.*;
//告诉编译器本程序中用到系统的AWT包
import javawork.newcentury;
/*告诉编译器本程序中用到用户自定义的包javawork.newcentury*/
 public class HelloWorldApp{...｝
/*公共类HelloWorldApp的定义，名字与文件名相同*/ 
class TheFirstClass｛...｝;
//第一个普通类TheFirstClass的定义 
interface TheFirstInterface{......}
/*定义一个接口TheFirstInterface*/
```

**package语句：**由于Java编译器为每个类生成一个字节码文件，且文件名与类名相同因此同名的类有可能发生冲突。为了解决这一问题，Java提供包来管理类名空间，包实 提供了一种命名机制和可见性限制机制。