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