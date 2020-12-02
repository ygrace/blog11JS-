# JS的执行时机
## 为什么以下代码会打印6个6
~~~javascript
let i = 0
for(i = 0; i<6; i++){
  setTimeout(()=>{
    console.log(i)
  },0)
}
~~~
setTimeout有延时机制.
举一个例子来解释，就像学生时期的吃饭打游戏，饭点的时候妈妈叫小明吃饭，而小明正在打游戏，大部分情况他会选择打完游戏再去吃饭，此处的马上去吃饭就相当于setTimeout，相当于走完循环之后，此时i已经变成了6，再console.log 打出6.

## 打印出0，1，2，3，4，5
~~~javascript
for(let i = 0; i<6; i++){
  setTimeout(()=>{
    console.log(i)
  },0)
}
~~~
这是因为let放在for循环中为代码块的作用域并且在每次循环中都人为的创建了一个保存i的值的变量,相当于下列代码,所以代码结果为0、1、2、3、4、5.

## 不用for let的解决方法
~~~javascript
for (var i = 0; i < 6; i++) { 
  (function(i){  
    setTimeout(function (){
      console.log(i); 
     },0); 
  })(i); 
}
~~~
立即执行函数，i在立即执行的函数中。