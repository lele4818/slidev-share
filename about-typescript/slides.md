---
# try also 'default' to start simple
theme: seriph
highlighter: shiki
colorSchema: dark
class: 'text-center'
# use UnoCSS (experimental)
css: unocss
---

# About Typescript

TypeScript is JavaScript with syntax for types.

---

# 数据类型

<section grid grid-cols-2 gap-x-4>
  <section>
  string类型

  ```ts
    const name: string = '天气真好'
  ```
  boolean类型

  ```ts
    const isSuccess: boolean = true
  ```
  number类型

  ```ts
    const age: number = 18
  ```  
  symbol类型

  ```ts
    const sy: symbol = Symbol('hhh')
  ```
  Array类型
  ```ts
    const list1: number[] = [1, 2, 3]

    // 数组泛型写法
    const list2: Array<number> = [1, 2, 3]
  ```
  </section>
  <section>
  null类型

  ```ts
    const isNull: null = null
  ```
  undefined类型

  ```ts
    const isUndefined: undefined = undefined
  ```
  Object类型
  ```ts
  type Person = {
    name: string,
    age: number
  }

  const o: Person= { name: '小明', age: 18 }
  ```

  </section>
</section>


---

# TS独有的数据类型 - any 与 unknown
<section grid grid-cols-2 gap-x-4>
<section>
any类型（top-type | bottom-type）

```ts
  let xx: any = '小明'
  xx = true
  xx = 20
  xx = '你好'
  xx = []
  xx = {}
```
unknown类型（top-type）
```ts
  // 
  let un: unknown
  un = true
  un = 20
  un = '你好'
  un = []
  un = {}
  ...
``` 
</section>

<section> 

<section v-click>

相同点
  - 都属于是顶级类型
  - 都能被任意类型赋值
</section>

<section mt>
  <section v-click>
  不同点

  - any可以是任意类型的父类型，同时也是任意类型的子类型；unknown只是任意类型的父类型，只是unknown和any的子类型
  </section>
  
  <section grid grid-cols-2 gap-x-4 v-click>
  <section>

  ```ts
  // ok
  let anyV: any 
  let value1: unknown = anyV 
  let value2: any = anyV 
  let value3: boolean = anyV 
  let value4: undefined = anyV 
  ...                           
  ```  

  </section>
  <section>

  ```ts
  // ok
  let unV: unknown 
  let value1: unknown = unV 
  let value2: any = unV 

  // error
  let value3: boolean = unV 
  let value4: undefined = unV 
  ...                           
  ```  
  
  </section>
  </section>

</section>

</section>
</section>

---

# TS独有的数据类型 - any 与 unknown

### 不同点
- any: 我不在乎它是什么类型；unknown: 我不知道它是什么类型（意味着unknown类型需要重点关注）

<section grid grid-cols-2 gap-x-4 v-click>
<section>

```ts
// any 语法检查都会通过
let value: any

// ok
value.name
value.trim()
value.push()
...
```
</section>
<section>

```ts
// unknown 语法检查都会失败
let value: unknown

// error
value.name
value.trim()
value.push()
...
```
</section>
</section>

<section grid grid-cols-2 gap-x-4 v-click>
<section>

```ts
  // any
  function addItem (list: any, item: number) {
    list.push(item)
  }

  const arr: number[] = []

  // 语法检查会通过，但是执行结果会报错
  addItem('你好', 2)
```
</section>

<section>

```ts
  // unknown 迫使开发者手动去做一些类型检查
  function addItem (list: unknown, item: number) {
    // list.push(item) // error Object is of type 'unknown'
    if (list instanceof  Array) {
      list.push(item)
    }
  }

  const arr: number[] = []

  // 语法检查时就会报错
  addItem('你好', 2)
```
</section>

</section>

---

# TS独有的数据类型 - Enum类型（枚举）

<section grid grid-rows-2 grid-cols-2 gap-x-4>
<section>
数字枚举

```ts
enum HttpCode {
  SUCCESS = 200
  FAILED = 500
}

const code: HttpCode = HttpCode.SUCCESS // 200

```
</section>
<section>
常量枚举

```ts
const enum NumberCollection {
  NORTH, // 0
  SOUTH, // 1
  EAST, // 2
  WEST, // 3
}
```
</section>
<section>
字符串枚举

```ts
enum Status {
  S = 'success',
  F = 'failed'
}

const s: Status = Status.s // success

```
</section>
<section>
异构枚举

```ts
enum EnumMix {
  A,       // 0
  B,       // 1  
  C = "C", // C
  D = "D", // D
  E = 8,   // 8
  F,       // 9
}

```
</section>
</section>

---

# TS独有的数据类型 - Tuple（元组）、Void、Never

<section grid grid-cols-2 gap-x-4>
<section>
元组类型：数组一般支持同种类型，元组可以支持不同类型且长度固定

```ts
let tupleType: [string, number]
tupleType = ['小明', 18]
```

元组：设置别名
```ts
let tupleType: [name: string, age: number];
tupleType = ['小明', 18]

// tupleType[0]的别名是name  tupleType[1]的别名是age
// 但是无法通过别名访问到具体的值 tupleType.name 为 undefined
```
</section>

<section>
Void：函数特有的类型

```ts
function doSomething(): void {
  //...
}
```

<section>
never类型：表示永远不存在的值的类型

```ts
function rejectError(message: string): never {
  throw new Error(message);
}  

// 可以利用never类型尽可能的保证类型的绝对安全
type Info = string | number
// type Info = string | number | boolean
function getInfo(msg: Info): void {
  if (typeof msg === 'string') {
    // ...
  } else if (typeof msg === 'number') {
    // ...
  } else {
    let value: never = msg;
    // ...
  }
}
```
</section>

</section>
</section>

--- 
--- 

# 函数（Function）

##### 类型：函数类型、入参类型、返回值类型

```ts
// 定义一个函数类型
type DoSumFn = (a: number, b: number) => number;

const doSum: DoSumFn = function(a: number, b: number): number {
  return a + b
}

doSum(1, 2) // 3
```

##### 可选参数、默认参数

```ts
// 注意把可选参数放在后面

function printInfo(name: string, age: number = 18, hobby?:string ): string {
  return `姓名：${name}, 年龄：${age}, 爱好：${hobby}`
}

printInfo('小明') // 姓名：小明, 年龄：18, 爱好：undefined
printInfo('小明', 20, '睡觉') // 姓名：小明, 年龄：20, 爱好：睡觉
```

---

# 函数（Function）

##### 函数重载

在javascript中没有重载的概念，重名函数会被覆盖

```js

function a () {
  console.log('出太阳了')
}

function a () {
  console.log('下雨了')
}

a() // 下雨了
```
---

# 函数（Function）

##### 函数重载

typescript中的重载指的是，声明多个同名函数，它们的参数类型不同

```ts
// 声明
type NumberOrString = string | number
function add (arg1: string, arg2: string): string
function add (arg1: number, arg2: number): number

// 实现
function add(a: NumberOrString, b: NumberOrString) {
  // 实现上要严格判断两个参数的类型是否相等
  if (typeof a === 'string' && typeof b === 'string') {
    return a + b
  } else if (typeof a === 'number' && typeof b === 'number') {
    return a + b
  }

  return ''
}
```
---

# 类型别名（type）与接口（interface）

<section grid grid-cols-2 gap-x-4>
<section>
`type`：用来给类型起一个新的名字，定义类型

```ts
  type isString = string
  const msg: isString = 'hello ts' 
```

只读属性、可选属性、任意属性
```ts
type Person = {
  name: string,
  age: number,
  // 只读 readonly
  readonly sex: string,
  // 可选 ?
  email?: string,
  // 任意属性：索引签名
  [prop: string]: any
}
```
</section>

<section>
`interface`: 定义一个对象类型

```ts
interface Person {
  name: string;
  age: number;
}
const p:Person = { name: '小明', age: 18 }
```
只读属性、可选属性、任意属性
```ts
interface Person {
  name: string,
  age: number,
  // 只读 readonly
  readonly sex: string,
  // 可选 ?
  email?: string,
  // 任意属性：索引签名
  [prop: string]: any
}
```
</section>

</section>

--- 

# type 与 interface的区别

<section v-click>

##### type可以为基本类型、联合类型、元组类型定义别名，而interface不行
```ts
type N = number // 基本类型
type A = string | number // 联合类型
type B = [number, string] // 元组类型
```
</section>

<section v-click>


<section grid grid-cols-2 gap-x-4>

```ts
interface A {
  name: string,
}

interface A {
  age: number
}

const value: A = {
  name: '小明',
  age: 18
}
```

```ts
type A = {
  name: string,
}

type A = {
  age: number
}

const value: A = {
  name: '小明',
  age: 18
}

// error: 重复定义类型A
```
</section>

</section>

---

# type 与 interface的扩展（& 与 extends）

<section grid grid-cols-2 gap-x-4>
<section v-click>
interface从interface扩展

```ts
interface A { x: number }

interface B extends A { y: number }

let value:B = { x: 1, y: 2 }
```
</section>
<section v-click>
interface从type扩展

```ts
type A = {
  x: number
}

interface B extends A { y: number }

let value:B = { x: 1, y: 2 }
```
</section>
<section v-click>
type从type扩展

```ts
type A = { x: number }

type B = A & { y: number }

let value:B = { x: 1, y: 2 }
```
</section>
<section v-click>
type从interface扩展

```ts
interface A { x: number }

type B = A & { y: number }

let value:B = { x: 1, y: 2 }
```
</section>
</section>

<section mt-5 v-click>
<font color=NavajoWhite> WARNING：type扩展仅能使用&，interface扩展可以使用extends 或者 & </font>

<section>
type <font color=red> & </font> (type 或者 interface) <br/>
interface <font color=red> & </font> (type 或者 interface) <br/>
interface <font color=red> extends </font> (type 或者interface)
</section>
</section>

---

# type与interface的使用场景

<section grid grid-cols-2 gap-x-4>
<section v-click>
type

- 定义基本类型的别名时

- 定义元组类型时
- 定义函数类型时

```ts
  type StringReturnFn = (name: string) => string
  
  let test: StringReturnFn = function (name: string):string {
    // ...
    return name
  }
```

- 定义联合类型时

</section>
<section v-click>
interface

- 需要利用接口自动合并特性的时
- 定义对象类型时
</section>
</section>


---

# 联合类型与交叉类型

- 联合类型：产生一个包含所有类型的选择集
- 交叉类型：产生一个所有属性的新类型
<section grid grid-cols-2 gap-x-4 mt>
<section v-click>
联合类型（|）

```ts
  type EmptyValue = null | undefined | ''
  // null、undefined、''
  const v: EmptyValue = null 

  // 定义对象
  type A = { name: string}
  type B = { age: number }
  type C = A | B

  let o: C = { name: '小明', age: 20 }
```
</section>
<section v-click>
交叉类型（& ）: 用于对象

```ts
  type A = { name: string}
  type B = { age: number }
  type C = A & B

  let o: C = { name: '小明', age: 20 }
```
</section>
</section>

---

# 联合类型与交叉类型
<section>

<font color=NavajoWhite> WARNING </font>

当有多个类型中有重复属性且类型不同时，联合类型会表现正常，交叉类型会表现异常
<section>

```ts
type A = { 
  value: string
}
type B = { 
  value: boolean
}

// 联合类型
type C = A | B 
let v:C = { 
  value: 'hello'
}
v = { 
  value: true
}

// 交叉类型
type D = A & B // 此时D为never类型
```
</section>
</section>

--- 

# 泛型 T

<section grid grid-cols-2 gap-x-4>
<section>

```ts
function sayHi(value: string): string {
  console.log(value)
  return value
}

sayHi('hi')
```

</section>
<section>

```ts
function sayHi<T>(value: T): T {
  console.log(value)
  return value
}

sayHi<string>('hi')
```
</section>

<section mt v-click>
  多个泛型参数

  ```ts
  function saySomething<T, U>(value: T, msg: U) : T {
    console.log(msg)
    return value
  }

  // 显示指定泛型变量的类型 T => string 、U => number
  saySomething<string, number>('你好', 20)
  // 让typescript自己去推导泛型变量的类型
  saySomething('你好', 20)
  ```
</section>

<section mt-5 v-click>
  泛型变量不一定只能用T表示，理论上可以用任意字母

  常见的有
  
  - T (Type)： 表示类型
  - K (Key)：  表示对象的键的类型
  - V (Value)：表示对象中的值的类型
</section>
</section>

---

# 常见操作符
<section v-click>
typeof
<section grid grid-cols-2 gap-x-2>
  <section>
  <h6>判断基本类型</h6>

  ```ts
  let s = 'hello'
  let n = 1
  let b = true

  typeof s === 'string'
  typeof n === 'number'
  typeof b === 'boolean'
  ```
  </section>

  <section>
  <h6>获取变量的声明或者对象的类型</h6>

  ```ts
  interface P {
    name: string
    age: number
  }
  const a: P = { 
    name: '小明', 
    age: 20
  }
  type S = typeof somebody // Person

  const obj = { name: '小明', age: 20 }
  type O = typeof obj // { name: sting, age: number }
  ```
  </section>
</section>
</section>

<section grid grid-cols-2 gap-x-4>
<section v-click>
in：遍历枚举值

```ts
type Keys = 'name' | 'age' | 'hobby'

type Info = {
  [prop in Keys]: string
}

// { 'name': string, 'age': 'string', 'hobby': sting }
```
</section>

<section v-click>
keyof：遍历key

```ts
interface Person {
  name: string;
  age: number;
}
type P = {
  [ name in keyof Person ]: Person[name]
}
// { name: string, age: number }
```
</section>
</section>

