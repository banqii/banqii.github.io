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
