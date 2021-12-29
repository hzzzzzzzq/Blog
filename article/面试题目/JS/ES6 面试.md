## **ES6面试题**


**ES6新增方法面试题**

- 1.let const var比较
- 2.反引号（`）标识
- 3.函数默认参数
- 4.箭头函数
- 5.属性简写
- 6.方法简写
- 7.Object.keys()方法，获取对象的所有属性名或方法名
- 8.Object.assign ()原对象的属性和方法都合并到了目标对象
- 9.for...of 循环
- 10.import和export
- 11.Promise对象
- 12.解构赋值
- 13.set数据结构（可用于快速去重）
- 14.Spread Operator 展开运算符(...)
- 15.字符串新增方法



**ES6数组面试题**

- 1.forEach()

回调函数，带三个参数 item,index, array 

item 当前值，index当前索引 array为原数组

- 2.map()

创建一个新数组，其结果是该数组中的每个元素都调用一次提供的函数后的返回值

- 3.filter()

过滤，创建一个新数组，包含通过提供函数实现的所有元素。

```javascript
const words = ['spray', 'limit', 'elite', 'exuberant', 'destruction', 'present'];

const result = words.filter(word => word.length > 6);

console.log(result);
// expected output: Array ["exuberant", "destruction", "present"]
```

- 4.reduce()

对数组中的每个元素执行一个reducer函数，将结果汇总为单个返回值

- 5.some()

测试数组中是不是至少有一个元素通过了被测试函数，返回一个布尔值

- 6.every()

返回一个布尔值，判断某个数组中所有的元素是否都满足回调函数的条件，如果满足，返回 true

```javascript
const isBelowThreshold = (currentValue) => currentValue < 40;

const array1 = [1, 30, 39, 29, 10, 13];

console.log(array1.every(isBelowThreshold));
// expected output: true
```

- 7.all()方法

**ES6编程题**

- 1.使用解构，实现两个变量的值的交换

[a, b] = [b, a]

- 2.利用数组推导，计算出数组 [1,2,3,4] 每一个元素的平方并组成新的数组。
- 3.使用ES6改下面的模板
- 4.把以下代码使用两种方法，来依次输出0到9？