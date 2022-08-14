# type与interface的区别

<section v-click>

##### type可以为基本类型、联合类型、元组类型定义别名，而interface不行
```ts
type N = number // 基本类型
type A = string | number // 联合类型
type B = [number, string] // 元组类型
```
</section>

<section v-click mt-5>

<section grid grid-cols-2 gap-x-4>

```ts
interface A {
  name: string
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
  name: string
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