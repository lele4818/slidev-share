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