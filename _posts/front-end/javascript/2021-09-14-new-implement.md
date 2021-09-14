---
layout: post
title: JS 中 new 的原理以及实现
---

一句话总结：执行 new 关键词后，总是返回一个对象，要么是构造函数加空对象原型生成的对象，要么是构造函数 return 的对象

## 原理
1. 创建一个新对象
2. 新对象原型指向构造函数的 prototype
3. 执行构造函数并传入参数
4. 如果构造函数结果是一个对象，则返回这个对象，否则返回第一步创建的新对象

## 简便实现
```
const _new = (fn, ...rest) => {
  const obj = Object.create(fn.prototype);
  const result = fn.call(obj, ...rest);
  return (typeof result === 'object') ? result : obj;
};
```

## 参考链接

https://cloud.tencent.com/developer/article/1526901
https://juejin.cn/post/7006232342398238733
https://juejin.cn/post/6844904082310692872
