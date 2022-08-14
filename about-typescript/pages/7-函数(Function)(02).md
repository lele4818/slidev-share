# 函数(Function)

##### 函数重载

在javascript中没有重载的概念，重名函数会被覆盖

```js

function a () {
  console.log('出太阳了')
}

function a () {
  console.log('下雨了')
}

a() // 下雨了
```