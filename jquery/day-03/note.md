### jquery节点操作

#### 创建节点
1. `$()里面放html字符串`
2. `$('<button>看我是一个按钮</button>')`

#### 添加节点

##### append  给父级元素内部从后面追加子元素

```javascript
   // parent.append(child)
    $('div').append( $('<p>这是新建的p标签</p>') );
```
##### appendTo  子元素从最后往父级元素内追加元素

```javascript
    // child.appendTo(parent)
    $('<span>这是个span </span>').appendTo($('div'));
```
##### prepend  往父级元素的子元素的最前面追加元素
```javascript
    // parent.prepend(child)
    $('div').prepend($('<div>这是新建的最前边？标签</div>'));
```
##### prependTo  元素追加到父级元素的内部元素的最前面

```javascript
    // child.prependTo(parent)
    $('<p>这是一个P</p>').prependTo( $('div') );
```
##### before  追加到元素的前面(同级)

```javascript
    $('div').before('<p>前面一个P</p>') 
```
##### after   追加到元素后面(同级)

```javascript
    $('div').after('<p>后面一个P</p>')
```

##### 城市选择案例

```css
  <style>
    select {
      width: 200px;
      background-color: teal;
      font-size: 24px;
      height: 300px;
    }
  </style>
```

```html
  <select multiple id="src">
    <option>北京</option>
    <option>上海</option>
    <option>深圳</option>
    <option>杭州</option>
  </select>
  <button>></button>
  <button>>></button>
  <button><</button>
  <button><<</button>
  <select multiple id="tar"></select>
```

```javascript
 <script src="jquery-1.12.4.js"></script>
  <script>
    $(function(){
      $('button').eq(0).click(function(){
          $('#src > option:selected').appendTo($("#tar")).removeAttr('selected')
      })
      $('button').eq(1).click(function(){
        $('#src > option').appendTo("#tar")
        })
      $('button').eq(2).click(function(){
        $('#tar > option:selected').appendTo($("#src")).removeAttr('selected')
        })
      $('button').eq(3).click(function(){
        $('#tar > option').appendTo("#src")
       })
    });
  </script>
```

#### 删除和清空节点

##### remove() 
1. 删除自身，内部子元素一并删除
##### empty()
2. 清空内部所有元素，不包括自身

#### 克隆节点

##### clone()
1. 参数默认false
2. 参数false：克隆标签元素等
3. 参数true: 深度克隆 **包括事件**

##### 克隆节点 demo 　
```css
    <style>
    div{
        height: 400px;
        width: 400px;
        background-color: seagreen;
        margin-top: 10px
    }
    .child{
     height: 100px;
     width: 100px;
     background-color: rebeccapurple
    }
    </style>
```

```html
  <div id="test">
        <div class="child"></div>
    </div>
```

```javascript
    <script src="jquery-1.12.4.js"></script>
    <script>
     $('#test').click(function(){
         console.log('呵呵哒~');  
     })
     // 参数默认false，只克隆标签元素等等
     $('#test').clone().appendTo("body")
      // 参数true，克隆包括事件
     $('#test').clone(true).appendTo("body")
    </script>
```

#### 发布微博案例

```css
  <style>
    * {
      margin: 0;
      padding: 0;
    }

    ul {
      list-style: none;
    }

    .box {
      width: 600px;
      margin: 100px auto;
      border: 1px solid #000;
      padding: 20px;
    }

    textarea {
      width: 450px;
      height: 160px;
      outline: none;
      resize: none;
    }

    ul {
      width: 450px;
      padding-left: 80px;
    }

    ul li {
      line-height: 25px;
      border-bottom: 1px dashed #cccccc;
    }

    .fr {
      float: right;
    }
  </style>
```

```html
<div class="box" id="weibo">
  <span>微博发布</span>
  <textarea name="" id="txt" cols="30" rows="10"></textarea>
  <button id="btn">发布</button>
  <ul id="ul">

  </ul>
</div>
```

```javascript
<script src="jquery-1.12.4.js"></script>
<script>
  $(function(){
    // 1、点击发布创建一个li
    // 2、获取文本域内容给到li
    // 3、将li追加到ul中
    // 4、给li追加一个button
    // 5、点击button删除li
    $('#btn').click(function(){
        var txt=$("#txt").val().trim()
        $('#txt').val('')
        if(!txt){
            return
        }
        var $li=$('<li></li>')
        $li.text(txt)
        $($li).appendTo("#ul")
        var $btn=$("<button class='fr'>删除评论</button>")
        $btn.appendTo("li")
        $btn.click(function(){
            $(this).parent().remove()
        })
    })
  });
</script>
```
### jquery特殊属性操作

#### val()  设置和获取表单元素的值，如text，textarea等等

##### 搜索框体验 demo

```html
   <input type="text" value="哒哒哒~">
```

```javascript
  <script src="jquery-1.12.4.js"></script>
  <script>
    $('input').focus(function(){
        if($(this).val()==='哒哒哒~'){
            $(this).val('')
        }
    })
    $('input').blur(function(){
        if($(this).val()===''){
            $(this).val('哒哒哒~')
        }
    })
```

#### html()和text()

1. html() 相当于 innerHtml
2. text() 相当于 innerText

#### width()-height()-innerWidth()-outerWidth()-innerHeight()-outerHeight()
##### width() 

1. 无参数：获取元素width 
2. 有Number类型参数：设置width

##### innerWidth() 

1. 获取元素panding和width

##### oputerWidth() 

1. 无参数，参数默认是false时：获取元素pading和border和width
2. 参数是true时：获取元素pading和border和width和margin

##### height() 

1. 无参数：获取元素高度 
2. 有Number类型的参数:设置height

##### innerHeight() 

1. 获取元素padding和height

##### outerHeight() 

1. 无参数，默认参数是false时： 获取元素padding和border和height
2. 参数是true时：获取元素padding和border和height和margin

#### scrollTop()和scrollLeft()

1. scrollTop() 获取被卷曲的高度, 可设置卷曲高度
2. scrollLeft() 获取被卷曲的宽度，可设置卷曲高度

#### js相关的屏幕滚动

1. window.pageYOffset
2. window.pageXOffset  
3. 以屏幕左上角为基准获取卷曲宽高----只读
4. document.documentElement.scrollTop
5. document.documentElement.scrollLeft
6. 这两个属性可读可写
7. $(window) 不支持的动画,可用$('html')

#### 固定导航案例

[从这获取固定导航的代码](https://github.com/sunhailiang/teachingMaterials_code/tree/master/jquery/day-03/code/08-%E5%9B%BA%E5%AE%9A%E5%AF%BC%E8%88%AA)

#### 回到顶部案例

[从这获取回到顶部的代码](https://github.com/sunhailiang/teachingMaterials_code/tree/master/jquery/day-03/code/09-%E5%9B%9E%E5%88%B0%E9%A1%B6%E9%83%A8)

#### position()和offset()
1. offset方法和position方法都是用来获取盒子的位置的  left和top
2. offset方法获取的是盒子在整个body中的位置
3. position方法获取的盒子距离有定位的最近的父元素的位置 offsetLeft offsetTop
4. 都是返回一个对象

#### 弹幕案例

```css
  <style type="text/css">
    html,
    body {
      margin: 0px;
      padding: 0px;
      width: 100%;
      height: 100%;
      font-family: "微软雅黑";
      font-size: 62.5%;
    }

    .boxDom {
      width: 100%;
      height: 100%;
      position: relative;
      overflow: hidden;
    }

    .idDom {
      width: 100%;
      height: 100px;
      background: #666;
      position: fixed;
      bottom: 0px;
    }

    .content {
      display: inline-block;
      width: 430px;
      height: 40px;
      position: absolute;
      left: 0px;
      right: 0px;
      top: 0px;
      bottom: 0px;
      margin: auto;
    }

    .title {
      display: inline;
      font-size: 4em;
      vertical-align: bottom;
      color: #fff;
    }

    .text {
      border: none;
      width: 300px;
      height: 30px;
      border-radius: 5px;
      font-size: 2.4em;
    }

    .btn {
      width: 60px;
      height: 30px;
      background: #f90000;
      border: none;
      color: #fff;
      font-size: 2.4em;
    }

    span {
      height: 40px;
      position: absolute;
      overflow: hidden;
      color: #000;
      font-size: 4em;
      line-height: 1.5em;
      cursor: pointer;
      white-space: nowrap;
    }
  </style>
```

```html
 <div class="boxDom" id="boxDom">
    <div class="idDom" id="idDom">
      <div class="content">
        <p class="title">吐槽:</p>
        <!-- autocomplete="on" ： 自动补全 -->
        <!-- autocomplete="off" 关闭自动补全 -->
        <input type="text" class="text" id="text" autocomplete="off" />
        <button type="button" class="btn" id="btn">发射</button>
      </div>
    </div>
  </div>
```

```javascript
<script src="../jQuery版本/jquery-1.12.4.js"></script>
<script>
  $(function () {

    // 1. 给按钮注册点击事件
    // 2. 获取input的value值， 如果值为空 ，return   清空value值
    // 3. 动态创建span，添加到boxDom中
    // 4. 设置span的颜色为随机
    // 5. 设置span的top: 随机 0 - 屏幕高度/3
    // 6. 设置span的left: 一个屏幕宽度
    // 7. span要有动画， 从右边慢慢到左边   left: - 自身的宽度
    // 8. 等待span运动到屏幕的外边了，就需要移除span

    // 9. 回车的时候，发送弹幕

    var $btn = $('#btn');
    var $text = $('#text');
    var colors = ['purple', 'red', 'black', 'hotpink', 'green', 'orange', 'blue', 'lime', 'yellowgreen', 'teal'];
    var $boxDom = $("#boxDom")

    // 点击发射按钮，生成一个带span
    $btn.click(function () {

      if ($text.val().trim() === '') {
        return false
      }
      // 获取当前弹幕容器的宽高
      var boxH = $boxDom.height()
      var boxW = $boxDom.width()
      // 弹幕高度随机数
      var spanH = parseInt(Math.random() * (boxH / 2))
      // 颜色随机数 
      var colorIdx = parseInt(Math.random() * colors.length)
      // 创建span
      var $span = $("<span></span>")
      // 将输入内容放入span
      $span.text($text.val())
      // 定义弹幕样式
      $span.css({
        left: boxW,
        color: colors[colorIdx],
        top: spanH
      })
      // 定义弹幕动画
      $span.animate({
        left: -$boxDom.width()
      }, 10000, 'linear', function () {
        $(this).remove()
      })
      // 追加弹幕
      $span.appendTo($boxDom)
      // 发射完清空
      $text.val('')

    })

    // 按下enter键快速发射
    $(document).keyup(function (e) {
      if (e.keyCode == 13) {
        $btn.click()
      }
    })
  });
</script>

```
### 事件注册

#### 简单注册方式

`click(func) / mouseenter(handler) / mouseleave(handler) `
缺点: 不能注册多个事件

#### bind注册

`$("p").bind("click mouseenter", function(){});`
缺点：不支持动态事件绑定

#### delegate 事件委托

```javascript
// 第一个参数：selector，要绑定事件的元素
// 第二个参数：事件类型
// 第三个参数：事件处理函数
$(".parentBox").delegate("p", "click", function(){
    //为 .parentBox下面的所有的p标签绑定事件
});
```
缺点：只能注册委托事件

#### **on注册事件(重点)**

1. jQuery1.7之后，jQuery用on统一了所有事件的处理方法。
2. 最现代的方式，兼容zepto(移动端类似jQuery的一个库)，强烈建议使用。

##### on注册简单事件

```javascript
 // 表示给$(selector)绑定事件，并且由自己触发，不支持动态绑定。
  $(selector).on( "click", function() {});
```

##### on注册委托事件

```javascript
// 表示给$(selector)绑定代理事件，当必须是它的内部元素span才能触发这个事件，支持动态绑定
$(selector).on( "click",“span”, function() {});
```

##### on注册事件的语法

```javascript
// 第一个参数：events，绑定事件的名称可以是由空格分隔的多个事件（标准事件或者自定义事件）
// 第二个参数：selector, 执行事件的后代元素（可选），如果没有后代元素，那么事件将有自己执行。
// 第三个参数：data，传递给处理函数的数据，事件触发的时候通过event.data来使用（不常使用）
// 第四个参数：handler，事件处理函数
$(selector).on(events[,selector][,data],handler);
```

#### 表格操作(委托事件)案例

```css
<style>
    * {
      padding: 0;
      margin: 0;
    }
    
    .wrap {
      width: 410px;
      margin: 100px auto 0;
    }
    
    table {
      border-collapse: collapse;
      border-spacing: 0;
      border: 1px solid #c0c0c0;
    }
    
    th,
    td {
      border: 1px solid #d0d0d0;
      color: #404060;
      padding: 10px;
    }
    
    th {
      background-color: #09c;
      font: bold 16px "Î¢ÈíÑÅºÚ";
      color: #fff;
    }
    
    td {
      font: 14px "Î¢ÈíÑÅºÚ";
    }
    
    td a.get {
      text-decoration: none;
    }
    
    a.del:hover {
      text-decoration: underline;
    }
    
    tbody tr {
      background-color: #f0f0f0;
    }
    
    tbody tr:hover {
      cursor: pointer;
      background-color: #fafafa;
    }
    
    .btnAdd {
      width: 110px;
      height: 30px;
      font-size: 20px;
      font-weight: bold;
    }
    
    .form-item {
      height: 100%;
      position: relative;
      padding-left: 100px;
      padding-right: 20px;
      margin-bottom: 34px;
      line-height: 36px;
    }
    
    .form-item > .lb {
      position: absolute;
      left: 0;
      top: 0;
      display: block;
      width: 100px;
      text-align: right;
    }
    
    .form-item > .txt {
      width: 300px;
      height: 32px;
    }
    
    .mask {
      position: absolute;
      top: 0px;
      left: 0px;
      width: 100%;
      height: 100%;
      background: #000;
      opacity: 0.15;
      display: none;
    }
    
    .form-add {
      position: fixed;
      top: 30%;
      left: 50%;
      margin-left: -197px;
      padding-bottom: 20px;
      background: #fff;
      display: none;
    }
    
    .form-add-title {
      background-color: #f7f7f7;
      border-width: 1px 1px 0 1px;
      border-bottom: 0;
      margin-bottom: 15px;
      position: relative;
    }
    
    .form-add-title span {
      width: auto;
      height: 18px;
      font-size: 16px;
      font-family: ËÎÌå;
      font-weight: bold;
      color: rgb(102, 102, 102);
      text-indent: 12px;
      padding: 8px 0px 10px;
      margin-right: 10px;
      display: block;
      overflow: hidden;
      text-align: left;
    }
    
    .form-add-title div {
      width: 16px;
      height: 20px;
      position: absolute;
      right: 10px;
      top: 6px;
      font-size: 30px;
      line-height: 16px;
      cursor: pointer;
    }
    
    .form-submit {
      text-align: center;
    }
    
    .form-submit input {
      width: 170px;
      height: 32px;
    }
  </style>

```
```html
<div class="wrap">
  <input type="button" value="清空内容" id="btn">
  <input type="button" value="添加" id="btnAdd">
  <table>
    <thead>
    <tr>
      <th>课程名称</th>
      <th>所属学院</th>
      <th>操作</th>
    </tr>
    </thead>
    <tbody id="j_tb">
    <tr>
      <!-- <td><input type="checkbox"/></td> -->
      <td>JavaScript</td>
      <td>传智播客-前端与移动开发学院</td>
      <td><a href="javascrip:;" class="get">DELETE</a></td>
    </tr>
    <tr>
      <!-- <td><input type="checkbox"/></td> -->
      <td>css</td>
      <td>传智播客-前端与移动开发学院</td>
      <td><a href="javascrip:;" class="get">DELETE</a></td>
    </tr>
    <tr>
      <!-- <td><input type="checkbox"/></td> -->
      <td>html</td>
      <td>传智播客-前端与移动开发学院</td>
      <td><a href="javascrip:;" class="get">DELETE</a></td>
    </tr>
    <tr>
      <td>jQuery</td>
      <td>传智播客-前端与移动开发学院</td>
      <td><a href="javascrip:;" class="get">DELETE</a></td>
    </tr>
    </tbody>
  </table>
</div>
```
```javascript

<script src="jquery-1.12.4.js"></script>
<script>
  $(function(){
    // 清空内容
    $('#btn').on('click',function(){
        $('#j_tb').empty()
    })
    // 添加数据
    $("#btnAdd").on('click',function(){
        var $tr=$('<tr><td>JavaScript</td><td>传智播客-前端与移动开发学院</td><td><a href="javascrip:;" class="get">DELETE</a></td></tr>')
        $('#j_tb').append($tr)
    })
    // 给delete注册委托事件
    $('#j_tb').on("click",'a',function(){
        $(this).parents('tr').remove();
    })

  });
</script>
```

