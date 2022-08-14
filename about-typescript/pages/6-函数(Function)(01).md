# 函数(Function)

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
