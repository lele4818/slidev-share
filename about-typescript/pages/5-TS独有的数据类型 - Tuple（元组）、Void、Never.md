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