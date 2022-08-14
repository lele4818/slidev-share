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