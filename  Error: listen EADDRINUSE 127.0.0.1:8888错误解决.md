#  Error: listen EADDRINUSE 127.0.0.1:8888错误解决

在开发过程中，突然出现了那么一个错误：

```js
Error: listen EADDRINUSE 127.0.0.1:8888
    at Object.exports._errnoException (util.js:1022:11)
    at exports._exceptionWithHostPort (util.js:1045:20)
    at Server._listen2 (net.js:1259:14)
    at listen (net.js:1295:10)
    at net.js:1405:9
    at _combinedTickCallback (internal/process/next_tick.js:77:11)
    at process._tickCallback (internal/process/next_tick.js:98:9)
```



其实 EADDRINUSE 的意思就是说明这个地址的这个端口号已经有在使用了。解决的办法有2个，一个是转换另外一个端口号，在构建命令的后面使用：

```js
... --port 8000
```

这样就可以换一个端口开发，而绕开这个坑。



如果是使用一些全局命令开发，无法绕过这个端口号，那么我们可以查杀这个正在使用的端口号。由于本人使用的是MAC，所以只提供MAC的指令了,打开terminal终端：

```js
//首先输入查询指令
sudo lsof -i :8888
COMMAND   PID    USER   FD      TYPE             DEVICE                      SIZE/OFF      NODE       NAME

java              716      a           313u   IPv6               0x1111111111111     0t0                    TCP        *:cslistener (LISTEN)

//然后根据PID杀进程：
sudo kill -9 716
```



