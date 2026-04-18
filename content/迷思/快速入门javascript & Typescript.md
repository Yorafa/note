### 类型

可以使用 `interface` 或者 `type` 快速定义类型。当你不知道某个function返回的是什么类型的值的时候可以使用`ReturnType<typeof someFunc>`来获得返回值类型.
js/ts 除了主要类型 `string, number, boolean, null, undefined, symbol, bigint` 之外都是`Object`. 也就是说`Array, Object, Function, Map, Set, ...` 都是`Object` 都可以用`obj[key] = val` 进行赋值并访问。而主要类型都是`immutable`的.
`new` ? 如果不使用 `new` 则只会将后面的 `Constructor()` 当普通function运行。

### `===` ? `==` ?

`===` use to compare two variables' values if same
`==` use to compare two variables if same

### for loop?

`for (const x in smth)` or `for (const x of smth)`
`in` 通常用在 enumerable properties of an object .  It iterates over the keys (property names) of the object.
`of` 通常用在 iterable object

### Closure 闭包

当你在函数中定义了并返回了其他函数，并且其他函数会引用原来函数内容时，这就是一个闭包函数。外部通常无法访问闭包内的变量数据等。

### 数组的Callback Function

1. `arr.reduce((accumulator, curr) => {}, init);`: 这里的reduce是推理归纳而非减少, 使用reduce可以将`curr`以某种你想要的方式结合到`init`里. 也就是说，`accumulator` 在刚开始是`init`, 随着`reduce`的进行，`accumulator` 等于一个把所有遍历过的`curr`整合进`init`里的值
2. `arr.filter((val, idx) => {})`: 可以利用filter把不想要的设置成false这样就不会被选中，想要的设置成true，filter会return一个新的数组
3. `arr.map((val, idx) => {})`: 可以把每个值都进行一次你想要的transform，map会return一个新的数组

### Promise

js的promise感觉就是python的coroutine. 生成`Promise` 对象需要实现对应的函数如:
`const prom = new Promise((resolve, reject) => {})`

#### async && await

所有`async function` 的返回值一定是Promise, 如果没有做promise处理会隐式的帮你处理。
`await promise` 只能用在`async function`中用于暂停`function`直到后面的`promise`完成
假如说我们有`const prom = new Promise((res, rej) => {...});`. 我们可以使用`await prom`等待它完成, 对于多个promise，可以使用`await Promise.all([...])` 一次性等待全部完成。

#### then && catch && finally

此外 Promise有三种状态Pending, fulfilled 和 Reject.
如果不使用 `await`或者有什么要连锁处理的， 则需要使用

```javascript
prom
  .then((result) => {}) // promise fulfilled
  .catch((error) => {}) // promise reject
  .finally(() => {}) // promise done
```

其中`.then()` 可以进行连锁处理，也就是说可以`.then().then().{....}.then()` 如果前面的`.then()`中返回promise对象。因为是连锁的所以我们`.catch()`和`.finally()`不需要做更改保持原来放在后面的位置就可以处理对应的错误

#### Race

利用`Promise.race(promiseList)` 返回最先完成的`Promise`

### Time

`const timerID = setTimeout(funcCallAfterTimeOut, time);` 在`time`毫秒过后执行`funcCallAfterTimeOut` 函数，同时返回了一个`timerID`可以用于暂停这个timeout。例如使用`clearTimeout(timerID)`
`const intervalId = setInterval(funcCall, time);` 每`time`毫秒过后执行`funcCall` 函数，同时返回了一个`intervalId`可以用于暂停这个interval。例如使用`clearInterval(intervalId)`

### 杂项迷思

object 没有大小，`obj.length` 是一个 `undefined` 值。 如果想把它当unordered map来使用需要配合 `Object` 内置库使用，例如`Object.keys, Object.values, Object.entries`. Object 根据 numeric string / number keys 排序. 如果key不属于这个范畴则按照插入顺序。`symbol`则会被排到最后。
`Map` 只能 通过`Map.entries(), Map.keys(), Map.values()` 来进行 for loop
