## Vue3小兔鲜电商项目

### 项目起步

#### 1、项目初始化

- 脚手架：create-vue（底层：vite）创建项目初始框架

npm init vue@latest

> [!NOTE]
>
> 报错You can rerun the command with `--loglevel=verbose` to see the logs in your terminal时，可以使用管理员方式打开cmd再次运行

项目名称：vue-rabbit

包含的功能：router（单页面应用开发）,pinia（状态管理）,eslint（错误预防）

试验特性：无

> 项目初始化完成，可执行以下命令：
>
>    cd vue-rabbit
>    npm install
>    npm run dev
>
> 尝试运行项目出现页面则创建成功

- 项目文件夹

![image-20250911191856882](C:\Users\王怡倩\AppData\Roaming\Typora\typora-user-images\image-20250911191856882.png)

需要手动添加下面五个文件夹：

**apis**:用于存放与后端 API 交互的代码，包括请求函数和接口定义等。

 **composables**:用于存放组合式函数（Composables)，它们是一些可复用的逻辑片段，可以在多个组件之间共享。   

**directives**:包含了自定义指令的定义。

**styles**:包含了全局样式文件，如 CSS、SCSS 等。

**utils**:包含了各种工具函数和辅助函数

其他文件夹：

**node_modules**: 这个文件夹包含了项目依赖的所有 npm 包。

**public**: 这个文件夹包含了静态资源文件，如 HTML、图片、字体等。

**assets**: 这个文件夹包含了项目中使用的静态资源文件，如图片、图标、字体等。

**components**: 这个文件夹包含了可复用的 Vue 组件。

**router**: 这个文件夹包含了路由相关的配置文件，如路由表定义、导航守卫等。

**stores**: 这个文件夹包含了状态管理相关的代码，如 Pinia 或 Vuex 的 store 定义。

**views**: 这个文件夹包含了页面级别的 Vue 组件

**App.vue**: 这是项目的根组件，所有的其他组件都是它的子组件。它通常包含应用的布局和全局样式。

**main.js**: 这是项目的入口文件，它负责初始化 Vue 应用、注册全局组件、挂载根组件等。

> [!NOTE]
>
> | 特性         | `components`                                    | `views`                                         |
> | ------------ | ----------------------------------------------- | ----------------------------------------------- |
> | 中文名       | 组件                                            | 视图 / 页面                                     |
> | 作用         | 封装可复用的 UI 片段                            | 表示一个完整的页面                              |
> | 是否对应路由 | ❌ 一般不直接对应 URL                            | ✅ 通常对应一个路由（如 `/home`, `/login`）      |
> | 复用性       | ✅ 高，多个页面都可以用                          | ❌ 低，一般只在一个路由下使用                    |
> | 大小和复杂度 | 较小，功能单一（如按钮、轮播图）                | 较大，可能包含多个组件                          |
> | 示例         | `<MyButton />`, `<Header />`, `<ProductCard />` | `HomeView.vue`, `LoginView.vue`, `CartView.vue` |
>
> | 特性         | `src/assets`                                                 | `public`                                                     |
> | ------------ | ------------------------------------------------------------ | ------------------------------------------------------------ |
> | 是否参与构建 | ✅ 是，会被 Vite 处理（压缩、重命名、生成 hash 名等）         | ❌ 否，直接复制，不做任何处理                                 |
> | 如何引用     | 在代码中作为模块导入（如 `import img from '@/assets/logo.png'`） | 通过根路径 `/` 直接访问（如 `<img src="/images/logo.png">`） |
> | 输出路径     | 打包后可能变成 `assets/logo.abc123.png`（带 hash）           | 文件名不变，路径为 `/images/logo.png`                        |
> | 适用场景     | 组件中使用的图标、背景图、CSS 中引用的资源等                 | favicon.ico、robots.txt、大型静态文件、第三方 SDK 文件等     |

#### 2、git管理

- 在GitHub账号上创建一个新仓库（new repository）

- ```
  # 添加远程仓库地址（第一次需要）
  git remote add origin https://github.com/你的用户名/你的仓库名.git
  
  #创建一个main分支
  git branch -M main
  ```

- ```
  #本地操作
  git add .
  git commit -m "测试：更新 README"
  
  #拉取（pull）远程的更改到本地
  git pull origin main
  
  # 推送本地提交到 GitHub 的 main 分支
  git push origin main
  git push -u origin main（若第一次推送使用）
  ```
  
  > 最常见的原因是Git配置了代理但代理服务未运行。
  >
  > ```
  > git config --global --unset http.proxy
  > git config --global --unset https.proxy
  > ```

#### 3、elementplus配置

小兔鲜儿组件分为通用性组件和业务定制性组件，**通用型组件（element Plus）**需要配置引入项目。

1. 打开[element Plus网址](https://element-plus.org/zh-CN/guide/design.html)

2. 安装两个包（npm安装）

   ```
   npm install element-plus --save
   npm install -D unplugin-vue-components unplugin-auto-import
   ```

3. 在vite.config.ts文件中插入相关代码（指南中有）

4. 为插入的element组件设置主题色

   > Element Plus 使用 SCSS 预处理器和 CSS 变量来管理样式，这使得主题定制成为可能。其核心原理是**变量覆盖**：在 Element Plus 加载其默认样式之前，先用你的自定义变量覆盖掉默认变量值。

   - 安装scss

     ```
     npm i sass -D
     ```

   - 准备定制样式文件，放在styles/element/index.scss

     ```javascript
     @forward 'element-plus/theme-chalk/src/common/var.scss' with ($colors: ('primary':( // 主色
           'base':#27ba9b,
         ),
         'success':( // 成功色
           'base':#1dc779,
         ),
         'warning':( // 警告色
           'base':#ffb302,
         ),
         'danger':( // 危险色
           'base':#e26237,
         ),
         'error':( // 错误色
           'base':#cf4444,
         ),
       ))
     ```

   - 对Element Plus样式进行覆盖，通知Element采用scss语言，导入定制scss文件覆盖

     ```javascript
     export default defineConfig({
       plugins: [
         vue(),
         vueDevTools(),
         AutoImport({
           resolvers: [ElementPlusResolver()],
         }),
         Components({
           resolvers: [
             // 1.配置elementPlus采用sass样式配色系统
             ElementPlusResolver({ importStyle: "sass" })],
         }),
       ],
       resolve: {
         alias: {
           '@': fileURLToPath(new URL('./src', import.meta.url))
         },
       },
       css: {
         preprocessorOptions: {
           scss: {
             // 2.自动导入定制样式文件进行样式覆盖
             additionalData: `
             @use "@/styles/element/index.scss" as *;
             `,
           }
         }
       }
     })
     ```


#### 4、axios基础配置

主要作用：能够轻松地向服务器发送异步 HTTP 请求（如 GET, POST, PUT, DELETE 等）并处理响应数据。

1. 安装

   ```
   npm i axios
   ```

2. 配置基础实例（统一接口配置）

   避免直接修改全局的 `axios` 默认值。可以为不同的后端API创建多个实例（例如 `apiClient1`, `apiClient2`），每个拥有独立的配置，互不干扰。

   - 接口基地址
   - 接口超时时间
   - 请求拦截器
   - 响应拦截器

   ```javascript
   //utils/http.js
   // axios基础封装
   import axios from "axios";
   
   // 创建axios实例
   const httpInstance = axios.create({
     baseURL: 'https://pcapi-xiaotuxian-front-devtest.itheima.net',
     timeout: 5000
   })
   
   // axios请求拦截器
   httpInstance.interceptors.request.use(
    	//成功回调函数，接受一个config对象   
       config => {return config},
       //错误回调函数
       e => Promise.reject(e)
   )
   //config请求配置对象，e请求错误
   
   // axios响应式拦截
   httpInstance.interceptors.response.use(
       res => res.data, 
       e => {return Promise.reject(e)}
   )
   //res返回的响应对象
   
   //暴露
   export default httpInstance
   ```

   > **拦截器 (Interceptors)**
   >
   > 拦截器本质上是一个**函数**，它允许你在请求发送前或响应被处理前，对它们进行**拦截**并做一些统一的处理。

3. 按功能模块组织API

    将每个接口封装成一个独立的函数并导出。

   ```javascript
   //apis/test.js
   import httpInstance from "@/utils/http";
   
   //表示是一个GET请求，与分类数据有关的接口函数
   export function getCategoryAPI() {
     return httpInstance({
       url: 'home/category/head'
     })
   }
   ```

   > URL 是 `'home/category/head'`，它是一个**相对路径**。它会自动与我们在 `http.js` 中为 `httpInstance` 配置的 `baseURL`拼接在一起，形成完整的请求地址：`'http://api.example.com/home/category/head'`

4. 在项目入口文件调用接口函数

   ```javascript
   import './assets/main.css'
   import { createApp } from 'vue'
   import { createPinia } from 'pinia'
   import App from './App.vue'
   import router from './router'
   
   // 测试接口函数
   import { getCategoryAPI } from '@/apis/test'
   getCategoryAPI().then(res => {
     console.log(res) // 测试请求是否成功，成功后会打印数据
   })
   
   const app = createApp(App)
   app.use(createPinia())
   app.use(router)
   app.mount('#app')
   ```

   > `.then(...)`这是 **Promise 对象的核心方法**。
   >
   > - 它用于**处理一个异步操作成功完成后的结果**。你可以将它理解为：“**然后呢？成功了之后做什么？**”
   > - **语法**：`promise.then(onFulfilled, onRejected)`
   >   - `onFulfilled`：一个**回调函数**，当 Promise 成功解决（fulfilled）时被调用。
   >   - `onRejected`：另一个回调函数（可选），当 Promise 被拒绝（rejected）时被调用。你的代码中只提供了第一个参数。

##### 内在逻辑与数据流

**逻辑链条：**
组件 (View层) -> 导入并使用 -> API函数 (Service层) -> 导入并使用 -> HTTP实例 (Utils层) -> 发送请求 -> 服务器

**数据返回链条：**
服务器返回数据 -> HTTP实例的拦截器处理 -> API函数返回Promise -> 组件await拿到数据 -> 更新页面

**设计思想：** **“关注点分离”** 和 **“分层架构”**

1. **`http.js` (工具层)：负责所有**通用的、技术性的**事情。
   - **改一处，处处改**：如果后端接口地址换了，你只需要修改 `http.js` 里的 `baseURL`，所有接口自动生效。如果要在每个组件里都写完整URL，你得改到吐血。
   - **统一管理**：所有请求都要加Token？所有错误都要弹窗提示？在拦截器里写一次就行了，不用在每个请求里重复写。
2. **`test.js` (API服务层)：负责**定义有什么功能**。
   - **清晰易懂**：项目有多少个接口，每个接口是干什么的，一看这个文件就知道了，就像一本书的目录。
   - **易于维护**：某个接口的路径变了？直接来这里修改`url`字符串即可，不需要去vue组件里大海捞针。
3. **Vue组件 (视图层)：负责**显示数据和用户交互**。
   - **专注于UI**：组件里的代码应该非常干净，主要是“点击这个按钮 -> 调用那个函数 -> 把返回的数据显示出来”。它不应该关心请求的细节（比如怎么加Token、基地址是什么）。
   - **可复用性**：同一个`getCategoryAPI()`函数，可以在不同的组件（比如首页、管理页）里被调用，避免了代码重复。

#### 5、项目路由设计

一级路由：页面整体切换

二级路由：页面部分切换

```javascript
import { createRouter, createWebHistory } from 'vue-router'
//`createRouter`: Vue Router 的函数，用于创建路由实例。`createWebHistory`: 使用HTML5的History模式
import Login from '@/views/Login/index.vue'
import Layout from '@/views/Layout/index.vue'
import Home from '@/views/Home/index.vue'
import Category from '@/views/Category/index.vue'
//把一个功能相关的所有文件打包到一个文件夹里，然后通过导入文件夹来访问它的主入口（index 文件）

const router = createRouter({
  history: createWebHistory(import.meta.env.BASE_URL),
  routes: [
    //一级路由
  	{
      path: '/',
      component: Layout,
        //二级路由
      children: [
        {
          path: '',
          component: Home
        },
        {
          path: 'catagory',
          component: Category
        }
      ]
    },
    {
      path: '/login',
      component: Login
    }
  ],
})

export default router
```

> `path: ''`：当路径是**精确匹配**父路径 `/` 时，在 `Layout` 中显示 `Home` 组件。
>
> `path: 'category'`：当路径是 `/category` 时，在 `Layout` 中显示 `Category` 组件。

> 当写 `import ... from '@/views/Login/index.vue'` 时，你是在**显式地、精确地**指定要导入 `index.vue` 这个文件。这是最直接、绝对不会出错的方式。
>
> 但是，当你写 `import ... from '@/views/Login'`（省略了 `/index.vue`），模块解析器（由 Vite 或 Webpack 提供）会遵循一个**默认的解析规则**：
>
> **规则：当你导入的路径是一个文件夹（而不是一个文件）时，模块解析器会自动尝试在这个文件夹中寻找一个名为 `index` 的文件（`index.js`, `index.vue`, `index.ts` 等），并将其作为该模块的入口点。**
