## Rax 开发记录

#### render

在 web 侧，如果不传递 container，默认直接 render 在 body 上，且不会清除 body 上已有的元素。

#### appendType

NativeComponent 有两种 appendType，分别是 node 和 tree，默认为 node。在 node 模式下，一个节点创建完后会立刻 append 到视图上，
随后再处理子节点，而 tree 模式下则是等整棵树完全处理完后再一起 append 到视图上。

#### style

本质上是 `css in js`，可以利用 `stylesheet-loader` 结合 `babel-plugin-transform-jsx-stylesheet` 
辅助开发，`rax` 已在内部解决 prefix 的问题。

#### rem

对于单位为 `rem` 或者没有写单位的样式，rax 会自动进行适配，内部基准为 750px，在 web 侧会基于此基准自动进行适配，
比如 iPhone6 的 375px 屏宽下（rem = 1/2），样式的像素值会自动减半。

- 在 weex 侧，rem 始终为 1
- 有单位的样式，rax 不会自动做适配

#### rax-components

rax 官方的跨容器组件，从实现上看，风格以 `isWeex` 作为差异化条件，比如：

```js
import { Component } from 'rax';
import { isWeex } from 'universal-env';

class MyComponent extends Component {
  render() {
    if (isWeex) {
      // weex env
    } else {
      // web env
    }
  }
}
```

建议所有跨容器组件都遵从此风格。
