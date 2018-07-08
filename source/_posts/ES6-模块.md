---
title: ES6-模块
date: 2018-07-08 11:02:23
tags: [ES6,js]
---

> 一直在用ES6的模块机制, 现在系统学习下, 记录一下.

## ES6模块的特性

- 自动运行在严格模式下
- 是一个隔离的作用域, 不会污染全局
- 模块顶层作用域没有this, this为undefined
- 导出的才能被方法, 没有导出的相当于是模块私有的

## 模块的定义
 
  模块的定义和普通js代码并没有太大区别, 只是多了一个导出的操作. 

  ```javascript
  1. first.js
  export function fn1() {};
  export const a = 1;
  export class A {};

  // 可以导出 函数, 变量, 和类

  2. second.js
  function fn1() {}
  export fn1;

  // 可以这样直接导出引用

  3. third.js
  function fn1() {};
  export fn1 as fn2;

  // 可以用as指定导出的别名

  4. forth.js

  function fn1() {};
  const a = 1;
  export default fn1;
  export a;

  // 可以这样导出一个默认的东西

  ```

## 模块的导入
  模块的导入使用的是import语句, 分为几种情况:
  - 普通导入
  - 全部导入
  - 导入一部分
  - 定义导入别名
  - 导入默认导出的
  - 同时导入默认导出的和非默认导出的

  *默认的必须在非默认的前面*
  ```javascript
  import {fn1, a, A} from './first.js';
  import * as F from './first.js';
  import {fn1} from './first.js';
  import {fn1 as fn2} from './first.js';
  import fn1 from 'forth.js';
  import fn1, {a} from 'forth.js';

  ```
## 模块的加载顺序

1. 有三种方式可以将模块放到html中

```javascript
1. <script type="module" src = './a.js'></script>
2. 
<script type="module">
  import {fn1} from './first.js';

</script>
3. 通过worker
let worker = new Worder('a.js', {type:'module'});
区别,无法通过self.importScripts()加载其他模块

```
2. 这些模块会顺序加载, 如果有引入其他的模块则递归加载

3. 会被加上defer属性, 所以会在文档加载完成后顺序执行, 同样,如果有引入其他模块会递归执行

## 模块与脚本的对比
| 项目 | 模块 | 脚本|
|:---:|:---:|:----:|
|作用域|一个模块是一个作用域|全局作用域|
|严格非严格|默认就是严格模式|需要加use strict 才进入严格模式|
|引入方式|type为module|type为text/javasctipt|

## 一些值得注意的地方
- 模块导入的东西不能再改变引用
- 模块的导入路径开头必须为., ./或/, 或者直接是url,否则不能解析

------------------------

参考:

- <深入理解ES6>

