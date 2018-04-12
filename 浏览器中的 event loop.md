# 浏览器中的 event loop

浏览器的 event loop, 可以用一下这张经典图呈现出来:



![图片](/Users/toti/Documents/article/pic/event_loop_1.jpeg)

> event loop 只有一个, task queue 可以有多个



在 task 里面, 还有 macrotask 和 microtask 的区别:

*macrotask(宏任务):*

- script 脚本
- setTimeout\setInterval\setImmediate(记住3S)
-  I/O



*microtask:*

- process.nextTick
- promise
- Object.observe
- MutationObserver



关于它们的执行顺序:

script 脚本-> process.nextTick->promise->3S->I/O->Object.observe->MutationObserver



留待解决:

>  setTimeout\setInterval\setImmediate里面的执行顺序是个问题,如果有人知道,可以留言





