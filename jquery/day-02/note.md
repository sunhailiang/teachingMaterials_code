# jquery动画
1. jquery提供了三组基本动画，这些动画都是标准的、有规律的效果，jquery还提供了自定义动画的功能
## 2. 隐藏/展示动画(**参数为空,没有动画效果**):本质就是改变元素的width,height,opacity
   1. show(time,func) 展示动画
      1. time：元素展开的动画时间，单位毫秒，可以直接数字，也可以固定字符串形式：fast:快=200ms normal：正常=400ms slow:慢=600ms 
      2. func: 回调函数[可选参数],动画执行完成后执行
   2. hide() 隐藏动画
      1. **用法和show()一致，只是动画效果是逆向的**
   3. toggle()
      1. 动画切换，如果当前状态是展示，触发toggle()则隐藏，否则展示

### 隐藏展示 demo
```css
  <style>
    div {
      width: 400px;
      height: 400px;
      background-color: pink;
      display: none;
    }
  </style>
```
```html
  <button>显示</button>
  <button>隐藏</button>
  <button>切换</button>
  <div></div>
```

```js
  <script src="jquery-1.12.4.js"></script>
  <script>
    $('button:first').click(function() {
      $('div').show(1000,'linear',function() {
        console.log('展开动画执行完成');
      });
    });

    $('button').eq(1).click(function() {
      $('div').hide(1000,function(){
        console.log('隐藏动画执行完成');
      });
    });
    $('button').eq(2).click(function() {
      // 如果是显示状态，就会隐藏， 如果是隐藏状态，就会显示
      $('div').toggle(1000,function(){
       console.log("动画切换完成了");
      });
    })
  </script>
```

## 2. 淡入/淡出动画(**没有参数时默认是normal也就是400ms**):本质就是改变元素透明度
   1. fadeIn() 
   2. fadeOut()
   3. fadeToggle()
   4. **参数，用法和show()/hide()/toggle()一致可以一并记忆，只是动画效果不同**
### 淡入淡出 demo
```css
  <style>
    div {
      width: 400px;
      height: 400px;
      background-color: red;
      display: none;
    }
  </style>
```

```html
  <button>显示</button>
  <button>隐藏</button>
  <button>切换</button>
  <div></div>
```

```javascript
  <script src="jquery-1.12.4.js"></script>
  <script>
    $('button').eq(0).click(function() {
      $('div').fadeIn()  // 淡入
    });

    $('button').eq(1).click(function() {
      $('div').fadeOut(1000); // 淡出
    });

    $('button').eq(2).click(function() {
      $('div').fadeToggle(); // 淡入淡出切换
    })
  </script>
```
### 2.1 京东商品轮播图案例
[从这里获取代码](https://github.com/sunhailiang/teachingMaterials_code/tree/master/jquery/day-02/code/03-%E4%BA%AC%E4%B8%9C%E5%95%86%E5%93%81%E8%BD%AE%E6%92%AD%E5%9B%BE)

## 3. 拉/上卷动画(**没有参数时默认是normal也就是400ms**):本质就是改变元素的height属性
 1. slideDown()
 2. slideUp()
 3. slideToggle()
 4. **参数，用法和show()/hide()/toggle()一致可以一并记忆，只是动画效果不同**

### 3.1 下拉菜单案例
[从这里获取代码](https://github.com/sunhailiang/teachingMaterials_code/tree/master/jquery/day-02/code/05-%E4%B8%8B%E6%8B%89%E8%8F%9C%E5%8D%95)

## 4. 自定义动画 animate()
   1. 参数1：必填，给动画设置样式 **是个对象**
   2. 参数2：指定动画时间，默认是normal
   3. 参数3：指定动画效果 默认是swing ,常用的还有linear等等
   4. 参数4：回调函数，动画完成后执行

### 自定义动画 demo

```css
  <style>
    div {
      width: 100px;
      height: 100px;
      background-color: red;
      position: absolute;
      left: 0;
    }
    div:nth-of-type(2) {
      margin-top: 200px; 
    }
  </style>
```

```html
  <button>执行动画</button>
  <div></div>
  <div></div>
```

```js
  <script src="jquery-1.12.4.js"></script>
  <script>
    $('button').eq(0).click(function() {
      $('div').animate({ width: '400px', height: 400, borderRadius: 200},2000 )
      $('div').eq(0).animate({left: 1000}, 5000);
      $('div').eq(1).animate({left: 1000}, 5000, 'linear', function() {
        console.log('动画执行结束了');
      });
    });
  </script>
```
###　4.1 小米手风琴效果案例
[从这里获取代码](https://github.com/sunhailiang/teachingMaterials_code/tree/master/jquery/day-02/code/06-%E6%89%8B%E9%A3%8E%E7%90%B4)

# 5. jquery动画队列
>>> 1. jquery为了保证动画不会丢失，使用队列的形式，依次执行动画
>>> 2. 所以只要你触发动画事件，就相当于向队列添加一个动画任务,直到执行完成

##　5.1 队列演示demo
```css
  <style>
    div {
      width: 100px;
      height: 100px;
      background-color: pink;
      position: absolute;
    }
  </style>
```

```html
  <div></div>
```

```java
  <script src="jquery-1.12.4.js"></script>
  <script>
    // 类似回调地狱执行完在执行下一个,保证不会丢失
    // $('div').animate({left: 400}, function() {
    //   $('div').animate({width: 300}, function() {
    //     $('div').animate({height: 300}, function(){
    //       $('div').animate({borderRadius: 150})
    //     })
    //   })
    // });

    // 采用链式比较直观
     $('div').animate({left: 400}).animate({width: 300}).animate({height: 300}).animate({borderRadius: 150})  
    // 1. 跑到left:400的地方
    // 2. 宽度变大为300
    // 3. 高度变为300
    // 4. 变圆
    // 四个步骤依次执行
  </script>
```
#　6. stop()停止动画
1. 参数一：是否清除被选元素所有加入队列的动画？true/false，默认false
2. 参数二: 是否直接跳到最后的执行结果？true/false,默认false
3. **如果参数stop(true,true)  第一参数是true动画队列会被清除，所以即使第二参数也是true,但因为动画队列被清除后没有了后续动画也就执行不到最终的效果**

## top() demo

```css
 <style>
    div {
      width: 400px;
      height: 400px;
      background-color: pink;
    }
  </style>
```
```html
  <button>开始</button>
  <button>停止</button>
```
```javascript
  <script src="jquery-1.12.4.js"></script>
  <script>
    $(function(){
      $('button').eq(0).click(function() {
        $('div').animate({left: 400}).animate({width: 300}).animate({height: 300}).animate({borderRadius: 150}) 
      })
      $('button').eq(1).click(function() {
        $('div').stop(false, true);
      })
    });
  </script>
```
# 6. 音乐导航
 [音乐导航案例的源码从这里取](https://github.com/sunhailiang/teachingMaterials_code/tree/master/jquery/day-02/code/09-%E9%9F%B3%E4%B9%90%E5%AF%BC%E8%88%AA)
# 7. 自定义动画综合案例
 [旋转木马案例的源码从这里取](https://github.com/sunhailiang/teachingMaterials_code/tree/master/jquery/day-02/code/10-%E6%97%8B%E8%BD%AC%E6%9C%A8%E9%A9%AC)