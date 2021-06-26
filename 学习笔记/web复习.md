# web复习

## ch00WEB应用开发课程介绍

没有什么知识点233

## ch01WEB技术概述

#### WWW概述

- WWW也称为万维网，万维网只是一基于超文本相互链接而成的全球性系统，且是因特网所能提供的服务其中之一

- 万维网并不等同因特网（Internet），只是因特网的一个子集

#### 理解Web

- Web是Internet提供的一种服务
- Web是一个巨大的信息宝库
- Web上的信息彼此关联
- Web上的信息被保存在Web站点中
- Web简单易用

#### web的技术基础

- 统一资源定位技术（URL）
- 超文本传送协议（HTTP）
- 超文本标记语言（HTML）
- 浏览器（Browser）
- Web服务器

#### 客户端和服务器的概念

- 客户端
  - 是指用来与数据提供者（服务器）通信的软件和硬件。客户端和服务器相连，发送和接受信息。

- 服务器
  - 一般是指能向许多客户端同时提供数据的大型计算机，能响应客户端请求
  - 服务器一词既可以指实际的计算机，也可以指一套软件。

- 客户端和服务器可以在同一台电脑上，但它们通常是在由网络相连的不同电脑上

#### Web浏览器

- Web浏览器是客户端程序，它向服务器端发出请求，并用来解释Web页面并完成相应转换和显示
  - 解释HTML文档
  - 运行并显示Java、ActiveX以及脚本语言等编程语言创建的应用、程序、动画等；

#### Web服务器

- Web服务器又称WWW服务器、网站服务器、站点服务器，就是将本地的信息用超文本组织，为用户在Internet上搜索和浏览信息提供服务

- 从本质上来说Web服务器实际上就是一个软件系统
  - 一台计算机可以充当多个Web服务器
  - 为提高用户的访问效率，一般情况下一台计算机只充当一个Web服务器；为提供大量用户的访问，多台计算机可以形成集群，只提供一个Web服务

#### HTTP协议

- 它不仅保证计算机正确快速地传输超文本文档，还确定传输文档中的哪一部分，以及哪部分内容首先显示（如文本先于图形）等
- 它是建立在TCP/IP协议基础上地应用层协议，采用URL定位WWW服务器的资源，并获取它

#### URL——统一资源定位器

- URL的构成
  - <协议><主机【端口号】><路径><文件名>

- 例子：http://www.yahoo.com.cn/index.htm
  - http指的是采用的传输协议是http
  - www.yahoo.com.cn为主机名
  - index.htm为文件名

- 通过不同的协议来访问因特网上的不同资源
  - FTP、SMTP、POP等

#### Web工作模式之HTTP协议

- 建议链接
- 发送请求
- 发送响应
- 关闭连接

![image-20210104173934809](C:\Users\why19991031\AppData\Roaming\Typora\typora-user-images\image-20210104173934809.png)

#### HTTP的特点

- 以Client/Server模型为基础。
- 简易性。
  - 客户机要连接到服务器，只需发送请求方式和URL路径等少量信息

- 灵活性
  - HTTP允许任意类型数据的传送。内容-类型标识指示了所传输数据的类型

- 无状态性
  - 每次连接只限处理一个请求。客户要建立连接需先发出请求，收到响应，然后断开连接
  - 这既是优点也是缺点。一方面，由于缺少状态使得HTTP累赘少，系统运行效率高；另一方面，缺少状态意味着所需的前面信息必须重现，导致每次连接需要传送较多的信息

![image-20210104174435804](C:\Users\why19991031\AppData\Roaming\Typora\typora-user-images\image-20210104174435804.png)

### 1.3Web应用开发的需求与方法

- #### 静态页面

- #### 动态页面

  - 需要服务器实时生成，服务器负荷重

- #### 活动页面

  - 在传统HTML静态页面上加入脚本、插件等
  - 一部分工作在客户端进行

#### 应用程序发展的需求

- 三层结构
  - 表示层、功能层和数据层
  - 瘦客户机/胖服务器
  - 更灵活，更好的弹性

- 基于Web的B/S模式
  - 静态模式
  - 多层动态模式
    - 增加了应用服务器
    - 使用分布式组件COM(+),CORBA
  - 一般动态模式
    - 增加数据库服务器
    - ASP.net、PHP等服务器脚本

#### 脚本描述语言定义

- 所谓脚本描述语言就是可以和HTML语言混在一起使用的语言，可以用来在浏览器的客户端控制浏览器等对象操作。最常用的脚本描述语言是JavaScript和VBScript等。

## ch03 HTML教程

#### <!DOCTYPE>声明

- 帮助浏览器正确地显示网页
- \<!DOCTYPE>不是HTML标签。它为浏览器提供一项信息（声明），即HTML是用什么版本编写的
  </!doctype>

#### head元素

- \<head>元素出现在文档的开头部分。\<head>与\</head>之间的内容不会再浏览器的文档窗口显示，但是其间的元素有特殊重要的意义。

- \<title>元素定义HTML文档的标题

  \<title>与\</title>之间的内容将显示在浏览器窗口的标题栏

- \<meta>元素

  - \<meta name="keywords" content="study,computer">

    用来标记搜索引擎在搜索你的页面时所取出的关键词

  - \<meta name="author" content="wutao">

    用来标记文档的作者

  - \<meta http-equiv="Content-Type" content="text/html;charset=gb2312">

    用来标记你的页面的解码方式

    HTML5:\<meta charset="UTF-8">

  - \<meta http-equiv="refresh" content="5;URL=http://www.ecust.edu.cn">

    用来自动刷新页面

#### 超文本中的标签

\<>我们称这个为标签，是用来分割和标记文本的元素

- 单标签
  - 某些标记称为“单标签”，因为它只需单独使用就能完整地表达意思，这类标记地语法是：
  - <标签名称>
  - 最常用的单标签是
    - \<br  />它表示换行
    - \<hr  />表示画水平线

- 双标签
  - “双标签”由“始标签”和“尾标签”两部分构成，必须成对使用
  - 始标签告诉Web浏览器从此处开始执行该标记所表示的功能
  - 尾标签告诉Web浏览器在这里结束该功能
  - 语法是：<标签>内容</  标签>
  - “内容”部分就是要被这对标记施加作用的部分。例如，想突出对某段文字的显示：
  - \<EM>第一\</EM>

- 标签属性
  - 许多单标记和双标记的始标记内可以包含一些属性，其语法是：
  - <标签名字 属性1 属性2 属性3...>
  - 各属性之间无先后次序，属性也可省略（即取默认值）

#### HTML注意点

- 1、html文件扩展名为：htm或html
- 2、列宽不受限制，文件在文本中可以写成一行
- 3、标记用<>括起来，大小写作用相同\<A>与\<a>一样，除汉字以外其它必须用半角表示

- 4、注释语句组成：\<!--注释内容-->
- 5、HTML标记只能嵌套不能交叉

#### HTML字符实体

在HTML中，有些字符拥有特殊含义，比如小于号“<”定义为一个HTML标签的开始。假如想要浏览器显示这些字符的话，比如在HTML代码中插入字符实体

![image-20210104183003316](C:\Users\why19991031\AppData\Roaming\Typora\typora-user-images\image-20210104183003316.png)

- 名字相对于使用数字的优点是容易记忆，缺点是并非所有的浏览器都支持最新的实体名，但是几乎所有的浏览器都能很好地支持实体号

#### 文本设置

![image-20210104183139725](C:\Users\why19991031\AppData\Roaming\Typora\typora-user-images\image-20210104183139725.png)

- 了解即可，建议用CSS设置

#### HTML元素——图像

- \<IMG>标签，使用：
- \<IMG SRC="" ALT="">
- ![image-20210104183304194](C:\Users\why19991031\AppData\Roaming\Typora\typora-user-images\image-20210104183304194.png)

- SRC属性指明了所要链接地图象文件地址，这个图形文件可以在本地机器，也可以位于远端主机

- 地址的表示有相对和绝对之分
  - \<IMG SRC="images/ball.gif">
  - <IMG SRC=“http://www.suda.edu.cn/images/ball.gif">

#### HTML元素——声音

![image-20210104183616664](C:\Users\why19991031\AppData\Roaming\Typora\typora-user-images\image-20210104183616664.png)

- HTML5推荐使用
- \<audio controls>
  \<source src="horse.ogg" type="audio/ogg">
  \<source src="horse.mp3" type="audio/mpeg">
  您的浏览器不支持 audio 元素。
  \</audio>

#### HTML元素——视频

![image-20210104183743739](C:\Users\why19991031\AppData\Roaming\Typora\typora-user-images\image-20210104183743739.png)

- Html5 推荐使用

- \<video width="320" height="240" controls>
  \<source src="movie.mp4" type="video/mp4">
  \<source src="movie.ogg" type="video/ogg">
  您的浏览器不支持Video标签。
  \</video>

#### HTML元素——超链接

超文本中的链接是其最重要的特性之一，使用者可以从一个页面直接跳转到其他的页面、图像或者服务器

- 超级链接的类型
- 创建超链接的方法
- 创建锚点链接
- 创建E-mail链接
- 创建导航条
- 网页中的图像热点链接

##### 超级链接的类型

- 文本链接：用文本作为链接载体，简单实用
- 图像链接：用图像作为链接载体，可使网页美观、生动活泼，它既可以指向单项链接，也可以根据图像的不同区域建立多个连接

- 内部链接：同一网站之间的链接
  - 一般是不用绝对路径的，因为资源常常是放在网上供其他人浏览的，写成绝对路径比如说C盘的资源用户无法访问到
  - ./
  - ../
  - /\*\*/\*\*
- 外部链接：不同网站文档之间的链接
  - 一般指不同网站的文档之间的链接，这种链接地址需要用URL地址
- 锚点链接：同一网页或不同网页中指定位置的链接
- E-mail链接：发送电子邮件的链接

#### 段落标签

- 为了排列的整齐、清晰，文字段落之间，可以用\<p>\</p>标记进行文字简单布局

#### 表格

- 表格的caption标签
  - \<caption>我的标题\</caption>

#### 跨多行、多列的表元

- 要创建跨多行、多列的表元，只需在\<th>或\<td>中加入rowspan或colspan属性，这两个属性的值，表明了表元中要跨越的行或列的个数
- 跨多列的表元\<td colspan>
- 跨多行的表元\<td rowspan>

#### 无序号列表

- 无序号列表使用的一对标签是\<ul>\</ul>
- 每一个列表项前使用\<li>。其结构如下所示：
- ![image-20210104191455290](C:\Users\why19991031\AppData\Roaming\Typora\typora-user-images\image-20210104191455290.png)

#### 序号列表

- 把无序号列表的ul改成ol即可

#### 表单

- 表单定义的语法如下:
- ![image-20210104191656334](C:\Users\why19991031\AppData\Roaming\Typora\typora-user-images\image-20210104191656334.png)

- form标记的属性含义如下：
  - method——取值为post或get。二者的区别是：get方法将在浏览器的URL栏中显示所传递变量的值，而post方法则不显示；在服务器端的数据提取方式也不同
  - action——指出用户所提交的数据将由哪个服务器的哪个程序处理。可处理用户提交的数据的服务器程序种类较多，如ASP脚本程序、ASPX程序、PHP程序等

## ch04 层叠样式表

### CSS基本语法

- CSS的定义是由三个部分构成：选择符、属性和属性的取值，定义方法如下:
- ![image-20210105111502670](C:\Users\why19991031\AppData\Roaming\Typora\typora-user-images\image-20210105111502670.png)

- 注释
  - 可以在CSS中插入注释来说明代码的含义，注释有利于自己或别人今后在编辑和更改代码时理解代码的含义
  - 在浏览器中，注释是不显示的
  - 注意与HTML中的注释方式的区别，此处只能以“/\*”开头，以“\*/”结尾

![image-20210105111906995](C:\Users\why19991031\AppData\Roaming\Typora\typora-user-images\image-20210105111906995.png)

### 样式的分类一

根据样式代码的位置，分为三类

- 行内样式

  ![image-20210105112958222](C:\Users\why19991031\AppData\Roaming\Typora\typora-user-images\image-20210105112958222.png)

- 内嵌样式

  ![image-20210105113014596](C:\Users\why19991031\AppData\Roaming\Typora\typora-user-images\image-20210105113014596.png)

- 外部样式

  - 链接外部样式表
    - 语法为
    - ![image-20210105113210406](C:\Users\why19991031\AppData\Roaming\Typora\typora-user-images\image-20210105113210406.png)
  - 导入外部样式表
    - 语法为
    - ![image-20210105113228751](C:\Users\why19991031\AppData\Roaming\Typora\typora-user-images\image-20210105113228751.png)

#### 样式的混合使用

![image-20210105113307697](C:\Users\why19991031\AppData\Roaming\Typora\typora-user-images\image-20210105113307697.png)

- 如果有多种样式，如果规定的样式没有冲突，则叠加；
- 如果有冲突，则最先考虑行内样式表显示，如果没有，再考虑内嵌样式显示，如果还没有，最后采用外面样式表显示，否则就按HTML的默认样式显示

### 样式的分类二

- HTML选择器

  p、h1

- 类（CLASS）选择器

  .class1

- ID选择器

  #name1

- 复合选择器

  - 交集选择器
    - p.special{}
  - 后代选择器
    - td p{}
  - 并集选择器
    - h1,h2,h3,h4,h5,h6{}

- 特殊的伪类选择器

  - a:link
  - a:visited
  - a:hover

- 伪对象

#### 没有定义CSS规则的HTML元素从它的父元素中继承样式！

#### 样式的优先级

- 行内联样式中所定义的样式优先级最高
- 按其在HTML文件中出现或被引用的顺序，越在后出现，优先级越高

- 选择符的作用顺序由高到低为:id选择符，类选择符。
- 未在任何文件中定义的样式，将遵循浏览器的默认样式

#### 常用CSS属性

- CSS背景属性

  ![image-20210105132832032](C:\Users\why19991031\AppData\Roaming\Typora\typora-user-images\image-20210105132832032.png)

- CSS边框属性

  ![image-20210105132904691](C:\Users\why19991031\AppData\Roaming\Typora\typora-user-images\image-20210105132904691.png)

  ![image-20210105132924166](C:\Users\why19991031\AppData\Roaming\Typora\typora-user-images\image-20210105132924166.png)

- CSS文本、字体属性

  ![image-20210105132950153](C:\Users\why19991031\AppData\Roaming\Typora\typora-user-images\image-20210105132950153.png)

- CSS外边距、内边距属性

  ![image-20210105133507094](C:\Users\why19991031\AppData\Roaming\Typora\typora-user-images\image-20210105133507094.png)

- CSS列表属性

  ![image-20210105133610604](C:\Users\why19991031\AppData\Roaming\Typora\typora-user-images\image-20210105133610604.png)

#### 首字下沉

\<span style=“font-size:2em;float:left;”>

#### CSS布局

#### CSS+DIV

- DIV是什么
- 布局涉及到的常用属性
  - 尺寸
  - 边框
  - 浮动和position定位
  - 内边距和外边距

#### 盒模型示意图

![image-20210105134320740](C:\Users\why19991031\AppData\Roaming\Typora\typora-user-images\image-20210105134320740.png)

#### 盒子模型

![image-20210105134500432](C:\Users\why19991031\AppData\Roaming\Typora\typora-user-images\image-20210105134500432.png)

![image-20210105134507937](C:\Users\why19991031\AppData\Roaming\Typora\typora-user-images\image-20210105134507937.png)

#### 有关CSS盒子设定边框属性的简写

![image-20210105134607078](C:\Users\why19991031\AppData\Roaming\Typora\typora-user-images\image-20210105134607078.png)

#### position定位

- Static：文档流正常位置
- Relative
  - 原来位置的区域保留
  - 配合left、top时，相对于原来的位置起作用

- Absolute
  - 不占流位置，即原来区域空出
  - 有z-index属性
  - 配合left、top时

- position配合left和top可以实现浮动效果

## ch05 javascript语言

### JavaScript简介

- 基于对象和事件驱动，并具有较高安全性能的脚本语言，特点如下：
  - 一种脚本语言
  - 基于对象的语言
  - 简单性
  - 安全性
  - 动态性
  - 跨平台性

- 使用JavaScript
  - 可直接将代码加入网页
  - JavaScript可出现在网页中的任意位置，但必须使用标记\<script>\</script>
  - “\<!--”和“//-->”的作用，
    是让不能解析\<script>标签的浏
    览器忽略JavaScript代码
  - 第四行前边的双反斜杠“//”是JavaScript里的注释标号

- 一个简单的JavaScript实例

  ![image-20210105135926668](C:\Users\why19991031\AppData\Roaming\Typora\typora-user-images\image-20210105135926668.png)

#### JavaScript是基于对象编程的

- 编程所设计的成分划分成大大小小的对象，对象下面还可继续划分为更小的对象直至不能进一步划分为止
- 对象是属性和方法的集合
- 获得对象的方式
  - 由浏览器环境所提供的对象
  - 引用JavaScript的内部对象
  - 自行创建的对象

#### JavaScript的数据类型：

![image-20210105140132144](C:\Users\why19991031\AppData\Roaming\Typora\typora-user-images\image-20210105140132144.png)

- JavaScript的变量名称符合：只包含字母、数字或下划线；必须以字母开头；不能太长；不能与JavaScript保留字重复
- 变量是区分大小写的
- 变量名及函数名一般用小写，多个单词中除首单词外其余单词首字母大写

- 声明变量的方式：![image-20210105140345911](C:\Users\why19991031\AppData\Roaming\Typora\typora-user-images\image-20210105140345911.png)

#### 基本语法

- 注释语句

- 条件语句

  - if语句

  - switch语句

    - 例子

    - ```javascript
      <script language="javascript">
      var grade;
      var scorestr=prompt("please input a score",90);
      var score=parseInt(scorestr)/10;
      switch(score){
      case 10:
      case 9: grade=“A”; break;
      case 8:
      case 7: grade=“B”;break;
      case 6: grade=“C";break;
      default: grade=“D”;
      }
      alert(scorestr+" is grade “+grade);
      </script>
      ```

      

- 循环语句

  - for语句
  - while语句
  - do-while语句
  - break和continue

if语句举例

```javascript
<script language="javascript">
var numstr=prompt("please input an integer",12);
var num=parseInt(numstr);
if (num%2==0)
alert(numstr+" is an even number");
else
alert(numstr+" is an odd number");
</script>
```

### JavaScript基本语法——函数

#### 内置函数

- parseInt()和parseFloat()函数

- eval函数：用于计算字符串表达式的值
- isNaN函数：用户验证参数是否为NaN(非数字)

#### 变量的作用域

- 全局变量
  - 在任何函数外声明的都属于全局变量

- 局部变量
  - 属于某个函数或者语句块，局部变量优先

### JavaScript的使用

- JavaScript在网站开发中具有以下作用：
- HTML输出
- 对事件做出反应
- 验证用户输入

```javascript
<input id="demo" type="text">
<script>
function myFunction()
{
var x=document.getElementById("demo").value;
if(x==""||isNaN(x))
alert("Not Numeric");
}
</script>
<button type="button" onclick="myFunction()">点击这里</button>
```

- 改变HTML内容

  - ```javascript
    function myFunction()
    {
    x=document.getElementById("demo"); // 找到元素
    x.innerHTML="Hello JavaScript!"; // 改变内容
    }
    ```

- 改变样式

  - ```javascript
    x=document.getElementById("demo") 
    x.style.color="#ff0000";
    ```

- 改变HTML元素属性

#### JavaScript-对象化编程

- 对象是属性和方法的组合
- 属性是对象所拥有的一组外观特征，一般为名词
- 方法是对象可以执行的功能，一般为动词

#### 对象化编程

- 对象属性的引用
  - 使用“.“、下标或字符串形式

- 对象方法的引用
- this关键词
- new运算符

#### JavaScript的内部对象

- 数字对象Number
- 字符串对象String
  - 创建字符串有两种不同方法：
    - 使用var语句
      - var newstr=”这是我的字符串“
    - 创建String对象
      - var newstr=new String（”这是我的字符串“）
  - 属性：length
  - 方法:
    - charAt
    - indexOf
    - substr
    - toLowerCase
    - Eval
- 数组对象Array
- 算术对象Math
  - ![image-20210105143650743](C:\Users\why19991031\AppData\Roaming\Typora\typora-user-images\image-20210105143650743.png)
- 日期对象Date

### JavaScript事件处理程序

![image-20210105144025390](C:\Users\why19991031\AppData\Roaming\Typora\typora-user-images\image-20210105144025390.png)

#### JavaScript对象系统

![image-20210105144413354](C:\Users\why19991031\AppData\Roaming\Typora\typora-user-images\image-20210105144413354.png)

## ch06 jsp基本语法和内置对象

### 4.1 JSP基本语法

#### JSP运行原理：

- 当Web服务器上的一个JSP页面第一次被请求时，服务器JSP引擎首先将JSP页面转换为Java源文件（即Servlet），然后将其编译为字节码（.class)文件，再执行字节码文件返回结果

- 当改页面被再次请求时，JSP引擎只需加载并执行已编译的字节码即可，因此JSP页面访问更高效

#### 4.1.3 JSP脚本标识

##### JSP声明

- JSP声明在页面中使用的变量和方法。语法格式如下：
- \<%！Java声明 %>

##### JSP表达式

- JSP表达式的值被转换为字符串直接输出到页面
- 其语法格式为：
- \<% = 表达式 %>其中表达式必须为合法的Java表达式

- 例如：
  - <% = sum(100) %> //调用sum方法
  - <% = 100*2+10 %>

##### JSP程序段

- JSP程序段是JSP页面中嵌入的Java代码或脚本代码，可包含变量、表达式和流程控制语句等。

- 通过程序段可处理请求与响应、向页面输出内容、访问session会话等。
-  语法格式为：<% 程序段 %>
- 程序段的使用比较灵活，主要包括：声明变量、显示表达式、使用JSP内置对象或JavaBean对象实现应用逻辑等。
- JSP页面可以包含多个程序段，这些程序段将被JSP引
  擎按顺序执行

### 4.2 JSP内置对象

#### 4.2.1 request对象

- request对象封装了客户端的请求信息，包括头信息、系统信息、请求方式及请求参数等。

![image-20210105151330696](C:\Users\why19991031\AppData\Roaming\Typora\typora-user-images\image-20210105151330696.png)

#### 4.2.2 response对象

#### 4.2.3 session对象

#### 4.2.4 application对象

#### 4.2.5 其他对象

- page对象
- pageContext对象
- config对象
- exception对象

### 4.3 JSP动作标识

- jsp:include
- jsp:forward
- jsp:param
- jsp:useBean
- jsp:setProperty
- jsp:getProperty
- jsp:plugin

可能会用上的代码：

