---
title: react
date: 2019-02-14 11:30:10
tags: 前端
---
## 创建一个简单的jsx
简介：React是由Facebook创建和维护的开源视图库。它是渲染现代Web应用程序的用户界面（UI）的绝佳工具。
React使用名为JSX的JavaScript语法扩展，允许您直接在JavaScript中编写HTML。这有几个好处。它允许您在HTML中使用JavaScript的完整程序功能，并有助于保持代码的可读性。在大多数情况下，JSX与您已经学过的HTML类似，但是在这些挑战中将会涉及一些关键差异。
例如，因为JSX是JavaScript的语法扩展，所以您实际上可以直接在JSX中编写JavaScript。
但是，由于JSX不是有效的JavaScript，因此必须将JSX代码编译为JavaScript。转换器Babel是这个过程的流行工具。
`ReactDOM.render(JSX, document.getElementById('root'))。`这个函数调用是将JSX置于React自己的DOM轻量级表示中的原因。然后，React使用自己的DOM快照来优化仅更新实际DOM的特定部分。


```
const JSX = <h1>Hello JSX!</h1>;
```
## 创建一个复杂的jsx
关于嵌套JSX的一个重要事项是它必须返回一个元素。 这个父元素将包装所有其他级别的嵌套元素。

## 在jsx中加注释
SX是一种可以编译成有效JavaScript的语法。有时，为了便于阅读，您可能需要在代码中添加注释。像大多数编程语言一样，JSX有自己的方法来做到这一点。
要将注释放在JSX中，可以使用语法{/ * * /}来包含注释文本。

## 将HTML元素渲染到DOM
到目前为止，您已经了解到JSX是一种在JavaScript中编写可读HTML的便捷工具。使用React，我们可以使用React的渲染API（称为ReactDOM）将此JSX直接渲染到HTML DOM。
ReactDOM提供了一种将React元素呈现给DOM的简单方法，如下所示：ReactDOM.render（componentToRender，targetNode）,其中第一个参数是要渲染的React元素或组件，第二个参数是要将组件渲染到的DOM节点。
正如您所料，必须在JSX元素声明之后调用ReactDOM.render（），就像在使用它们之前必须声明变量一样。

```
const JSX = (
  <div>
    <h1>Hello World</h1>
    <p>Lets render this to the DOM</p>
  </div>
);
// change code below this line
ReactDOM.render(JSX, document.getElementById('challenge-node'))
```

## 在JSX中定义HTML类
现在您已经开始编写JSX了，您可能想知道它与HTML的区别。 到目前为止，似乎HTML和JSX完全相同。
JSX的一个关键区别是你不能再使用单词class来定义HTML类。这是因为class是JavaScript中的保留字。相反，JSX使用className。
事实上，JSX中所有HTML属性和事件引用的命名约定都变成了camelCase。例如，JSX中的单击事件是onClick，而不是onclick。同样，onchange变为onChange。虽然这是一个微妙的差异，但重要的是要记住前进。

```const JSX = (
  <div className="myDiv"> 
    <h1>Add a class to this div</h1>
  </div>
);
```

## 了解自我关闭的JSX标签
到目前为止，您已经看到JSX与HTML的不同之处在于使用className与class来定义HTML类。
JSX与HTML的另一个重要区分是自闭标签。

```
在HTML中，几乎所有标签都有开始和结束标签：<div> </ div>;结束标记在您要关闭的标记名称之前始终具有正斜杠。但是，HTML中有一些称为“自关闭标记”的特殊实例，或者在另一个标记可以启动之前不需要开始和结束标记的标记。
例如，换行标记可以写成<br>或<br />，但不应该写为<br> </ br>，因为它不包含任何内容。
在JSX中，规则略有不同。任何JSX元素都可以使用自闭合标记编写，并且必须关闭每个元素。例如，换行标记必须始终写为<br />才能成为可以转换的有效JSX。
另一方面，<div>可以写为<div />或<div> </ div>。不同之处在于，在第一个语法版本中，无法在<div />中包含任何内容。
```

```
const JSX = (
  <div>
    <h2>Welcome to React!</h2> <br/>
    <p>Be sure to close all tags!</p>
    <hr/>
  </div>
);

```

## 创建无状态功能组件
组件是React的核心。 React中的所有内容都是一个组件，在这里您将学习如何创建一个组件。
有两种方法可以创建React组件。第一种方法是使用JavaScript函数。以这种方式定义组件会创建无状态功能组件。应用程序中的状态概念将在以后的挑战中介绍。现在，将无状态组件视为可以接收数据并对其进行渲染的组件，但不管理或跟踪对该数据的更改。 （我们将介绍在下一次挑战中创建React组件的第二种方法。）
要使用函数创建组件，只需编写一个返回JSX或null的JavaScript函数。需要注意的一件重要事情是，React要求您的函数名称以大写字母开头。这是一个在JSX中分配HTML类的无状态功能组件的示例：

```
// After being transpiled, the <div> will have a CSS class of 'customClass'
const DemoComponent = function() {
  return (
    <div className='customClass' />
  );
};
```

因为JSX组件代表HTML，所以您可以将几个组件放在一起以创建更复杂的HTML页面。这是React提供的组件架构的关键优势之一。它允许您从许多独立的独立组件中组合UI。这使得构建和维护复杂的用户界面变得更加容易。无状态功能组件又称为纯组件SFC


## 创建有状态的react组件
定义React组件的另一种方法是使用ES6类语法。在以下示例中，Kitten扩展了React.Component：

```
class Kitten extends React.Component {
  constructor(props) {
    super(props);
  }

  render() {
    return (
      <h1>Hi</h1>
    );
  }
}
```

这将创建一个ES6类Kitten，它扩展了React.Component类。因此，Kitten类现在可以访问许多有用的React功能，例如本地状态和生命周期钩子。如果您还不熟悉这些术语，请不要担心，在以后的挑战中将更详细地介绍它们。
另请注意，Kitten类在其中定义了一个调用super（）的构造函数。它使用super（）来调用父类的构造函数，在本例中为React.Component。构造函数是在使用class关键字创建的对象初始化期间使用的特殊方法。最好使用super调用组件的构造函数，并将props传递给它们.这可确保组件正确初始化。现在，知道包含此代码是标准的。很快你会看到构造函数和道具的其他用途。

## 在父组件中调用子组件
现在我们来看看如何组合多个React组件。想象一下，您正在构建一个应用程序并创建了三个组件，一个Navbar，Dashboard和Footer。
要将这些组件组合在一起，您可以创建一个App父组件，它将这三个组件中的每一个都呈现为子组件。要在React组件中将组件呈现为子组件，您在JSX中包含作为自定义HTML标记编写的组件名称。例如，在render方法中，您可以编写：

```
return (
<App>
  <Navbar />
  <Dashboard />
  <Footer />
</App>
)

```
## 使用React渲染嵌套组件
组件组合是React强大的功能之一。当您使用React时，重要的是开始根据组件（如上一个挑战中的App示例）考虑您的用户界面。您将UI分解为其基本构建块，这些块成为组件。这有助于将负责UI的代码与负责处理应用程序逻辑的代码分开。它可以大大简化复杂项目的开发和维护。


## 从头开始写一个React组件
请记住，典型的React组件是扩展React.Component的ES6类。它有一个返回HTML（来自JSX）或null的render方法。这是React组件的基本形式。一旦你理解了这一点，你就会准备开始构建更复杂的React项目。
    

```
class MyComponent extends  React.Component{
  constructor(props) {
    super(props);
  }
  render() {
    return (<h1>My First React Component!</h1>)
  }
};

ReactDOM.render(<MyComponent/>, document.getElementById('challenge-node'));

```

## 将属性传递给无状态功能组件
有了这个基础，现在是时候看看React中常见的另一个特性：道具。在React中，您可以将props或属性传递给子组件。你有一个App组件，它呈现一个名为Welcome的子组件，它是一个无状态的功能组件。您可以通过编写以下方式传递欢迎用户属性：
先定义无状态组件,{Date()}为获取当前日期：

```
const CurrentDate = (props) => {
  return (
    <div>
      <p>The current date is: {props.date}</p>
    </div>
  );
};

class Calendar extends React.Component {
  constructor(props) {
    super(props);
  }
  render() {
    return (
      <div>
        <h3>What date is it?</h3>
        <CurrentDate date={Date()}/>
      </div>
    );
  }
};

```

## 传一个数组作为参数
着眼于如何将数组作为道具传递。要将数组传递给JSX元素，必须将其视为JavaScript并用大括号括起来。

```<ParentComponent>
  <ChildComponent colors={["green", "blue", "red"]} />
</ParentComponent>
```

然后子组件可以访问数组属性颜色。访问属性时可以使用诸如join（）之类的数组方法。

```
const ChildComponent = (props) => <p>{props.colors.join(', ')}</p>
```

这会将所有颜色数组项连接成逗号分隔的字符串并生成：

```
<p>green, blue, red</p>
```

## 使用默认属性
React还有一个设置默认道具的选项。您可以将默认道具分配给组件作为组件本身的属性，如果需要，React会分配默认属性。

```
MyComponent.defaultProps = { location: 'San Francisco' }
```

## 覆盖默认属性
直接传具体值过去，以下覆盖了quantity的默认为0的属性值

```
const Items = (props) => {
  return <h1>Current Quantity of Items in Cart: {props.quantity}</h1>
}

Items.defaultProps = {
  quantity: 0
}

class ShoppingCart extends React.Component {
  constructor(props) {
    super(props);
  }
  render() {
    return <Items quantity={10}/>
  }
};
```


## 使用PropTypes定义您期望的属性,[参考](https://reactjs.org/docs/typechecking-with-proptypes.html)
您可以在组件上设置propTypes，以要求数据类型为数组。当数据是任何其他类型时，这将发出有用的警告。
当您提前知道道具类型时，设置propTypes被认为是最佳做法。您可以使用与定义defaultProps相同的方式为组件定义propTypes属性。这样做将检查给定键的道具是否存在给定类型。这是一个需要类型函数的示例，名为handleClick的prop：

```
MyComponent.propTypes = { handleClick: PropTypes.func.isRequired }
```

在上面的示例中，PropTypes.func部分检查handleClick是否为函数。添加isRequired告诉React handleClick是该组件的必需属性。如果未提供该属性，您将看到警告。还要注意func代表函数。在七种JavaScript原语类型中，函数和布尔值（写为bool）是唯一使用异常拼写的两种类型。除了原始类型之外，还有其他类型可用。例如，您可以检查prop是否为React元素。有关所有选项，请参阅文档：

```  
  optionalArray: PropTypes.array,
  optionalBool: PropTypes.bool,
  optionalFunc: PropTypes.func,
  optionalNumber: PropTypes.number,
  optionalObject: PropTypes.object,
  optionalString: PropTypes.string,
  optionalSymbol: PropTypes.symbol,
```
  
  
## 使用this.props来访问属性
无论何时在您自己引用类组件时，都使用this关键字。要访问类组件中的props，请在前面使用此代码来访问它。例如，如果ES6类组件具有名为data的prop，则在JSX中编写{this.props.data}。

## 检查使用无状态功能组件的属性
无状态功能组件是您编写的任何接受道具并返回JSX的函数。另一方面，无状态组件是扩展React.Component的类，但不使用内部状态（在下一个挑战中涵盖）。最后，有状态组件是保持其自身内部状态的任何组件。您可能会看到有状态组件简称为组件或React组件。

一种常见的模式是尽可能地减少有状态并创建无状态功能组件。这有助于将状态管理包含到应用程序的特定区域。反过来，通过更容易地了解状态更改如何影响其行为，这可以改善应用程序的开发和维护。

## 创建有state的组件
React最重要的主题之一是state。 State包含应用程序需要了解的任何数据，这些数据可能会随时间而变化。您希望应用程序响应状态更改并在必要时显示更新的UI。 React为现代Web应用程序的状态管理提供了一个很好的解决方案

您可以通过在构造函数中声明组件类的状态属性来在React组件中创建状态。这会在创建组件时使用状态初始化组件。必须将state属性设置为JavaScript对象。

```
this.state = {
  // describe your state here
}
```

您可以在组件的整个生命周期内访问状态对象。您可以更新它，在UI中呈现它，并将其作为道具传递给子组件。状态对象可以像您需要的那样复杂或简单。请注意，您必须通过扩展React.Component来创建类组件，以便创建这样的状态。

## 在UI上渲染state
定义组件的初始状态后，可以在呈现的UI中显示它的任何部分。如果组件是有状态的，它将始终可以访问其render（）方法中的状态数据。您可以使用this.state访问数据。
如果要在render方法的返回中访问状态值，则必须将值括在花括号中。
State是React中组件最强大的功能之一。它允许您跟踪应用程序中的重要数据并呈现UI以响应此数据中的更改。如果您的数据发生变化，您的UI将会发生变化。React使用所谓的虚拟DOM来跟踪幕后的变化。当状态数据更新时，它会触发使用该数据重新呈现组件 - 包括作为属性接收数据的子组件。React更新实际DOM，但仅在必要时更新。这意味着您不必担心更改DOM。您只需声明UI应该是什么样子。
请注意，如果使组件成为有状态，则其他任何组件都不会知道其状态。除非您将状态数据作为props传递给子组件，否则它的状态是完全封装的，或者是该组件的本地状态。这种封装状态的概念非常重要，因为它允许您编写某些逻辑，然后在代码中的某个位置包含和隔离该逻辑。

## 用户界面中的渲染状态另一种方式
还有另一种访问组件状态的方法。在render（）方法中，在return语句之前，您可以直接编写JavaScript。例如，你可以声明函数，从state或props访问数据，对此数据执行计算，等等。然后，您可以将任何数据分配给您可以在return语句中访问的变量。

## 使用this.setState设置状态

```
    this.setState({
      itemCount: this.state.itemCount + 1
    });
```


## 在class类方法中绑定this
除了设置和更新状态外，您还可以为组件类定义方法。类方法通常需要使用this关键字，以便它可以访问方法范围内的类（例如state和props）上的属性。有几种方法可以让您的类方法访问它。
一种常见的方法是在构造函数中显式绑定它，以便在初始化组件时绑定到类方法。您可能已经注意到最后一个挑战使用this.handleClick = this.handleClick.bind（this）作为构造函数中的handleClick方法。然后，当您在类方法中调用类似this.setState（）的函数时，这将引用该类，并且不会被定义。


```
class MyComponent extends React.Component {
  constructor(props) {
    super(props);
    this.state = {
      itemCount: 0
    };
    this.addItem = this.addItem.bind(this);
  }
  addItem() {
    this.setState({
      itemCount: this.state.itemCount + 1
    });
  }
  render() {
    return (
      <div>
        { /* change code below this line */ }
        <button onClick={this.addItem}>Click Me</button>
        { /* change code above this line */ }
        <h1>Current Item Count: {this.state.itemCount}</h1>
      </div>
    );
  }
};

```

## 及时显示input内容值

```
class ControlledInput extends React.Component {
  constructor(props) {
    super(props);
    this.state = {
      input: ''
    };
    // change code below this line
    this.handleChange = this.handleChange.bind(this);
    // change code above this line
  }
  // change code below this line
  handleChange(event) {
    this.setState({
      input: event.target.value
    })
  }
  // change code above this line
  render() {
    return (
      <div>
        { /* change code below this line */}
        <input onChange={this.handleChange} value={this.state.input}/>
        { /* change code above this line */}
        <h4>Controlled Input:</h4>
        <p>{this.state.input}</p>
      </div>
    );
  }
};
```

## 使用state给子组件传参数


```class MyApp extends React.Component {
  constructor(props) {
    super(props);
    this.state = {
      name: 'CamperBot'
    }
  }
  render() {
    return (
       <div>
         <Navbar name={this.state.name} />
       </div>
    );
  }
};
class Navbar extends React.Component {
  constructor(props) {
    super(props);
  }
  render() {
    return (
    <div>
      <h1>Hello, my name is: {this.props.name} </h1>
    </div>
    );
  }
};
```


