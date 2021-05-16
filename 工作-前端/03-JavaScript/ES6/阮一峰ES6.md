#### [let 和 const 命令](https://es6.ruanyifeng.com/#docs/let)

**let 命令**

1. 形成自身**代码块**，只有在自身代码块内生效
2. **不存在变量提升**，var 声明会进行变量提升
3. **暂时性死区**
   - 暂时性死区的本质就是，只要一进入当前作用域，所要使用的变量就已经存在了，但是不可获取，只有等到声明变量的那一行代码出现，才可以获取和使用该变量。
4. 不允许重复声明

**块级作用域**

​	ES5 只有全局作用域和函数作用域，没有块级作用域

**const 命令**

​	`const`实际上保证的，并不是变量的值不得改动，而是变量指向的那个内存地址所保存的数据不得改动。对于简单类型的数据（数值、字符串、布尔值），值就保存在变量指向的那个内存地址，因此等同于常量。但对于复合类型的数据（主要是对象和数组），变量指向的内存地址，保存的只是一个指向实际数据的指针，`const`只能保证这个指针是固定的（即总是指向另一个固定的地址），至于它指向的数据结构是不是可变的，就完全不能控制了。

**顶层对象属性**

​	顶级对象 window， var 声明会认为是顶级对象， let 则不会

**globalThis 对象**

- 浏览器里面，顶层对象是`window`，但 Node 和 Web Worker 没有`window`。
- 浏览器和 Web Worker 里面，`self`也指向顶层对象，但是 Node 没有`self`。
- Node 里面，顶层对象是`global`，但其他环境都不支持。

​      全局环境中，`this`会返回顶层对象。但是，Node.js 模块中`this`返回的是当前模块，ES6 模块中`this`返回的是`undefined`。

#### [变量的解构赋值](https://es6.ruanyifeng.com/#docs/destructuring)

​	ES6 允许按照一定模式，从数组和对象中提取值，对变量进行赋值，这被称为解构（Destructuring）。

**数组解构 、对象结构**

1. 不完全解构
2. 允许解构赋值有默认值
3. 数组解构是有序的，按照位置解析结构，对象的解构时无序的，需要对应的 key值进行解构，对象解构可以对对象 key 值进行重命名，对象的解构也可以进行赋值默认值 

```js
// 数组的解构
let [a, b, c, [z, x ]] = [1, 2, 3, [4]]  x === undefind
let [a, b, c, [z, x ]] = 1/ undefind/ true... // 报错
// 对象结构
let {foo, bar:rename} = { foo:110, bar: 120 }
```

**字符串解构**

​	字符串结构会字符串被转换成了一个类似数组的对象，所以这个对象有一个 length

**数值和布尔值的解构**

​	解构赋值时会将数值和布尔值转换成一个对象

**函数参数的解构**



#### [字符串的扩展](https://es6.ruanyifeng.com/#docs/string)

1. 字符的 Unicode 表示法？

2. 字符串的遍历器接口？

3. JSON.stringify()  改造？

4. 模板字符串， 模板字符串可以嵌套多层

   ```js
   $('#result').append(`
     There are <b>${basket.count}</b> items
      in your basket, <em>${basket.onSale}</em>
     are on sale!
   `);
   ```

5. 编译模板  解析模板生成模板实例？

6. 标签模板？



#### [字符串的新增方法](https://es6.ruanyifeng.com/#docs/string-methods)

1. String.fromCodePoint()

   用于从 Unicode 码点返回对应字符，但是这个方法不能识别码点大于`0xFFFF`的字符。

2. String.raw()？

   该方法返回一个斜杠都被转义（即斜杠前面再加一个斜杠）的字符串，往往用于模板字符串的处理方法。

3. 实例方法：codePointAt()

   `codePointAt()`方法是测试一个字符由两个字节还是由四个字节组成的最简单方法

4. 实例方法：normalize()

   unicode 的合成？

5. 实例方法：**includes(), startsWith(), endsWith()**

   - **includes()**：返回布尔值，表示是否找到了参数字符串。
   - **startsWith()**：返回布尔值，表示参数字符串是否在原字符串的头部。
   - **endsWith()**：返回布尔值，表示参数字符串是否在原字符串的尾部。

6. 实例方法：**repeat()**

   `repeat`方法返回一个新字符串，表示将原字符串重复`n`次。

7. 实例方法：**padStart()，padEnd()**

   字符串补全长度的功能。如果某个字符串不够指定长度，会在头部或尾部补全。`padStart()`用于头部补全，`padEnd()`用于尾部补全。

8. 实例方法：**trimStart()，trimEnd()**

   `trimStart()`消除字符串头部的空格，`trimEnd()`消除尾部的空格。它们返回的都是新字符串，不会修改原始字符串，它们的行为与`trim()`一致。

9. 实例方法：**matchAll()**

   返回一个正则表达式在当前字符串的所有匹配

10. 实例方法：**replaceAll()**

    替换所有匹配到的内容，有两个参数

    `replaceAll()`的第二个参数`replacement`是一个字符串，表示替换的文本，其中可以使用一些特殊字符串。

    - `$&`：匹配的子字符串。
    - `$` `：匹配结果前面的文本。
    - `$'`：匹配结果后面的文本。
    - `$n`：匹配成功的第`n`组内容，`n`是从1开始的自然数。这个参数生效的前提是，第一个参数必须是正则表达式。
    - `$$`：指代美元符号`$`。

#### [正则的扩展](https://es6.ruanyifeng.com/#docs/regex)

1. **RegExp 构造函数**

   构造一个正则实例，new RegExp()  == /xxxxx/

   有两个参数，也可只传一个参数

2. **字符串的正则方法**

   可以使用正则表达式：`match()`、`replace()`、`search()`和`split()`。

3. u 修饰符

4. RegExp.prototype.unicode 属性

5. y 修饰符

6. RegExp.prototype.sticky 属性

7. RegExp.prototype.flags 属性

8. s 修饰符：dotAll 模式

9. 后行断言

10. Unicode 属性类

11. 具名组匹配

12. 正则匹配索引

13. **String.prototype.matchAll()**

    可以一次性取出所有匹配。不过，它返回的是一个遍历器（Iterator），而不是数组。

#### [数值的扩展](https://es6.ruanyifeng.com/#docs/number)

2 的 53 次方

1. 二进制和八进制表示法

   二进制和八进制数值的新的写法，分别用前缀`0b`（或`0B`）和`0o`（或`0O`）表示。

2. Number.isFinite(), Number.isNaN()

   用来检查一个数值是否为有限的（finite）

   用来检查一个值是否为`NaN`

3. **Number.parseInt(), Number.parseFloat()**

   函数可解析一个字符串，并返回一个整数，两个参数，第一个解析对象，第二个2-36之间的基数

   函数可解析一个字符串，并返回一个浮点数，一个参数，解析对象

4. **Number.isInteger()**

   判断是否为整数

5. Number.EPSILON

   表示最小常量

6. 安全整数和 Number.isSafeInteger()

7. Math 对象的扩展

   新增了 17 个与数学相关的方法

8. 指数运算符 （**）

   运算方式为从右往左  

   ```javascript
   // 相当于 2 ** (3 ** 2)
   2 ** 3 ** 2
   ```

9. **BigInt 数据类型**

   一种新的数据类型 BigInt（大整数），来解决这个问题，这是 ECMAScript 的第八种数据类型。BigInt 只用来表示整数，没有位数的限制，任何位数的整数都可以精确表示

   BigInt 对象继承了 Object 对象的两个实例方法。

   - `BigInt.prototype.toString()`
   - `BigInt.prototype.valueOf()`

   它还继承了 Number 对象的一个实例方法。

   - `BigInt.prototype.toLocaleString()`

   此外，还提供了三个静态方法。

   - `BigInt.asUintN(width, BigInt)`： 给定的 BigInt 转为 0 到 2width - 1 之间对应的值。
   - `BigInt.asIntN(width, BigInt)`：给定的 BigInt 转为 -2width - 1 到 2width - 1 - 1 之间对应的值。
   - `BigInt.parseInt(string[, radix])`：近似于`Number.parseInt()`，将一个字符串转换成指定进制的 BigInt。

#### [函数的扩展](https://es6.ruanyifeng.com/#docs/function)

1. **函数参数的默认值**

   可以给函数参数赋值默认值

2. **rest 参数**

   rest 参数（形式为`...变量名`），用于获取函数的多余参数，这样就不需要使用`arguments`对象了

3. **严格模式**

   函数内部可以设置严格模式 `use strict`

4. name 属性

   函数的`name`属性，返回该函数的函数名

5. **箭头函数**

   1. 函数体内没有 this 对象
   2. 不可以当做构造函数使用，不能使用 new
   3. 不可以使用 arguments 对象，可以使用 rest 参数
   4. 不可以使用`yield`命令，因此箭头函数不能用作 Generator 函数？

   不使用场合

   第一个场合是定义对象的方法，且该方法内部包括`this`

   第二个场合是需要动态`this`的时候，也不应使用箭头函数。

6. **尾调用优化**？

   函数最后一步调用另一个函数

   **尾递归** 函数调用自身

   递归非常耗费内存，因为需要同时保存成千上百个调用帧，很容易发生“栈溢出”错误（stack overflow）。但对于尾递归来说，由于只存在一个调用帧，所以永远不会发生“栈溢出”错误。

7. 函数参数的尾逗号

   允许函数的最后一个参数有尾逗号（trailing comma）。

8. **Function.prototype.toString()**

   将函数转换成字符串

9. **catch 命令的参数省略**

   catch(err) 可以不跟参数了

   ```
   try{
   	// ...
   } catch {
   	// ...
   }
   ```

   

#### [数组的扩展](https://es6.ruanyifeng.com/#docs/array)

1. **扩展运算符 spread**

   rest 的逆运算，将一个数组转为用逗号分隔的参数序列。

   扩展运算符的应用

   - **复制数组**
   - **合并数组**
   - **与结构赋值的结合**
   - **字符串转数组**
   - **实现了 Iterator 接口的对象**
   - **Map 和 Set 结构，Generator 函数**

2. **Array.from()**

   将类数组（字符串）转换成真正的数组，接收两个参数，第一个为目标值，第二个为回调函数，类似 map 操作

3. **Array.of()**

   用于将一组值，转换为数组

   ```js
   // 实现 Array.of()
   function ArrayOf(){
     return [].slice.call(arguments);  // 转换成数组
   }
   ```

4. 数组实例的 copyWithin()

   指定位置的成员复制到其他位置（会覆盖原有成员），然后返回当前数组。

   三个参数：

   - target（必需）：从该位置开始替换数据。如果为负值，表示倒数。
   - start（可选）：从该位置开始读取数据，默认为 0。如果为负值，表示从末尾开始计算。
   - end（可选）：到该位置前停止读取数据，默认等于数组长度。如果为负值，表示从末尾开始计算。

5. 数组实例的 **find() 和 findIndex(**)

   查找出第一个匹配到的数组成员，有则返回一个这个成员，find() 返回 undefined，findIndex() 返回 -1，

   接收两个参数，回调函数接收三个参数

   ```js
   arr.find((value, index, arr) = { return value == 0 }, this)
   ```

6. 数组实例的 fill()

   使用给定值，填充一个数组。

   接收三个参数

   ```js
   fill(o, 3, 5) // fill(给定值, 开始位置，结束位置)
   ```

7. 数组实例的 **entries()，keys() 和 values()**

   遍历数组  for .... of  Arr.keys()/values()/entries()

8. 数组实例的 **includes()**

   表示某个数组是否包含值，接收两个参数

   `includes(targer,[,index])`

9. 数组实例的 **flat()，flatMap()**

   `flat()`数组扁平化，多个数组拉成一个数组，接收一个参数，指定扁平化次数 Infinity 全部扁平处理

   `flatMap()` map 和 flat 的结合，将数组扁平化后再进行数据处理

   有两个参数

   - callback：(value [, index [, array ]]) => {}
   - this 指向

10. **数组的空位**

    ES5 对空位的处理，已经很不一致了，大多数情况下会忽略空位。

    - `forEach()`, `filter()`, `reduce()`, `every()` 和`some()`都会跳过空位。
    - `map()`会跳过空位，但会保留这个值
    - `join()`和`toString()`会将空位视为`undefined`，而`undefined`和`null`会被处理成空字符串。

    ES6 中会对空位进行 undefined，有些数组方法不会对空位进行处理

    `entries()`、`keys()`、`values()`、`find()`和`findIndex()`会将空位处理成`undefined`。

11. Array.prototype.sort() 的排序稳定性

#### [对象的扩展](https://es6.ruanyifeng.com/#docs/object)

1. **属性的简洁表示法**

   对对象的属性和方法进行了简写

   > 使用
   >
   > 1. 函数的返回值
   > 2. CommonJS 模块输出一组变量
   > 3. 简洁写法在打印对象时也很有用

   ```js
   const Person = {
     name: '张三',
     //等同于birth: birth
     birth,
     // 等同于hello: function ()...
     hello() { console.log('我的名字是', this.name); }
   };
   ```

   

2. **属性名表达式**

   ES6 允许字面量定义对象时

   ```javascript
   let obj = {
     [propKey]: true,  // [propKey]  === 'prop key'
     ['a' + 'bc']: 123  // ['a' + 'bc'] === [abc]
     // 也可用于定义方法
     ['h' + 'ello']() {
       return 'hi';
     }
   };
   ```

3. 方法的 name 属性

   对象新增 name 方法返回函数名（方法名）

4. 属性的可枚举性和遍历

   **可枚举**

   `Object.getOwnPropertyDescriptor`方法可以获取该属性的描述对象

   ```js
   let obj = { foo: 123 };
   Object.getOwnPropertyDescriptor(obj, 'foo')
   //  {
   //    value: 123,
   //    writable: true,
   //    enumerable: true,  // 可枚举性
   //    configurable: true
   //  }
   ```

   enumerable 为 false 时会忽略该属性

   - `for...in`循环：只遍历对象自身的和继承的可枚举的属性。
   - `Object.keys()`：返回对象自身的所有可枚举的属性的键名。
   - `JSON.stringify()`：只串行化对象自身的可枚举的属性。
   - `Object.assign()`： 忽略`enumerable`为`false`的属性，只拷贝对象自身的可枚举的属性

   > 尽量不要用`for...in`循环，而用`Object.keys()`代替

   **遍历**

   **（1）for...in**

   `for...in`循环遍历对象自身的和继承的可枚举属性（不含 Symbol 属性）。

   **（2）Object.keys(obj)**

   `Object.keys`返回一个数组，包括对象自身的（不含继承的）所有可枚举属性（不含 Symbol 属性）的键名。

   **（3）Object.getOwnPropertyNames(obj)**

   `Object.getOwnPropertyNames`返回一个数组，包含对象自身的所有属性（不含 Symbol 属性，但是包括不可枚举属性）的键名。

   **（4）Object.getOwnPropertySymbols(obj)**

   `Object.getOwnPropertySymbols`返回一个数组，包含对象自身的所有 Symbol 属性的键名。

   **（5）Reflect.ownKeys(obj)**

   `Reflect.ownKeys`返回一个数组，包含对象自身的（不含继承的）所有键名，不管键名是 Symbol 或字符串，也不管是否可枚举。

5. **super 关键字？**

   指向当前对象的原型对象

6. **对象的扩展运算符**

   **解构赋值**

   对象的解构赋值用于从一个对象取值，相当于将目标对象自身的所有可遍历的（enumerable）、但尚未被读取的属性，分配到指定的对象上面。所有的键和它们的值，都会拷贝到新对象上面

   **扩展运算符**

   对象的扩展运算符（`...`）用于取出参数对象的所有可遍历属性，拷贝到当前对象之中

7. **链判断运算符**

   ```js
   const firstName = (message
     && message.body
     && message.body.user
     && message.body.user.firstName) || 'default';
   // 等同于
   const firstName = message?.body?.user?.firstName || 'default';
   ```

   链判断运算符有三种用法。

   - `obj?.prop` // 对象属性
   - `obj?.[expr]` // 同上
   - `func?.(...args)` // 函数或对象方法的调用

8. Null 判断运算符

   读取对象属性的时候，如果某个属性的值是`null`或`undefined`，有时候需要为它们指定默认值。常见做法是通过`||`运算符指定默认值。

   ```js
   const headerText = response.settings.headerText || 'Hello, worl
   ```

   只要属性的值为`null`或`undefined`或空字符串或`false`或`0`默认值都会生效

   ```js
   const headerText = response.settings.headerText ?? 'Hello, worl
   ```

   `??`可以解决上面的问题

#### [对象的新增方法](https://es6.ruanyifeng.com/#docs/object-methods)

1. Object.is()

   JavaScript 不能判断 NaN === NaN  +0 === -0

   通过Object.is(NaN, NaN) 可以判断返回一个布尔值 

2. **Object.assign()**

   用于对象的合并，将源对象（source）的所有可枚举属性，复制到目标对象（target）

   第一个参数为目标对象，其余参数都为源对象

   undefined 和 null 无法转换成对象，其余都将转换成对象

   > 1. 该方法实行的是浅拷贝
   > 2. 同名属性会进行替换
   > 3. 数组的处理
   > 4. 取值函数的处理

   用法：

   1. 为对象添加属性

   2. 为对象添加方法

   3. 克隆对象

      ```js
      // 克隆原始对象的值
      function clone(origin) {
      	return Object.assign({}, origin)
      }
      // 克隆原始和继承对象的值
      function clone(origin) {
        let originProto = Object.getPrototypeOf(origin)
        return Object.assign(Object.create(originProto), origin)
      }
      ```

   4. 合并多个对象

   5. 为属性指定默认值？

3. Object.getOwnPropertyDescriptors()

   方法会返回某个对象属性的描述对象

   ```js
   // { value: 123,
   //      writable: true,
   //      enumerable: true,
   //      configurable: true 
   // },
   ```

   

4. __proto__属性，**Object.setPrototypeOf()，Object.getPrototypeOf()**

   `Object.setPrototypeOf()`（写操作）

   用来设置一个对象的原型对象（prototype），返回参数对象本身。

   两个参数，第一个为对象，第二个参数为

   Object.getPrototypeOf()`(读操作)`

   用于读取一个对象的原型对象

   Object.create()`（生成操作）

   创建一个对象

5. **Object.keys()，Object.values()，Object.entries()**

   Object.keys() 返回对象所有可遍历属性的键名

   Object.values() 返回对象所有可遍历属性的值，过滤 Symbol 属性名值

   Object.entries()  返回对象的键值对数组

   以上方法返回一个数组

6. Object.fromEntries()

   是`Object.entries()`的逆操作，用于将一个键值对数组转为对象

#### [Symbol](https://es6.ruanyifeng.com/#docs/symbol)

ES6 引入了一种新的原始数据类型`Symbol`，表示独一无二的值。它是 JavaScript 语言的第七种数据类型，前六种是：`undefined`、`null`、布尔值（Boolean）、字符串（String）、数值（Number）、对象（Object）。

使用

```js
let obj = Symbol()
```

1. Symbol.prototype.description

   创建一个 Symbol 值的描述

2. 作为属性名的 Symbol

3. 实例：消除魔术字符串

4. 属性名的遍历

   属性遍历中不会被遍历到，需要使用`Object.getOwnPropertySymbols()`方法获取

5. Symbol.for()，Symbol.keyFor()

   Symbol.for('cat') 调用的是同一个值，而 Symbol('cat') 每次调用都不同

   Symbol.keyFor() 返回一个登记过的 Symbol 的值

6. 实例：模块的 Singleton 模式

7. 内置的 Symbol 值

   

#### [Set 和 Map 数据结构](https://es6.ruanyifeng.com/#docs/set-map)

1. **Set**

   它类似于数组，但是成员的值都是唯一的，没有重复的值

   ```js
   // 去除数组的重复成员
   [...new Set(array)]
   // 去除字符串重复值
   [...new Set('ababbc')].join('')
   ```

   > 1. 两个 NaN 是相等的
   > 2. 两个对象总是不相等的

   Set 结构的实例有以下属性。

   - `Set.prototype.constructor`：构造函数，默认就是`Set`函数。
   - `Set.prototype.size`：返回`Set`实例的成员总数。

   Set 实例的四个操作方法。

   - `Set.prototype.add(value)`：添加某个值，返回 Set 结构本身。
   - `Set.prototype.delete(value)`：删除某个值，返回一个布尔值，表示删除是否成功。
   - `Set.prototype.has(value)`：返回一个布尔值，表示该值是否为`Set`的成员。
   - `Set.prototype.clear()`：清除所有成员，没有返回值。

   Set 结构的实例有四个遍历方法。

   - `Set.prototype.keys()`：返回键名的遍历器
   - `Set.prototype.values()`：返回键值的遍历器
   - `Set.prototype.entries()`：返回键值对的遍历器
   - `Set.prototype.forEach()`：使用回调函数遍历每个成员

2. **WeakSet**

   WeakSet 结构与 Set 类似，也是不重复的值的集合。但是，它与 Set 有两个区别。

   首先，WeakSet 的成员只能是对象，而不能是其他类型的值，其次，WeakSet 中的对象都是弱引用，即垃圾回收机制不考虑 WeakSet 对该对象的引用，

   WeakSet 结构有以下三个方法。

   - **WeakSet.prototype.add(value)**：向 WeakSet 实例添加一个新成员。
   - **WeakSet.prototype.delete(value)**：清除 WeakSet 实例的指定成员。
   - **WeakSet.prototype.has(value)**：返回一个布尔值，表示某个值是否在 WeakSet 实例之中。

3. **Map**

   ES6 提供了 Map 数据结构。它类似于对象，也是键值对的集合，但是“键”的范围不限于字符串，各种类型的值（包括对象）都可以当作键。也就是说，Object 结构提供了“字符串—值”的对应，Map 结构提供了“值—值”的对应

   **（1）size 属性**

   `size`属性返回 Map 结构的成员总数。

   **（2）Map.prototype.set(key, value)**

   `set`方法设置键名`key`对应的键值为`value`，然后返回整个 Map 结构。如果`key`已经有值，则键值会被更新，否则就新生成该键

   `set`方法返回的是当前的`Map`对象，因此可以采用链式写法。

   ```javascript
   let map = new Map()
     .set(1, 'a')
     .set(2, 'b')
     .set(3, 'c');
   ```

   **（3）Map.prototype.get(key)**

   `get`方法读取`key`对应的键值，如果找不到`key`，返回`undefined`。

   **（4）Map.prototype.has(key)**

   `has`方法返回一个布尔值，表示某个键是否在当前 Map 对象之中。

   **（5）Map.prototype.delete(key)**

   `delete`方法删除某个键，返回`true`。如果删除失败，返回`false`。

   **（6）Map.prototype.clear()**

   `clear`方法清除所有成员，没有返回值。

   Map 结构原生提供三个遍历器生成函数和一个遍历方法。遍历顺序是插入顺序

   - `Map.prototype.keys()`：返回键名的遍历器。
   - `Map.prototype.values()`：返回键值的遍历器。
   - `Map.prototype.entries()`：返回所有成员的遍历器。
   - `Map.prototype.forEach()`：遍历 Map 的所有成员。

   > 1.**（1）Map 转为数组**
   >
   > 前面已经提过，Map 转为数组最方便的方法，就是使用扩展运算符（`...`）。
   >
   > **（2）数组 转为 Map**
   >
   > 将数组传入 Map 构造函数，就可以转为 Map。
   >
   > **（3）Map 转为对象**
   >
   > 如果所有 Map 的键都是字符串，它可以无损地转为对象。遍历返回
   >
   > 如果有非字符串的键名，那么这个键名会被转成字符串，再作为对象的键名。
   >
   > **（4）对象转为 Map**
   >
   > 对象转为 Map 可以通过`Object.entries()`。
   >
   > 实现一个转换函数。
   >
   > ```javascript
   > function objToStrMap(obj) {
   >   let strMap = new Map();
   >   for (let k of Object.keys(obj)) {
   >     strMap.set(k, obj[k]);
   >   }
   >   return strMap;
   > }
   > 
   > objToStrMap({yes: true, no: false})
   > // Map {"yes" => true, "no" => false}
   > ```
   >
   > **（5）Map 转为 JSON**
   >
   > Map 转为 JSON 要区分两种情况。一种情况是，Map 的键名都是字符串，这时可以选择转为对象 JSON。
   >
   > ```javascript
   > function strMapToJson(strMap) {
   >   return JSON.stringify(strMapToObj(strMap));
   > }
   > 
   > let myMap = new Map().set('yes', true).set('no', false);
   > strMapToJson(myMap)
   > // '{"yes":true,"no":false}'
   > ```
   >
   > 另一种情况是，Map 的键名有非字符串，这时可以选择转为数组 JSON。
   >
   > ```javascript
   > function mapToArrayJson(map) {
   >   return JSON.stringify([...map]);
   > }
   > 
   > let myMap = new Map().set(true, 7).set({foo: 3}, ['abc']);
   > mapToArrayJson(myMap)
   > // '[[true,7],[{"foo":3},["abc"]]]'
   > ```
   >
   > **（6）JSON 转为 Map**
   >
   > JSON 转为 Map，正常情况下，所有键名都是字符串。

4. **WeakMap**

   `WeakMap`与`Map`的区别有两点。

   首先，`WeakMap`只接受对象作为键名（`null`除外），不接受其他类型的值作为键名。

   其次，`WeakMap`的键名所指向的对象，不计入垃圾回收机制。

   `WeakMap`只有四个方法可用：`get()`、`set()`、`has()`、`delete()`。

#### [Proxy](https://es6.ruanyifeng.com/#docs/proxy)

Proxy 可以理解成，在目标对象之前架设一层“拦截”，外界对该对象的访问，都必须先通过这层拦截，因此提供了一种机制，可以对外界的访问进行过滤和改写。Proxy 这个词的原意是代理，用在这里表示由它来“代理”某些操作，可以译为“代理器”。

Proxy 支持的拦截操作一览，一共 13 种。

- **get(target, propKey, receiver)**：拦截对象属性的读取，比如`proxy.foo`和`proxy['foo']`。
- **set(target, propKey, value, receiver)**：拦截对象属性的设置，比如`proxy.foo = v`或`proxy['foo'] = v`，返回一个布尔值。
- **has(target, propKey)**：拦截`propKey in proxy`的操作，返回一个布尔值。
- **deleteProperty(target, propKey)**：拦截`delete proxy[propKey]`的操作，返回一个布尔值。
- **ownKeys(target)**：拦截`Object.getOwnPropertyNames(proxy)`、`Object.getOwnPropertySymbols(proxy)`、`Object.keys(proxy)`、`for...in`循环，返回一个数组。该方法返回目标对象所有自身的属性的属性名，而`Object.keys()`的返回结果仅包括目标对象自身的可遍历属性。
- **getOwnPropertyDescriptor(target, propKey)**：拦截`Object.getOwnPropertyDescriptor(proxy, propKey)`，返回属性的描述对象。
- **defineProperty(target, propKey, propDesc)**：拦截`Object.defineProperty(proxy, propKey, propDesc）`、`Object.defineProperties(proxy, propDescs)`，返回一个布尔值。
- **preventExtensions(target)**：拦截`Object.preventExtensions(proxy)`，返回一个布尔值。
- **getPrototypeOf(target)**：拦截`Object.getPrototypeOf(proxy)`，返回一个对象。
- **isExtensible(target)**：拦截`Object.isExtensible(proxy)`，返回一个布尔值。
- **setPrototypeOf(target, proto)**：拦截`Object.setPrototypeOf(proxy, proto)`，返回一个布尔值。如果目标对象是函数，那么还有两种额外操作可以拦截。
- **apply(target, object, args)**：拦截 Proxy 实例作为函数调用的操作，比如`proxy(...args)`、`proxy.call(object, ...args)`、`proxy.apply(...)`。
- **construct(target, args)**：拦截 Proxy 实例作为构造函数调用的操作，比如`new proxy(...args)`。

1. Proxy 实例的方法

   **get()**

   `get`方法用于拦截某个属性的读取操作，可以接受三个参数，依次为目标对象、属性名和 proxy 实例本身（严格地说，是操作行为所针对的对象），其中最后一个参数可选。

   > 1. 可以继承
   > 2. 实现链式调用

   **set()**

   `set`方法用来拦截某个属性的赋值操作，可以接受四个参数，依次为目标对象、属性名、属性值和 Proxy 实例本身，其中最后一个参数可选。

   > 1. 可以对设置对象值进行校验

   **apply()**

   `apply`方法拦截函数的调用、`call`和`apply`操作。

   `apply`方法可以接受三个参数，分别是目标对象、目标对象的上下文对象（`this`）和目标对象的参数数组。

2. Proxy.revocable()

   `Proxy.revocable()`方法返回一个可取消的 Proxy 实例。

3. this 问题

   目标对象内部的`this`关键字会指向 Proxy 代理。

4. 例：Web 服务的客户端

#### [Reflect](https://es6.ruanyifeng.com/#docs/reflect)

Reflect 对象可以拿到函数内部的方法

1. **静态方法**

`Reflect`对象一共有 13 个静态方法。

- Reflect.get(target, name, receiver)
  - 查找并返回 target 对象的 name 属性，没有则返回 undefined
- Reflect.set(target, name, value, receiver)
  - 设置`target`对象的`name`属性等于`value`。
- Reflect.has(target, name)
  - 判断对象是否在目标内，返回布尔值  ===  name in target
- Reflect.deleteProperty(target, name)
  - 删除对象属性，返回布尔值  === delete target.name
- Reflect.construct(target, args)
  - 创建一个构造函数  === new Target(args)， 参数必须为函数
- Reflect.getPrototypeOf(target)
  - 读取对象的`__proto__`属性 === Object.getPrototypeOf(target)
- Reflect.setPrototypeOf(target, prototype)
  - 设置目标对象的原型（prototype）=== Object.setPrototypeOf(obj, newProto)，返回布尔值
- Reflect.apply(func, thisArg, args)
- - 用于绑定`this`对象后执行给定函数  === Object.prototype.appay.call()
- Reflect.defineProperty(target,  propertyKey, attributes )
  - 为对象定义属性  === Object.definedProperty()
- Reflect.getOwnPropertyDescriptor(target, propertyKey)
  - 指定属性的描述对象 === Object.getOwnPropertyDescriptor()
- Reflect.isExtensible (target)
  - 表示当前对象是否可扩展  === Object.isExtensible()  只能设置对象
- Reflect.preventExtensions(target)
  - 设置对象不可扩展  ===  Object.preventExtensions()  （es6新增）
- Reflect.ownKeys (target)
  - 返回对象的所有属性 === Object.getOwnPropertyNames() + Object.getOwnPropertySymbel()

2. 使用 Proxy 实现观察者模式

#### [Promise 对象](https://es6.ruanyifeng.com/#docs/promise)

1. Promise 的含义

   Promise 是异步编程的一种解决方案，比传统的解决方案——回调函数和事件——更合理和更强大。

   `Promise`对象有以下两个特点。

   （1）对象的状态不受外界影响。`Promise`对象代表一个异步操作，有三种状态：`pending`（进行中）、`fulfilled`（已成功）和`rejected`（已失败）。只有异步操作的结果，可以决定当前是哪一种状态，任何其他操作都无法改变这个状态。这也是`Promise`这个名字的由来，它的英语意思就是“承诺”，表示其他手段无法改变。

   （2）一旦状态改变，就不会再变，任何时候都可以得到这个结果。`Promise`对象的状态改变，只有两种可能：从`pending`变为`fulfilled`和从`pending`变为`rejected`。只要这两种情况发生，状态就凝固了，不会再变了，会一直保持这个结果，这时就称为 resolved（已定型）。

2. 基本用法

   ```js
   function fn() {
     return new Promise((resolve, reject) => {})
   }
   let promise = new Promise(function(resolve, reject) { })
   ```

   return resolve 和 return reject 都返回一个 promise 对象

3. Promise.prototype.then(fnres, fnrej)

   Promise 实例对象发生改变后调用，两个函数参数

4. Promise.prototype.catch(fnerr)

   发生错误后的回调

5. Promise.prototype.finally()

   不管Promise 状态如何都将执行的操作

6. Promise.all( [p1, p2, ....] )

   将多个 promise 进行封装执行，最终状态由 p1, p2, p3 结果决定

   1. 只有所有状态都成功才会返回成功
   2. 如果有状态返回失败就返回失败，失败优先级为最先返回的失败为失败

7. Promise.race( [p1, p2, ...])

   将多个 promise 进行封装执行，最先返回失败或者成功的实例，谁快谁执行

8. Promise.allSettled( [[p1, p2, ...]])

   将多个 promise 进行封装执行，只有当所有实例执行结束才会返回结果，不处理结果是失败还是成功

9. Promise.any()

   将多个 promise 进行封装执行，只要有一个实例是fulfilled 状态，就为 fulfilled ，只有所有状态都为 rejected 状态才为 rejected 状态

10. Promise.resolve()

    返回一个 promise  对象

11. Promise.reject()

    返回一个 promise 对象

12. 应用

    - 加载图片
    - 

13. Promise.try()

    报错

#### [Iterator 和 for...of 循环](https://es6.ruanyifeng.com/#docs/iterator)

Iterator 遍历器

#### [Generator 函数的语法](https://es6.ruanyifeng.com/#docs/generator)

异步编程的一种解决方案

#### [Generator 函数的异步应用](https://es6.ruanyifeng.com/#docs/generator-async)

ES6 诞生以前，异步编程的方法，大概有下面四种。

- 回调函数
- 事件监听
- 发布/订阅
- Promise 对象

#### [async 函数](https://es6.ruanyifeng.com/#docs/async)

是 generator 的语法糖

**语法**

```js
// 函数声明
async function foo() {}

// 函数表达式
const foo = async function () {};

// 对象的方法
let obj = { async foo() {} };
obj.foo().then(...)

// Class 的方法
class Storage {
  constructor() {
    this.cachePromise = caches.open('avatars');
  }

  async getAvatar(name) {
    const cache = await this.cachePromise;
    return cache.match(`/avatars/${name}.jpg`);
  }
}

const storage = new Storage();
storage.getAvatar('jake').then(…);

// 箭头函数
const foo = async () => {};
```



> 1. 返回 Promise 对象，返回的结果会进入 then，内部抛出的错误会被 catch 接收
> 2. 只有内部的所有 await 后 Promise 执行完毕才会调用
> 3. await 命令 后面是一个 promise 对象，如果不是返回对应值



#### [Class 的基本语法](https://es6.ruanyifeng.com/#docs/class)

class 只是作为一个语法糖，用 function 都可以进行实现

**类的实例**

```js
class Point {
  // ...
}
// 报错
var point = Point(2, 3);
// 正确
var point = new Point(2, 3);
```

**取值函数（getter）和存值函数（setter）**

> 1. 严格模式
> 2. 不存在变量提升
> 3. name 属性
> 4. Generator 方法？
> 5. this 的指向
>    - this 执行可能会找不到实例，可以使用 bind() 或者箭头函数解决

**constructor()**

类的构造函数，如果创建类没有定义，在生成实例的时候会自动创建一个构造函数

**静态方法**

添加 static 关键字，表示类的静态方法，不会被实例继承，只能通过类去调用，不过可以通过 super 关键字继承父类的静态方法

**静态属性**

新增， 通过 static 新增静态属性

**私有方法和私有属性**

1. 通过添加 `_` 加以区分私有性
2. 利用 Symbol 值的唯一性来添加私有方法

 私有属性还在提案中，通过 # 表示

**new.target**

返回作用于那个构造函数

#### [Class 的继承](https://es6.ruanyifeng.com/#docs/class-extends)

**通过 extends 关键字继承**

**Object.getPrototypeOf()**

`Object.getPrototypeOf`方法可以用来从子类上获取父类

**super 关键字**

`super`在静态方法之中指向父类，在普通方法之中指向父类的原型对象

**原生构造函数的继承**

- Boolean()
- Number()
- String()
- Array()
- Date()
- Function()
- RegExp()
- Error()
- Object()

**Mixin 模式的实现**



#### [Module 的语法](https://es6.ruanyifeng.com/#docs/module)

**严格模式**

ES6 的模块自动采用严格模式，不管你有没有在模块头部加上`"use strict";`。

严格模式主要有以下限制。

- 变量必须声明后再使用
- 函数的参数不能有同名属性，否则报错
- 不能使用`with`语句
- 不能对只读属性赋值，否则报错
- 不能使用前缀 0 表示八进制数，否则报错
- 不能删除不可删除的属性，否则报错
- 不能删除变量`delete prop`，会报错，只能删除属性`delete global[prop]`
- `eval`不会在它的外层作用域引入变量
- `eval`和`arguments`不能被重新赋值
- `arguments`不会自动反映函数参数的变化
- 不能使用`arguments.callee`
- 不能使用`arguments.caller`
- 禁止`this`指向全局对象
- 不能使用`fn.caller`和`fn.arguments`获取函数调用的堆栈
- 增加了保留字（比如`protected`、`static`和`interface`）



#### [Module 的加载实现](https://es6.ruanyifeng.com/#docs/module-loader)



[编程风格](https://es6.ruanyifeng.com/#docs/style)

[读懂规格](https://es6.ruanyifeng.com/#docs/spec)

[异步遍历器](https://es6.ruanyifeng.com/#docs/async-iterator)

[ArrayBuffer](https://es6.ruanyifeng.com/#docs/arraybuffer)

[最新提案](https://es6.ruanyifeng.com/#docs/proposals)

[Decorator](https://es6.ruanyifeng.com/#docs/decorator)

- [参考链接](https://es6.ruanyifeng.com/#docs/reference)