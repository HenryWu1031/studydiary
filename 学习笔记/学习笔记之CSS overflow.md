<h1>学习笔记

<h2>CSS中的overflow属性</h2>

<div>今天在写前端代码的时候偶然发现了一个平时没有注意过的CSS属性</div>

<div>这个属性叫overflow，初一看发现就是stackoverflow的overflow</div>

![QQ截图20201219002242](C:\Users\why19991031\Pictures\QQ截图20201219002242.png)

我们可以看到为什么会发现这个问题，是因为我在写前端代码的时候遇到了一个棘手的问题，我们看到这个页面应该是由左边的div和右边的div组成，但是我们发现右边的div盖住了左边的div，那么我们先使用float属性，把左右div都float:left看看情况如何：

```CSS
div.leftImage{
    width: 100px;
    float: left;
}
div.rightInfo{
    padding: 0px 20px;
    background-color: #2b542c;
    /*overflow: hidden;*/
    float: left;
}
```

这是我的代码，我先把overflow的效果给拿掉了，发现结果如下：

![QQ截图20201219002746](C:\Users\why19991031\Pictures\QQ截图20201219002746.png)

我们发现我们的要求被满足了，那我们尝试使用overflow属性看看会发生什么

代码如下：

```CSS
div.leftImage{
    width: 100px;
    float: left;
}
div.rightInfo{
    padding: 0px 20px;
    background-color: #2b542c;
    overflow: hidden;
    /*float: left;*/
}
```

![QQ截图20201219002910](C:\Users\why19991031\Pictures\QQ截图20201219002910.png)

我们发现都可以满足要求只不过在使用float属性的时候我们的div的宽度自动缩小了，而使用overflow:hidden我们只是简单的完成了左右的分离。

然后我去网上搜索了下overflow属性的使用方法，发现好像本意overflow的意思是如果内容超过了div的高度或者宽度，使用overflow可以取舍是把多余部分截掉还是出现一个卷轴进行查看，那为什么能够满足我需要的效果？可能是overflow属性认为那些部分就是超出div所在的部分，所以就把用左边的div对右边的div进行了切分。当然具体原因笔者也不是非常清楚，希望有知道的朋友们能够赐教。

最后希望大家都能够变强，成为一名优秀的程序员【doge】