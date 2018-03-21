# AJAX的get方法的小技巧

在一个老项目中,我处理接口的时候,发现了一个以前一直漏掉的Ajax知识点.



里面的源代码大概是这样的:

```js
DemoAjax({
     type: 'GET',
     url: '/demo/website?user_id='+encodeURI(data.userID)+'&user_name='+encodeURI(data.userName)
})
```



这是一个get的请求,一般对它的处理是,如果要发送些字段给服务器,一般都是通过url后面通过```?``` 和```&``` 来拼接key和value.当我们要发送的字段太多的话,开发者拼接起来其实蛮麻烦的,同时维护者也很难从这种长字符串中一眼读到信息.



改善这种对读者不良好的接口时候,可以尝试以下的改写.因为这个DemoAjax是基于JQ的AJAX改写的,里面保有基本的功能,就可以改写成这样子:

```js
DemoAjax({
  type: 'GET',
  url: '/demo/website'
  data:{
	user_id:userId,
    user_name:userName
  }
})
```



为什么说这是我之前漏掉的一个基础知识点,因为在之前,我一直认为get的参数只能在url后面拼接,但是在某一次翻查基础文档的过程中,我还遗漏了这样一条:

[点击文档链接](http://jquery.cuishifeng.cn/jQuery.Ajax.html) 

> #### **data**(Object,String)
>
> 发送到服务器的数据。将自动转换为请求字符串格式。GET 请求中将附加在 URL 后。查看 processData 选项说明以禁止此自动转换。必须为 Key/Value 格式。如果为数组，jQuery 将自动为不同值对应同一个名称。如 {foo:["bar1", "bar2"]} 转换为 "&foo=bar1&foo=bar2"。



也就是通过data对象的组装,可以应用在get和post方法中,如果是get方法,会自动帮我们处理好,拼接在url后面.这样对开发者和维护者来说,都十分友好了.



相信有些开发者知道这个点,也有些开发者遗漏了这一点.通过这个也告诉我们,当业务处理久了,不要忘了回头看看之前写的代码,优化一下,再耐心地重看一遍基础文档,会学到之前忽略掉遗忘掉的东西.