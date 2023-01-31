---
layout: post
title: 公平洗牌算法（Knuth-Shuffle）
---

# 问：设计一个公平的洗牌算法

## 一、洗牌
随机抽取数组中的一个元素，放入另一个数组即可

```
function shuffle (arr) {
    const ret = []
    while (arr.length > 0) {
        const r = parseInt(Math.random() * arr.length)
        ret.push(arr.splice(r, 1)[0])
    }
    return ret
}

shuffle([1, 2, 3])
```

## 二、Sort 洗牌
利用 Array 的 sort 方法，对交换函数进行改造，每次有 1/2 的机会交换位置，来实现随机
```
const shuffle = arr => arr.sort(() => 0.5 - Math.random())

shuffle([1, 2, 3, 4, 5]) // [1, 2, 5, 3, 4]
```

## 三、公平洗牌（Knuth-Shuffle）
从数组最后一位向第一位循环，每次随机取一个当前位置及之前的项，与当前位置的项替换

这样相当于每个项被放到每个位置上的概率都为 1/n ，以实现公平

```
var shuffle = function(arr) {
    var n = arr.length;
    for (let i = n-1; i > 0; i--) {
        var r = parseInt(Math.random() * (i + 1));
        [arr[r], arr[i]] = [arr[i], arr[r]];
    }
    return arr;
}
shuffle([1, 2, 3, 4, 6])
```

## 参考链接

1. https://cloud.tencent.com/developer/article/1462951
2. http://www.xiongdalin.com/2021/01/25/array-shuffle/
