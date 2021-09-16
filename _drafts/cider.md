---
layout: page
title: About
permalink: /about/
---

// 生成SKU
// 已知规格数据
const spu = 'AB1234567';
const specList = [ 
 ["a1", "a2", "a3"],
 ["b1", "b2"], 
 ['c1', 'c2'],
 ['d1', 'd2', 'd3'],
];
/** 
  输出结果：
 AB1234567-red-XL-a1-b1;
 AB1234567-red-XL-a1-b2;
 AB1234567-red-XL-a2-b1;
 AB1234567-red-XL-a2-b2;
 AB1234567-red-S-a1-b1;
 AB1234567-red-S-a1-b2;
 AB1234567-red-S-a2-b1;
 AB1234567-red-S-a2-b2;
 AB1234567-yellow-XL-a1-b1;
 AB1234567-yellow-XL-a1-b2;
 AB1234567-yellow-XL-a2-b1;
 AB1234567-yellow-XL-a2-b2;
 AB1234567-yellow-S-a1-b1;
 AB1234567-yellow-S-a1-b2;
 AB1234567-yellow-S-a2-b1;
 AB1234567-yellow-S-a2-b2;
  ....
*/
// 请完善如下createSKU函数及注释信息以符合输出结果;
/** 
* @param
* @return 
*/
function createSKU(){
  const result = []
  const fn = (i) => {
    const line = specList[i]
    if (!line) {
      console.log(`AB1234567-${result.join('-')}`)
      return
    }

    for (let j = 0; j < line.length; j++) {
      result.push(line[j])
      fn(i + 1)
      result.pop()
    }
  }

  fn(0)
}

createSKU()

二面：

http 如何实现可靠连接

tcp 滑动窗口

vue diff 算法

单链表，及单链表的部分反转
function Node(value) {
  this.value = value;
  this.next = null
}

let head = null;
function create() {
  head = new Node(1)
  let p = head;
  for (let i = 2; i < 10; i++) {
    p.next = new Node(i);
    p = p.next;
  }
}

function reverse(si, ei) {
  let p = head;
  let i = 0;
  let startNode = null;
  let endNode = null;
  while(p !== null) {
    i++;
    if (i === si) {
      startNode = p;
    }

    if (startNode) {
      const temp = p.next;
      const endNode.next = p

      if (i === ei) {
        startNode.next.next = p.next;
        startNode.next = p;
      }
    }
    p = p.next;
  }
}

function print() {
  let p = head
  while(p) {
    console.log(p.value)
    p = p.next
  }
}

create();
head.value
print();
reverse(1, 3);
head.value
print();



