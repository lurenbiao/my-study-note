# jQuery笔记

### jQuery的入口函数

第一种

```
$(function () {
            $('div').hide()   //此处是页面dom加载完成的入口
        })
```

第二种

```
 $(document).ready(function () {
            $('div').hide()   //此处是页面dom加载完成的入口
        })
```

1. 等着DOM结构渲染完毕即可执行内部代码，不必等到所有外部资源加载完成，jquery帮我们完成了封装。
2. 相当于原生js中的DOMContentLoad.
3. 不同于原生js中的load事件是等页面文档，外部js，css文件，图片加载完毕才执行内部代码
4. 更推荐使用第一种



DOM对象：用原生js获取过来的对象就是dom对象



### DOM对象和jQuery对象

```javascript
 let myDiv = document.querySelector('div')   //myDiv是dom对象
 $('div');   //是一个jquery对象
 // jQuery对象只能使用jquery方法,Dom对象则使用原生的javascript属性和方法
 myDiv.style.display = 'none'
 myDiv.hide()      //myDiv是一个dom对象不能使用jquery里面的hide()方法
 $('div').style.display='none'   //这个$('div')是一个jquery对象不能使用原生js的属性和方法
```

### DOM对象和jQuery对象的抓换

```
  let myvideo = document.querySelector('video')
  $('myvideo')  //将dom对象和转换为jquery对象
  $('video')[0]   //转换为dom对象
```



### 选择器

```
$('')   //类似document.querySelector('')里面的('')
```

子代选择器**$('ul > li')**    使用>号，获取亲儿子层级元素；注意，并不会获取孙子层级元素

后代选择器**$('ul  li')**      使用空格，代表后代选择器，获取ul下的所有li元素，包括孙子等



### 隐式迭代

遍历内部DOM元素（伪数组形式存储）的过程就叫隐式迭代

简单理解：给匹配到的所有元素进行循环遍历，执行相应的方法，而不用我们再进行循环，简化我们的操作，方便我们调用

```
<div></div>
    <div></div>
    <div></div>
    <div></div>
 <script>
        $('div').css('background', 'pink')
 </script>
```

### jquery筛选选择器

| 语法         | 用法          | 描述                                                    |
| ------------ | ------------- | ------------------------------------------------------- |
| ：first      | $('li:first') | 获取第一个li元素                                        |
| ：last       | $('li:last')  | 获取最后一个li元素                                      |
| ：eq (index) | $('li:eq(2)') | 获取到li元素中，选择索引号为2的元素，索引好index从0开始 |
| ：odd        | $('li:odd')   | 获取到的li元素中，选择索引号为奇数的元素                |
| ：even       | $('li:even')  | 获取到的li元素中，选择索引号为偶数的元素                |

### jquery筛选方法

| 语法                | 用法                         | 说明                                                 |
| ------------------- | ---------------------------- | ---------------------------------------------------- |
| parent()            | $('li').parent()             | 查找li的父级元素                                     |
| parents()           | $('li').parents('.')         | 可以返回指定的祖先元素                               |
| children (selector) | $('ul').children('li')       | 相当于$('ul>li'),最近一级（亲儿子）                  |
| find (selector)     | $('ul').find('li')           | 相当于$('ul li') ,后代选择器                         |
| siblings (selector) | $('.firstl').siblings ('li') | 查找兄弟节点，不包括自己本身                         |
| nextAll ([expr])    | $(.firstl').nextAll()        | 查找当前元素之后所有的同辈元素                       |
| prevtAll ([expr])   | $('.last').prevAll()         | 查找当前元素之前的所有同辈元素                       |
| hasClass (class)    | $('div').hasClass ('')       | 检查当前的元素是否包含某个特定的类，如果有则返回true |
| eq（index）         | $('li').eq(2)                | 相当于$('li:eq(2)'),index从0开始                     |



### 操作css方法

jQuery可以使用css方法来修改简单元素样式；可以操作类，修改多个样式

参数只写属性名，则返回属性值

```
$(this).css('color')
```

参数是属性名，属性值，逗号分隔，是设置一组样式，属性必须加引号，值如果是数学可以不用跟单位和引号

```
$(this).css('color','blue')
```

参数可以是对象形式，方便设置多组样式。属性名和属性值用冒号隔开，属性可以不用加引号

```
$(this).css({'color':'skyblue','font-size':'20px'})
```



### 设置类样式方法

作用等同于以前的classList,可以操作类样式，注意操作里面的参数不要加点

添加类

```
$('div').addClass('className')
```

删除类

```
$('div').removeClass('className')
```

切换类

```
$('div').toggleClass('className')
```



### jQuery效果

| 显示隐藏 | 滑动          | 淡入淡出     | 自定义动画 |
| -------- | ------------- | ------------ | ---------- |
| show（） | slideDown()   | fadeIn()     | animate()  |
| hide()   | slideUp()     | fadeOut()    |            |
| toggle() | slideToggle() | fadeToggle() |            |
|          |               | fadeTo()     |            |



### 事件切换

hover([over],out)

over：鼠标移到元素上要触发的函数（相当于mouseenter）

out:   鼠标移出元素要触发的函数（相当于mouseleave）

```
 $('.nav>li').hover(function () {
            $(this).children('ul').slideDown()
        }, function () {
            $(this).children('ul').slideUp()
        })
```



```
  $('.nav>li').hover(function () {
            $(this).children('ul').slideToggle()
        })
```



### 动画队列及其停止排队方法

**动画或效果队列**

动画或者效果一旦触发就会执行，如果多次触发，就会造成多个动画或者效果排队执行

**停止排队**

```
stop()
```

stop()方法用于停止动画或效果

注意：stop()写到动画或者效果的前面，相当于结束上一次的动画



### 设置或获取元素固有属性值prop()

所谓元素固有属性就是元素本身自带的属性，比如<a>元素里面的hre，比如input元素里面的type.

获取属性语法

```
prop('属性')
```

设置属性语法

```
prop('属性','属性值')
```

用户自己给元素添加的属性，我们称为自定义属性。比如给div添加index='1'

**获取属性语法**

```
attr('属性')  //类似原生getAttribute()
```

**设置属性语法**

```
attr('属性','属性值')  //类似原生 setAttribute()
```



### 数据缓存data()

data()方法可以在指定的元素上存取数据，并不会修改dom元素结构，一旦页面刷新，之前存放的数据都将被移除



### jquery内容文本值

主要针对元素的内容还有表单的值操作

**普通元素内容html()  相当于原生的innerHTML**

```
html()  //获取元素内容
html('内容')   //设置元素内容
```

**普通元素文本内容text()   相当于原生innerText()**

```
text()  //获取元素内容
text('内容')   //设置元素内容
```

**表单的值val()   相当于原生的value**

```.val
$('input').val()  //获取
$('input').val('修改的值')  //设置value的值
```



### 遍历元素

jquery隐式迭代是对同一类元素做了同样的操作，如果想要给同一类元素做不同操作，就需要用到遍历

语法1：

```
$('div').each(function(index,domele){xxxxx})
```

each()方法遍历匹配的每一个元素，主要用dom处理，each每一个

里面的回调函数有两个参数：index是每个元素的索引号，domele是每个dom元素，不是jquery对象

所以想要使用jquery方法，需要给这个dom元素转换为jquery对象$(domele)

语法2：

```
$.each(object,function(index,element){xxxxx})
```

$.each()方法用于遍历任何对象。主要用于数据处理，比如数组，对象

里面的函数有两个参数：index是每个元素的索引号；element遍历对象



### 创建元素

语法：

```
$('<li></li>')
```

动态的创建了一个<li>

### 添加元素

内部添加元素，生成后，它们是父子关系

外部添加元素，生成后，他们是兄弟关系

**内部添加**

```
element.append('内容')
```

把内容放入匹配元素内部最后面，类似原生appendChild

```
element.prepend('内容')
```

把内容放到匹配元素内部的最前面

**外部添加**

```
element.after('内容')
```

把内容放到目标元素后面

```
element.before('内容')
```

把内容放到目标元素前面



### 删除元素

```
element.remove()  //删除匹配的元素（本身）
```

```
element.empty() //删除匹配元素集合中所有的子节点
```

```
element.html('')  //清空匹配元素的内容
```



### jQuery尺寸

| 语法                                 | 用法                                           |
| ------------------------------------ | ---------------------------------------------- |
| width()  / height()                  | 取得匹配元素宽度和高度 只算 width /height      |
| innerWidth()       /   innerHeight() | 取得匹配元素宽度和高度 包含padding             |
| outerWidth()   /   outerHeight()     | 取得匹配元素宽度和高度值 包含padding, border   |
| outerWidth(true)  /outerHeight(true) | 取得匹配元素宽度和高度值 padding,border,margin |



### jquery位置

位置主要有三个：

**offset()**

offset() 方法设置或返回被选元素相对于文档的偏移坐标，跟父级没有关系

该方法有两个属性left,top. offset()用于获取距离文档顶部的距离，offset().left()用于获取距离文档左侧的距离

**position()**

position()方法用于返回被选元素相对带有定位的父级元素偏移坐标，如果父级都没有定位，则以文档为准

这个方法只能获取不能设置

**scrollTop()**

scrollTop()方法设置或返回被选元素被卷去的头部

**scrollLeft()**



**带有动画的返回顶部**

核心原理:使用animate动画返回顶部

animate动画函数里面有个scrollTop属性，可以设置位置

但是元素做动画，因此$('body,html').stop().animate({ scrollTop:0 })



### jquery事件注册

语法：

**单个事件注册**

```
element.事件(function(){})   
$('div').click(function(){事件处理程序})
```

### **事件处理 on() 绑定事件**

on()方法在匹配元素上绑定一个或多个事件处理函数

语法：

```
element.on(events,[selector],fn)
```

events; 一个或多个用空格分隔的事件类型，如‘click’或'keydown'

selector:元素的子元素选择器

fn：回调函数

```
 $('div').on({
            mouseenter: function () {
                $(this).css('background', 'blue')
            },
            click: function () {
                $(this).css('background', 'red')

            },
            mouseleave: function () {
                $(this).css('background', 'yellow')
            }
        })
```

```
 $('div').on('mouseenter mouseleave',function(){
            $(this).toggleClass('current');
        })
```

on() 方法优势2：

on() 可以给未来动态创建的元素绑定事件

可以事件委派操作。事件委派的定义就是，把原来加给子元素身上的事件绑定在父元素身上，就是把事件委派给父元素

```
$('ul').on('click','li',function(){
      alter('hello world')
})

```

触发事件是子元素li



### 事件处理off() 解绑事件

off() 方法可以移除通过on()方法添加的事件处理程序

```
$('div').off()  //这个是解除了div身上的所有事件
$('div').off('click')    //这个是解除了div身上的点击事件
```

### one()

如果事件只想触发一次，可以使用one()来绑定事件

```
$('div').one('click',function(){触发事件})
```



### 自动触发事件trigger()

有些事件希望自动触发，比如轮播图自动播放功能跟点击右侧按钮一致。可以利用定时器自动触发右侧按钮点击事件，不必鼠标自动触发

```
element.click() //第一种简写形式
element.trigger('type')  //第二种自动触发模式
element.triggerHandler('type')  //第三种自动触发模式   就是不会触发元素的默认行为，如input的光标
```



### jquery事件对象

事件被触发，就会有事件对象的产生

```
element.on(event,[selector],function(event){})
```

阻止默认行为：event.preventDefault() 或者 return false

阻止冒泡： event.stopPropagation()



### jquery对象拷贝

如果想要给某个对象拷贝（合并）给另外一个对象使用，可以使用$.extend() 方法

```
$.extend([deep],target,object1,[objectN])
```

- deep:如果设置为true为深拷贝，默认为false浅拷贝
- target:要拷贝的目标
- object1：待拷贝到第一个对象的对象
- 浅拷贝是把被拷贝对象复杂数据类型中的地址拷贝给目标对象，修改目标对象会被影响被拷贝的对象

```
var target={
	id:2
}
var obj={
     id:1,
     name:'小米'
 }
 $.extend(target,obj)    //如果数据有冲突，拷贝会覆盖原来对象的内容
```

```
 $.extend(true,target,obj)    //深拷贝把里面的数据完全复制一份给目标对象，如果里面有不冲突的属性，会合并到一起
```



### 多库共存

**问题概述**

jquery使用$作为标识符，随着jquery的流行。其他js库也会使用$作为标识符，这样一起使用会起冲突

**jquery解决方案：**

把里面的$符号统一改为jQuery.比如  jQuery('div')

jquery变量规定新的名称：$.noConflict()   var xx=$noConflict()

```
var suibian=$.noConflict()            //把suibian改为标识符
suibian('div')

```



### jquery插件

 

https://www.jq22.com/           

http://www.htmleaf.com/       //jquery之家
