# 项目1：计数器

![1.png](./images/1.png)

本节课程，我们使用一个简单的计数器App作为Vue开发的入门案例。

### 开发环境

Vue开发环境需要Nodejs支持，首先需要安装Nodejs运行环境。

Node安装成功之后，通过npm全局安装`vue-cli`工具。`npm i -g vue-cli`

本书中所有代码编辑器为VSCode

调试工具为谷歌浏览器

### 创建工程

通过`vue-cli`创建工程，在命令行运行：

```
vue create lesson1
```

![2.png](./images/2.png)

选择`default`模式，点击回车按钮，之后便自动构建一个名为`lesson1`的vue工程。

工程创建完毕之后，使用VSCode打开，在VSCode的终端中输入:

```
npm i -S mint-ui babel-plugin-component
```

安装结束之后，将工程根目录中的`babel.config`内容修改为如下：

```
module.exports = {
  presets: [
    '@vue/app',
    ["es2015", { "modules": false }]
  ],
  "plugins": [["component", [
    {
      "libraryName": "mint-ui",
      "style": true
    }
  ]]]
}
```

在`lesson1/src/main.js`文件中，添加如下代码：

```
import 'mint-ui/lib/style.css'
```

最后通过`npm run serve`启动工程。

### 构建静态页面

首先将`src`目录下的`App.vue`文件内容删除，然后添加如下两个标签：

```
<script>

</script>

<style>
</style>
```



在`<script>`中首先构造一个`render()`函数，在此函数中通过JSX语法构建静态页面。

```
<script>

function render(){

}

</script>
```

页面包含以下元素：

* Header
* 文字展示区
* 增加按钮
* 减少按钮
* 归零按钮

Header和按钮采用MintUI组件库中的Header和Button组件，文字展示区域使用HTML中p标签。

```
function render(h){
    return(
      <div id="app">
        <Header
          id="header"
          fixed={true}
          title={'计数器'}
        />
        <p id="content">
          {`点击次数为：0`}
        </p>
        <Button 
          class="btn"
          size="large"
          type="primary"
        >增加</Button>
        <Button 
          class="btn"
          size="large"
          type="primary"
        >减少</Button>
        <Button 
          class="btn"
          size="large"
          type="primary"
        >归零</Button>
      </div>
    )
}
```

### 添加页面数据

页面中的点击次数是需要动态维护的数据，通过构建一个`data`函数，该函数返回一个包含`count`属性的对象，在`render()`函数中，可以通过`this.count`直接访问该对象中的值。

```
const data = ()=>{
  return{
    count:0,
  }
}
```
修改`render()`函数中的p标签内容代码：

```
<p id="content">
    {`点击次数为：${this.count}`}
</p>
```

### 添加页面事件

该页面需要响应三个按钮的点击事件，首先需要构建一个`methods`对象，在该对象中构建按钮的响应事件函数，在按钮的响应事件函数中，可以通过`this`直接访问`data`函数返回的对象中的值：

```
const methods = {
  add:function(){
    this.count++;
  },
  dec:function(){
    this.count--;
  },
  zero:function(){
    this.count = 0;
  }
}
```

配置按钮的`onClick`事件属性，指导按钮的点击事件响应函数：

```
<Button 
    class="btn"
    size="large"
    type="primary"
    onClick={this.add}
>增加</Button>
<Button 
    class="btn"
    size="large"
    type="primary"
    onClick={this.dec}
>减少</Button>
<Button 
    class="btn"
    size="large"
    type="primary"
    onClick={this.zero}
>归零</Button>
```

### 暴露Vue组件对象

通过`export default`语法对Vue组件对象进行暴露。

```
export default {
  name: 'app',
  render,
  methods,
  data
}
```

通过暴露的Vue组件，在main.js文件中便可以进行渲染。

### 添加样式

在`style`标签中，可以为`render()`中的元素添加CSS样式:

```
<style>

#content{
  margin-top: 60px;
}

.btn{
  margin-top: 10px;
}

#header{
  font-size: 18px;
}
</style>
```

完整参考代码：

```
<script>

import { 
  Button ,
  Header,
} from 'mint-ui';

function render(h){
    return(
      <div id="app">
        <Header
          id="header"
          fixed={true}
          title={'计数器'}
        />
        <p id="content">
          {`点击次数为：${this.count}`}
        </p>
        <Button 
          class="btn"
          size="large"
          type="primary"
          onClick={this.add}
        >增加</Button>
        <Button 
          class="btn"
          size="large"
          type="primary"
          onClick={this.dec}
        >减少</Button>
        <Button 
          class="btn"
          size="large"
          type="primary"
          onClick={this.zero}
        >归零</Button>
      </div>
    )
}

const methods = {
  add:function(){
    this.count++;
  },
  dec:function(){
    this.count--;
  },
  zero:function(){
    this.count = 0;
  }
}

const data = ()=>{
  return{
    count:0,
  }
}

export default {
  name: 'app',
  render,
  methods,
  data
}
</script>

<style>

#content{
  margin-top: 60px;
}

.btn{
  margin-top: 10px;
}

#header{
  font-size: 18px;
}
</style>

```