---
layout: post
title: 浏览器缓存策略
---

一句话总结：使用 header 中的字段来控制缓存的使用；老字段是 Expires 记录绝对时间，新字段 Cache-Control 配合各种选项，记录的是相对值；协商缓存是本地缓存文件没有过期就用缓存的，缓存过期了就带着缓存标识询问服务器有没有过期，过期了就重新请求，没过期就用缓存的

[HTTP缓存流程图](/assets/images/HTTP缓存流程图.png)


## 参考链接

https://juejin.cn/post/6844903593275817998
https://segmentfault.com/a/1190000021716418
