# 类型别名(type)与接口(interface)

<section grid grid-cols-2 gap-x-4>
<section>
  type：用来给类型起一个新的名字，定义类型

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
interface: 定义一个对象类型

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