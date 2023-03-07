---
title: "React16.8中的effect"
date: 2023-03-07T16:48:25+08:00
draft: true
---

### 加入依赖是在做什么
useEffect本身是组件每次渲染都会执行的，加入effect是为了减少其执行的次数

加入空数组代表只执行一次

加入其他变量，表示在其改变的时候执行

当你调用 useEffect时，就是在告诉 React 在完成对 DOM 的更改后运行你的“副作用”函数。

useEffect是在dom更新完成后做的事情。

一般来说，函数退出后，变量会销毁，而state中的变量会被react保留

const [count, setCount] = useState(0);

我们声明了一个叫count的state变量，然后把它设置为0。React会在重新渲染时记住它当前的值，并提供最新的值给我们的函数。

之所以叫做useState而不是createState，就是我们并不是每次都create这个state变量，而是只在组件第一次渲染的时候创建。

当用户点击后，我们传递一个新的值给setCount。React会重新渲染Example组件，并把最新的count传给它。

如果我们想使用多个state变量，它允许我们给不同的state变量取不同的名称。

我们可以单独更新每一个state。（理解： 我们单独更新一个state, react会重新渲染函数组件，并用每个state的最新值去渲染，我们更新的那个state状态，得到更新，而那些没有setState的变量，之前的值就是最新的）

当我们的state变量是一个复杂的对象或者数组时，不同于class的this.setState，更新state变量总是替换而不是合并。（理解： clss组件中的setState是合并式的更新，因此我们得以单独的跟新state中的某一个值）

### 副作用
数据获取、设置订阅以及手动更改react组件中的dom都属于副作用。

1、无需清除的副作用

有时候，我们只想在react更新dom之后运行一些额外的代码。比如发送网络请求

，手动更新dom，记录日志等。

在class组件中，render函数是不应该有任何副作用的。

我们基本都希望在react更新dom之后才执行我们的操作。

这就是为什么我们把副作用操作放在componentDidMount 和

componentDidUpdate函数中。

useEffect(() => {
document.title = you clicked ${count} times
})

通过这个hook,你可以告诉react组件需要在渲染后执行某些操作。

React会保存你传递的函数（我们将它称之为effect，重点理解：effect是我们

传递的函数！！！而不是useEffect这个hooks api），并且在执行dom更新

之后调用它。（理解：在useEffect中我们给它传递的是一个回调函数，将我们

需要的操作放在回调函数中，react会在每次更改dom后执行我们的回调函数）

理解： 因为我们传递的是一个函数，而函数是一个引用数据类型的数组，

所以传递给useEffect的函数在每次渲染中都会不一样，每次渲染都会有自己的

回调函数（内存地址不同，不是同一个函数对象），这是刻意为之。这正是

我们可以在effect中获取最新的count的值，而不用担心其过期的原因。

每次我们重新渲染，都会生成新的effect，替换掉之前的（effect是我们写在useEffect中的回调函数！！）

某种意义上讲effect更像是渲染结果的一部分——每个effect 属于一次特定的渲染。

不理解的地方：提示
与 componentDidMount 或 componentDidUpdate 不同，使用 useEffect 调度的 effect 不会阻塞浏览器更新屏幕，这让你的应用看起来响应更快。大多数情况下，effect 不需要同步地执行。在个别情况下（例如测量布局），有单独的 useLayoutEffect Hook 供你使用，其 API 与 useEffect 相同。

是什么意思？

解惑： useLayoutEffect 的函数签名与useEffect相同，但是它会在所有的DOM变更之后同步调用effect。可以使用它来读取DOM布局并同步触发重渲染。在浏览器执行绘制之前，

useLayoutEffect内部的更新计划将被同步刷新。尽可能的使用标准的useEffect以避免阻塞视觉更新。

useLayoutEffect与componentDidMount componentDidUpdate 的调用阶段是一样的。

理解： 就是说类似vue中的nextTick componentDidMount componentDidUpdate useLayoutEffect, 会在dom更新完毕，浏览器执行绘制（肉眼看到新的页面）之前执行，如果在这里面做复杂的计算就会阻塞页面的渲染。而useEffect会在页面渲染完毕之后执行，所以不会阻塞页面的绘制渲染。

http://www.soolco.com/post/73226_1_1.html。 // 这篇文章说的很清楚

2、需要清除的effect

如果你的effect返回一个函数，react将会在执行清除操作时调用它（理解：写在这里的回调函数会在react卸载的时候执行，你可以在这块空间做任何自己的操作，同样我们也是return一个函数定义给react，react会在销毁的时机去调用它）

忘记正确地处理componentDidUpdate是React应用中常见的bug来源。

useEffect默认就会处理，它会在调用一个新的effect之前对前一个effect进行清理。

如果某些特定值在两次重新渲染之间没有发生变化，可以通知react跳过对effect的调用，只要传递数组作为useEffect的第二个参数即可。理解：所以我们传递第二个参数是为了减少effecta执行的次数。

自定义hook是一个函数，函数内部可以调用其他的hook
与React组件不同的是，自定义hook不需要具有特殊的标识。我们可以自由的决定它的参数是什么，以及它应该返回的是什么（理解： 自定义hook不必须返回 一个值和一个set值的函数，换句话说，不非要成对出现，可以自由定义返回的东西，根据需求来）

在多个hook之间传递信息：

由于hook本身是函数，因此我们可以在他们之间传递信息。就像下面这样：

const [recipentID, setRecipentID] = useState(1);

const isRecipentOnline = useFriendStatus(recipientID);

当我们通过select调用setRecipentID ，改变了recipentID后，useFriendStatus也会用最新的recipientID来执行。

惰性初始state

initialState参数只会在组件的初始化渲染中起作用，后续渲染时会被忽略。如果初始state需要通过复杂计算获得，则可以传入一个函数，在函数中计算并返回初始的state,此函数只在初始渲染的时候被调用：

const [state, setState] = useState(() => {
const initialState = someExpensiveComputation(props);
return initialState
})

调用state hook的更新函数并传入当前的state时，react会跳过子组件的渲染以及effect的执行，react使用Object.is比较算法来比较state.

useCallback

const memoizedCallback = useCallback(() => {
doSomething(a, b);
}, [a, b]),

返回一个memoized的回调函数。

把内联回调函数及依赖项数组作为参数传入useCallback,

它将返回该回调函数的memoized版本，该回调函数仅仅在

某个依赖项改变时才会更新。

当把回调函数传递给经过优化的并使用引用相等性去避免非必要

渲染的子组件时，它将非常有用。比如（shouldComponentUpdate）

useCallback(fn, deps)相当于useMemo(() => fn, deps).

useMemo

返回一个memoized值。

把创建函数和依赖项数组作为参数传入useMemo,它仅会在某个依赖改

变时才会重新计算memoized值。这种优化有助于避免每次渲染时

都进行高开销的计算。

传入useMemo的函数会在渲染期间执行。不要在这个函数中执行与

渲染无关的操作。

可以把useMemo作为性能优化的手段，但不要把它作为语义上的保证。

应该先编写在没有useMemo的情况下也可以执行的代码—之后再在代码中

添加useMemo，以达到性能优化的目的。