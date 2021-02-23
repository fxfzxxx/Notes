##### 字符编码

苹果 -> 10101010 (编码)

10101010 -> 苹果 (解码)

charset 字符集 (101 -> a    111 ->b)

##### **常见字符集**

ASCII

UTF-8 (主要开发字符集)

GBK

GB2312

```html
<meta charset="UTF-8">
```

##### **实体**

如空格，> <实现输出，要用转义符。 &nbsp 是空格。&gt >, &lt <。

##### **meta** **标签**

charset, name, content...



```html
<!-- 搜索引擎爬keywords: -->
<meta name = "keywords" content ="HTML5, CSS3"> 
<!-- 网页描述 -->
<meta name = "description" content ="This is a tutorial website.">
<!-- 搜索引擎超链接 -->
<title>Html5 tutorial website</title>
<!--3s 跳转到 -->
<meta http-equiv="refresh" content = "3;url=https://www.baidu.com"
```

##### **浏览器自动修正**

h1在body外，依然能够正确显示。因为浏览器修正，inspect后element选项，可查看内存中实际的代码。

##### **换行**

`<br></br>`

##### **相对路径**

./ 或../ 可加可不加

##### **超链接**

./ 当前目录 ../上一目录

```html
<a herf="#" target="_self"></a> // 当前页面
<a herf="#" target="_blank"></a> // 新的页面
```

/# 路径占位符

##### 图片

alt 用于搜索引擎搜索

图片提前裁好 尽量不要用缩放

webp 格式 效果好 还小 可动图

base64 编码图片 放再src直接显示，与网页同时显示，速度快。

##### **内联框架**

```html
<iframe src="https://www.baidu.com" width = '' height='' </iframe>
```

##### **音频和视频**

如果前面的无法显示，往下兼容更老的浏览器。

```html
<audio controls>
	<source src=".mp3">
    <source src=".ogg">
    <embed src=".mp3" type="audio/mp3" width="" height="">
</audio>

<video controls>
	<source src=".webm">
    <source src=".mp4">
    <embed src=".mp4" type="audio/mp4" width="" height="">
</video>
```

##### 表单

```html
<form action="target.html">
        Username: 
        <input type="text" name="Username" placeholder="tom123" autocomplete="off"/>
        <br /><br />
        Password:
        <input type="password" name="Password" placeholder="********" />
        <br /><br />
        Date: 
        <input type="month" name="Date" /> <br /><br />
        Payment method: 
        <input type="radio" name="method" value="P" />Paypal
        <input type="radio" name="method" value="C" checked />Credit Card
        <br /><br />
        Country:
        <select name="country">
            <option value="1">1</option>
            <option selected value="2">2</option>
            <option value="3">3</option>
        </select>
        <br><br>
        <input type="submit" value="Submit" />
        <br /><br />
    </form>
```

##### 收藏图标

favicon.ico

```html
<link ref='icon' href="facicon.ico" > 
```