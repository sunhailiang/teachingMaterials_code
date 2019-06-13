### 事件解绑
1. unbind方式（不用）
```js
$(selector).unbind(); //解绑所有的事件
$(selector).unbind("click"); //解绑指定的事件
```
2. undelegate方式（不用）
```js
$( selector ).undelegate(); //解绑所有的delegate事件
$( selector).undelegate( “click” ); //解绑所有的click事件
```
3. **off方式（推荐）**
```js
// 解绑匹配元素的所有事件
$(selector).off();
// 解绑匹配元素的所有click事件
$(selector).off("click");
// 解绑指定类型元素的委托事件
$('div').off("click",'p')
// 解绑所有的委托事件
('div').off("click",'**')
```

### 触发事件

```html
  <button>我是一个按钮</button>
  <input type="button" value="按钮">
```
```js
  <script src="jquery-1.12.4.js"></script>
  <script>
    $(function(){
      $('button').on('click', function() {
        console.log('这是给button注册的事件');
      });


      $('input').on('click', function() {
        // 触发button的点击事件
        // 触发方式1： 直接调用事件名
        // 触发方式2   trigger():触发 
        $('button').trigger('click');
      });
    });
  </script>
```

### jquery事件对象 event

1. jQuery事件对象其实就是js事件对象的一个封装，处理了兼容性。
```html
  <button>按钮</button>
  <a href="http://www.baidu.com">哈哈</a>
```
```js
  <script src="jquery-1.12.4.js"></script>
  <script>
    $(function(){
      $('a').on("click", function(e) {
 
        //  e:就是事件对象 

        // e.stopPropagation() 阻止事件冒泡
        // e.preventDefault(); // : 阻止浏览器默认行为
        // return false; 即可阻止事件冒泡， 也可以阻止浏览器的默认行为(不推荐)
        return false;
      });
    });
  </script>
```

### jquery链式编程

1. 在jquery中允许我们连续链装的调用jquery的方法
2. 但是要求链式编程中每次函数执行完都要返回原始对象
3. 一般在设置性操作时才会使用链式编程，因为一般设执行操作不会改变jquery对象
4. 在获取时一般不能使用链式编程，因为获取操作容易改变jquery对象
5. end() 恢复上一次的链

```css
 <style>
        * {
            margin: 0;
            padding: 0;
            list-style: none;
        }

        li {
            font-size: 50px;
            float: left;
            color: orange;
        }
    </style>
```
```html
 <ul>
        <li>☆</li>
        <li>☆</li>
        <li>☆</li>
        <li>☆</li>
        <li>☆</li>
    </ul>
```
```js
 <script src="jquery-1.12.4.js"></script>
    <script>
        $(function () {
            // 鼠标悬浮到li,当前li以及之前的兄弟成员需要被选中
            // 鼠标离开恢复空心
            // 鼠标点击当前对象以及之前的兄弟元素被选中
            var idx = -1
            $('li').mouseenter(function () {               
                $(this).text("★").prevAll().text("★").end().nextAll().text("☆")
            })
            $('li').mouseleave(function () {
                $('li').text('☆')
                if (idx >= 0) {
                    $('li').eq(idx).text('★').prevAll().text("★")
                }

            })
            $('li').click(function () {
                idx = $(this).index()
            })


        //========还有常用方法
        // prev() 获取上一个兄弟
        // prevAll() 获取前面所有兄弟
        // next() 获取下一个兄弟
        // nextAll() 获取后面所有兄弟
        /// siblings() 获取所有同级兄弟

        });
    </script>
```

### 隐式迭代的概念

1. 隐式迭代：jquery对象不需要自己写for循环，jquery内部会自动遍历 
   1. jquery设置操作：内部自动遍历，所有元素都会被设置同样的值，如果需要设置不同的值，就需要自己处理循环
   2. jquery获取操作，直接返回 **第一个元素** 的样式
2. 显示迭代：1.each()  // 参数一：内部dom元素的下标，参数二：dom元素，可以用this直接获取
3. 可以用for主动循环元素

### 多库共存

1. jQuery也是jquery文件暴露的一个对象，可当作$使用
2. $是jquery文件的暴露的第二个对象
3. 如果$冲突可以用jQuery替换
4. 也可以使用$.noConflic()放弃$控制权，使用 **自定变量** 接收该方法返回的对象替代$

### jquery插件

1. 依赖jquery开发的插件

### jquery.color库的使用

```css
  <style>
    div {
      width: 300px;
      height: 300px;
      background-color: green;
    }
  </style>
```
```html
  <div></div>
```
```js
  <script src="jquery-1.12.4.js"></script>
  <script src="jquery.color.js"></script>
  <script>
    $(function(){
      $('div').animate({
        width: 600,
        backgroundColor: 'red'
      }, 1000)
    });
  </script>
```

### jquery.lazyload库的使用

 ```css
  <style>
    div {
      height: 3000px;
    }
  </style>
 ```

```html
<div></div>
<!-- 真实图片的地址放在 data-original -->
  <img class="lazy" data-original="1.jpg" alt="" width="500" height="350">
  <img class="lazy" data-original="2.jpg" alt="">
```
``` js
  <script src="jquery-1.12.4.js"></script>
  <script src="jquery.lazyload.js"></script>
  <script>
    $(".lazy").lazyload();
  </script>
```
### jquery插件封装的原理

`$.fn.pluginName=function(){}`

###　封装一个小插件

```js
$.fn.bgc = function(color) {
  // 在$.fn的方法中， this指的就是当前的jquery对象
  this.css('backgroundColor', color);
  return this;
}
```

### 封装一个拖拽插件

```js
$.fn.drag = function() {
  // 使用变量把this给存起来
  var that = this;
  that.on('mousedown', function(e) {
    e.preventDefault();
    var x = e.offsetX;
    var y = e.offsetY;

    $(document).on('mousemove', function(e) {
      that.css({
        position: 'absolute',
        left: e.pageX - x,
        top: e.pageY - y
      });
    });
  });

  that.on('mouseup', function() {
    $(document).off('mousemove');
  });

  return that;
};
```


