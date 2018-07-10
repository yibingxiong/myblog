---
title: ES6-代理反射
date: 2018-07-08 12:43:55
tags: [ES6, js]
---

> 学习了ES6中的代理. 代理赋予了开发者访问js底层的一些东西的能力, 还是挺好玩的, 不过有点多, 对比一下.

1. 一些比较

|比较项|反射方法|Object的方法|备注|
|---|---|---|---|
|set|Reflect.set(trapTarget, key, value, redeiver)|-|拦截为对象属性赋值|
|get|Reflect.get(trapTraget, key, receiver)|-|拦截读取对象属性|
|has|Reflect.has(trapTarget, key)|-|拦截in操作|
|delete|Reflect.deleteProperty(trapTarget,key)|-|拦截delete操作|
|setPrototypeOf|Reflect.setPrototypeOf(trapTarget, proto) 底层操作,返回Boolean表示操作是否成功,成功则true,失败则false|Object.setPrototypeOf(trapTarget,proto) 上层操作, 操作失败直接抛出错误|拦截setPrototypeOf操作|
|getPrototypeOf|Reflect.getPrototypeOf(trapTarget) 参数不是对象直接报错|Object.getPrototypeOf(trapTarget),参数不是对象先转换成对象|拦截getPrototypeOf操作|
|preventExtensions|Reflect.preventExtensions(trapTarget),参数不是对象报错,参数是对象返回true或false|Object.preventExtensions(trapTarget),返回参数|拦截preventExtensions|
|isExtensible|Reflect.isExtensible(target) 非对象直接报错|Object.isExtensible(target) 非对象返回false|拦截isExtensible|
|defineProperty|Reflect.defineProperty(trapTarget, key, descriptor) 返回true或false|Object.defineProperty(trapTarget, key, descriptor) 出错时报错|拦截defineProperty|
|getOwnPropertyDescriptor|Refect.getOwnPropertyDescriptor(trapTarget,key) 非对象报错|Object.getOwnPropertyDescriptor(trapTarget,key) 非对象转换成对象|enumerable,configurable,value,writable,get,set|
|ownKeys|Reflect.ownKeys(target)|Object.keys(),Object.getOwnPropertyNames(),Object.assign(),Object.getOwnPropertySymbols()|返回数组就好|
|apply|Reflect.apply(trapTarget,thisArg,argumentList)|-|拦截函数调用|
|construct|Reflect.construct(target,argumentList)|-|拦截new调用|


2. 创建可撤销的代理

```javascript
Proxy.revocable();  => {proxy, revoke}

调用revoke()即可撤销
```
