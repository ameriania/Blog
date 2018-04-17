今天遇到了一个问题,也是我之前忽略的.在处理着一个点击事件,在某种情境下,要去禁止它点击.

我们都知道点击事件的组件,我们一般使用<a>标签或者<button>标签,然而很多人会忽略的一点是<a>标签并没有 disabled 属性.

------

对<button>进行点击事件的禁止相对简单点,就是:

```
/** demo.html */
<button class="btn">提交</button>

/** demo.js */
$('.btn').attr('disabled',true).css('cursor','not-allowed');
```

<button disabled>效果会如图:

![img](https://pic1.zhimg.com/80/v2-b078ba71a2a56aba5bf053388492a62f_hd.jpg)鼠标在上方会有🚫样式

------

对<a>标签进行禁止的话,则需要:

```
/** demo.html */
<a class="a">提交</button>

/** demo1.js
 *  css 方法
 */
$('.a').css('pointer-events','none');

/** demo1.js
 *  属性 方法
 */
$('.a').attr('href','javascript:;');
```

效果则如:

![img](https://pic3.zhimg.com/80/v2-f740580f223414ca08b22b0988f12b54_hd.jpg)鼠标在上方不能点击

这个时候则不能进行任何点击,但是样式的话,需要自己自行添加置灰.

------

**PS** 

- pointer-events:none, 代表<a>标签上的事件都取消了, cursor 属性自然也没有了
- pointer-events 这个 CSS3属性,对浏览器的兼容并不好

![img](https://pic4.zhimg.com/80/v2-9bd80976234890b790e563e2ad2d9d89_hd.jpg)IE只能兼容到v11

所以在使用 css 方法禁止<a>标签点击事件的时候,需要考虑兼容性的问题.