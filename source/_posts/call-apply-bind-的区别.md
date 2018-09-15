---
title: call apply bind 的区别
date: 2018-09-14 14:32:01
tags:
---
首先说一下 **call** 和 **apply** 的区别

**call** 和 **apply** 都是为了解决改变this的指向。作用都是相同的，只是传参的方式不同。除了第一个参数外，**call**可以接收一个参数列表，**apply**只接收一个参数数组。

```javascript
let a = {
  value: 1
}
function getValue (name, age) {
  console.log(name)
  console.log(age)
  console.log(this.value)
}
getValue.call(a, 'yck', '12')
getValue.apply(a, ['yck', '12'])
```
#### 模拟实现call和apply
可以从以下几点来考虑如何实现

- 不传如入第一个参数，那么默认window
- 改变this的指向，让新的对象可以执行该函数。那么思路是否可以变成给新的对象添加一个函数，然后在执行完后可以删除？
```javascript
Function.prototype.myCall = function () {
  var context = context || window
  // 给context添加一个属性
  // getVaule.call(a, 'yck', '12') => a.fn = getValue
  context.fn = this
  // 将 context 后面的参数取出来
  var args = [...arguments].slice(1)
  // getValue.call(a, 'yck', '12') => a.fn('yck', '12')
  var result = context.fn(...args)
  // 删除fn
  delete context.fn
  return result
}
```
以上是call的思路，apply的实现也类似
```javascript
Function.prototype.myApply = function (context) {
  var context = context || window
  context.fn = this

  var result
  // 需要判断是否存储第二个参数
  // 如果存在，就将第二个参数展开
  if (arguments[1]) {
    result = context.fn(...arguments[1])
  } else {
    result = context.fn()
  }

  delete context.fn
  return result
}
```
**bind** 和其他两个方法作用也是一致的，只是该方法会返回一个函数。并且我们可以通过 **bind** 实现柯里化。

同样的，我们也来模拟实现下 **bind**
```javascript
Function.prototype.myBind = function (context) {
  if (typeof this !== 'function') {
    throw new TypeError('Error')
  }
  var _this = this
  var args = [...arguments].slice(1)
  // 返回一个函数
  return function F() {
    // 因为返回了一个函数，我们可以 new F()，所以需要判断
    if (this instanceof F) {
      return new _this(...args, ...arguments)
    }
    return _this.apply(context, args.concat(...arguments))
  }
}
```