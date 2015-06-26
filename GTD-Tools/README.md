##GTD-Tools日程管理应用##

[点击这里可以看到这个应用][1]


----------
##简介##

这是一个基于LocalStorage的web前端应用。

实现了一个日程管理应用，可以添加任务（两级分类），记录任务标题、时间、内容、完成情况。


----------
##数据储存##

数据储存使用了HTML5的新特性LocalStorage（本地储存），允许开发者在浏览器端储存与域名绑定的字符串，字符串最大大小为4MB。

数据储存格式使用了JSON，这是一种轻量级的数据储存格式，与Javascript原生耦合。

数据的储存结构遵循了数据库设计的第三范式，即每个非关键字列都独立于其他非关键字列，并依赖于关键字。这里一共依赖了`_ID3_content`，`_ID123`，`_ID1_title`，`_ID2_title`这四张表。


----------
##事件管理##
这个应用的点击事件极多，而且存在大量的DOM结构变化，所以使用传统的事件绑定会使代码结构变得冗余。

这里我们使用了“事件代理”机制，监听了全局的`click`事件，然后把事件分发到各自回调函数中。

    var doc = document.getElementsByTagName('body')[0];
    	
    doc.onkeyup = function(e){
        //这里根据e.target来分发事件
    }


----------
##DOM操作##

**1、节点插入**

这里使用了类似“模板替换”的技术：

    var child_task_template = "<div class=\"childtask\" id=\"{{ID3}}\">{{title}}</div>";

然后在插入节点时，使用正则表达式将数据插入其中：

    $("#childtask-"+_ID3_content[arr[i]].date).innerHTML +=
    child_task_template.replace(/{{ID3}}/g,"childtask-"+arr[i]).replace(/{{title}}/g,_ID3_content[arr[i]]["title"]);


**2、节点获取**
虽然浏览器原生提供了getElementById、getElementByTagName等接口，但是无法复合查找节点，也无法使用CSS选择器的查找方式。

虽然在IE8+的浏览器上提供了querySelectAll接口，但是这个接口在IE6/7上无法兼容。

我们这里原生实现了一个选择器引擎util.js，支持id选择器、类选择器、后代选择器、属性选择器，以及他们的复合查找。

util.js的实现借鉴了jQuery的sizzle引擎，即先使用正则匹配解析条件语句，然后根据条件语句选择从最上级递归查找或者从最下级筛选查找。


----------
##存在的问题##

**1、状态管理**

由于这个项目并没有使用现在流行的前端MVC/MVVM框架例如angularJS、reactJS，导致状态管理比较混乱，具体的讨论在这里：
http://blog.csdn.net/stark1995/article/details/45742835

**2、移动端适配**

这个项目还尚未实现移动端适配，但是我写了一个[demo][2]，暂时没有实现添加任务、删除任务、数据储存的功能。


  [1]: http://starkwang.github.io/Project-for-Multimedia-Technology/GTD-Tools/
  [2]: http://starkwang.github.io/IFE-Homework/task0004/work/starkwang/index.html
