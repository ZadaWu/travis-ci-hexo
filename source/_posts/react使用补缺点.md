---
title: V4.0 react使用补缺点
date: 2019-01-14 14:56:36
tags:
---

## router与component属性结合使用时，如何传参数[参考链接](https://github.com/ReactTraining/react-router/issues/4105)

1. <Route exact path={"/"} component={() => <Start socket={socket} addUser={addUser}/>}/>
    这个解决方案是相当于自定义组件
    类似的：
    <Route path="/abc" render={()=><TestWidget num="2" someProp={100}/>}/>
    
2. <Route exact path="/abc" render={props => <TestWidget someProp="2" {...props} />} />

and what I do is I actually spread {...props.match.params} because then on TestWidget you can access the URL parameters with just this.props.urlVariableHere.
这个解决方案是站在组件中获取路由的参数


## 如何复用组件，[参考链接](https://react-cn.github.io/react/docs/reusable-components.html)
组件是 React 里复用代码最佳方式，但是有时一些复杂的组件间也需要共用一些功能。有时会被称为 跨切面关注点。React 使用 mixins 来解决这类问题。
```
var SetIntervalMixin = {
  componentWillMount: function() {
    this.intervals = [];
  },
  setInterval: function() {
    this.intervals.push(setInterval.apply(null, arguments));
  },
  componentWillUnmount: function() {
    this.intervals.forEach(clearInterval);
  }
};

var TickTock = React.createClass({
  mixins: [SetIntervalMixin], // 引用 mixin
  getInitialState: function() {
    return {seconds: 0};
  },
  componentDidMount: function() {
    this.setInterval(this.tick, 1000); // 调用 mixin 的方法
  },
  tick: function() {
    this.setState({seconds: this.state.seconds + 1});
  },
  render: function() {
    return (
      <p>
        React has been running for {this.state.seconds} seconds.
      </p>
    );
  }
});

ReactDOM.render(
  <TickTock />,
  document.getElementById('example')
);
```



