---
title: node.js基本使用
tags: [node.js]
categories: [node.js]
---
# Node.js

## 定义

基于v8引擎的JavaScript运行环境



## 背景

浏览器渲染引擎（内核）工作的过程 

![img](https://s2.loli.net/2022/08/07/WhipLaeEOkoBfxQ.png)

当遇到JS标签会停止解析html去执行JS

不会异步加载JS，因为浏览器不希望频繁的去生成新的DOM树



JS是一门高级语言，需要JS引擎进行解释

 

V8引擎

![image-20220517115219960](https://s2.loli.net/2022/08/07/eQGj7RcHWnqy9EM.png)

  





node.js和浏览器的区别

![image-20220623144143934](https://s2.loli.net/2022/08/07/rpZf9ATvCOmdIHB.png)



## 使用

​	REPL 一个交互式的编程环境，类似chrome F12

​	

传递参数

~~~javascript
node xx.js 参数1，参数2;		//传参
console.log(process.argv) //获取参数
~~~



## CommonJS

cjs 是一个规范，最初叫ServerJS

Node中实现cjs的本质就是对象引用赋值

module. exports导出，require导入

exports是一个全局模块对象，默认为空

> 将一个对象赋值给另一个对象其实是赋值了内存地址，此时这两个对象都可以通过保存的内存地址对内存数据进行更改，一个对象属性的更改就必然会引起另一个对象属性的变化



~~~js
module.exports = { xxx }//创建了新对象，所以不共享地址
module.exports.name = name //共享内存地址
~~~



## exports和module.exports的区别

Common.js中是没有module.expots这个概念的

但是为了实现模块的导出，Node中使用了Module，每一个模块都是Module的一个实例。

所以在Node中真正用于导出的是module.exports

在node内部中做了处理，让module.exports = exports

### 加载过程

==同步加载==

~~~javascript
require(x)
console.log('111')
//先执行x，再执行111
~~~



1.模块第一次被引入时，里面的代码会被执行一次

2.多次引入会缓存，最终只运行一次



> 为什么只会加载运行一次呢?
>
> 因为每个模块对象module都有一 个属性: loaded.
>
> 为false表示还没有加载,为true表示已经加载; 



![image-20220630212731829](https://s2.loli.net/2022/08/07/W9iOvG4NEsDeytP.png)

输出顺序：main, a, c, d, e, b

node采用 的是图结构的深度优先算法



## ES Module

 import导入, export导出



==export和export default的区别==

> 1. **export** 和 **export default** 都可用于导出常量、函数、文件、模块等 ，
>
> 2. 你可以在其它文件或模块中通过 **import** 将其导入，以便能够对其进行使用
>
> 3. 在一个文件或模块中，**export**、**import**可以有多个，**export default**仅有一个
>
> 4. 通过**export**方式导出，在导入时要加{ }，且不能自定义名字，**export default**不用加{ }，且可以自定义名字
>
>    https://blog.csdn.net/QXHBK/article/details/122285191

### 加载过程

==异步加载==



模块环境记录，单项绑定变量名

![image-20220630231055883](https://s2.loli.net/2022/08/07/3REb1X9ATm7QVGf.png)



通常情况下，==CJS不能加载ES Module==

因为CJS是同步加载，ES Module必须经过静态分析等操作



多数情况下，==ES Module可以加载CJS==

加载时会将其module.exports导出的内容作为default导出方式来使用



## 内置模块 

### path

不同操作系统的分隔符不同，为了兼容，推荐使用path内置模块

~~~javascript
const path = require('path')
const a = '/User/man'
const b = 'abc.txt'
const filepath = path.resolve(a, b)
~~~

resolve和join的区别

1. resolve会生成绝对路径，而join只是返回当前连接的路径。
2. resolve会以最后出现的 ‘/’为起点，作为根路径，忽略前面的片段，而join不会。



### fs（File System）



### events

