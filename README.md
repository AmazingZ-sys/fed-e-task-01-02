#### 练习一：

最终结果是10，全局中设置a为空数组，然后循环往数组中存入函数，此时存入的是函数体。在循环中变量 i 使用 var 关键字进行声明，不识别局部作用域，在循环完成之后变量 i 的值为10，调用函数输出的 i 的值也为 10

#### 练习二：

执行结果为报错，首先声明全局变量 temp ，之后执行 if 中的语句，先执行 console 时会在本身的作用域中找 temp 变量，找不到时才会沿着作用域链去全局执行环境中找，然后发现当前的作用域中有 temp 的声明，但是 temp 的声明在 console 语句之后，使用 let 关键字声明的变量不存在变量提升，所以报错

#### 练习三：

```javascript
var arr = [12, 34, 32, 89, 4]
let min = Math.min(...arr)
```

#### 练习四：

- var 关键字声明变量时存在变量提升（可以先使用后声明），可以重复声明，不识别块级作用域，可以先声明不赋值
- let 关键字声明的变量不存在变量提升，不能重复声明，可以识别块级作用域，可以先声明不赋值
- const 关键字声明的变量不存在变量提升，不能重复声明，声明之后值不能进行改动，可以识别块级作用域，不能在声明时不进行赋值

#### 练习五：

输出结果为20，在函数 fn 中输出 this.a 先找到当前的 this 指向，在函数调用 fn() 之前有 obj. 表示当前的 fn 函数是由 对象 obj 调用的，谁调用的函数内部的 this 就指向谁，没有调用者是指向 全局对象window 所以 this.a 指的是 obj.a

#### 练习六：

Symbol 表示一种独一无二的符号，我们可以使用 symbol 来给对象添加一个独一无二的标识符，避免同名对象的属性被污染，还可以给对象添加私有属性

#### 练习七：

浅拷贝就是只复制了值（即对象的引用），用浅拷贝拷贝的对象和源对象指向相同的内存地址，修改其中一个时另一个也会发生改变

深拷贝不止对对象进行值的拷贝，还重新开辟一块内存空间用于新对象的存储，修改其中一个对象时不会影响到另一个对象

#### 练习八：

typescript是JavaScript的超集，typescript代码编译之后其实也就是JavaScript代码，它在JavaScript的基础之上扩展了一些新特性（强大的类型系统），typescript补足了JavaScript作为弱类型语言的不足，使项目开发更加规范

#### 练习九：

优点：非常强大的类型系统，弥补了JavaScript作为弱类型语言的不足；通过类型系统的引入，能使我们在开发阶段就能在代码上看到错误，而不必和JavaScript一样等到编译时候才报错；因为有类型系统的引入，在协作开发上代码更加统一易读，有利于后期的项目维护

缺点：相比JavaScript，增加了学习成本（特别对于习惯JavaScript的各种隐式类型转换的人来说很不容易上手）；对于周期短的小型项目来说，增加开发成本，付出和收货不成正比

#### 练习十：

引用计数法通过引用计数器来对变量进行一个引用计数维护，在一个变量声明之后就开始计数，引用关系改变时即时修改引用数（多一个引用时引用数 + 1 ，少一个引用时引用数 -1），直到引用数为0时此变量占用的内存将释放回收

优点：当引用数为0时立即将垃圾进行立即回收；我们的程序运行内存是有上限的，内存占满时候程序就无法继续向下执行，因为引用计数算法实时回收引用数为0的变量，垃圾能得到及时回收，所以能最大限度的减少程序的暂停

缺点：因为是通过引用数来决定变量是否回收，对于循环引用的对象此算法不能即时回收；因为维护了一个引用计数器来监控变量的引用数是否需要修改，所以资源开销较大

#### 练习十一：

标记整理法分为标记和整理两个阶段，首先会遍历所有对象来对活动对象进行标记，然后再遍历所有对象，将有标记和没有标记的对象分开，整理内存空间使内存地址连续，之后配合标记清除算法对没有标记的对象进行内存的回收释放

#### 练习十二：

首先新生代存储区会将内存分为两个等大小的空间 from（使用空间） 和 to（空闲空间），这时候先对活动对象进行标记然后存储在 from 空间中，接着对 from 空间内的活动对象进行内存的整理并复制到 to 空间中，最后将 from 对象中的内存进行释放回收，再将 from 空间和 to 空间进行互换以待下一次的新生代存储区回收

#### 练习十三：

增量标记的算法主要用途是提升我们的垃圾回收效率，用在老生代存储区的垃圾回收中，因为我们的垃圾回收操作是会阻塞程序的执行的，我们不能长时间的进行垃圾回收而不管程序的执行，这会造成程序卡顿，增量标记算法就是将我们的程序执行中垃圾回收操作拆分成几个阶段在程序执行的空档期分别执行（我理解就跟JavaScript中的异步操作差不多，微任务和宏任务交替执行）