# react使用心得

## react理念

> React的理念，把JS作为主体，H5、CSS作为辅助，使用JS来控制构建HTML、CSS。

    正是因为这一理念，让React变得无比强大。我们不是在h5中嵌入JS来控制它，而是我们用JS来完全控制整个绘制、交互的一切，而HTML和CSS变成了JS的一个附属品。原来JS、CSS不过是HTML的一个附属品。整个关系链路发生了反转式的变化。  

[react 理念](https://www.yuque.com/basaltic/zy7k7h/ng6ogd)

## react两种开发模式

> class类组件开发 

    class Welcome extends React.Component {
      constructor(props) {
        super(props)
      }
      .
      .
      .
      render() {
        return <h1>Hello, {this.props.name}</h1>;
      }
    }

> 函数式组件开发

    const Welcome = function(porps) {
      return <h1>Hello, {props.name}</h1>;
    }

## 介绍不同类型组件模式

我在项目中均有使用两种开发组件的方式, 主要用在控制页面的函数式和公用components的class类式.

我在选型时考虑的方式比较特别, 因一些特殊需要, 项目中不能引入redux来管理状态集,所有采用了[Hooks React新特性](https://react.docschina.org/docs/hooks-intro.html),来管理store状态集, 使用页面层次的 useContext 来共享数据状态

我在制作components公用组件时, 比如多个页面使用同一个弹窗组件Modal, 表单组件Form, 以及列表Table时,可以使用class类声明

当然 Hooks 是不支持class类组件的,所以在页面的制做中没有使用 class类~~~~

> Hooks使用心得

  优点: 显而易见,项目中不在引入redux的插件, 使整个项目变得更加轻量级, 整体项目体积也变得小了很多, 不管是制作 H5移动端页面, 后台管理页面, PC客户端 都大大减少了数据消耗, 同时在webpack 的打包上, 速度也要更快

  缺点: 因为没有了redex的维护, 在页面中就产生了大量的 useState 变量, 同时出现在store中, 使得变量过于集中, 特别是在多人协同开发时, 如果没有很好的代码规范,代码注释,就会造成变量冗余, 相同数值的变量, 出现重复定义, 以至于在后期更改代码时,根本不敢轻易删除声明的useState变量, 也不知道使用的位置和数值情况,只能不断新增和不断尝试, 越来越难维护, 很是头疼~~~~ 


> class类组件心得

  优点: 类组件规定了非常明确的[react生命周期](https://reactjs.org/docs/react-component.html)规定了在不同的生命周期内做不同的事情, 使组件的逻辑更加清晰, 同时类组件不需要依赖store状态集, 增加了复用率, 减少了代码耦合

  缺点: Classes难以理解,我们在使用class类组件时,总会存在this的问题,需要过多的事件处理, 当我的组件实现功能较多时, 就需要大量的props和state的使用, 以及update钩子内的数值判断也让人感到无比头疼,同时还要关心在组件销毁时一些定时器和事件的销毁, 就需要写大量逻辑不相关的代码

## 如何取舍class类组件和hooks函数组件

  在项目是使用class类组件和hooks函数组件的取舍需要看组件复杂程度, 公用程度, 耦合度等等
  
  比如: 我的页面有登录功能, 分为: 账号输入/ 密码输入/ 验证码/ 登录按钮/ 注册按钮/ 报错文本组成, 如果把登录页面看成一个整体只需要一个hooks函数或者class类都能解决, 但是这就大大降低了服用, 如果有成型的输入框组件, 按钮组件, 表单组件整合, 数据源使用hooks就可以分为 form页面, 输入框组件, 按钮组件, 错误提示三部分. 分为login-hooks, form-class, input-class, button-class, text-class;

