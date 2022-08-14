# 函数(Function)

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