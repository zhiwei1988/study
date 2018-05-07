## Let 和 Const

在函数内部使用 `var` 声明变量时，在执行该函数之前，所有变量都会被提升到该函数作用域的顶部。

使用 `let` 和 `const` 声明的变量解决了这种提升问题，因为它们的作用域是**到块**，而不是函数。

使用 `let` 声明的变量可以重新赋值，但是不能在同一作用域内重新声明。

使用 `const` 声明的变量必须赋初始值，但是不能在同一作用域内重新声明，也无法重新赋值。

> 建议放弃使用 `var`，改为使用 `let` 和 `const`。

## 模版字面量

**模板字面量**本质上是包含嵌入式表达式的字符串字面量。

模板字面量用倒引号 ( ``` `)（而不是单引号 ( `''` ) 或双引号( `""` )）表示，可以包含用 `${expression}` 表示的占位符。这样更容易构建字符串。

下面是之前的示例使用模板字面量表示后的效果：

```javascript
let message = `${student.name} please see ${teacher.name} in ${teacher.room} to pick up your report card.`;
```

> **Returns:** Richard Kalehoff please see Mrs. Wilson in N231 to pick up your report card.

在使用模板字面量时，如果要换行也不需要额外添加`\n`，因为它也将换行符当做字符串的一部分。

> **提示：**模板字面量中的嵌入式表达式不仅仅可以用来引用变量。你可以在嵌入式表达式中进行运算、调用函数和使用循环！

## 解构

**解构**这一概念从 [Perl](https://baike.baidu.com/item/perl/851577?fr=aladdin) 和 [Python](https://baike.baidu.com/item/Python/407313) 等语言中获得灵感，使你能够指定要从赋值左侧上的数组或对象中提取的元素。

**解构数组中的值**

```javascript
const point = [10, 25, -34];

const [x, y, z] = point;

console.log(x, y, z);
```

> **Prints:** 10 25 -34

> **提示：**在解构数组时，还可以忽略值。例如，`const [x, , z] = point;` 忽略了 `y`坐标。

**解构对象中的值**

```javascript
const gemstone = {
  type: 'quartz',
  color: 'rose',
  karat: 21.29
};

const {type, color, karat} = gemstone;

console.log(type, color, karat);
```

> **Prints:** quartz rose 21.29

> **提示：**你还可以指定在解构对象时要选择的值。例如，`let {color} = gemstone;`将仅选择 `gemstone` 对象中的 `color` 属性。

**解构的陷阱**

```javascript
const circle = {
  radius: 10,
  color: 'orange',
  getArea: function() {
    return Math.PI * this.radius * this.radius;
  },
  getCircumference: function() {
    return 2 * Math.PI * this.radius;
  }
};

let {radius, getArea, getCircumference} = circle;
getArea();
```

> 调用 `getArea` 将返回 `NaN` 。在解构该对象并将 `getArea()` 方法存储到 `getArea` 变量中时，它无法再访问 `circle` 对象中的 `this`，得出面积 `NaN`。

## 对象字面量简写法

如果属性名称和所分配的变量名称一样，那么就可以从对象属性中删掉这些重复的变量名称。

**简写方法名称**

```javascript
let gemstone = {
  type,
  color,
  carat,
  calculateWorth() { ... } // 关键字 function 可以省略
};
```

## For 循环系列

**for...of 循环**是最新添加到 JavaScript 循环系列中的循环。

它结合了其兄弟循环形式 **for 循环**和 **for...in 循环**的优势，可以循环任何**可迭代**（也就是遵守[可迭代协议](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Iteration_protocols)）类型的数据。默认情况下，包含以下数据类型：String、Array、Map 和 Set，注意不包含 `Object` 数据类型（即 `{}`）。默认情况下，对象不可迭代。

**for 循环**

for 循环的最大缺点是需要跟踪**计数器**和**退出条件**。

**for...in 循环**

for...in 循环改善了 for 循环的不足之处，它消除了计数器逻辑和退出条件。 

```javascript
const digits = [0, 1, 2, 3, 4, 5, 6, 7, 8, 9];

for (const index in digits) {
  console.log(digits[index]);
}
```

但是依然需要使用 **index** 来访问数组的值，这样很麻烦。

此外，当你需要向数组中添加额外的方法（或另一个对象）时，for...in 循环会带来很大的麻烦。因为 for...in 循环循环访问所有可枚举的属性，意味着如果向数组的原型中添加任何其他属性，这些属性也会出现在循环中。

> **注意：** **forEach 循环** 是另一种形式的 JavaScript 循环。但是，`forEach()` 实际上是数组方法，因此只能用在数组中。也无法停止或退出 forEach 循环。如果希望你的循环中出现这种行为，则需要使用基本的 for 循环。

## For...of 循环

**for...of 循环**用于循环访问任何可迭代的数据类型，它即保留了 `for...in` 的简洁，又能随时退出循环且不会变了新增的属性。

## 展开运算符

`...` 是 ES6 中的新概念，使你能够将[字面量对象](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Guide/Iterators_and_Generators#%E8%BF%AD%E4%BB%A3%E5%99%A8)展开为多个元素。

展开运算符的一个用途是结合数组。

如果你需要结合多个数组，在有展开运算符之前，必须使用 Array 的 `concat()` 方法。

使用展开运算符后，就能在不使用 `concat()` 的情况下拼接数组。

```javascript
const fruits = ["apples", "bananas", "pears"];
const vegetables = ["corn", "potatoes", "carrots"];
const produce = [...fruits, ...vegetables];
console.log(produce);
```

## 剩余参数

**剩余参数**也用三个连续的点 ( `...` ) 表示，使你能够将不定数量的元素表示为数组。它在多种情形下都比较有用：

1. 结构数组时
2. 在可变函数中替换函数对象
