---
layout: post
title: 实现 Promise 中的方法
---

### Promise.all()
Promise.all() 方法接收一个 promise 的可迭代的（Array，Map，Set）输入，并返回一个 Promise 实例。这个 Promise 的 resolve 回调的参数是所有 promise 的 resolve 的数组，reject 回调的参数是第一个 reject 的 promise 的抛错信息

使用：
```
promise.all([promise1, promise2, promise]).then(([res1, res2, res3]) => {
}, (err) => {})
```

1. 输入是一个 promise 可迭代对象（[判断是否可迭代](/front-end/javascript/2021-09-10-iterator#判断对象是否可迭代)）
2. 输出一个 Promise 实例
   1. resolve 态：返回与输入顺序一致的结果数组
   2. reject 态：返回第一个 reject 的异常信息

实现：
```
static all(promises) {
  return new Promise((resolve, reject) => {
    let ret = []
    let count = 0
    for(let i = 0; i < promises.length; i++){
      promises[i].then((res) => {
        // 与 promise.race 的主要区别
        count++
        ret[i] = res
        if(count === promises.length){
          resolve(ret)
        }
      }, (err) => {
         reject(err)
      })
    }
  })
}
```

同步 promise：
队列中的 promises 依次执行

```
syncAll(promises) {
  return new Promise((resolve, reject) => {
    const ret = []

    const fn = () => {
      const promise = promises.shift()

      if (promise) { // 还能取到就递归调用
        promise.then((res) => {
          ret.push(res)

          fn() // 递归调用 promise
        },
        (err) => {
          reject(err)
        })
      } else { // 没有了就返回结果
        resolve(ret)
      }
    }
    fn()
  })
}
```

### Promise.allSettled()

### Promise.any()

### Promise.race()
Promise.race() 和 Promise.all() 的输入相同，只不过只返回最先 resolve 或者 reject 的 promise

使用：
```
Promise.race([promise1, promise2]).then((value) => {
  console.log(value);
});
```

实现：
```
static race(promises) {
  return new Promise((resolve, reject) => {
    for(let i = 0; i < promises.length; i++){
      promises[i].then((res) => {
        // 有一个 promise resolve，整个队列都 resolve
        resolve(res)
      }, (err) => {
        reject(err)
      })
    }
  })
}
```

### Promise.resolve()
```
static resolve(value) {
  return new Promise((resolve, reject) => resolve(value))
}
```
### Promise.reject()
```
static reject(reason) {
  return new Promise((resolve, reject) => reject(reason))
}
```
### Promise.prototype.then()
```

```
值得注意的是上面的方法都是 Promise 上的静态方法，then、catch 和 finally 则是原型上的方法
### Promise.prototype.catch()
```
catch(onRejected) {
  return this.then(null, onRejected)
}
```
then 有两个参数，一个成功一个失败，但是在参数位置写两个方法容易混淆，故在实际应用中，基本都是 then 处理成功，catch 处理失败

### Promise.prototype.finally()
```

```
