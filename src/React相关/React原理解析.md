# React 原理解析

React 本身只是一个 DOM 的抽象层，使用组件构建虚拟 DOM。

## 什么是 虚拟 DOM(Virtual DOM)？

Virtual DOM 是一种编程概念。用 js 对象来描述真实的DOM节点，存在内存当中，还需要通过 React DOM 这样的类库使之与真实的 DOM 保持同步，同步的这一过程称为 “协调”。协调的核心就是 diff 算法。

在两次更新之间通过 diff 算法来使 DOM 操作达到最少，这里就是优化的点。

## 为什么需要用虚拟 DOM（Why?）

DOM 对象非常庞大，所以它操作很慢（下面是一个空 div 的属性列表）；轻微的操作都可能导致页面重新排版，非常耗费性能。相对于 DOM 对象，js 对象处理起来更快，而且更简单。通过 diff 算法对比新旧 vDOM 之间的差异，可以批量地，最小化地执行 DOM 操作，从而提高性能。

虚拟DOM节点只会将定义时使用到的属性添加到虚拟对象上，这样对比时就只对比这些属性。

![image-20210421154137659](images/image-20210421154137659.png)

## 它用在哪里呢(where)？

React 中使用 jsx 来描述视图，通过 babel-loader 转译后他们变为 React.createElement 的形式，该函数将生成 vdom 来描述真实 dom。如果将来状态变化，vdom 将作出相应变化，再通过 diff 算法来对比新旧 vdom 区别，最终作出 dom 操作。



## 什么是 React Fiber?

Fiber 是 React16 中新的协调引擎，它的主要目的是使 Virtual DOM 可以进行增量式渲染。

## JSX

jsx 其实就是 `React.createElement` 方法的语法糖。

为什么需要用 jsx?

- 开发效率：使用 jsx 编写模版简单高效；
- 执行效率：JSX 编译为 javascript 代码后进行了优化，执行更快；
- 类型安全：在编译过程中就能发现错误。

原理：babel-loader 会预编译 jsx 为 React.createElement

与 Vue 的异同：

- React 中虚拟 dom+jsx 的设计是一开始就有，vue 则是演进过程中才支持的；
- jsx 本来就是 js 扩展，转移过程简单直接得多，vue 把 template 编译为 render 函数的过程需要复杂的编译器来转换字符串 - AST - JS函数字符串。



