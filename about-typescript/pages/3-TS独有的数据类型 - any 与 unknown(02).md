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