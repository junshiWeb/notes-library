#### 条件语句

- **if 语句** - 只有当指定条件为 true 时，使用该语句来执行代码
- **if...else 语句** - 当条件为 true 时执行代码，当条件为 false 时执行其他代码
- **if...else if....else 语句**- 使用该语句来选择多个代码块之一来执行
- **switch ... case 语句** - 使用该语句来选择多个代码块之一来执行

#### 循环语句

- **for语句** 

  ```ts
  for ( init; condition; increment ){
      statement(s);
  }
  ```

- **for ... in 语句** - 进行迭代循环

  ```ts
  for (var val in list) { 
      //语句 
  }
  ```

- **for…of** 、**forEach**、**every** 和 **some** 循环

- **while 循环**

- **do...while 循环** - 至少执行一遍

- **break 语句**：跳出循环，终止程序

- **continue 语句**： 跳出当前循环

#### 函数

```ts
// 定义函数
function definds() {
  let sum = 11
  console.log('调用函数');
  // 函数返回值
  return sum
}
// 调用函数
definds()
// 带参函数 默认参数函数 可选参数函数
function targetFn (x: number , y: number = 1.1, z?:number) {
  if(z) {
    return x + y + z
  } else {
    return x + y
  }
}
console.log(targetFn(3));
console.log(targetFn(3,2.3,4));
// 剩余参数
function buildName(firstname:number, ...restOfname:number[]) {
  return firstname + " " + restOfname.join("")
}
console.log(buildName(2,3,4,5,6));
// 匿名带参函数
var res = function(a:number,b:number) { 
  return a*b;  
}; 
console.log(res(9,9));

// 匿名自调用函数
(function () { 
  var x = "Hello!!";   
  console.log(x)     
})()
// 构造函数
var myFunction = new Function("a", "b", "return a * b"); 
// 递归函数
function factorial(number) {
  if (number <= 0) {         // 停止执行
      return 1; 
  } else {     
      return (number * factorial(number - 1));     // 调用自身
  } 
}; 
console.log(factorial(6));      // 输出 720
// Lambda 函数，也称之为箭头函数
var foo = (x:number)=>10 + x 
console.log(foo(100))      //输出结果为 110
// 函数重载？？
// 重载是方法名字相同，而参数不同，返回类型可以相同也可以不同
// 参数类型不同：
function disp1(string):void {}; 
function disp2(number):void {};
// 参数数量不同：
function disp3(n1:number):void {}; 
function disp4(x:number,y:number):void {};
// 参数类型顺序不同：
function disp5(n1:number,s1:string):void {}; 
function disp6(s:string,n:number):void {};
```