伯乐在线注：这是 Matt Smith 发起的一个小项目，可帮助大家提升 jQuery 技能。目前已有 15 个 小技巧。[伯乐在线](http://web.jobbole.com/84028/)会持续跟进更新。

1.  [回到顶部按钮](#回到顶部按)
2.  预加载图片
3.  检查图片是否加载完毕
4.  自动修复损坏的图片
5.  Hover 上的 Class 开关
6.  禁用 input 字段
7.  停止链接加载
8.  淡入淡出/滑动开关
9.  简单的折叠效果
10.  将两个 Div 设为相同高度
11.  在新窗口打开外部链接
12.  找到文本元素
13.  切换可视与隐藏的触发器
14.  Ajax 调用的错误处理
15.  链式操作

* * *

### 回到顶部按钮

通过使用 jQuery 中的 `animate` 和 `scrollTop` 方法，你无需插件便可创建一个简单地回到顶部动画：
```JavaScript
// Back to top
$('a.top').click(function (e) {
  e.preventDefault();
  $(document.body).animate({scrollTop: 0}, 800);
});
```
```JavaScript
<!-- Create an anchor tag -->
<a href="#">Back to top</a>
```

将 `scrollTop` 的值改为你想要 scrollbar 停止的地方。然后你要做的就是，设置在 800 毫秒内回到顶部。

### 预加载图片

如果你的页面使用了大量不能初始可见的图片（例如绑定在 hover 上），预加载它们是十分有用的：
```JavaScript
$.preloadImages = function () {
  for (var i = 0; i &lt; arguments.length; i++) {
    $('&lt;img&gt;').attr('src', arguments[i]);
  }
};

$.preloadImages('img/hover-on.png', 'img/hover-off.png');
```

### 检查图片是否加载完毕

有时你或许要检查图片是否完全加载完毕，才能在脚本中进行后续操作：
```JavaScript
$('img').load(function () {
  console.log('image load successful');
});
```

你也可以通过把 img 标签替换成 ID 或 class，来检查特定图片是否加载完成。

### 自动修复损坏的图片

如果你发现自己网站的图片链接挂了，一个一个替换很麻烦。这段简单的代码可以帮上大忙：
```JavaScript
$('img').on('error', function () {
  $(this).prop('src', 'img/broken.png');
});
```

即使你没有任何损坏的链接，增加这段代码也不会有什么影响。

### Hover 上的 Class 切换

如果用户的鼠标悬停在页面上某个可点击元素时，你想要改变这个元素的视觉表现。可以使用下面这段代码，当用户悬停时，为该元素增加一个 class；当用户鼠标离开后移除这个 class：
```JavaScript
$('.btn').hover(function () {
  $(this).addClass('hover');
}, function () {
  $(this).removeClass('hover');
});
```

你仅需增加必须的 CSS。如果需要更简单的方式，还可以使用 `toggleClass` 方法：
```JavaScript
$('.btn').hover(function () {
  $(this).toggleClass('hover');
});
```

**注意**：CSS 或许是这个例子更快速的解决方式，但大家仍然值得知道这一点。

### 禁用 input 字段

有时你也许想让表单的提交按钮或其文本输入框变得不可用，直到用户执行了一个特定行为（例如确认 “我已经阅读该条款” 的复选框）。增加 `disabled` attribute 到你的 input，就可以实现自己想要的效果：
```JavaScript
$('input[type="submit"]').prop('disabled', true);
```

当你想把 `disabled` 的值改为 `false` 时，仅需在该 input 上再运行一次 `prop` 方法。
```JavaScript
$('input[type="submit"]').prop('disabled', false);
```

### 停止链接加载

有时你不想链接跳转到某个页面或重加载该页面，而希望可以做一些其他事情，比如触发其他脚本。下面的代码是禁止默认行为的一个小诀窍：
```JavaScript
$('a.no-link').click(function (e) {
  e.preventDefault();
});
```

### 淡入淡出/滑动开关

淡入淡出与滑动是我们经常使用 jQuery 做成的动画效果。或许你只是想在用户点击某物时展现一个元素，使用 `fadeIn` 和 `slideDown` 都很棒。但如果想让该元素在第一次点击时显现，第二次点击时消失，下面的代码可以很好地完成这个工作：
```JavaScript
// Fade
$('.btn').click(function () {
  $('.element').fadeToggle('slow');
});

// Toggle
$('.btn').click(function () {
  $('.element').slideToggle('slow');
});
```

### 简单的手风琴效果

这是一个快速实现手风琴效果的简单方法：
```JavaScript
// Close all panels
$('#accordion').find('.content').hide();

// Accordion
$('#accordion').find('.accordion-header').click(function () {
  var next = $(this).next();
  next.slideToggle('fast');
  $('.content').not(next).slideUp('fast');
  return false;
});
```

增加这段脚本后，你所需做的所有事就是，查看脚本是否在必须的 HTML 中正常工作。

### 使两个 Div 高度一样

有时你也许想让两个 div 拥有同样高度，不管它们里面有什么内容：
```JavaScript
$('.div').css('min-height', $('.main-div').height());
```

该例设置了 `min-height`，意味着它可以比主要 div 更大，但永远不能更小。但有一个更加灵活的方法是遍历一组元素的设置，然后将高度设为元素中的最高值：
```JavaScript
var $columns = $('.column');
var height = 0;
$columns.each(function () {
  if ($(this).height() &gt; height) {
    height = $(this).height();
  }
});
$columns.height(height);
```

如果你想让所有列都有相同高度：
```JavaScript
var $rows = $('.same-height-columns');
$rows.each(function () {
  $(this).find('.column').height($(this).height());
});
```

### 在新标签/窗口打开站外链接

在一个新标签或者新窗口中打开外置链接，并确保站内链接会在相同的标签或窗口中打开：
```JavaScript
$('a[href^="http"]').attr('target', '_blank');
$('a[href^="//"]').attr('target', '_blank');
$('a[href^="' + window.location.origin + '"]').attr('target', '_self');
```

**注意**：`window.location.origin` 在 IE 10 中不可用，该 issue 的[修复方法](http://tosbourn.com/a-fix-for-window-location-origin-in-internet-explorer/)。

通过文本找到元素

通过使用 jQuery 中的 `contains()` 选择器，你可以找到某个元素中的文本。如果文本不存在，该元素将会隐藏：
```JavaScript
var search = $('#search').val();
$('div:not(:contains("' + search + '"))').hide();
```

### 视觉改变触发

当用户焦点在另外一个标签上，或重新回到标签时，触发 JavaScript：
```JavaScript
$(document).on('visibilitychange', function (e) {
  if (e.target.visibilityState === "visible") {
    console.log('Tab is now in view!');
  } else if (e.target.visibilityState === "hidden") {
    console.log('Tab is now hidden!');
  }
});
```

### Ajax 调用的错误处理

当某次 Ajax 调用返回 404 或 500 错误，就会执行错误处理。但如果没有定义该处理，其他 jQuery 代码或许会停止工作。可以通过下面这段代码定义一个全局 Ajax 错误处理：
```JavaScript
$(document).ajaxError(function (e, xhr, settings, error) {
  console.log(error);
});
```

**[更新：2015-11-02]**

### 插件链式调用

jQuery 支持链式调用插件，以减缓反复查询 DOM，并创建多个 jQuery 对象。看下面示例代码：
```JavaScript
$('#elem').show();
$('#elem').html('bla');
$('#elem').otherStuff();
```

上面这段代码，可以通过链式操作大大改进：
```JavaScript
$('#elem')
  .show()
  .html('bla')
  .otherStuff();
```
还有另外一种方法，把元素缓存在变量中（前缀是  `$`）：
```JavaScript
var $elem = $('#elem');
$elem.hide();
$elem.html('bla');
$elem.otherStuff();
```

jQuery 中的链式操作和缓存方法，都极大精简和提速了代码。
