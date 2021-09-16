---
layout: page
title: About
permalink: /about/
---



1. 实现发布订阅模式

// 实现一个发布订阅模式 on off emit once
// var eventbus = new EventBus()
// eventbus.on('click', fn)
// eventbus.off('click', fn)
// eventbus.emit('click', 123)
// eventbus.once('click2', fn2)

function EventBus() {
  const events = {};
  
  this.on = function on(name, fn) {
    events[name] = events[name] || [];   
    events[name].push(fn)
  }

  this.off = function off(name, fn) {
    const fns = events[name]
    if (!fns) return;
    let removes = [];
    for (let i = 0; i < fns.length; i++) {
      if (fn === fns[i] || fn === fns[i].fn) {
        removes.push(i)
      }
    }
    for (let i = removes.length - 1; i >= 0; i--) {
      if (fns[removes[i]]) {
        fns.splice(removes[i], 1);
      }
    }
  }

  this.emit = function emit(name, ...params) {
    let fns = events[name]
    if (!fns) return;
    fns = [...fns];
    for (let i = 0; i < fns.length; i++) {
      if (typeof fns[i] === 'function') {
        fns[i](...params);
      } else if (fns[i]._once === true) {
        if (typeof fns[i].fn === 'function') {
          fns[i].fn(...params);
        }
        fns[i]._once = false;
      }
    }
  }

  this.once = function once(name, fn) {
    events[name] = events[name] || [];   
    events[name].push({
      _once: true,
      fn
    })
  }
}

2. 数组变成 children 树，然后，删除评论，有子评论时不可删除
// 原始数据
const data = [
  {
     id: 10002,
     content: '该评论已删除',
     author: '小B',
     createAt: 1618389235,
     replyId: 0,
     status: 1
  },
  {
     id: 10007,
     content: '该评论已删除',
     author: '小7',
     createAt: 1618389335,
     replyId: 10006,
     status: 1
  },
  {
     id: 10006,
     content: '该评论已删除',
     author: '小6',
     createAt: 1618389235,
     replyId: 10002,
     status: 1
  },
  {
     id: 10004,
     content: '哈哈我也是',
     author: '小D',
     createAt: 1618389535,
     replyId: 10005,
     status: 0
  },
  {
     id: 10005,
     content: '的确不错，有学习到',
     author: '小C',
     createAt: 1618389335,
     replyId: 10002,
     status: 0
  },
  {
     id: 10001,
     content: '这写的真好，我也要学习',
     author: '小F',
     createAt: 1618389035,
     replyId: 0,
     status: 0
  },
  {
     id: 10003,
     content: '这写的真好，我也要学习到了一些东西真的是很干货啊',
     author: '小A',
     createAt: 1618389335,
     replyId: 0,
     status: 0
  },
]

// {
//   id: 10002,
//   content: '该评论已删除',
//   author: '小B',
//   createAt: 1618389235,
//   replyId: 0,
//   status: 1
// },

const tree = [];
function getChildren(replyId, parent) {
  const children = data.filter((item) => {
    return item.replyId === replyId;
  })
  parent.children = children;

  children.forEach((item) => {
    getChildren(item.id, item);
  })
}

getChildren(0, tree)





