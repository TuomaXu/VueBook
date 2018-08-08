# 项目5：留言板

### 产品原型

登录注册模块：

提供用户登录和注册功能

![30.png](../images/30.png)
![31.png](../images/31.png)

消息发布模块：

提供发布消息功能，消息具有标题、内容和最多9张图片

![32.png](../images/32.png)

消息浏览模块：

提供浏览所有用户发布的消息：

![33.png](../images/33.png)

消息评论模块:

用户可以针对某一天消息发布自己的评论

![34.png](../images/34.png)

评论展示模块：

展示该消息下的所有评论内容

![35.png](../images/35.png)


### API文档

**元数据**

账户

```
{
	"id": 1,
	"username": "tom1",
	"password": "1234",
	"access_token": "e1fa63bed5f5eff45c9147ff27fcef28",
	"updatedAt": "2018-06-07T05:08:04.452Z",
	"createdAt": "2018-06-07T05:08:04.452Z"
}
```

消息

```
{
	"id": 10,
	"title": "xxx3",
	"content": "yyy3",
	"createdAt": "2018-06-07T05:25:47.000Z",
	"updatedAt": "2018-06-07T05:25:47.000Z",
	"messageUserId": 1,
	"images": [],
	"message_user": {
		"id": 1,
		"username": "tom1"
	}
}
```

评论

```
{
	"id": 2,
	"content": "xxx",
	"createdAt": "2018-06-07T05:32:59.000Z",
	"updatedAt": "2018-06-07T05:32:59.000Z",
	"messageId": 10,
	"messageUserId": 1,
	"message": {
		"id": 10,
		"title": "xxx3"
	},
	"message_user": {
		"id": 1,
		"username": "tom1"
	}
}
```


**错误代码**

|错误代码|内容|
|:---|:---|
|10001|系统错误|
|10002|用户名错误|
|10003|密码错误|
|10004|access_token无效|
|10005|TodoID无效|
|10006|参数无效|
|10007|用户名已存在|
|10008|MessageID无效|

错误返回值：

```
{
    success:false,
    errorCode:10001,
    errorMessage:'系统错误'
}
```

**接口描述**

注册

请求链接：`/api/register`

请求方式：`POST`

|参数名称|参数描述|
|:---|:---|
|username|用户名|
|password|密码|

```
{
    "success": true,
    "data": {
        "id": 2,
        "username": "tom1",
        "password": "1234",
        "access_token": "16e088f3d62c4c132e8728ef79eaf353",
        "updatedAt": "2018-06-06T08:05:13.664Z",
        "createdAt": "2018-06-06T08:05:13.664Z"
    }
}
```

登录

请求链接：`/api/login`

请求方式：`POST`

|参数名称|参数描述|
|:---|:---|
|username|账户名|
|password|密码|

```
{
    "success": true,
    "data": {
        "id": 2,
        "username": "tom1",
        "password": "1234",
        "access_token": "8e58260409dc169009b87800dfe5128f",
        "createdAt": "2018-06-06T08:05:13.000Z",
        "updatedAt": "2018-06-06T08:11:18.442Z"
    }
}

```

发留言

请求链接：`/api/postMessage`

请求方式：`POST`

|参数名称|参数描述|
|:---|:---|
|access_token|登录令牌|
|title|消息标题|
|content|消息内容|
|image1-9|图片file对象|

返回值：

```
{
    "success": true,
    "data": {
        "id": 10,
        "title": "xxx3",
        "content": "yyy3",
        "createdAt": "2018-06-07T05:25:47.000Z",
        "updatedAt": "2018-06-07T05:25:47.000Z",
        "messageUserId": 1,
        "images": [],
        "message_user": {
            "id": 1,
            "username": "tom1"
        }
    }
}
```

发布对指定消息的评论

请求路径：`/api/postComment`

请求方式：`POST`

|参数名称|参数描述|
|:---|:---|
|access_token|登录令牌|
|messageID|消息ID|
|content|评论内容|

返回值：

```
{
    "success": true,
    "data": {
        "id": 2,
        "content": "xxx",
        "createdAt": "2018-06-07T05:32:59.000Z",
        "updatedAt": "2018-06-07T05:32:59.000Z",
        "messageId": 10,
        "messageUserId": 1,
        "message": {
            "id": 10,
            "title": "xxx3"
        },
        "message_user": {
            "id": 1,
            "username": "tom1"
        }
    }
}
```


获取全部消息

请求地址：`/api/allMessages`

请求方式：`POST`

|参数名称|参数描述|
|:---|:---|
|access_token|登录令牌|

返回值：

```
{
    "success": true,
    "data": [
        {
            "id": 3,
            "title": "xxx3",
            "content": "yyy3",
            "createdAt": "2018-06-07T05:08:55.000Z",
            "updatedAt": "2018-06-07T05:08:55.000Z",
            "messageUserId": 1,
            "images": [],
            "message_user": {
                "id": 1,
                "username": "tom1"
            }
        },
        {
            "id": 6,
            "title": "xxx3",
            "content": "yyy3",
            "createdAt": "2018-06-07T05:22:16.000Z",
            "updatedAt": "2018-06-07T05:22:16.000Z",
            "messageUserId": 1,
            "images": [],
            "message_user": {
                "id": 1,
                "username": "tom1"
            }
        },
        {
            "id": 7,
            "title": "xxx3",
            "content": "yyy3",
            "createdAt": "2018-06-07T05:22:46.000Z",
            "updatedAt": "2018-06-07T05:22:46.000Z",
            "messageUserId": 1,
            "images": [],
            "message_user": {
                "id": 1,
                "username": "tom1"
            }
        },
        {
            "id": 8,
            "title": "xxx3",
            "content": "yyy3",
            "createdAt": "2018-06-07T05:23:05.000Z",
            "updatedAt": "2018-06-07T05:23:05.000Z",
            "messageUserId": 1,
            "images": [],
            "message_user": {
                "id": 1,
                "username": "tom1"
            }
        },
        {
            "id": 9,
            "title": "xxx3",
            "content": "yyy3",
            "createdAt": "2018-06-07T05:23:43.000Z",
            "updatedAt": "2018-06-07T05:23:43.000Z",
            "messageUserId": 1,
            "images": [],
            "message_user": {
                "id": 1,
                "username": "tom1"
            }
        },
        {
            "id": 10,
            "title": "xxx3",
            "content": "yyy3",
            "createdAt": "2018-06-07T05:25:47.000Z",
            "updatedAt": "2018-06-07T05:25:47.000Z",
            "messageUserId": 1,
            "images": [],
            "message_user": {
                "id": 1,
                "username": "tom1"
            }
        },
        {
            "id": 4,
            "title": "xxx3",
            "content": "yyy3",
            "createdAt": "2018-06-07T05:09:57.000Z",
            "updatedAt": "2018-06-07T05:09:57.000Z",
            "messageUserId": null,
            "images": [],
            "message_user": null
        },
        {
            "id": 5,
            "title": "xxx3",
            "content": "yyy3",
            "createdAt": "2018-06-07T05:11:13.000Z",
            "updatedAt": "2018-06-07T05:11:13.000Z",
            "messageUserId": null,
            "images": [],
            "message_user": null
        }
    ]
}
```

获取指定消息的评论内容

请求地址：`/api/allComments`

请求方式：`POST`

|参数名称|参数描述|
|:---|:---|
|access_token|登录令牌|
|messageID|消息ID|

返回值：

```
{
    "success": true,
    "data": [
        {
            "id": 1,
            "content": "xxx",
            "createdAt": "2018-06-07T05:32:14.000Z",
            "updatedAt": "2018-06-07T05:32:15.000Z",
            "messageId": 10,
            "messageUserId": 1,
            "message_user": {
                "id": 1,
                "username": "tom1"
            }
        },
        {
            "id": 2,
            "content": "xxx",
            "createdAt": "2018-06-07T05:32:59.000Z",
            "updatedAt": "2018-06-07T05:32:59.000Z",
            "messageId": 10,
            "messageUserId": 1,
            "message_user": {
                "id": 1,
                "username": "tom1"
            }
        }
    ]
}
```

### 数据服务层构建

1，构建URLConfig文件

```
const host = 'http://localhost:';
const port = 5000;

const loginURL = host+port+'/api/login';
const registerURL = host+port+'/api/register';
const postMessageURL = host+port+'/api/postMessage';
const postCommentURL = host+port+'/api/postComment';
const allMessagesURL = host+port+'/api/allMessages';
const allCommentsURL = host+port+'/api/allComments';

const imageBaseURL = host+port+'/resource/image/';


export {
    loginURL,
    registerURL,
    postMessageURL,
    postCommentURL,
    allMessagesURL,
    allCommentsURL,
    imageBaseURL,
}
```

2，构建`UserManager`数据服务对象，对用户相关操作进行封装。该数据对象提供以下功能支撑：

* 用户注册（异步）
* 用户登录（异步）
* 保持登录信息
* 查询当前登录状态
* 登出操作（清空登录信息）

实现代码：

```
import { loginURL,registerURL } from './URLConfig';

class UserManager {
    
    async login(username,password){
        try {
            const user = {
                username,
                password
            }

            const res = await fetch(loginURL,{
                method:'POST',
                headers:{
                    'Accept':'application/json',
                    'Content-Type':'application/json'
                },
                body:JSON.stringify(user)
            });

            const result = await res.json();

            if(result.success === true){
                localStorage.access_token = result.data.access_token 
            }

            return result;

        } catch (error) {
            return {
                success:false,
                errorMessage:'网络错误'
            }
        }
    }

    logout(){
        localStorage.access_token = '';
    }

    isLogin(){
        if(localStorage.access_token === ''){
            return false;
        } else {
            return true;
        }
    }

    async register(username,password){
        try {
            const user = {
                username,
                password
            }

            const res = await fetch(registerURL,{
                method:'POST',
                headers:{
                    'Accept':'application/json',
                    'Content-Type':'application/json'
                },
                body:JSON.stringify(user)
            });

            const result = await res.json();

            if(result.success === true){
                localStorage.access_token = result.data.access_token 
            }

            return result;

        } catch (error) {
            return {
                success:false,
                errorMessage:'网络错误'
            }
        }
    }

}

export default new UserManager();
```


3，构建MessageManager数据服务对象，该对象封装了消息和评论的相关操作。

* 发布消息
* 发布消息评论
* 获取所有用户的消息
* 获取某一天消息的所有评论

```
import {
    postMessageURL,
    postCommentURL,
    allMessagesURL,
    allCommentsURL,
} from './URLConfig';

class MessageManager {

    async postMessage(title,content,images){
        try {
            
            const formData = new FormData();

            formData.append('access_token',localStorage.access_token);
            formData.append('title',title);
            formData.append('content',content);
            images.map((item,index)=>{
                return formData.append(`image${index}`,item.file);
            })  

            const res = await fetch(postMessageURL,{
                method:'POST',
                body:formData
            });

            const result = await res.json();

            console.log(result);

            return result;

        } catch (error) {
            return {
                success:false,
                errorMessage:'网络错误'
            }
        }
    }

    async postComment(messageID,content){
        try {
            const comment = {
                access_token:localStorage.access_token,
                messageID,
                content
            }

            const res = await fetch(postCommentURL,{
                method:'POST',
                headers:{
                    'Accept':'application/json',
                    'Content-Type':'application/json'
                },
                body:JSON.stringify(comment)
            });

            const result = await res.json();

            return result;

        } catch (error) {
            return {
                success:false,
                errorMessage:'网络错误'
            }
        }
    }

    async allMessages(){
        try {
            const message = {
                access_token:localStorage.access_token,
            }

            const res = await fetch(allMessagesURL,{
                method:'POST',
                headers:{
                    'Accept':'application/json',
                    'Content-Type':'application/json'
                },
                body:JSON.stringify(message)
            });

            const result = await res.json();

            return result;

        } catch (error) {
            return {
                success:false,
                errorMessage:'网络错误'
            }
        }
    }

    async allComments(messageID){
        try {
            const comment = {
                access_token:localStorage.access_token,
                messageID
            }

            const res = await fetch(allCommentsURL,{
                method:'POST',
                headers:{
                    'Accept':'application/json',
                    'Content-Type':'application/json'
                },
                body:JSON.stringify(comment)
            });

            const result = await res.json();

            return result;

        } catch (error) {
            return {
                success:false,
                errorMessage:'网络错误'
            }
        }
    }

    
}

export default new MessageManager();
```

### 构建页面路由

1，此WebApp中包含的4个Screen，需要通过路由表将其访问路径做规划：

* HomeScreen，访问路径为`/`
* LoginScreen，访问路径为`/LoginScreen`
* RegisterScreen，访问路径为`/RegisterScreen`
* CommentScreen，访问路径为`/CommentScreen`
* CreateCommentScreen，访问路径为`/CreateCommentScreen`
* CreateMessageScreen，访问路径为`/CreateMessageScreen`

路由表实现代码：

```
import Vue from 'vue'
import Router from 'vue-router'
import LoginScreen from './Screen/LoginScreen.vue'
import RegisterScreen from './Screen/RegisterScreen.vue'
import HomeScreen from './Screen/HomeScreen.vue'
import CommentScreen from './Screen/CommentScreen.vue'
import CreateMessageScreen from './Screen/CreateMessageScreen.vue'
import CreateCommentScreen from './Screen/CreateCommentScreen.vue'


Vue.use(Router)

export default new Router({
  routes: [
    {
      path: '/',
      name: 'HomeScreen',
      component: HomeScreen
    },
    {
      path: '/LoginScreen',
      name: 'LoginScreen',
      component: LoginScreen
    },
    {
      path: '/RegisterScreen',
      name: 'RegisterScreen',
      component: RegisterScreen
    },
    {
      path: '/CommentScreen/:id',
      name: 'CommentScreen',
      component: CommentScreen
    },
    {
      path: '/CreateMessageScreen',
      name: 'CreateMessageScreen',
      component: CreateMessageScreen
    },
    {
      path: '/CreateCommentScreen/:id',
      name: 'CreateCommentScreen',
      component: CreateCommentScreen
    }
  ]
})

```

2，main.js中加载路由表

```
import Vue from 'vue'
import App from './App.vue'
import router from './router'

import Vant from 'vant'
import 'vant/lib/vant-css/index.css'

Vue.use(Vant)

Vue.config.productionTip = false

new Vue({
  router,
  render: h => h(App)
}).$mount('#app')
```

3，App.vue中渲染一个`router-view`组件，以来根据访问路径显示相应的Screen

```
<template>
  <div id="app">
    <router-view/>
  </div>
</template>
```

### Screen对象实现

在Screen对象实现过程中，主要是用Vant组件库和Manager对象，通过组件库中的组件构建页面，通过Manager对象处理数据操作。

1，登录页面  LoginScreen

```
<template>
  <div>
      <van-nav-bar
        title="登录"
      />
      <br/>
      <van-cell-group>
      <van-field
        v-model="username"
        label="用户名"
        placeholder="请输入用户名"
      />
      <van-field
        v-model="password"
        type="password"
        label="密码"
        placeholder="请输入密码"
      />
    </van-cell-group>
    <br/>
    <van-button 
      size="large"
      type="primary"
      @click="denglu"
    >登录</van-button>
    <br/>
    <br/>
    <van-button 
      size="large"
      type="primary"
      @click="zhuce"
    >注册</van-button>
  </div>
</template>


<script>
import { Toast } from 'vant'
import userManager from '../DataServer/UserManager'

export default {
  name:'LoginScreen',
  data:function(){
    return{
      username:'',
      password:''
    }
  },
  methods:{
    denglu:async function(){
      const reslut = await userManager.login(this.username,this.password);
      if(reslut.success === false){
          Toast.fail(reslut.errorMessage);
          return;
      }
      this.$router.push('/');
    },
    zhuce:function(){
      this.$router.push('/RegisterScreen');
    }
  },
}
</script>

```

2，注册页面 RegisterScreen

```
<template>
  <div>
      <van-nav-bar
        title="注册"
        left-text="返回"
        left-arrow
        @click-left="onClickLeft"
      />
      <br/>
      <van-cell-group>
      <van-field
        v-model="username"
        label="用户名"
        placeholder="请输入用户名"
      />
      <van-field
        v-model="password"
        label="密码"
        placeholder="请输入密码"
      />
    </van-cell-group>
    <br/>
    <van-button 
      size="large"
      type="primary"
      @click="zhuce"
    >提交注册</van-button>
  </div>
</template>


<script>
import { Toast } from 'vant'
import userManager from '../DataServer/UserManager'

export default {
  name:'RegisterScreen',
  data:function(){
    return{
      username:'',
      password:''
    }
  },
  methods:{
    zhuce:async function(){
      const reslut = await userManager.register(this.username,this.password);
      if(reslut.success === false){
          Toast.fail(reslut.errorMessage);
          return;
      }
      this.$router.push('/');
    },
    onClickLeft:function(){
      this.$router.go(-1);
    }
  },
}
</script>

```

3，主页 HomeScreen

首先构建MessageCell组件来展现主页中的消息条目：

```
<template>
    <div 
        id='root'
        @click="click">
        <van-cell 
            :title="message.title" 
            :value="date" 
            :border="false"
        />
        <van-cell 
            :value="message.content" 
            :border="false"
        />
        <div class="sudoku_row">
            <div 
                class="sudoku_item" 
                v-for="image in message.images"
                :key="image.id"
            > 
                    <img :src="imageBaseURL+image.url" width="80" height="80" /> 
            </div>
        </div>
        <van-cell 
            :value="message.message_user.username" 
            :border="false"
        />
    </div>
</template>

<script>

import moment from 'moment';

import {
    imageBaseURL
} from '../DataServer/URLConfig';

export default {
  name:'MessageCell',
  props:[
      'message'
  ],
  data:function(){
      return{
          imageBaseURL
      }
  },
  methods:{
      click:function(){
          this.$emit('tap',this.message.id);
      },
  },
  computed:{
      date:function(){
          return moment(this.message.createdAt).format('YYYY-MM-DD HH:mm')
      }
  }
}
</script>

<style>
    .sudoku_row{
        display: flex;
        align-items: center;
        width:100%;
        flex-wrap: wrap;
    }
    .sudoku_item{
        display: flex;
        justify-content: center;
        align-items: center;
        flex-direction: column;
        width:33%;
        padding-top: 10px;
        padding-bottom: 10px;
    }
    .opacity{
        opacity: 0.4;
        background: #e5e5e5;
    }
    .sudoku_item img{
        margin-bottom: 3px;
        display: block;
    }
    #root{
        border-width: 1px;
        border-style: solid;
        border-color: gray;
    }
</style>
```

在主页中使用MessageCell构建页面：

```
<template>
  <div>
      <van-nav-bar
        title="留言板"
        left-text="退出"
        right-text="发布"
        @click-left="onClickLeft"
        @click-right="onClickRight"
      />
      <van-list>
        <MessageCell 
          v-for="message in messages" 
          :key="message.id" 
          :message="message"
          @tap="tapMessage"
        />
      </van-list>
  </div>
</template>

<script>

import { Toast } from 'vant'

import messageManager from '../DataServer/MessageManager';
import userManager from '../DataServer/UserManager';

import MessageCell from '../ViewComponent/MessageCell.vue'


export default {
  name:'HomeScreen',
  components:{
    MessageCell
  },
  data:function(){
    return{
      messages:[]
    }
  },
  methods:{
    onClickLeft:function(){
      userManager.logout();
      this.$router.replace('/LoginScreen');
    },
    onClickRight:function(){
      this.$router.push('/CreateMessageScreen');
    },
    tapMessage:function(id){
        this.$router.push('/CommentScreen/'+id);
    }
  },
  mounted:async function (){
    if(userManager.isLogin() === false){
        this.props.history.replace('/LoginScreen');
        return;
    }

    Toast.loading({
        duration: 0,       // 持续展示 toast
        forbidClick: true, // 禁用背景点击
        loadingType: 'spinner',
        message: '数据加载中'
    });

    const result = await messageManager.allMessages();
    Toast.clear();
    console.log(result)
    if(result.success === false){
        Toast.fail(result.errorMessage);
        return;
    }

    this.messages = result.data;

  }
}
</script>
```

4，评论页面 CommentScreen

首先构建CommentCell组件来展示评论内容：

```
<template>
    <van-cell
        :title="comment.message_user.username" 
        :value="date" 
        :label="comment.content" 
    />
</template>


<script>

import moment from 'moment'

export default {
  name:'CommentCell',
  props:[
      'comment'
  ],
  computed:{
      date:function(){
          return moment(this.comment.createdAt).format('YYYY-MM-DD HH:mm')
      }
  }
}
</script>

```

使用CommentCell来构建评论页面

```
<template>
    <div>
        <van-nav-bar
            title="评论"
            left-text="返回"
            right-text="发评论"
            @click-left="onClickLeft"
            @click-right="onClickRight"
        />
        <CommentCell
            v-for="comment in comments"
            :key="comment.id"
            :comment="comment"
        />
    </div>
</template>

<script>

import { Toast } from 'vant'

import messageManager from '../DataServer/MessageManager';
import userManager from '../DataServer/UserManager';

import CommentCell from '../ViewComponent/CommentCell';

export default {
  name:'CommentScreen',
  components:{
    CommentCell
  },
  data:function(){
      return{
          comments:[]
      }
  },
  methods:{
    onClickLeft:function(){
      this.$router.go(-1);
    },
    onClickRight:function(){
      this.$router.push('/CreateCommentScreen/'+this.$route.params.id);
    }
  },
  computed:{
      date:function(){
          return moment(this.comment.createdAt).format('YYYY-MM-DD HH:mm')
      }
  },
  mounted:async function(){

    if(userManager.isLogin() === false){
        this.props.history.replace('/LoginScreen');
        return;
    }

    Toast.loading({
        duration: 0,       // 持续展示 toast
        forbidClick: true, // 禁用背景点击
        loadingType: 'spinner',
        message: '评论加载中'
    });

    const result = await messageManager.allComments(this.$route.params.id);
    Toast.clear();
    console.log(result)
    if(result.success === false){
        Toast.fail(result.errorMessage);
        return;
    }

    if(result.data.length === 0){
        Toast('无评论');
        return;
    }

    this.comments = result.data;

  }

}
</script>

```

5，消息发布页面 CreateMessageScreen

```
<template>
    <div>
        <van-nav-bar
            title="发消息"
            left-text="返回"
            left-arrow
            @click-left="onClickLeft"
        />
        <van-cell-group>
            <van-field
                v-model="title"
                label="标题"
            />
            <van-field
                v-model="content"
                type="textarea"
                placeholder="请输入内容"
                rows="1"
                autosize
            />
            <div
                v-for="(image,index) in images"
                :key="index"
                style="display:inline"
            >
            <van-icon  
                id="del" 
                name="close" 
                @click="del(index)"
            />
            <img  
                :src="image.content"
                :alt="index"
                id="image"
            />
            </div>
            <van-uploader 
                :after-read="onRead"
                v-if="images.length<9"
            >
                <van-icon id="icon" name="add-o" />
            </van-uploader>
            <br/>
            <van-button 
                size="large"
                type="primary"
                @click="submit"
            >提交</van-button>
        </van-cell-group>
    </div>
</template>

<script>

import { Toast,Dialog } from 'vant'

import messageManager from '../DataServer/MessageManager';
import userManager from '../DataServer/UserManager';

export default {
  name:'CreateMessageScreen',
  data:function(){
      return{
          title:'',
          content:'',
          images:[]
      }
  },
  methods:{
    del(index){
        this.images.splice(index,1);
    },
    onRead(file) {
      this.images.push(file);
    },
    submit:async function(){
        Toast.loading({
          duration: 0,       // 持续展示 toast
          forbidClick: true, // 禁用背景点击
          loadingType: 'spinner',
          message: '数据提交中'
      });
      const result = await messageManager.postMessage(this.title,this.content,this.images);
      Toast.clear();
      console.log(result);
      if(result.success === false){
          Toast.fail(result.errorMessage);
          return;
      }
      Dialog.alert({
        title: '提交成功',
        message: '点击确认按钮返回'
      }).then(() => {
        this.$router.go(-1);
      });
    },
    onClickLeft:function(){
      this.$router.go(-1);
    }
  },
  mounted:function(){
      if(userManager.isLogin() === false){
        this.props.history.replace('/LoginScreen');
        return;
    }
  }
}
</script>


<style>
#image{
    width: 80px;
    height: 80px;
    margin: 10px;
}


#icon {
    font-size: 80px;
    margin: 10px;
}

#del {
    display: inline-block;
    left:90px;
    bottom:70px;
    font-size: 20px;
}
</style>

```

6，评论发布页面 CreateCommentScreen

```
<template>
    <div>
        <van-nav-bar
            title="发评论"
            left-text="返回"
            left-arrow
            @click-left="onClickLeft"
        />
        <van-cell-group>
            <van-field
                v-model="content"
                type="textarea"
                placeholder="请输入评论内容"
                rows="1"
                autosize
            />
            <br/>
            <van-button 
                size="large"
                type="primary"
                @click="submit"
            >提交</van-button>
        </van-cell-group>
    </div>
</template>

<script>

import { Toast,Dialog } from 'vant'

import messageManager from '../DataServer/MessageManager';
import userManager from '../DataServer/UserManager';

export default {
  name:'CreateCommentScreen',
  data:function(){
      return{
          content:'',
      }
  },
  methods:{
    submit:async function(){
        Toast.loading({
          duration: 0,       // 持续展示 toast
          forbidClick: true, // 禁用背景点击
          loadingType: 'spinner',
          message: '数据提交中'
      });

      const result = await messageManager.postComment(this.$route.params.id,this.content);
      Toast.clear();
      console.log(result);
      if(result.success === false){
          Toast.fail(result.errorMessage);
          return;
      }
      Dialog.alert({
        title: '提交成功',
        message: '点击确认按钮返回'
      }).then(() => {
        this.$router.go(-1);
      });
    },
    onClickLeft:function(){
      this.$router.go(-1);
    }
  },
  mounted:function(){
      if(userManager.isLogin() === false){
        this.props.history.replace('/LoginScreen');
        return;
    }
  }
}
</script>


<style>
#image{
    width: 80px;
    height: 80px;
    margin: 10px;
}

#uploader{
    width: 80px;
    height: 80px;
    margin: 10px;
    background-color: red;
    display: inline-block;
}

#icon {
    font-size: 80px;
    margin: 10px;
}

#del {
    display: inline-block;
    left:90px;
    bottom:70px;
    font-size: 20px;
}
</style>

```