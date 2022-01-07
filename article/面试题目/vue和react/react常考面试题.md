## 1. 生命周期

**不展示不常用的生命周期**

![image-20210630171416757](/Users/hzq/Library/Application Support/typora-user-images/image-20210630171416757.png)

**展示不常用生命周期**

![image-20210630171407188](/Users/hzq/Library/Application Support/typora-user-images/image-20210630171407188.png)

#### 常用的三个

**componentDidMount()**

- 方法在组件挂载后（插入 DOM 树中） 立即调用。依赖于 DOM 节点的初始化应该放在这里。如需通过网络请求获取数据，此处是实例化的好地方。
- 这个方法是比较适合添加订阅的地方。如果添加了订阅，请不要忘记在 `componentWillUnmount()` 里面取消订阅
- 也可以在方法里**直接调用 setState()**. 它将触发额外渲染，但是此渲染会发生在浏览器更新屏幕之前。如此保证了即使在 `render()` 两次调用的情况下，用户也不会看到中间状态。需要谨慎使用该模式，因为它会导致性能问题。通常，你应该在 `constructor()` 中初始化 state。如果你的渲染依赖于 DOM 节点的大小或位置，比如实现 modals 和 tooltips 等情况下，你可以使用此方式处理

**componentDidUpdate()**

- 方法在更新后会被立即调用。首次渲染不会执行此方法。
- 当组件更新后，可以在此处对 DOM 进行操作。如果你对更新前后的 props 进行了比较，也可以选择在此处进行网络请求。（例如，当 props 未发生变化时，则不会执行网络请求）。

```jsx
componentDidUpdate(prevProps) {
  // 典型用法（不要忘记比较 props）：
  if (this.props.userID !== prevProps.userID) {
    this.fetchData(this.props.userID);
  }
}
```

- 你也可以在 componentDidUpdate() 中**直接调用 setState()**，但请注意它必须被包裹在一个条件语句里，正如上述的例子那样进行处理，否则会导致死循环。它还会导致额外的重新渲染，虽然用户不可见，但会影响组件性能，不要将 props“镜像”给 state，请考虑直接使用 props。

如果 shouldComponentUpdate() 返回 false 就不会调用 componentDidUpdate()

**componentWillUnmount()**

- 会在组件卸载及销毁之前直接调用。在此方法中执行必要的清理操作，例如，清除 timer，取消网络请求或清除在 componentDidMount() 中创建的订阅等
- **不应调用 setState()**，因为该组件将永远不会重新渲染。组件实例卸载后，将用户不会再挂载它。

#### 不常用生命周期

**shouldComponentUpdate(nextProps, nextState)**

- 根据该方法的返回值，判断 React 组件的输出是否受当前 state 或 props 更改的影响。默认行为是 state 每次发生变化组件都会重新渲染。大部分情况下，你应该遵守默认行为
- 当 props 或 state 发生变化时，shouldComponentUpdate() 会在渲染执行之前被调用。返回值默认 true。首次渲染或使用 forceUpdate() 时不会调用该方法
- 此方法仅作为性能优化的方式而存在。不要企图依靠此方式来"阻止"渲染，因为这可能会产生 bug。你应该考虑使用内置的 PureComponent 组件，而不是手动编写该方法。PureComponent 会对 props 和 state 进行浅层比较。并减少了跳过必要更新的可能性。
- 如果你一定要手动编写，可以将 this.props 与 nextProps 以及 this.state 与 nextState 进行比较，并返回 false 以告诉 React 可以跳过更新。请注意，返回 false 并不会阻止组件在 state 更改时重新渲染。
- 不建议在改函数中进行深层次比较或者使用 JSON.stringify()。这样非常影响效率，且会损害性能。
- 目前，如果该函数返回 false，则不会调用 UNSAFE_componentWillUpdate()，render() 和 componentDidUpdate()。后续版本，React 可能会讲 该函数 视为提示而不是严格的指令，并且，当返回 false 时，仍可能导致组件重新渲染

**static getDerivedStateFromProps(props, state)**

- getDerivedStateFromProps 会在调用 render 方法之前调用，并且在初始挂载及后续更新时都会被调用。它应返回一个对象来更新 state，如果返回 null 则不更新内容。
- 此方法适用于罕见的用例，即 state 的值在任何时候都取决于 props。

**getSnapshotBeforeUpdate(prevProps, prevState)**

- 在最近一次渲染输出（提交到 DOM 节点）之前调用。它使得组件能在发生更改之前从 DOM 中捕获一些信息（例如，滚动位置）。此生命周期的任何返回值将作为参数传递给 `componentDidUpdate()`


## 2. setState

## 3. 性能优化

## 4. husky