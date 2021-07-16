## 历史

历史上，JavaScript 一直没有模块（module）体系，无法将一个大程序拆分成互相依赖的小文件，再用简单的方法拼装起来。而其他语言基本上都有 `import` 导入方式。

在 ES6 之前，社区制定了一些模块加载方案，最主要的有 CommonJS 和 AMD 两种。前者用于服务器，后者用于浏览器。ES6 在语言标准的层面上，实现了模块功能，而且实现得相当简单，完全可以取代 CommonJS 和 AMD 规范，成为浏览器和服务器通用的模块解决方案。

ES6 模块的设计思想是尽量的静态化，使得编译时就能确定模块的依赖关系，以及输入和输出的变量。CommonJS 和 AMD 模块，都只能在运行时确定这些东西。比如，CommonJS 模块就是对象，输入时必须查找对象属性。


## CommandJS

`CommandJS` 是服务端 `JavaScript` 的标准规范，主要核心为 `module.exports` 和 `require` ，加载方式是同步的。

- 单个导出/导入

```javascript
// commandJs.js
module.exports.name = 'hzzzzzzzzq';
module.exports.age = '20';
module.exports.weight = 178;
```

我们使用的是 `module.exports` 的导出方式，使用的是单个导出。

而我们在导入文件中，可以使用 require 进入导入，然后使用 `info. ` 进行调用。

```javascript
let info = require('./commandJs.js');

console.log(info);
// { name: 'hzzzzzzzzq', age: '20', weight: 178 }
console.log(info.name); // hzzzzzzzzq
console.log(info.age); // 20
console.log(info.weight); // 178
```

- 整体导出/导入

```javascript
module.exports = {
  info: {
    name: 'hzq',
    age: '21',
    height: '178',
    weight: 'noWay',
  },
  school: {
    name: '大学',
    position: '不给',
  },
};
```
这样的来取值是可取的

```javascript
let  info = require('./commandJs.js');

console.log(info.info);
// { name: 'hzq', age: '21', height: '178', weight: 'noWay' }
console.log(info.school);
// { name: '大学', position: '不给' }
```

通常我们会写成下面的样子，结果是一样的。

```javascript
let { info, school } = require('./commandJs.js')

console.log(info);
// { name: 'hzq', age: '21', height: '178', weight: 'noWay' }
console.log(school);
// { name: '大学', position: '不给' }
```


## ES6 Module

