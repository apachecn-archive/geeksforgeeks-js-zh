# 理解 JavaScript 中的异步

> 原文:[https://www . geesforgeks . org/understanding-the-async-in-JavaScript/](https://www.geeksforgeeks.org/understanding-the-async-in-javascript/)

**定义:** Async 是“异步”的简称。同步意味着一个接一个地执行语句，这意味着只有在前一条语句完全执行之后，下一条语句才会被执行。而在异步调用中，下一条语句甚至不用等待前一条语句的执行就能被执行。

JavaScript 是一种同步语言。这意味着默认情况下，文件中的第 10 行将在第 9 行之后运行。如果你在第 9 行声明一个变量并在第 10 行使用它，如果你在第 9 行之前运行第 10 行，你可能会撞到自己的头。

然而，打破这种流动也有一些好处，特别是当涉及到任何类型的网络数据传输时，因为这需要时间。这就是我们需要引入异步的地方——超越正常执行流程的能力，以节省时间。

我们刚刚听说 JavaScript 已经建立了同步，我们最好不要对该语言进行任何突破性的更改。此外，异步意味着我们必须引入线程并处理死锁。Java 做到了，相信我，我们最好不要用同样的方式让 JavaScript 复杂化。

**我们怎么做？**
答案在于 JavaScript 是如何工作的，或者更确切地说，它在浏览器的什么地方工作。它使用这些内置函数，通常称为网络浏览器应用编程接口，用于控制命令流、使用调用堆栈、网络数据提取等。这些网络浏览器应用编程接口通常被误认为是 JavaScript 的一部分，但实际上，它们是浏览器的一部分，JavaScript 只使用它们。

现在这样想，我们并不是真的希望 JavaScript 扰乱执行的流程，但是我们仍然希望一些代码行在预期之前运行。我们怎么做？很简单，让在控制流程方面有发言权的其他人暂停一些代码，同时，JavaScript 可以继续执行代码，本质上就是生成同步代码 Async。

听起来很可笑，但这是 JavaScript 一直在做的事情。

我们大多数人都听说过一个叫 **setTimeout()** 的函数方法。我们错误地认为它是一个 JavaScript 函数，但不幸的是，它不是。这是一个门面，一个幕后发生的奇怪事情的门面。而“幕后发生的怪事”就是名为“计时器”的网络浏览器应用编程接口。这就是我们的同步 JavaScript 代码开始异步的地方。

让我们用一个示例代码来看看这个。

## java 描述语言

```
function whoSaysGfg(){
    console.log('g');
}
setTimeout(whoSaysGfg, 1000);

console.log('f');
```

我们可能倾向于相信 **setTimeout()** 所做的是，等待 1000 毫秒，然后执行*whosesgfg()*函数，然后继续前进。

1000 毫秒内会发生什么？JavaScript 只是坐着拍苍蝇吗？如果他们那样做，他们将会是非常糟糕的开发者。相信我，他们一点也不差劲。实际发生的情况是 **setTimeout()** 是对 Timer API 的调用，timer limit 作为一个参数传入，在这种情况下是 1000ms，另一个参数是一个回调函数，当计时器计数到 1000 ms 时会运行。

**注意:【JavaScript 本质上所做的，是把*whosesgfg*执行的控制权让给了网页浏览器。JavaScript 的 **setTimeout** 行已经结束。它可以很好地继续下一行代码，而不用关心*whosesgfg*是否已经运行。所以，JavaScript 就变成了异步。**

试着猜测这可能是什么输出？

## java 描述语言

```
function whoSaysGfg(){
    console.log('g');
}

setTimeout(whoSaysGfg, 0);

console.log('fg');
```

如果你在想“gfg”，那是不正确的。如果你认为“fgg”，你是对的。我们可能倾向于认为超时值为 0 基本上没有任何意义，并且会立即回调*whosesgfg()*函数。

这与函数在浏览器中的调用和运行方式有关。当脚本运行并从那里被调用时，函数被添加到调用堆栈中。现在，当一个函数的执行被推迟到浏览器时，如 **setTimeout** 的情况，该函数位于一个队列中，称为任务队列或回调队列，或宏任务队列。它一直呆在那里，直到整个调用栈都是空的。

“事件循环”是一种服务，它不断检查调用堆栈和任务队列，并调度任务队列上的函数在调用堆栈为空时立即进入调用堆栈。

这样，同步语言 JavaScript 就变成了异步语言。

请注意，这不是最佳解决方案。像承诺和异步等待这样的解决方案已经出现，但这是理解异步概念的开始。