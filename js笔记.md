## Promise
### Promise是什么
* promise是一个对象，对象和函数的区别就是对象可以保存状态，函数不可以（闭包除外）

* 并未剥夺函数return的能力，因此无需层层传递callback，进行回调获取数据
* 代码风格，容易理解，便于维护
* 多个异步等待合并便于解决
### 作用
1. 主要用于异步计算

2. 可以将异步操作队列化，按照期望的顺序执行，返回符合预期的结果
3. 可以在对象之间传递和操作promise，帮助我们处理队列
### Promise详解
```javascript
new Promise(
  function (resolve, reject) {
    // 一段耗时的异步操作
    resolve('成功') // 数据处理完成
    // reject('失败') // 数据处理出错
  }
).then(
  (res) => {console.log(res)},  // 成功
  (err) => {console.log(err)} // 失败
)
```
* resolve作用是，将Promise对象的状态从“未完成”变为“成功”（即从 pending 变为 resolved），在异步操作成功时调用，并将异步操作的结果，作为参数传递出去；

* reject作用是，将Promise对象的状态从“未完成”变为“失败”（即从 pending 变为 rejected），在异步操作失败时调用，并将异步操作报出的错误，作为参数传递出去。

* promise有三个状态：

        1. pending[待定]初始状态
        2. resolved[实现]操作成功
        3. rejected[被否决]操作失败

    * 当promise状态发生改变，就会触发then()里的响应函数处理后续步骤；promise状态一经改变，不会再变。

* Promise对象的状态改变，只有两种可能：

        1. 从pending变为resolved
        2. 从pending变为rejected

    * 这两种情况只要发生，状态就凝固了，不会再变了。
