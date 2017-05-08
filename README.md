# 基于vue2重写Cnodejs移动端 [线上访问地址](http://120.24.230.56/index.html)

### 技术栈
`vue2 + vue-router + vuex + ES6 + less + flex.css`


遇到的一个问题，就是如何能在页面前进时记录数据和滚动条位置，选择的方案是window.sessionStorage,
一开始不会vuex 时候全部都是props传递数据好痛苦，后期更换成vuex,

通过require.ensure在路由的那个地方来按需加载，作用类似于angular的resolve的lazyload
webpack 打包，把disk里面的文件丢到阿里云上，配置nginx代理80端口，pm2守护进程，可惜网站还正在备案中，只能通过ip访问：http://120.24.230.56/index.html

有一个问题啊，线上的vue的路由会被后台视为请求的url,一刷新就404了，目前的解决思路是通过nginx来开启重写url把vue中定义的路由全指到index.html，还在解决汇总，欢迎大神指教，感激不尽~

### 安装

项目地址：（`git clone`）

```shell
git clone https://github.com/dujuncheng/cnode-vue.git
```

通过`npm`安装本地服务第三方依赖模块(需要已安装[Node.js](https://nodejs.org/))

```
npm install
```

启动服务(http://localhost:8020)

```
npm run dev
```

发布代码
```
npm run build
```

### 开发

### 目录结构
<pre>
.
├── README.md           
├── build              // 构建服务和webpack配置
├── config             // 项目不同环境的配置
├── dist               // 项目build目录
├── index.html         // 项目入口文件
├── package.json       // 项目配置文件
├── src                // 生产目录
│   ├── assets         // css js 和图片资源
│   ├── components     // 各种组件
│   ├── views          // 各种页面
│   ├── vuex           // vuex状态管理器
│   ├── filters.js     // 各种过滤器
│   └── main.js        // Webpack 预编译入口
</pre>


### 更新

1. 新增下拉加载组件开发，增强用户体验
2. 新增页面左上角后退按钮
3. 新增loading 动画
4. 用上了Element UI，统一一下ui


小广告: 勤奋刻苦能干活的小生暑假求实习啊，微信号：dujuncheng1 （注意后面有个1）

