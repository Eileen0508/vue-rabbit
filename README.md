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
  
  # 推送本地提交到 GitHub 的 main 分支
  git push -u origin main
  ```

  

