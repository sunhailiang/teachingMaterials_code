
# jquery基础

## 1 为什么要学习jquery?
 **先来看一个案例(点击元素展示隐藏)**
```css
<style>
        div {
            height: 100px;
            background-color: orangered;
            list-style: none;
            margin-top: 10px;
        }
 </style>
```
``` html
 <button>展开</button>
 <button>收起</button>
 <div></div>
 <div></div>
 <div></div>
```
``` javascript
 <script>
        // 1、获取元素的方法很长，写起来费劲
        var show = document.getElementsByTagName('button')[0]
        var hide = document.getElementsByTagName('button')[1]
        var divs = document.getElementsByTagName('div')
        // 点击展开
        show.onclick = function () {
            //2、手动循环
            for (var i = 0; i < divs.length; i++) {
                divs[i].style.display = 'block'
            }
        }
        // 点击隐藏
        hide.onclick = function () {
            for (var i = 0; i < divs.length; i++) {
                divs[i].style.display = 'none'
            }
        }
        //3、假设我想给元素展示加一个展开的动画呢？再复杂一点的动画呢？
    </script>
```

## 2 体验jquery
``` css
    <style>
        div {
            height: 100px;
            background-color: orangered;
            margin-top: 10px;
        }
    </style>
```
``` html
    <button>展开</button>
    <button>收起</button>
     <div></div>
     <div></div>
     <div></div>
```
``` javascript
    <script src="jquery-1.12.4.min.js"></script>
    <script>
        $(function () {
            $('button:last').click(function () {
               $('div').hide(1000)
            })
            $('button:first').click(function () {
                $('div').show(1000)
            })
        })
        // 相对于js
        // 1、div并没有for循环，jquery内部做了
        // 2、不需要写 document.getElementById 等等复杂写法了
    </script>
```
## 3 学习使用jquery的好处
   1、不需要考虑浏览器的兼容性问题
   2、jquery隐式迭代特性不需要再写繁琐的for循环
   3、获取元素的方式简单多样，不需要原生js那么繁琐
   4、提供一些列动画相关的函数,直接使用，简洁高效

## 4 jquery是什么？
1. 官方网址：[jQuery官方网站](http://jquery.com/)
2. 一个快速、小巧、功能丰富的JavaScript库
## 5 jquery的特点是什么？
1. **特点**：
快速：jquery内部实现很多功能丰富的函数，我们只需要直接调用-开发快，而且多次迭代使得jquery的代码性能方面处理的相对优越-速度快
小巧：1.x 95kb  2.x 84kb  3.x 85kb
功能丰富: 内部api丰富
通用：跨平台，支持所有的主流浏览器
扩展好：各种jquery插件的存在都是给予jquery扩展出来的。如：[jquer插件库](http://www.jq22.com/)
2. **它使HTML文档遍历和操作、事件处理、动画和Ajax等操作变得更加简单，因为它提供了一个易于使用的API，可以跨多种浏览器工作。**
3. jquery的版本信息
   1. 1.x 兼容IE678(jquery最受欢迎的特色：处理浏览器的兼容性)
   2. 2.x 不兼容IE678
   3. 3.x 不兼容IE678
   4. 如今还在使用jquery绝大部分还在用1.x的版本
## 6 jquery的使用步骤
1. jquery引入
` <script src="jquery-1.12.4.min.js"></script>`
2. 入口函数
```javascript
   $(function(){

   })
```
3. 功能实现
``` javascript
   $(function(){
   
     // 功能代码

   })
```
## 7 jquery入口函数
1. 写法一
```javascript
$(document).ready(function(){//直观解析(document)文档(此处文档指页面元素)加载完成(ready)执行函数
   // 功能代码
})
```
2. 写法二(简写)
```javascript
$(function(){
   // 功能代码
})
```
3. 入口函数的好处
   1. 文档加载完成执行函数，确保能够获取到元素
   2. 形成了一个沙箱，避免了全局变量的污染

4. 相比js的入口函数有何不同？
   1. JavaScript的入口函数要等到页面中所有资源（包括图片、文件）加载完成才开始执行。
   2. jQuery的入口函数只会等待文档树加载完成就开始执行，并不会等待图片、文件的加载。
   3. jquery入口函数可以多次调用且不会覆盖，onload只能执行一次

# 8 jquery对象和dom对象
 ## 基本概念
1. 使用js方法获取页面的元素返回的对象就是dom对象
2. 使用jquery方法获取页面元素的返回的对象就是jquery对象
3. 两者联系：jquery对象内部是一个伪数组，内部存放就是dom对象

## jquery对象和js对象的区别
   jquery对象不能直接使用dom的方法，dom对象也不能使用jquery对象的方法

## dom对象转换成jquery对象
   DomObj+$()=>$(DomObj)  // 只需要用$()包住dom对象即可

## jquery对象转dom对象
   1. 方法一：`$('li').get(1)`
   2. 方法二：`$('li')[1]`
   3. 解析：jquery对象是dom对象的合集，是一个伪数组，我们只需要从伪数组中取出dom即可

## 隔行变色demo -(jquery对象->dom对象)
```html
 <ul>
        <li>1</li>
        <li>2</li>
        <li>3</li>
        <li>4</li>
        <li>5</li>
        <li>6</li>
        <li>7</li>
        <li>8</li>
    </ul>
```
```javascript
  <script src="jquery-1.12.4.min.js"></script>
    <script>
        // jquery对象
        var $li = $('li')
        for (var i = 0; i < $li.length; i++) {
            if (i % 2 == 0) {
                //$li[i] dom对象 
                $li[i].style.backgroundColor='red'
            }else{
                $li[i].style.backgroundColor='green'
            }
        }
    </script>
```

##  开关灯案例-(jquery对象->dom对象)
```html
    <button>开灯</button>
    <button>关灯</button>
```
```javascript
    <script src="jquery-1.12.4.min.js"></script>
    <script>
      var $btn=$('button')
      // 直接通过下表取出dom
      $btn[0].onclick=function(){
          $('body')[0].style.backgroundColor="white"
      }
      $btn[1].onclick=function(){
          $('body')[0].style.backgroundColor="black"
      }
    </script>
```
# 1.9 jquery选择器
## 1. 什么是jquery选择器？
   1. jquery为我们提供的一组方法，目的是让我们更加方便的获取到页面的元素
   2. jquery兼容了几乎所有的css的选择器，也添加了更多复杂的选择器
   3. jquery的选择器很多，所以获取一个元素的方式就不止一种，所以我们常用的选择器并不多
## 2.  回顾一下css的选择器
> jQuery完全兼容css选择器

| 名称    | 用法                 | 描述                              |
| ----- | ------------------ | :------------------------------ |
| ID选择器 | $(“#id”);          | 获取指定ID的元素                       |
| 类选择器  | $(“.class”);       | 获取同一类class的元素                   |
| 标签选择器 | $(“div”);          | 获取同一类标签的所有元素                    |
| 并集选择器 | $(“div,p,li”);     | 使用逗号分隔，只要符合条件之一就可。              |
| 交集选择器 | $(“div.redClass”); | 获取class为redClass的div元素          |
| 子代选择器 | $(“ul>li”);        | 使用>号，获取儿子层级的元素，注意，并不会获取孙子层级的元素  |
| 后代选择器 | $(“ul li”);        | 使用空格，代表后代选择器，获取ul下的所有li元素，包括孙子等 |

> 跟CSS的选择器一模一样。

## 3. 过滤选择器
> **注意**这类选择器都带 **冒号:**

| 名称         | 用法                                 | 描述                                 |
| ---------- | ---------------------------------- | :--------------------------------- |
| :eq（index） | $(“li:eq(2)”).css(“color”, ”red”); | 获取到的li元素中，选择索引号为2的元素，索引号index从0开始。 |
| :odd       | $(“li:odd”).css(“color”, ”red”);   | 获取到的li元素中，选择索引号为奇数的元素              |
| :even      | $(“li:even”).css(“color”, ”red”);  | 获取到的li元素中，选择索引号为偶数的元素              |
| :first     | $(“li:first”).css(“color”, ”red”); | 获取到的li元素中的第一个                      |
| :last      | $(“li:last”).css(“color”, ”red”);  | 获取到的li元素中的最后一个                     |
##  4. 筛选选择器(jquery方法)
> 筛选选择器的功能与过滤选择器有点类似，但是用法不一样，`筛选选择器`主要是方法。

| 名称                 | 用法                          | 描述                           |
| ------------------ | --------------------------- | :--------------------------- |
| children(selector) | $(“ul”).children(“li”)      | 获取当前元素的所有子元素中的li元素           |
| find(selector)     | $(“ul”).find(“li”);         | 获取当前元素中的后代元素中的li元素           |
| siblings(selector) | $(“#first”).siblings(“li”); | 查找兄弟节点，不包括自己本身。              |
| parent()           | $(“#first”).parent();       | 查找父亲                         |
| eq(index)          | $(“li”).eq(2);              | 相当于`$(“li:eq(2)”)`,index从0开始 |
| next()             | $(“li”).next()              | 找下一个兄弟                       |
| prev()             | $(“li”).prev()              | 找上一次兄弟                     |

## 5. 下拉菜单案例

[children()查找子元素 children(selector)查找指定子元素mouseover鼠标经过事mouseout:鼠标离开事件mouseenter:鼠标进入事件mouseleave：鼠标离开事件](https://github.com/sunhailiang/teachingMaterials_code/tree/master/jquery/day-01/code/06-%E4%B8%8B%E6%8B%89%E8%8F%9C%E5%8D%95)

## 6. 突出展示案例

[find(selector)找到指定元素，siblings()找到所有兄弟元素](https://github.com/sunhailiang/teachingMaterials_code/tree/master/jquery/day-01/code/07-%E7%AA%81%E5%87%BA%E5%B1%95%E7%A4%BA)

## 7. 手风琴案例

```css
  <style type="text/css">
        * {
            padding: 0;
            margin: 0;
        }

        ul {
            list-style-type: none;
        }

        .parentWrap {
            width: 200px;
            text-align: center;

        }

        .menuGroup {
            border: 1px solid #999;
            background-color: #e0ecff;
        }

        .groupTitle {
            display: block;
            height: 20px;
            line-height: 20px;
            font-size: 16px;
            border-bottom: 1px solid #ccc;
            cursor: pointer;
        }

        .menuGroup>div {
            height: 200px;
            background-color: #fff;
            display: none;
        }
    </style>
```
```html
 <ul class="parentWrap">
        <li class="menuGroup">
            <span class="groupTitle">标题1</span>
            <div>我是弹出来的div1</div>
        </li>
        <li class="menuGroup">
            <span class="groupTitle">标题2</span>
            <div>我是弹出来的div2</div>
        </li>
        <li class="menuGroup">
            <span class="groupTitle">标题3</span>
            <div>我是弹出来的div3</div>
        </li>
        <li class="menuGroup">
            <span class="groupTitle">标题4</span>
            <div>我是弹出来的div4</div>
        </li>
    </ul>
```
```javascript
 <script>
        $(function () {
            // 点击span标题展示div 其他所有li下面的div全部关闭
            $('.groupTitle').click(function () {
                $(this).next().show().parent().siblings().find('div').hide()
            })
        });
 </script>
```

## 9. 淘宝精品案例
[.eq(index)根据下标获得指定jquery对象 .get(index)根据下标获得dom对象index()方法获得jquery对象的索引值](https://github.com/sunhailiang/teachingMaterials_code/tree/master/jquery/day-01/code/09-%E6%B7%98%E5%AE%9D%E7%B2%BE%E5%93%81)

2.0 jquery操作样式
1. style：行内样式
2. class：类样式（主要方式）
3. css()：采用的是行内
   1. 情况一： css(name,value)给元素添加一个样式，直接给样式名称和值
   2. 情况二： css({key:value,key2:value2}) 给元素添加多个样式，参数传入对象
   3. 情况三： css(name) 当只传入样式名的时候，返回该样式名称的值  
4. **注意**
   1. 隐式迭代：设置操作的时候，如果是多个元素，那么给所有的元素设置相同的值
   2. 获取操作的时候，如果是多个元素，那么只会返回第一个元素的值。
```css
    <style>
      div{
        width: 500px;
        height: 500px;
      }
    </style>
```
```html
 <div></div>
```
```javascript
   <script src="jquery-1.12.4.min.js"></script>
    <script>
      // 给元素添加单个样式
      $('div').css("backgroundColor",'red')
      // 给元素添加多个样式
      $('div').css({
        "backgroundColor":'red',
        'border':'2px solid black',
        "margin":'100px auto'
      })
      // 获取样式的值
      var sv=$('div').css('border')  //此处如果有多个div，只返回第一个元素的该样式的值
      console.log("样式的值",sv)
    </script>
```

#  jquery操作class
## 常用方法介绍
```css
  <style>
    .base {
      background-color: pink;
    }

    .fz {
      font-size: 50px;
    }

    .red {
      color: red;
    }
  </style>
```
```html
 <div>AAAAA</div>
 <div>BBBBB</div>
 <div>CCCCC</div>
```
1. addClass(name): 添加类名
```javascript
  $('div').addClass('base fz')
```
2. removeClass(name): 移除指定类 
```javascript
  $('div').removeClass('fz')  // 如果参数为空，就会移除掉该元素所有的类名
```
3. toggleClass(name): 切换类名
```javascript
  $('div').toggleClass('red') // 所谓切换，就是如果有该类名则删除，如果没有则添加
```
4. hasClass(name): 是否有某个类名
```javascript
  $('div').hasClass('red') // 返回true或者false，如果有多个元素只判断"第一个"
```
## 淘宝tab栏切换案例
[addClass()添加了名siblings()获取兄弟节点index()获取索引值removeClass()移除class](https://github.com/sunhailiang/teachingMaterials_code/tree/master/jquery/day-01/code/tab%E6%A0%8F%E5%88%87%E6%8D%A2)

# 3. jquery操作属性
## 常用方法
```html
 <img src="imgs/01.jpg" alt="">
 <img src="imgs/02.jpg" alt="">
```
1. attr() 设置属性
   1. 情况一： attr(name,value)  //设置单个属性
   `$('img').attr("title","这是图片")`
   2. 情况二:  attr({key:value,key2:value2})  // 设置多个属性
   `$('img').attr({ "title": "这是图片", 'alt': '哈哈' })`
   3. 情况三:  attr(name) // 获取属性的值
   `$('img').attr('title')`
2. removeAttr() 移除单个或者多个属性
```javascript
$('img').removeAttr('alt')  // 移除单个属性
$('img').removeAttr('alt title') // 移除多个属性中间用"空格隔开"
```
## 3. 美女相册案例
[点击获取案例](https://github.com/sunhailiang/teachingMaterials_code/tree/master/jquery/day-01/code/13-%E7%BE%8E%E5%A5%B3%E7%9B%B8%E5%86%8C)

# 4. 布尔类型的属性操作

## attr操作布尔属性的bug
```html
 <!-- 这段代码使用attr操作布尔类型的属性有Bug -->
<button>选中</button>
<button>不选中</button>
<input type="checkbox">
```
```javascript
       $('button:first').click(function () {
            $('input').attr('checked', true);
            console.log($('input').attr('checked'));
        });
        $('button:last').click(function () {
            $('input').attr('checked', false);
            console.log($('input').attr('checked'));  // undefined
        });
```
## prop()

**1.6版本以后凡是布尔类型属性如：checked disabled selected不在使用attr来操作，换成prop**
### prop()的 demo
```javascript
      $('button:first').click(function() {
        $('input').prop('checked', true);
        console.log($('input').prop('checked'));
      });

      $('button:last').click(function() {
        $('input').prop('checked', false);
        console.log($('input').prop('checked'));
      });
```
>功能正常

##  表格全选案例
```css
    <style>
        * {
            padding: 0;
            margin: 0;
        }

        .wrap {
            width: 300px;
            margin: 100px auto 0;
        }

        table {
            border-collapse: collapse;
            border-spacing: 0;
            border: 1px solid #c0c0c0;
            width: 300px;
        }

        th,
        td {
            border: 1px solid #d0d0d0;
            color: #404060;
            padding: 10px;
        }

        th {
            background-color: #09c;
            font: bold 16px "微软雅黑";
            color: #fff;
        }

        td {
            font: 14px "微软雅黑";
        }

        tbody tr {
            background-color: #f0f0f0;
            text-align: center;
        }

        tbody tr:hover {
            cursor: pointer;
            background-color: #fafafa;
        }
    </style>
```
```html
    <div class="wrap">
        <table>
            <thead>
                <tr>
                    <th>
                        <input type="checkbox" id="all" />
                    </th>
                    <th>菜名</th>
                    <th>饭店</th>
                </tr>
            </thead>
            <tbody id="tb">
                <tr>
                    <td>
                        <input type="checkbox" />
                    </td>
                    <td>红烧肉</td>
                    <td>田老师</td>
                </tr>
                <tr>
                    <td>
                        <input type="checkbox" />
                    </td>
                    <td>西红柿鸡蛋</td>
                    <td>田老师</td>
                </tr>
                <tr>
                    <td>
                        <input type="checkbox" />
                    </td>
                    <td>红烧狮子头</td>
                    <td>田老师</td>
                </tr>
                <tr>
                    <td>
                        <input type="checkbox" />
                    </td>
                    <td>日式肥牛</td>
                    <td>田老师</td>
                </tr>
            </tbody>
        </table>
    </div>
```
```javascript
<script src="jquery-1.12.4.min.js"></script>
    <script>
        $(function () {
            var $all = $('#all')
            var $input = $("#tb input")
            // 点击#all 则#tb input 属性selected全部变为true/否则全部变为false
            $all.click(function () {
                $input.prop("checked", $all.prop("checked"))
            })
            // 选择#tb input 所有的input的selected都是true的时候，#all被选中，否则取消选中
            $input.click(function () {
                if ($("#tb input:checked").length == $input.length) {
                    $all.prop("checked", true)
                } else {
                    $all.prop("checked", false)
                }
            })
        });
    </script>
```