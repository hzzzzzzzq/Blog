## this-指向

### 普通函数的 this 指向

```javascript
let obj = {
  num: 10,
  fun: function () {
    console.log(this.num);
    return this.num;
  },
};
obj.fun(); // 10
let newFun = obj.fun;
newFun(); // undefined
```

上面一个输出 `10` ，`this` 指向的是 **最后调用它的对象**，在上面函数中 `this` 指向了 `obj` 对象，所以可以取到 `this.num` 。

而在 `newFun` 中输出为 `undefined`， `fun` 函数在 `obj` 对象中作为方法被引用，但是在赋值给 `newFun` 之后，`newFun` 的执行仍然是在 `window` 的全局环境中，因此指向的是 `window` 对象，而在 `window` 对象中没有定义 `num`。因此输出 `undefined`，它们相当于：

```javascript
console.log(window.num);
```

我们在代码顶部添加一行

```javascript
// this.js
window.num = 0; // 设置 window 对象来验证
let obj = {
  num: 10,
  fun: function () {
    console.log(this.num);
    return this.num;
  },
};

obj.fun(); // 10

let newFun = obj.fun;
newFun(); // 0
```

当然在这里我们需要建一个 `html` 文件来引入 `js` 了，然后在 **浏览器** 中执行，如果只是 `js` 在 `node` 中运行是不行的。

```html
// index.html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta http-equiv="X-UA-Compatible" content="IE=edge" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Document</title>
  </head>
  <body>
    <script src="./this.js"></script>
  </body>
</html>
```

那么现在输出的值就是我们设置的 `window.num` 了，也就是 `100`。

> 注意： **在执行函数时，如果函数中的 this 是被上一级的对象所调用，那么 this 指向的就是上一级的对象；否则指向全局环境。**

所以在普通函数中，有一个说法，就是 **谁调用，那就指向谁**。

事实上，调用函数会创建新的属于函数自身的执行上下文。执行上下文的调用创建阶段会决定 this 的指向。到此，我们可以得出的一个结论：

> this 的指向，是在调用函数时, `根据执行上下文所动态确定的`。

可以总结为以下几条规律 ：

1. 在函数体中，简单调用该函数时（非显式/隐式绑定下），严格模式下 `this` 绑定到 `undefined`，否则绑定到全局对象 `window／global`；
2. 一般构造函数 `new` 调用，绑定到新创建的对象上；
3. 一般由 `call/apply/bind` 方法显式调用，绑定到指定参数的对象上；
4. 一般由上下文对象调用，绑定在该对象上；
5. 箭头函数中，根据外层上下文绑定的 `this` 决定 `this` 指向。

#### 案例

**全局环境下的 this**

严格模式下为 `undefined`，普通环境下指向的是 window

```javascript
function f1() {
  console.log(this);
}
function f2() {
  'use strict';
  console.log(this);
}
f1(); // window 对象
f2(); // undefined
```

来一个进阶题目

```javascript
const foo = {
  bar: 10,
  fn: function () {
    console.log(this);
    console.log(this.bar);
  },
};
var fn1 = foo.fn;
fn1();
```

这时候的 `this` 仍然指向的是 `window`，所以 `this.bar` 输出 `undefined`

### 箭头函数 this 指向

箭头函数的 this 指向就是 **在定义函数时所在的作用域指向的对象**，而不是在调用时确认。我们来看段代码验证一下。

```javascript
window.a = '我是 window 下的 a';
let obj = {
  a: '我是 obj 下的 a',
  func: () => {
    return this.a;
  },
};
console.log(obj.func()); // 我是 window 下的 a
let fun = obj.func;
console.log(fun()); // 我是 window 下的 a
```

这里的 `func` 函数，因为在定义时就已经决定了 this 的指向，而所在的作用域在定义时就是在 `全局 window 环境` 下，因此指向的是 `window 对象`，无论是 `obj` 调用或者是 `window` 调用输出都是在 `window 环境` 下了.

如果有不知道作用域链的读者，就可以去看看之前的一篇文章 [hzq：作用域与作用域链](#1)

我们来对代码稍做修改，就会指向 `obj` 对象。

```javascript
window.a = '我是 window 下的 a';
let obj = {
  a: '我是 obj 下的 a',
  func: function () {
    return () => {
      console.log(this.a);
    };
  },
};
let fun = obj.func();
fun(); // 我是 obj 下的 a
```

这里我们在定义时，所在的作用域其实就是 外层 `function 作用域`，而外层 `function` 指向的对象就是 `obj 对象`，所以输出的结果就是 `我是 obj 下的 a`

### 小结

到此为止呢，this 的指向问题就告一段落了。来做一个小结吧，简单概括为以下两句话。

**普通函数：`this` 指向的是调用时的对象**

**箭头函数：`this` 指向的是定义函数时所在的作用域指向的对象**
