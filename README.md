<p align="center"><img src="http://wx2.sinaimg.cn/mw690/0060lm7Tly1ftpm5b3ihfj3096097aaj.jpg" alt="fre logo" width="180"></p>
<h1 align="center">Fre</h1>
<p align="center">:ghost: Fast 1kb JavaScript library got Fiber scheduler and hooks API</p>
<p align="center">
<a href="https://npmjs.com/package/fre"><img src="https://img.shields.io/npm/v/fre.svg?style=flat-square" alt="npm-v"></a>
<a href="https://npmjs.com/package/fre"><img src="https://img.shields.io/npm/dm/fre.svg?style=flat-square" alt="npm-d"></a>
<a href="https://bundlephobia.com/result?p=fre"><img src="https://img.shields.io/bundlephobia/minzip/fre.svg?style=flat-square" alt="gzip"></a>
</p>

### Feature

- :tada: hooks API , really functionalComponents
- :confetti_ball: Fiber scheduler instead of diff algorithm
- :telescope: All in one , just 1 KB

### Introduction

Fre (pronounced `/fri:/`, like free) is a tiny and perfect javascript library, It means freedom ~

其实，free 是一部动漫名，也是我最喜欢的番没有之一，haru 是我儿子！ [参见 c 站](https://www.clicli.top/search/free)

### Compare

|        | 尺寸 |    组件化     |     特性     |
| :----: | :--: | :-----------: | :----------: |
|  fre   | 1kb  |     hooks     |    Fiber     |
| preact | 3kb  |     class     |     diff     |
|  vue   | 10kb |      SFC      | Proxy + diff |
| react  | 33kb | class + hooks |    Fiber     |

### Use

```JavaScript
import { h, render, useState } from 'fre'

function Counter() {
  const [count, setCount] = useState(0)
  return (
    <div>
      <h1>{count}</h1>
      <button onClick={() => setCount(count + 1)}>+</button>
    </div>
  )
}

render(<Counter />, document.getElementById('root'))

```

### Hooks API

纯 hooks API，完全移除 class ，class 和 hooks 是水火不容的，没办法配合使用，所以 hooks 对 class 是替代关系，而不是替补关系
所以现在的 react 可以说是两个框架，而 fre，hooks 是主角

```JavaScript
function Counter() {
  const [up, setUp] = useState(0)
  const [down, setDown] = useState(0)
  return (
    <div>
      <h1>{up}</h1>
      <button onClick={() => setUp(up + 1)}>+</button>
      <h1>{down}</h1>
      <button onClick={() => setDown(down -1)}>-</button>
    </div>
  )
}

render(<Counter />, document.getElementById('root'))
```

### FunctionalComponent

新的组件化方案，完全的 functional，组件通讯和 react 几乎一致

```JavaScript
function App() {
  const [count, setCount] = useState(0)
  return (
    <div>
      <h1>{count}</h1>
      <button onClick={() => setCount(count + 1)}>+</button>
      <Sex count={count}/>
    </div>
  )
}

function Sex(props){
  const [sex, setSex] = useState('boy')
  return (
    <div>
      <h2>{props.count}</h2>
      <h1>{sex}</h1>
      <button onClick={() => {sex==='boy'?setSex('girl'):setSex('boy')}}>x</button>
    </div>
  )
}

render(<App />, document.getElementById('root'))
```

### props

props 用于组件间通信，正在考虑将生命周期放到 props 中，也可能是单独写一个生命周期的 hook

```javascript
function App() {
  const [sex, setSex] = useState('boy')
  return (
    <div>
      <Sex sex={sex} />
      <button onClick={() => {sex === 'boy' ? setSex('girl') : setSex('boy')}}/>
    </div>
  )
}
function Sex(props) {
  return <div>{props.sex}</div>
}
```

#### Fiber

fre 可以说是 fiber 的最小实现了，不过 fiber 是内部调度，用来替代 diff 的，用户无需关注

fiber 中最关键的 `requestIdleCallbak` 默认兼容 ie11 ，使用 [polyfill](https://github.com/aFarkas/requestIdleCallback) 可兼容到 ie9+

#### JSX

默认也对外暴露了 h 函数，可以选用 JSX

```JavaScript
import { h } from 'fre'
```

webpack 需配置：

```JavaScript
{
  "plugins": [
    ["transform-react-jsx", { "pragma":"h" }]
  ]
}
```

当然，现在的 fre 更适合运行于浏览器环境，可以使用 [htm](https://github.com/developit/htm)

#### License

_MIT_ ©132yse
