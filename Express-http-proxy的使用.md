# Express-http-proxy的使用

前言，最近开发的时候，碰到了个问题。平常我们的开发的时候，应该都会面对三个环境，一个是本地环境，一个是测试环境，一个是线上环境。本地环境开发的时候，有时候本地mock api的数据，也有时候通过代理去读测试环境或者线上环境的api，那么proxy这个时候就可以派上用场了



## Express-http-proxy

这里付上它的[github](https://github.com/villadora/express-http-proxy) ，一些简单的安装使用，仓库里面的readme其实已经说得很清楚了，在此不再赘诉。我反倒想介绍下我在实战中，遇到的一些问题。

```js

var express = require('express');
var app = express();

//路由管理
app.use('/reading', proxy);

//...
```



当我们在当前host下，跳转/reading这个页面的时候，正常情况下，它是读取本地服务器的接口的。我们可以使用这个proxy参数，进行测试环境和线上环境的切换。

```js

var express = require('express');
var app = express();
var proxy = require('express-http-proxy');

var proxy = proxy('www.test.demo.com', {
    https: true,
  	//使用https协议
    proxyReqPathResolver: function(req, res) {
        return req.originalUrl;
    },
  	//请求的路径，可提供修改
    proxyReqOptDecorator: function(proxyReqOpts, srcReq) {
       proxyReqOpts.headers['Referer'] = 'www.test.demo.com';
    },
  	//请求头的信息，可提供修改
    userResHeaderDecorator(headers, userReq, userRes, proxyReq, proxyRes) {
      //
      return headers;
    }
  	//响应头信息也提供修改
});
  
//路由管理
app.use('/reading', proxy);


```

当我们使用了这个proxy之后，请求www.demo.com/reading,它会进行代理转发，变成请求www.test.demo.com/reading这个网址。

而且，它只在路由是/reading的时候，才会进行这样的代理，如果请求www.demo.com/writing,它就不会改变。

而且proxy里面还提供修改，协议，host，请求头，响应头这些重要信息。



我把它介绍给大家，更详细的，大家可以进一步去探讨下。



