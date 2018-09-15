---
title: Map 、FlatMap 和 Reduce
date: 2018-09-15 10:39:14
tags:
---
`Map` 作用是生成一个新的数组，遍历原数组，将每个元素拿出来做一些变换后 `append` 到新的数组中

```javascript
[1, 2, 3].map((v) = > v + 1)
// -> [2, 3, 4]
```
`Map` 有三个参数，分别是当前索引元素，索引，原数组。
```javascript
['1', '2', '3'].map(parseInt)
//  parseInt('1', 0) -> 1
//  parseInt('2', 1) -> NaN
//  parseInt('3', 2) -> NaN
```
FlatMap 和 map 的作用几乎是相同的，但是对于多维数组来说，会将原数组降维，可以将 FlatMap 看成是 map + flatten 目前该函数再浏览器中还不支持。
```javascript
[1, [2], 3].flatMap((v) => v + 1)
// -> [2, 3, 4]
```
如果想将一个多维数组彻底降维，可以这样实现
```javascript
const flattenDeep = (arr) => Array.isArray(arr)
  ? arr.reduce( (a, b) => [...a, ...flattenDeep(b)] , [])
  : [arr]

flattenDeep([1, [[2], [3, [4]], 5]])
```
reduce 的作用是数组中的值结合起来，最终得到一个值
```javascript
function a() {
  console.log(1)
}
function b() {
  console.log(2)
}
[a, b].reduce((a, b) => a(b()))
```