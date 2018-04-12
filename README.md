# Virtual DOM

> 第一次听说虚拟DOM这个名词是初识React这门技术，当时的我太菜（现在也菜），连实体DOM都说不清楚，更别说这么一个新的概念，潜意识里就觉得好难我肯定理解不了，就这样不了了之了。直到最近开始接触React项目，我想我有必要好好的去理解和认识React思想，故再次学习React的相关知识。

## 虚拟DOM由来

前端性能优化有很多方式，在将其他优化性能的方式都做到了极致，发现性能还是差强人意，这就意味着不能仅仅通过减少HTTP请求、使用CDN加速（内容分发网络），将CSS和JS放到外部文件中引用，CSS放头，JS放尾，压缩资源等方式优化性能。

我们都知道对DOM操作的代价是高昂的，这是网页应用中的一个性能瓶颈。DOM操作天生就慢，而DOM元素非常庞大，导致操作DOM的代价更大。前端工程师将前端工作进行抽象，就要是状态的维护和视图的更新，而更新视图和维护状态都需要DOM操作，所以解放DOM操作成为近年来前端框架的主要发展方向。

最开始我们直接操作DOM结构，这种方式复杂度高且兼容性不好；接着jQuery给我们提供了操作DOM的API(选择器)，解决了原始操作DOM的复杂性和兼容性问题，但前端开发人员并不满足于此，于是各种MVVM模式框架诞生了，例如AngularJS、avalon、Vue.js等，MVVM模式使数据双向绑定，不需要手动操作DOM，数据变化就可更新视图，改变视图数据也可自动更新数据，MVVM模式使得前端开发效率大大提高，可是这并没有很好得解决操作DOM的性能问题，于是兼顾开发效率和执行效率的方案诞生 —— ReactJS。而Virtual DOM（虚拟DOM）就是ReactJS提出一个新概念。

## 虚拟DOM 

DOM其实是浏览器引出的一组让Javascript操作HTML文档的API而已，在即时编译的时代，调用DOM的开销是很大的。

虚拟DOM的核心思想 —— 对复杂的文档DOM结构，提供一种方便的工具，进行最小化地DOM操作。

虚拟DOM不是原生的DOM，它是用js表示DOM结构的JavaScript对象，即模拟DOM树的JavaScript对象。这样虚拟DOM的执行完全都在Javascript引擎中，完全不会有操作DOM的开销。

## 原理

操作原生DOM简单来说就是直接重置innerHTML，这在大型的应用中，所有的数据都变了还算合理，但是，当只有一个数据发生变化而去重置整个innerHTML显然造成了巨大的浪费。

避开直接操作原生DOM，操作虚拟DOM就不会因极少的数据变化而去重置整个innerHTML，再通过对新旧虚拟DOM的对比可得到必要更新的DOM，从而达到节省开销的作用（DOM很慢，而JavaScript很快，用JavaScript对象很容易地表示一个DOM节点和diff出虚拟DOM的变化）。

![](/images/renderProcess.jpg)

比较innerHTML 和Virtual DOM 的重绘过程如下：

- innerHTML: render html string + 重新创建所有 DOM 元素
- Virtual DOM: render Virtual DOM + diff + 必要的 DOM 更新

和 DOM 操作比起来，js计算是非常便宜的。Virtual DOM render + diff 显然比渲染 html 字符串要慢，但是，它依然是纯 js 层面的计算，比起后面的 DOM 操作来说，依然便宜了太多。

## 实现

虚拟DOM的渲染模式的实现非常简单，就是将DOM结构使用JavaScript对象表示出来、新旧虚拟DOM的diff算法和如何根据diff结果对真实DOM做最小化的修改的实现。

### JS表示DOM结构


### diff虚拟DOM


### 对真实DOM最小化修改
