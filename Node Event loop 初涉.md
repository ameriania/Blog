# Node Event loop 初涉



Event loop在 node 中和在浏览器中实现是不太一样的.下面,只是简单地介绍下 event loop 的六个阶段,待深入了解后,再分享更仔细的内容.



- timers: 里面执行 setTimeout 和 setInterval 中的 callback 函数
- I/O :执行上轮遗留的I/O callback
- idle,prepare: 内部的一个阶段
- poll:执行 I/Ocallback
- check: 执行 setImmediate 的 callback
- close callback: 执行 close 事件的 callback



除了上述的六个阶段外,还有 process.nextTick() 也会在每个阶段结束后,都执行一次.



