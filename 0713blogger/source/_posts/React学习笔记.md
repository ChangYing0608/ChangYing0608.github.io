---
title: React学习笔记
date: 2017-07-20 10:20:15
tags:
     -学习笔记
     -react
---
![Alt text](./React学习笔记.md)
<h4>1.React 是什么？</h4>
<p>React 是一个采用声明式，高效而且灵活的用来构建用户界面的框架。
React 采用数据驱动视图的模式，区别于现在的JavaScript的MVC模式，是基于组件化的开发。</p>
<h4>2.ReactJS的背景和原理</h4>
<p>在Web开发中，我们总需要将变化的数据实时反应到UI上，这时就需要对DOM进行操作。而**复杂或频繁的DOM操作通常是性能瓶颈产生的原因**（如何进行高性能的复杂DOM操作通常是衡量一个前端开发人员技能的重要指标）。React为此引入了**虚拟DOM（Virtual DOM）**的机制：在浏览器端用Javascript实现了一套DOM API。基于React进行开发时所有的DOM构造都是通过虚拟DOM进行，每当数据变化时，React都会重新构建整个DOM树，然后React将当前整个DOM树和上一次的DOM树进行对比，得到DOM结构的区别，然后仅仅将需要变化的部分进行实际的浏览器DOM更新。而且React能够批处理虚拟DOM的刷新，在一个事件循环（Event Loop）内的两次数据变化会被合并，例如你连续的先将节点内容从A变成B，然后又从B变成A，React会认为UI不发生任何变化，而如果通过手动控制，这种逻辑通常是极其复杂的。尽管每一次都需要构造完整的虚拟DOM树，但是因为虚拟DOM是内存数据，性能是极高的，而对实际DOM进行操作的仅仅是Diff部分，因而能达到提高性能的目的。这样，在保证性能的同时，开发者将不再需要关注某个数据的变化如何更新到一个或多个具体的DOM元素，而只需要关心在任意一个数据状态下，整个界面是如何Render的。</p>
<!-- more -->
<p style="color:blue">传统开发的思路，你的开发过程需要知道哪条数据过来了，如何将新的DOM结点添加到当前DOM树上；而基于React的开发思路，你永远只需要关心数据整体，两次数据之间的UI如何变化，则完全交给框架去做。可以看到，使用React大大降低了逻辑复杂性，意味着开发难度降低，可能产生Bug的机会也更少。</p>
<h4>3.需要理解的一些概念</h4>
<p>
<strong>组件化</strong><br>
所谓组件，即封装起来的具有独立功能的UI部件。React推荐以组件的方式去重新思考UI构成，将UI上每一个功能相对独立的模块定义成组件，然后将小的组件通过组合或者嵌套的方式构成大的组件，最终完成整体UI的构建。
如果说MVC的思想让你做到视图-数据-控制器的分离，那么组件化的思考方式则是带来了UI功能模块之间的分离</p>
<p>对于MVC开发模式来说，开发者将三者定义成不同的类，实现了表现，数据，控制的分离。开发者更多的是从技术的角度来对UI进行拆分，实现松耦合。
对于React而言，则完全是一个新的思路，开发者从功能的角度出发，将UI分成不同的组件，每个组件都独立封装。</p>
<p>在React中，你按照界面模块自然划分的方式来组织和编写你的代码，对于评论界面而言，整个UI是一个通过小组件构成的大组件，每个组件只关心自己部分的逻辑，彼此独立。</p>
![Alt text](1500520210782.png)
<p>React认为一个组件应该具有如下特征：</p>
<p><strong>（1）可组合（Composeable）</strong>：一个组件易于和其它组件一起使用，或者嵌套在另一个组件内部。如果一个组件内部创建了另一个组件，那么说父组件拥有（own）它创建的子组件，通过这个特性，一个复杂的UI可以拆分成多个简单的UI组件；</p>
<p><strong>（2）可重用（Reusable）</strong>：每个组件都是具有独立功能的，它可以被使用在多个UI场景；</p>
<p><strong>（3）可维护（Maintainable）</strong>：每个小的组件仅仅包含自身的逻辑，更容易被理解和维护；</p>
<h4>JSX语法</h4>
<p>HTML 语言直接写在 JavaScript 语言之中，不加任何引号，这就是 JSX 的语法，它允许 HTML 与 JavaScript 的混写，了解过AngularJs的看到下面的代码一定会感觉很熟悉的，我们来看代码：</p>
![Alt text](1500518347585.png)
<p>这里我们声明了一个names数组，然后遍历在前面加上Hello,输出到DOM中，输出结果如下：</p>
![Alt text](1500518373707.png)
<p>JSX 允许直接在模板插入 JavaScript 变量。如果这个变量是一个数组，则会展开这个数组的所有成员，代码如下：</p>
![Alt text](1500518409275.png)
显示结果如下：
![Alt text](1500518417811.png)
这里的星号只是做标识用的，大家不要被迷惑了~~
<h4>ReactJS组件</h4>
<strong>组件属性</strong>
<p>React 允许将代码封装成组件（component），然后像插入普通 HTML 标签一样，在网页中插入这个组件。</p>
直接使用es6的语法结合React.Component{}方法实现组件的创建
![Alt text](1500518480285.png)
这里有几点需要注意：
1）获取属性的值用的是this.props.属性名
2）创建的组件名称首字母必须大写。
3）为元素添加css的class时，要用className。
4）组件的style属性的设置方式也值得注意，要写成style={{width: this.state.witdh}}。
5）input标签中要想显示value，需要把value变成defaultValue
![Alt text](1500518501148.png)
<strong>组件状态</strong>
组件免不了要与用户互动，React 的一大创新，就是将组件看成是一个状态机，一开始有一个初始状态，然后用户互动，导致状态变化，从而触发重新渲染 UI。</p>
![Alt text](1500518532478.png)

这里，我们使用到了一个属性this.state,这个属性在组件初始化的时候执行，必需赋值一个对象。这里我们将enable这个值跟input的disabled绑定，当要修改这个属性值时，要使用setState方法。我们声明handleClick方法，来绑定到button上面，实现改变state.enable的值。效果如下：
![Alt text](1500518561932.png)
<p>原理分析：<br>
当用户点击组件，导致状态变化，this.setState 方法就修改状态值，每次修改以后，自动调用 this.render 方法，再次渲染组件。</p>
这里值得注意的几点如下：
1）this.state相当于一个初始化的get必须赋值为一个对象，里面的键值对为初始数据，键为属性。
2）修改state的方法是this.setState方法，通常在事件中使用this.setState改变初始数据从而改变视图，<span style="color:red">如果给input表单赋值用的是state里初始化的值，同样只能通过setState方法才能修改，否则输入无效果。</span>
3）变量用{}包裹，不需要再加双引号。
4）因为是虚拟dom，如果this不进行绑定，值为null。绑定的方法有两种
     可以在插值中绑定{this.方法名.bind(this)}
     可以在初始化constructor中绑定，this.方法名=this.方法名.bind(this)
<strong>无状态组件的写法</trong>
![Alt text](1500518684985.png)
不需要写render()方法
<strong>组件的生命周期</strong>
组件的生命周期分成三个状态：
  ● Mounting：已插入真实 DOM
  ● Updating：正在被重新渲染
  ● Unmounting：已移出真实 DOM
React 为每个状态都提供了两种处理函数，will 函数在进入状态之前调用，did 函数在进入状态之后调用，三种状态共计五种处理函数。
  ● componentWillMount()
  ● componentDidMount()
  ● componentWillUpdate(object nextProps, object nextState)
  ● componentDidUpdate(object prevProps, object prevState)
  ● componentWillUnmount()
此外，React 还提供两种特殊状态的处理函数。
  ● componentWillReceiveProps(object nextProps)：已加载组件收到新的参数时调用
  ● shouldComponentUpdate(object nextProps, object nextState)：组件判断是否重新渲染时调用
下面来看一个例子：
![Alt text](1500518721248.png)
上面代码在hello组件加载以后，通过 componentDidMount 方法设置一个定时器，每隔100毫秒，就重新设置组件的透明度，从而引发重新渲染。
<strong>组件嵌套</strong>
父级向子级传值，通过自定义属性 如下图 songs
![Alt text](1500519063293.png)
子级接收父级的值需要使用到一个属性props
![Alt text](1500519071510.png)
子级通过this.props.自定义属性名.forEach()方法来遍历父级传过来的数据
![Alt text](1500519081827.png)
<strong>【react】子组件向父组件传值</strong>
<p>reactjs是一枚新进小鲜肉，跟gulp搭配流行一段时间了。工作或者面试中 经常遇到这样的问题，“子组件如何向父组件传值？”。其实很简单，概括起来就是：react中state改变了，组件才会update。父写好state 和处理该state的函数，同时将函数名通过props属性值的形式传入子，子调用父的函数，同时引起state变化。子组件要写在父组件之前。具体写法 看下面3个例子。</p>
例子1.这里如下图，用户邮箱为父，绿色框为子。 父组件为用户输入的邮箱设好state，即“{email: ''}”，同时写好处理state的函数，即“handleEmail”，这两个名称随意起；再将函数以props的形式传到子组件，子组件只需在事件发 生时，调用父组件传过来的函数即可。 
![Alt text](1500519131039.png)

<p style="color:green">//以下所有例子对应的html</p>

```
<body>
    <div id="test"></div>
</body>
```

例子2.有时候往往需要对数据做处理，再传给父组件，比如过滤或者自动补全等等，下面的例子对用户输入的邮箱做简单验证，自动过滤非数字、字母和"@."以外的字符。
![Alt text](1500519200507.png)

<p style="color:green">//子组件，handleVal函数处理用户输入的字符，再传给父组件的handelEmail函数</p>

```
var Child = React.createClass({
    handleVal: function() {
        var val = this.refs.emailDom.value;
        val = val.replace(/[^0-9|a-z|\@|\.]/ig,"");
        this.props.handleEmail(val);
    },
    render: function(){
        return (
            <div>
                请输入邮箱：<input ref="emailDom" onChange={this.handleVal}/>
            </div>
        )
    }
});
```

<p style="color:green">//父组件，通过handleEmail接受到的参数，即子组件的值</p>

```
var Parent = React.createClass({
    getInitialState: function(){
        return {
            email: ''
        }
    },
    handleEmail: function(val){
        this.setState({email: val});
    },
    render: function(){
        return (
            <div>
                <div>用户邮箱：{this.state.email}</div>
                <Child name="email" handleEmail={this.handleEmail.bind(this)}/>
            </div>
        )
    }
});
React.render(
  <Parent />,
  document.getElementById('test')
);
```

例子3.如果还存在孙子组件的情况呢？如下图，黑框为父，绿框为子，红框为孙，要求子孙的数据都传给爷爷。原理一样的，只是父要将爷爷对孙子的处理函数直接传下去。

<p style="color:green">//孙子，将下拉选项的值传给爷爷</p>

```
var Grandson = React.createClass({
    render: function(){
        return (
            <div>性别：
                <select onChange={this.props.handleSelect}>
                    <option value="男">男</option>
                    <option value="女">女</option>
                </select>
            </div>
        )
    }
});
```

<p style="color:green">//子，将用户输入的姓名传给爹  <br>
//对于孙子的处理函数，父只需用props传下去即可</p>

```
var Child = React.createClass({
    render: function(){
        return (
            <div>
                姓名：<input onChange={this.props.handleVal}/>
                <Grandson handleSelect={this.props.handleSelect}/>
            </div>
        )
    }
});
```

<p style="color:green">//父组件，准备了两个state，username和sex用来接收子孙传过来的值，对应两个函数handleVal和handleSelect</p>

```
var Parent = React.createClass({
    getInitialState: function(){
        return {
            username: '',
            sex: ''
        }
    },
    handleVal: function(event){
        this.setState({username: event.target.value});
    },
    handleSelect: function(event) {
        this.setState({sex: event.target.value});
    },
    render: function(){
        return (
            <div>
                <div>用户姓名：{this.state.username}</div>
                <div>用户性别：{this.state.sex}</div>
                <Child handleVal={this.handleVal.bind(this)} handleSelect={this.handleSelect.bind(this)}/>
            </div>
        )
    }
});
React.render(
  <Parent />,
  document.getElementById('test')
);


 
React.render(
  <Parent />,
  document.getElementById('test')
);
```

React中到底是如何实现组件的复用的，这里我们还写一个例子来说吧，代码如下：
![Alt text](1500519429111.png)
这里我们创建了一个Search组件，然后又创建了一个Page组件，然后我们在Page组件中调用Search组件，并且调用了两次，这里我们通过属性searchType传入值
<h4>4.React能做什么</h4>
<p>React.render 是 React 的最基本方法，用于将模板转为 HTML 语言，并插入指定的 DOM 节点。</p>
<p>render里面第二个参数必须使用JavaScript原生的getElementByID方法，不能使用jQuery来选取DOM节点。</p>
<h4>5.React怎么用</h4>
<strong>git中的操作</strong>
全局安装 create-react-app
npm install create-react-app -g
生成react项目
create-react-app <目录名字>
进入项目目录
cd <目录名称>
启动项目
npm start
打包
npm run build
<strong>index.js中的操作</strong>
引入两个模块
import React from 'react'
import ReactDOM from 'react-dom'
创建DOM元素
ReactDOM.render()方法
<p style="color:green">//第一个参数是插入的dom元素，第二个参数是插入的位置<br>
//被插入到index.html中的虚拟dom的外包裹标签中有一个data-reactroot属性，这个属性存在dom元素才能被渲染出来<p>
<strong>创建组件</strong>
<p>class 组件名称(首字母大写) extends React.Component{}
里面必须包含render(){}方法，render(){}方法中所写的内容必须包裹在return()中
如果想要使用React.Component中的属性和方法，需要继承
constructor(){ super() }</p>
state是组件中的属性(相当于get方法)，setState是里面原生的方法
用this.state给其赋值一个对象，对象中用键值对的方式存值

在render(){}方法中可以使用{this.state.time}的方式获取到值插入到标签中

要想修改state中的值，需要使用setState()方法

自定义的组件抛出需要在最后加上export default <组件名称>

在index.js中引入自定义组件要使用import

<strong>引入第三方的框架</strong>
<p>在webpack-dev-server中已经配置好了一个express的静态服务器并且把静态资源目录也设置好了所有在引入的操作中不用写根目录</p>
<strong>动态创建元素标签</strong>
<p>react里面有一个针对标签的属性key,在动态创建标签元素的时候通常使用key作为该标签唯一的标记</p>