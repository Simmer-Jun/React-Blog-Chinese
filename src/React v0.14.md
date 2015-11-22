# React v0.14 # 
2015年10月7日 By [Ben Alpert](http://benalpert.com/)

我们很高兴的宣布React v0.14版本在今天正式发布！这个版本将会有一些较大的改变，首要的目的是简化你写的代码和对像React Native这样的环境有更好的支持。

如果你已经尝试了预选版本的话，十分感谢－你的支持是宝贵的，我们也已经修复了一些你们报告的bug。

在我们所有已发布的版本汇总，我们认为这次的版本已经足够稳定在生产环境中使用，并且为了能够享受到我们最新的功能希望你能够更新。

# 升级指南 #

像往常一样，我们在这个版本中有一些较大的改变。我们知道改变是十分痛苦的(Facebook的代码库有超过15000个React组件)，所以我们通常会逐渐地改变来将这个痛苦降到最低。

如果你的代码在React 0.13以下没有警告的话，升级React是十分简单的。在React 0.13版本中我们有2个新的重大更改没有给出警告(见下文)。在 React 0.14 中每一个新的改变(包括下面给出的重大变化)在运行的时候会发出警告，但是这些已经被摒弃的特性将会一直工作到React 0.15 版本，所以你不用担心由于本次版本的更新你的应用会出现错误。

由于此次2个主要的更新而导致需要改显著更新代码，我们还提供了[codemodscripts](https://github.com/reactjs/react-codemod/blob/master/README.md)来帮助你自动化更新代码。

阅读下面的更新日志来获取更多的细节。

## 安装 ##

我们推荐通过npm下载并使用React和使用像[browserify](https://github.com/substack/node-browserify)或者[WebPack](https://github.com/webpack/webpack)这样的工具来构建你的代码到一个单一的包中。像下面这样使用npm下载这2个工具

 * `npm install --save react react-dom`

一定要记住在默认的情况下，开发版本的React会作出额外的检查并提供一些有用的警告。在部署你的应用时，在生产环境设置`NODE_ENV`环境变量来使用不包含警告并且运行显著加快的生产版本React包。

如果你目前无法之用`npm`，为了你的方便起见，我们还提供了预先编译好的React浏览器包。同样在基于bower的`react`包中是同样可以获取的。

 * React 
   * 包含警告的功能开发版本: [https://fb.me/react-0.14.0.js](https://fb.me/react-0.14.0.js)
   * 用于生产环境的压缩版本: [https://fb.me/react-0.14.0.min.js](https://fb.me/react-0.14.0.min.js)

 * React with Add-Ons
   * 包含警告的功能开发版本: [https://fb.me/react-with-addons-0.14.0.js](https://fb.me/react-with-addons-0.14.0.js)
   * 用于生产环境的压缩版本: [https://fb.me/react-with-addons-0.14.0.min.js](https://fb.me/react-with-addons-0.14.0.min.js)

 * React DOM（在React DOM之前引入React）
    * 包含警告的功能开发版本: [https://fb.me/react-dom-0.14.0.js](https://fb.me/react-dom-0.14.0.js)
    * 用于生产环境的压缩版本: [https://fb.me/react-dom-0.14.0.min.js](https://fb.me/react-dom-0.14.0.min.js)

# 更新日志 #

## 主要的更新 ##

###  2个包：React 和 React DOM ###

当我们看着像[react-native](https://github.com/facebook/react-native),[react-art](https://github.com/reactjs/react-art),[react-canvas](https://github.com/Flipboard/react-canvas)和[react-three](https://github.com/Izzimach/react-three)这样的包时，我们清楚的知道React的魅力和本质与浏览器或者DOM无关。

为了让这个理念更加清楚并且使React能轻松的在更多的环境中渲染，我们将`react`一分为二: `react`和`react-dom`。这铺平了让在web版本的React和React Native编写的组件实现共享的道路。我们不奢求在一个app上共用所有的代码，但是我们希望在不同平台上分享的的React组件能够有着同样的行为。

`react`包含`react.createElement`,`react.createClass`,`.Component`,`PropTypes`,`.Children`和一些其他的与元素和组件类有帮助的方法。我们认为在你编写组件的时候这些是作为同构或通用的有用工具

`react-dom`包含`ReactDOM.render`,`.unmountComponentAtNode`,和`.findDOMNode`。在`react-dom/server`中我们有包括`ReactDOMServer.renderToString`和`.renderToStaticMarkup`在内的服务端的渲染支持。

```js
    var React = require('react');
    var ReactDOM = require('react-dom');

    var MyComponent = React.createClass({
      render: function() {
        return <div>Hello World</div>;
      }
    });

    ReactDOM.render(<MyComponent />, node);
```

旧的功能将会带着警告正常工作，一直到React 0.15发布，同时我们也发布了Facebook使用的[ automated codemod script](https://github.com/reactjs/react-codemod/blob/master/README.md)来帮助你完成更新的过度。

`add-ons`也被移动到不同的包中：
 * `react-addons-clone-with-props`
 * `react-addons-create-fragment`
 * `react-addons-css-transition-group`
 * `react-addons-linked-state-mixin`
 * `react-addons-perf`
 * `react-addons-pure-render-mixin`
 * `react-addons-shallow-compare`
 * `react-addons-test-utils`
 * `react-addons-transition-group`
 * `react-addons-update`
 * `ReactDOM.unstable_batchedUpdates in react-dom`

从现在开始。请在你的应用中使用相匹配的`react`和`react-dom`(还有添加了工具的add-ons，如果你需要他们的话)以避免版本不匹配引发的问题。
