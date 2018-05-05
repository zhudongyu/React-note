## JSX语法
> 简介

    JSX 是Facebook为React开发的一套语法糖，创建 JSX 语法的本质目的是为了使用基于 xml 的方式表达组件的嵌套，保持和 HTML 一致的结构，语法上除了在描述组件上比较特别以外，其它和普通的 Javascript 没有区别。 并且最终所有的 JSX 都会编译为原生 Javascript。
    XML特点 : 随意嵌套,要闭合.
    很方便的表示某一种 层级关系,衍生到数据的层级关系

> 1.基本规则

    JSX 构建组件的规则和 XML 规则一致

> 2.嵌套规则 -> 标签可以任意嵌套
```JavaScript
function render() {
    return <p>
                text content
                <ul>
                    <li>...</li>
                    <li>...</li>
                </ul>
            </p>
}

```

> 3.标签闭合 -> 标签必须严格闭合，否则无法编译通过

```JavaScript
// 自闭合
function render () {
    return <input type="text"/>
}
```
```JavaScript
// 标签闭合
function render () {
    return <p></p>
}
```
> 4.JSX组件 -> JSX 组件分为 HTML 组件和 React 组件

```JavaScript
// HTML 组件就是 HTML 中的原生标签
function render () {
    return <p>Hello React world !</p>
}
```
```JavaScript
// React 组件就是自定义的组件

// 定义一个自定义组件
var CustomComponent = React.createClass({
    render : function () {
        return <p> custom component </p>
    }
})

// 使用自定义组件
function render () {
    return <p> <CustomComponent/> </p>
}
```

> 5.组件属性 -> 和 HTML 一样,JSX 中组件也有属性，传递属性的方式也相同

```JavaScript
// 对于 HTML 组件：
function render () {
    return <p title="title"> Hello React world ! </p>
}
```
```JavaScript
// 对于 React 组件可以定义自定义属性（Props）


// 属性可以是字符串，
function render () {
    return <p> <CustomComponent customProps="data"/> </p>
}
//也可以是任意的JavaScript变量，传递方式是将变量放在花括号里
function render () {
    var data = {a : 1,b : 2};
    return <p> <CustomComponent customProps={data}/> </p>
}
```
```JavaScript
// 注意：组件属性的写法上和HTML存在区别，在写JSX的时候，所有属性都是驼峰式的,(特殊的：WebKit,ms)
function render () {
    return （
        <div className="....">
            <label htmlFor="...">...</label>
            <input onChange="..."/>
        </div>
    ）
}

// 而原生的写法为
<div class="...">
    <label for="...">...</label>
    <input onchange="..."/>
</div>

// 1.主要是出于标准的原因，驼峰式是 Javascript 的标准写法.
//   因为 JSX 的特性更接近 JavaScript 而不是 HTML , 所以 React DOM 使用 camelCase 小驼峰命名 来定义属性的名称，而不是使用 HTML 的属性名称。
// 2.React 底层是将属性直接对应到原生 DOM 的属性
// 3.也就可以理解为什么类名不是 class 而是 className 了, 又因为 class 和 for 还是 js 关键字，所以 在jsx 中:
//   class    =>  calssName
//   for      =>  htmlFor
//   tabindex => tabIndex。
// 4.除此之外比较特殊的地方是 `data-*` 和 `aria-*` 两类属性是和 HTML 一致的。

```

> 6.显示文本 -> 很多情况，我们需要将 JS 中的文本直接显示，做法和显示变量属性一样，用花括号

```JavaScript
function render () {
    var text = "Hello React world !"
    return <p> { text } </p>
}
```
> 7.运算 -> 花括号里边实际上除了变量以外，还可以是一段 JS 表达式，我们可以利用花括号做简单的运算

```javaScript
function render () {
    var text = "text";
    var isTrue = false;
    var arr = [1,2,3];
    return 
        <p>
            { text }
            { isTrue ? "true" : "false" }
            { 
                arr.map(function(){
                    return <span> { it }</span>
                })
            }
        </p>
}
```
> 8.注释 -> 注释写法如下

```javaScript
function render () {
    return 
        <p>
            /* 这里是注释内容 */        
        </p>
}
```

> 9.限制规则 -> render 方法返回的组件必须是有且只有一个根组件

```javaScript
// 错误情况的例子
// 无法编译通过，JSX会提示编译错误
function render () {
    return (
        <p> ... </p>
        <p> ... </p>
    )
}
```
> 10.JSX 代码块如果换行后应该包在 ( ) 中

```javaScript
function render () {
    return (
        <div>
            <p>hello</p>
            <p>world</p>
        </div>
    )
}
var element = (
    <div>
        <p>hello</p>
        <p>world</p>
    </div>
)

```
> 11.组件命名空间 -> JSX 可以通过命名空间的方式使用组件, 通过命名空间的方式可以解决相同名称不同用途组件冲突的问题。

```javaScript
function render () {
    return 
        <p>
            <CustomCoponent1.SubElement/>
            <CustomCoponent2.SubElement/>
        </p>
} 
```

> 12.JSX 防注入攻击 -> 可以放心地在 JSX 当中使用用户输入

```javaScript
const title = response.potentiallyMaliciousInput;
// 直接使用是安全的：
const element = <h1>{title}</h1>;
// React DOM 在渲染之前默认会 过滤 所有传入的值。它可以确保你的应用不会被注入攻击。所有的内容在渲染之前都被转换成了字符串。这样可以有效地防止 XSS(跨站脚本) 攻击。
```

## 理解JSX

1.JSX的写法实际上是调用 React 的工厂方法 createElement 而生成的。
2.JSX的渲染是需要通过 ReactDOM.render 方法的。
  ReactDOM.render接收两个参数：第一个组件 第二个挂载的节点
3.JSX中遇到 HTML 标签以 "<" 开头，就用 HTML 规则解析；
  遇到代码块以 "{" 开头，就用JavaScript 规则解析。 { } 花括号内为表达式
4.JSX中 在花括号里存在数组的 "{[123,123,23]}",会将其展开进行解析


> 对比 JSX 和 createElement 的写法

```javaScript
// 作用是完全相同的两行代码
// JSX
const element = <h1 className="greeting">Hello, world!</h1>;
// 上面的JSX代码被编译为：
const element = React.createElement('h1',{className: 'greeting'},'Hello, world!');
// React.createElement() 这个方法首先会进行一些避免bug的检查，之后会返回一个类似下面例子的对象：
const element = {
    type: 'h1',
    props: {
        className: 'greeting',
        children: 'Hello, world'
    }
};
```
```javaScript
 // 接收组件参数
React.createElement(App)
// 第一个参数 自身根节点  
// 第二个参数 属性/样式 （以对象形式存在）
// 第三个参数 子节点(包括文本) 可以放在一个数组中，也可以展开
React.createElement('div',null,'hello React world !')
React.createElement('div',null,<h1>hello React</h1>,<h1>hello React</h1>)
React.createElement('div',null,[<App/>,<App/>,<App/>])
React.createElement('div',null,[React.createElement(App),React.createElement(App)]

// 添加属性
// 在JSX中 属性的值需要写在 {  } 中
ReactDOM.render(<div style={{backgroundColor:"blue"}} title={123}>hello everyone !</div>,document.getElementById('root'))
// 在JS中的 
ReactDOM.render(React.createElement('div',{style : {backgroundColor : "red"}, propsName : '123'},'hello React world !'))

// 三元运算 
const flag = false;
ReactDOM.render(<div>{ flag ? "hello world !" : "hello React world !"}</div>,document.getElementById('root'))
ReactDOM.render(React.createElement('div',null,flag ? "hello world !" : "hello React world !"),document.getElementById('root'))

// if else 
var result = []; 
if(flag) {
    result.push(<App/>)
    result.push(<App/>)
    result.push(<App/>)
}else {
    result.push(<h1>hello React world !</h1>)
    result.push(<h1>hello React world !</h1>)
    result.push(<h1>hello React world !</h1>)
}
ReactDOM.render(<div>{ result }</div>,document.getElementById('root')) // {  } 中的 [ ] 会被展开进行解析
ReactDOM.render(React.createElement('div',null,result),document.getElementById('root'))

```
    
    






