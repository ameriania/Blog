# ajax发送json数据到后端的坑



最近在处理一项很简单的需求,后端新增了一个接口,接受数据的格式是json格式.但是原有的方法,是基于ajax改造的,发送的数据是不支持json的.那么这个时候需要对方法进行一点改造,让它适应新的接口.



发送数据到服务端那边,方法可以写成:

```js
var DemoAjax = require('DemoAjax');//原有的请求方法

DemoAjax({
	type:'post',
  	url:'demo/api',
  	data:JSON.stringify({
    	name:'toti',
      	age:'18'
  	}),
  	processData:false
})

return DemoAjax;
```



那么这个方法就是已经对json数据友好的了.里面有个参数processData,它的作用是,在发送数据到服务器的时候,会被转化成查询字符串的形式,那么通过设置false,来禁止这种自动转化.