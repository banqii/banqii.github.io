---
layout: post
title: JS 中 new 的原理以及实现
---

一句话总结：执行 new 关键词后，总是返回一个对象，要么是构造函数加空对象原型生成的对象，要么是构造函数 return 的对象

## 原理
1. 在内存中创建一个新对象
2. 这个新对象内部的`[[Prototype]]`特性被赋值为构造函数的 prototype 属性。
3. 构造函数内部的 this 被赋值为这个新对象(即 this 指向新对象)
4. 执行构造函数内部的代码(给新对象添加属性)
5. 如果构造函数返回非空对象，则返回该对象;否则，返回刚创建的新对象

## 实现
```
const _new = function (fn, ...regs) {
  const o = {};
  o.__proto__ - fn.prototype
  fn = fn.bind(o)
  const res fn(...regs)
  return (typeof res === 'object') ? res : o
}
```

## 简便实现
```
const _new = function (fn, ...regs) {
  const o = Object.create(fn.prototype);
  const res = fn.call(obj, ...regs);
  return (typeof res === 'object') ? res : o;
};
```

## 参考链接

https://cloud.tencent.com/developer/article/1526901
https://juejin.cn/post/7006232342398238733
https://juejin.cn/post/6844904082310692872
