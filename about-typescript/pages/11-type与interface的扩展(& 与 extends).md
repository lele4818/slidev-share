# type与interface的扩展(& 与 extends)

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
type <font color=green> & </font> (type 或者 interface) <br/>
interface <font color=green> & </font> (type 或者 interface) <br/>
interface <font color=green> extends </font> (type 或者interface)
</section>
</section>