##### **选择器**

通配选择器

```css
*{
    font-weight: 400;
}
```

并集选择器

```css
div,p{
    font-size = 30px;
}
```

##### **关系选择器**

子元素选择器

```css
div>span{
	color = orange;
}
```

后代选择器

```css
div span{
    color=orange;
}
```

相邻选择器: 相邻两个元素(所有挨着的)

```css
p+span{ 
    color=orange;
}
```

选择所有同级别, 之后的。属于 + 的扩展。

```css
p~span{
    color=orange;
}
```

##### 属性选择器

```html
<span title="span">人人网完了.</span>
<style>
    span[title= span]{ //不加双引号
        color=orange;
    }
    span[title^=abc]{
        color=orange; // 以abc开头
    }
    span[title$=abc]{
        color=orange; // 以abc结尾
    }
    span[title*=abc]{
        color=orange; // 含有abc
    }
</style>
```

##### 伪类选择器

```css
<style>
        ul>li:first-child{
            color: orange;
        }
</style>
```

**超链接**

```css
<style>
        ul>li:nth-child(odd){
            color: orange;
        }
        a:link {
            color: orange;
        }
        a:visited{
            color: red;
        }
        a:active{
            color: green;
        }
        a:hover{
            font-size: larger;
        }
        
    </style>
```

##### 伪元素选择器

```css
p::first-letter{
            font-size:50px;
        }
span::before{
            content: "▣"
        } 
span::after{
            content: "▣"
        }
```

##### 像素和百分比

百分比是指占上一层的百分比.

- 1 em = 1 font-size 相对于字体大小 font-size 默认16px

- 1 rem =1 font-size 但是固定16的倍数

##### RGB 值

0-255

```css
background-color: rgb(255,255,255)
background-color: rgbr(255,255,255,0.5) 透明度
background-color: #ff0000 16进制
background-color: #f00 16进制 两位重复简写
background-color: hsl(0,100%,0%) H色相 S饱和度 L亮度
```

##### 文档流 Normal Flow

多层机构的最底层

块元素独占一行 (div)垂直排列

- 宽度默认父元素全部
- 高度被内容撑开 (子元素全部)

行内元素(span)只占自身水平排列

- 高度宽度都是被内容撑开

还有不在文档流的情况

##### 盒子模型 Box Model

- width  和 height 默认是内容区.
- 500x500的盒子说的总大小（边距边框内容）

**border 边框**

```css
 			border-radius: 5px;
            border-color: aqua red green blue;
            border-width: 10px 5px 3px 1px; 上右下左
            border-style: solid;
```

**padding 内边距**

**margin 外边距**

可为负值 相反方向移动

**居中示例**

```css
width: 200px;
margin: 0 auto; 0:上下 auto：左右
```

**垂直分布**

```css
overflow: hidden 一剪梅
overflow: scrol 滚动
```

##### 外边距折叠

兄弟元素 外边距重叠

父子元素 子元素外边距传给父元素

##### display 属性

```css
display: inline 行内元素
display: block 块状元素
display: inline-block 不会独占一行的块元素（不好用） h2 是块元素
display: none 隐藏元素 取消占位
```

##### visibility 属性

```css
visibility: hidden 不显示 但占位置 跟上面的区分
visibility: visible 默认值 显示
```

##### 默认样式表重置

两个css文件：

- reset.css
- nomalize.css

##### 盒子大小

```css
height: 200px;
width: 200px;
boxing-size:content-box;高宽是内容区
boxing-size:border-box;高宽是边框包含
```

##### 轮廓和阴影

```css
outline:
box-shadow: 10px 10px 50px black; 水平 垂直 模糊半径 颜色
border-radius: 10px; 圆半径
```

##### 浮动

元素设置浮动后 水平等式不需要满足 用于水平布局

文字环绕效果

块元素设置后 不再独占一行

行内元素设置后 编程块元素 可以设置宽高

##### 文字在块元素内居中

```css
 height: 60px;
 line-height: 60px;//居中
```

##### 网页简单布局

```html
<header></header>
<main></main>
<footer></footer>
```

##### 高度塌陷

子元素按理说会撑开父元素 但用float之后 border包裹不住 就不会了

BFC Block Format Context 独立布局区域

- 不会被下面的浮动元素盖住
- 子父外边距不会重叠
- 可以包裹浮动子元素

可以通过

- `display: inline-block;`
- `float: left;`
- `overflow: hidden;`

开启.

##### Clear

如果一个元素因为`float: left;`影响了其他元素. 可以使用`clear: left` 来取消影响.

原理就是浏览器自动增加外边距.

##### ::after

不用额外添加标签, 直接通过css把 内容撑开

```css
.box3{
    content:'';
    display: block;
    clear: both;
}
```

相当于在最后一个div后面加一个div做clear: both

##### 解决高度塌陷和外边距重叠问题的终极方法

```css
.clearfix::before, .clearfix::after{
    display:table;
    clear:both;
    content:"";
}
注意此方法只是解决float造成的高度塌陷 绝对定位造成的无法解决 需要指定高度
```

##### 定位

- **相对定位 relative:** 

  ```css
  position:relative;
  top:100px;
  ```

  区别于margin-top, 不会挤压下面的元素.

  相对与自己的位置

- **绝对定位 absolute:**

  ```css
  position:absolute;
  ```

  脱离文档流, 提升元素层级. **直接变成块元素**

  如果祖先没有relative 则到视口

  z-index: 确定层级, 越大越靠前

  祖先元素层级再高 也不会盖住子元素

  

- **固定定位 fixed:**

  ```css
  position: fixed;
  ```

  直接去视口

- **粘滞定位 sticky:**

  到达某位置, 固定. 距离S相对于body

##### 包含快(containing block)

- 文档流中最近的父元素
- 绝对定位中的包含快: 离他最近的开启相对定位的**祖先元素**. 若都没有开启, 则是根元素.

##### 居中的方式之一: 绝对定位

```css
position:absolute;
margin:auto;
left:0;
right:0;
top:0;
bottom:0;
```

同理，水平和垂直居中，只需要设定两侧的位置是0；

##### 字体

- **font-family**: serif 衬线字体; sans-serif  非衬线; monospace 等宽;

  ```css
  @font-face{
      font-family: 'my-font';
      src:url('./font/appledefault.ttf') format('woff2')
  }
  font-family: 'my-font'
  ```

- **Iconfont**

  ```css
  <i class="fas fa-bell"></i> 插入铃铛图标 要在class最前面加fas (font-awsome 图标库)
  ```

  

- **对齐**: 

  ```css
  text-align: justify; 两端对齐
  vertical-align: bottom; 只要不是Baseline对齐 就能取消图片和边框之间的缝隙
  ```

  

- **显示省略号:**

  ```css
  width: 200px;
  white-space: nowrap;
  overflow: hidden;
  text-overflow: ellipsis;
  ```

  

##### 背景

```css
background-color: white;
background-image:url("../image/apple.png");
background-repeat:no-repeart; repeat-x 渐变做法
background-position:center center; 10px 10px;
background-clip: content/padding/border-box;
background-orgin: content/padding/border-box; 原点
background-size: 100px 100px; 设置图片尺寸 (100% auto / cover) 铺满 保持比例 content 保证完整显示
background-attachment: scroll/fixed 跟随或者固定
bakcground: white url() content-box #bfa
```

##### 雪碧图 sprite image

为了一次性加载所有图片 就把图片放在一个background图片里 然后通过控制postion: px px 来显示特定图片

##### 线性渐变

```css
background-image: linear-gradient(to right(从左向右),red 50px(从50开始渐变),yellow);
background-image:repeat-linear-gradient()
```

##### 径向渐变

```css
background-image: radial-gradient()
```

##### 图片大小设置

```css
.img-wrapper img{
	width:100%
    vertical-align: bottom;(图片底部与border 距离)

}
```

##### 表格样式

```css
 table {
                width: 50%;
                border: 1px solid;
                border-collapse: collapse;
                margin: 0 auto;
            }

            td{
                height: 100px;
                border: 1px solid;
                vertical-align: middle;
                text-align: center; 文字居中
            }

            tr:nth-child(2n){
                background-color: #bfa;
            }
```

##### 通过表格设置居中

```css
.box1{
                background-color: #bfa;
                width: 300px;
                height: 300px;
                display: table-cell;
                vertical-align: middle;
                text-align: center;
            }
            .box2{
                background-color: orange;
                width: 50px;
                height: 50px;
                margin: 0 auto;
            }
```

##### 显示一个三角并在父元素中居中

```css
.app{
    position: relative;
}
.app::after{
    position: absolute;
    content: '';
    width:0;
    height: 0;
    border: 10px solid transparent;
    border-top:none;
    border-bottom-color:red;
    bottom:0;
    left: 0;
    right: 0;
    margin: 0 auto;

}
```

##### hover子元素选择器的例子:

```css
li:hover>.app::after{

    position: absolute;
    content: '';
    width:0;
    height: 0;
    border: 8px solid transparent;
    border-top:none;
    border-bottom-color:white;
    bottom:0;
    left: 0;
    right: 0;
    margin: 0 auto;
}
```

只有在li的hover情况下 并且有直接的子集app class, 给app class的后一个元素增加样式.

##### 隐藏首页logo文字手段

```css
text-indent:-9999px;
```

##### transition 过渡

```css
.box4{
                height: 271px;
                width: 132px;
                background-image: url(../images/bigtap-mitu-queue-big.png);
                transition-property: all;
                transition-duration: .5s;   
                transition-timing-function: steps(4);
                background-position: 0 0;
                
            }
            .box1:hover .box4{
                background-position: -528px 0;
```

##### animation 动画

```css
.box4{
                height: 271px;
                width: 132px;
                background-image: url(../images/bigtap-mitu-queue-big.png);
                animation-name: mitu;
                animation-duration: 0.5s; 
                animation-timing-function: steps(4);
                background-position: 0 0;
                animation-iteration-count: infinite;
                animation-play-state: running;
                
            }
@keyframes mitu{
                from {
                    background-position: 0 0;
                }
                to{
                    background-position: -528px 0;
                }
            }

@keyframs full{
    0%{
        
    }
    30%{
        
    }
    50%{
        
    }
    100%{
        
    }
}
```

搜索sprite animation 可以找到很多用于动画的雪碧图

##### 变形和平移

##### 利用平移水平居中

```css
div.box3{
          background-color: orange;
          position: absolute;
          left:50%;
          transform: translateX(-50%);
      }

```

脱离文档流以后，div不再是块元素。在没有确定高宽的情况下，没法用l0,r0,t0,b0 m:auto的方法设置居中。

```css
z轴平移 要先设置视距 延x轴旋转的近大远小也需要设置视距来体现
<style>
html{
    perspective: 800px
}
		
</stylr>
```

##### 旋转

```css
.box4{
          width: 300px;
          height: 300px;
          margin:200px auto;
          border: 1px solid red;
          background-image: url(../images/animation.jpg);
          background-size:content;
          transition: all 3s;
          backface-visibility: hidden;

      }
      .box4:hover{
          /* transform:translateX(50%); */
            transform: translateY(50%)  rotateX(90deg) 
      }
```

##### CSS变量设置

```css
<style>
            html{
                --color:#bfa;
            }
            .box1{
                width: 200px;
                height: 200px;
                background-color:var(--color)
            }
</style>
```

##### LESS

变量重名时,优先使用最近的

可以声明前就用

```css
@import "test.less";// 模块化 分别开发 变量 变形 等

body{
    width: 1000px;
    height: 1000px;
}
// 声明变量
@a:220px;
@b:#bfa;
@c:box3;
// 变量选择
.box5{
    width: @a;
    background-color: @b;

}
// 类选择
.@{c}{
    width: @a;
    //属性选择
    height: $width;
}

.box1{

    .box2{
        color:red;
    }
    >.box3{
        color:red;
    }
    // &表示外侧的父元素
    &:hover{
        color:green;
    }
    &{width: 100px;}
}
// 继承
.p1{
width: 100px;
height: 100px;

}
.p2:extend(.p1){
    color:red;
}
// mixin 
.box2{
    color:red;
}
.box1{
    .box2()//注意与嵌套的区别是括号
}
// 可以直接创建一个mixin类 类名后加括号
.box3(){
    color: #000;
}
.box-bc(){
    background-color: #fff;
}
.box5{
    .box2();
    .box-bc;
    .box3
}
// 继承与mixin的区别是继承生成的css,各类之间是逗号,mixin则是分开的类

// 混合函数 mixin function 
.wFunction(@w,@h){
    width: @w;
    height: @h;
}

.box6{
    .wFunction(200px,300px)
}
// 自带函数
.box7{
    color: average(red,black);
    background-color:darken(#bfa,20%)
}
.box8{
    height: 200px+200px;
    width: 200px-20px;
}
```

##### flex 弹性盒子 

```css
 <style>
            *{
                padding:0;
                margin:0;
                list-style: none;
            }
            /* 弹性盒子 */
            ul{
                width: 500px;
                border: 3px solid red;
                display: flex;
                /* 弹性元素排列方式 默认为row */
                flex-direction:row; 
            }
            /* ?弹性盒子的直接子元素是弹性元素 */
            li{
                width: 200px;
                height: 50px;
                float: left;
            }
            li:nth-child(1){
                background-color: #bfa;
                /* 元素的大小 覆盖width 一般auto 不指定 */
                flex-basis: 100px;
                /* 元素伸长属性 拉长的大小 根据值的大小按比例分配 */
                flex-grow: 2;
                /* 元素收缩属性 收缩的大小  根据值的大小按比例分配*/
                flex-shrink: 3;
                /* order 顺序*/
                order:1;
            }
            li:nth-child(2){
                background-color: orange;
                flex-grow: 3;
            }
        </style>
    </head>
    <body>
        <ul>
            <li>1</li>
            <li>2</li>
            <li>3</li>
        </ul>
        
        <script src="" async defer></script>
    </body>
```

##### 弹性盒属性

```css
<style>
        * {
            padding: 0;
            margin: 0;
            list-style: none;
        }

        /* 弹性盒子 */
        ul {
            width: 800px;
            height: 500px;
            border: 3px solid red;
            display: flex;
            /* 自动换行 */
            flex-wrap: wrap;
            /* 如何排列 */
            /* justify-content:center; */
            /* justify-content:space-evenly; */
            /* justify-content:flex-end; */
            /* 辅轴纵向排列 */
            align-items: flex-end;

            /* 居中 */
            justify-content:center;
            align-items:center;
            
        }

        /* ?弹性盒子的直接子元素是弹性元素 */
        li {
            width: 200px;
            line-height: 50px;
            /* height: 100px; */
            /* flex-shrink: 0; */
        }

        li:nth-child(1) {
            background-color: #bfa;
        }

        li:nth-child(2) {
            background-color: orange;
        }

        li:nth-child(3) {
            background-color: rgb(113, 113, 255);
        }
        li:nth-child(4) {
            background-color: rgb(113, 113, 255);
        }
        li:nth-child(5) {
            background-color: rgb(113, 113, 255);
        }
    </style>
```

##### vw (viewport width)单位

Iphone6的实际屏幕尺寸 为375像素, 所以一般设计图的大小都是这个宽度的倍数. 倍数越大, 缩放到手机上越清晰.

视口总大小是100vw, 如果设计图宽度为750, 其中按钮宽度为150px, 那么在css文件中, 宽度为 150/750 * 100 = 20vw

```css
<style>
            *{
                margin:0;
                padding: 0;
            }
            /* 利用全局字体大小来适配 */
            /* 设计图750px 一共100vw/
            /* 设计图按钮宽度50px 转换为vw为 50/750 *100 */
            /* 100/750 = 0.1333333vw=1px 在知道其他元素宽度后成 这个数会不方便 每次都得输入算一遍 */
            /* 解决办法为设置全局字体大小 */
            /* 但 浏览器最小字体是12px 所以需要用倍数来解决 比如100倍 0.133333*100 = 13.3333vw*/
            /* 1 rem = 13.3333vw = 100px */
            /* 设计图中50px 对应 50/100 = 0.5 rem */
            html{
                font-size: 13.3333vw;

            }
            .box1{
                width: 0.5rem; 
            }
        </style>
```

##### 响应式布局

```css
<style>
@media (max-width:500px){ 
    body{
        background-color:#bfa;
    }
}
</style>
/*
中间可用 , 连接是或 and连接是同时满足
小于768 超小屏幕 max-width:768px; 
大于768 小屏幕   min-width:768px;
大于992 中屏幕   min-width:992px;
大于1200 大屏幕 	min-width:1200px;
*/
```



