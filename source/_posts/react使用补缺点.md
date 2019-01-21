---
title: V4.0 react使用补缺点
date: 2019-01-14 14:56:36
tags:
---

## router与component属性结合使用时，如何传参数[参考链接](https://github.com/ReactTraining/react-router/issues/4105)

1. `<Route exact path={"/"} component={() => <Start socket={socket} addUser={addUser}/>}/>`
    这个解决方案是相当于自定义组件
    类似的：
    `<Route path="/abc" render={()=><TestWidget num="2" someProp={100}/>}/>`
    
2. `<Route exact path="/abc" render={props => <TestWidget someProp="2" {...props} />} />`

and what I do is I actually spread {...props.match.params} because then on TestWidget you can access the URL parameters with just this.props.urlVariableHere.
这个解决方案是站在组件中获取路由的参数


## 如何复用组件[参考链接](https://react-cn.github.io/react/docs/reusable-components.html)
组件是 React 里复用代码最佳方式，但是有时一些复杂的组件间也需要共用一些功能。有时会被称为 跨切面关注点。React 使用 mixins 来解决这类问题。
但是 mixins 在ES6 的情况下不支持

## 如何操作dom [参考链接](https://react.docschina.org/docs/refs-and-the-dom.html)
方法一：使用ref来访问组件
步骤：
1. 在constructor里面来创建ref：this.textInput学习学习 = React.createRef();
2. 在render中绑定dom节点： <CustomTextInput ref={this.textInput} />

方法二： 在函数式组间内部使用ref,使之指向一个DOM元素活着class组件：
1. <input type="text" ref={(input) => { textInput = input; }} />


## 具体属性改变时，采取重新渲染，使用shouldComponentUpdate
`shouldComponentUpdate(nextProps, nextState) {
    if (this.props.color !== nextProps.color) {
      return true;
    }
    if (this.state.count !== nextState.count) {
      return true;
    }
    return false;
}
`


