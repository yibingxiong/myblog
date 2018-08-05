---
title: redux学习笔记
date: 2018-08-05 21:30:44
tags:
---

# 四个东西

1. store

一个存放应用所有状态的地方

2. state
应用的状态, 整体是个对象, 像这样  

```javascript
{
  todos: [{
    text: 'Eat food',
    completed: true
  }, {
    text: 'Exercise',
    completed: false
  }],
  visibilityFilter: 'SHOW_COMPLETED'
}
```

3. action

一个用于描述发生了某件事的对象, 像这样

```javascript
{type:'type', id:1...}
```
4. reducer
用于描述一个事件发生后状态应该如何改变, 是一个纯函数. 根据action的type和参数得到新的state并return

```
reducer(state, action) {
  return newState;
}
```

------------------
## 关于这几个的理解

![redux几个概念的理解](/2018/08/redux学习笔记1.png)


* 几个方法
