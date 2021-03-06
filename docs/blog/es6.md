# ES6

## 首先我们要知道什么是 ES6?

2011 年，ECMAScript 5.1 版发布后，就开始制定 6.0 版了。因此，一般情况下 ES6 这个词就是指 JavaScript 语言的下一个版本。

是，因为这个版本引入的语法功能太多，而且制定过程当中，还有很多组织和个人不断提交新功能。事情很快就变得清楚了，不可能在一个版本里面包括所有将要引入的功能。常规的做法是先发布 6.0 版，过一段时间再发 6.1 版，然后是 6.2 版、6.3 版等等。

但是，标准的制定者不想这样做。他们想让标准的升级成为常规流程：任何人在任何时候，都可以向标准委员会提交新语法的提案，然后标准委员会每个月开一次会，评估这些提案是否可以接受，需要哪些改进。如果经过多次会议以后，一个提案足够成熟了，就可以正式进入标准了。这就是说，标准的版本升级成为了一个不断滚动的流程，每个月都会有变动。

标准委员会最终决定，标准在每年的 6 月份正式发布一次，作为当年的正式版本。接下来的时间，就在这个版本的基础上做改动，直到下一年的 6 月份，草案就自然变成了新一年的版本。这样一来，就不需要以前的版本号了，只要用年份标记就可以了。

ES6 的第一个版本，就这样在 2015 年 6 月发布了，正式名称就是《ECMAScript 2015 标准》（简称 ES2015）。2016 年 6 月，小幅修订的《ECMAScript 2016 标准》（简称 ES2016）如期发布。

一种新的语法从提案到变成正式标准，需要经历五个阶段。每个阶段的变动都需要由 TC39 委员会批准。

- Stage 0 - Strawman（展示阶段）
- Stage 1 - Proposal（征求意见阶段）
- Stage 2 - Draft（草案阶段）
- Stage 3 - Candidate（候选人阶段）
- Stage 4 - Finished（定案阶段）

## Let

这个可以先看一道经典的面试题目

```js
var a = []
for (var i = 0; i < 10; i++) {
  a[i] = function() {
    console.log(i)
  }
}
a[6]()
//10
```

上面代码中，变量 i 是 var 命令声明的，在全局范围内都有效，所以全局只有一个变量 i。所以`a[6]()`执行的`for`循环已经结束，所以会输出循环之后的最终值，就是`10`。解决方案也很简单，就是将 `var`改成`let`。

```js
var a = []
for (let i = 0; i < 10; i++) {
  a[i] = function() {
    console.log(i)
  }
}
a[6]()
// 6
```

它为什么就可以呢，我们可以将它转成 ES5 的代码你就有更直观的感受了。

```js
var a = []

var _loop = function _loop(i) {
  a[i] = function() {
    console.log(i)
  }
}

for (var i = 0; i < 10; i++) {
  _loop(i)
}
a[6]()
```

另外，for 循环还有一个特别之处，就是设置循环变量的那部分是一个父作用域，而循环体内部是一个单独的子作用域。

```js
for (let i = 0; i < 3; i++) {
  let i = 'abc'
  console.log(i)
}
// abc
// abc
// abc
```

这表明函数内部的变量 i 与循环变量 i 不在同一个作用域，有各自单独的作用域。
