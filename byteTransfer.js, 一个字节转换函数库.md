# byteTransfer.js, 一个字节转换函数库



最近在处理着数据容量转换的需求,后端返回来一串数字,代表着容量的大小.于是写了一个工具方法,处理那么一个需求.



这个方法目前只满足了基本的需求,更丰富的转换,可待日后慢慢完善.代码如下:



```js
/* 
*  Author:Toti 
*/
function byteTransfer(byte) {

    var k = 1024;

    var sizes = ['B', 'K', 'M', 'G', 'T'];

    var i = 0;

    var byteTransfered;

    if (byte === 0) {

        i=0;

    }else{

        i=Math.floor(Math.log(byte)/Math.log(k));

    }

    byteTransfered = byte/Math.pow(k,i).toFixed(1)+sizes[i];

    return byteTransfered;

}

console.log(byteTransfer(1024));   // 输出1.0K
```

