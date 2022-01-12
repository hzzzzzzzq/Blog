### call/apply/bind

### 构造函数和 this

这方面最直接的例题为：

```javascript
function Foo() {
  this.bar = 'Tom';
}
const instance = new Foo();
console.log(instance.bar);
```

答案将会输出 `Tom`。

但是这样的场景往往伴随着下一个问题：`new` 操作符调用构造函数，具体做了什么？

以下供参考：

1. 创建一个新的对象；
2. 将构造函数的 this 指向这个新对象；
3. 为这个对象添加属性、方法等；
4. 最终返回新对象。

以上过程，也可以用代码表述：

```javascript
var obj = {};
obj.__proto__ = Foo.prototype;
Foo.call(obj);
```

当然，这里对 `new` 的模拟是一个简单基本版的。

需要指出的是，如果在构造函数中出现了显式 `return` 的情况，那么需要注意分为两种场景：

```javascript
function Foo() {
  this.user = 'Tom';
  const o = {};
  return ol;
}
const instance = new Foo();
console.log(instance.user);
```

将会输出 `undefined`，此时 `instance` 是返回的空对象 `o`。

```javascript
function Foo() {
  this.user = 'Tom';
  return 1;
}
const instance = new Foo();
console.log(instance.user);
```

将会输出 Tom，也就是说此时 instance 是返回的目标对象实例 this。

结论：

> 如果构造函数中显式返回一个值，且返回的是一个对象，那么 this 就指向这个返回的对象；

> 如果返回的不是一个对象，那么 this 仍然指向实例。
