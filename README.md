# vue-element-manage

#### 介绍
使用element ui和node expres做的epub电子书管理后台

#### 软件架构
软件架构说明


#### 安装教程

1.  npm run dev
2.  xxxx
3.  xxxx

#### 使用说明

1.  xxxx
2.  xxxx
3.  xxxx

#### 参与贡献

1.  Fork 本仓库
2.  新建 Feat_xxx 分支
3.  提交代码
4.  新建 Pull Request


#### 码云特技

1.  使用 Readme\_XXX.md 来支持不同的语言，例如 Readme\_en.md, Readme\_zh.md
2.  码云官方博客 [blog.gitee.com](https://blog.gitee.com)
3.  你可以 [https://gitee.com/explore](https://gitee.com/explore) 这个地址来了解码云上的优秀开源项目
4.  [GVP](https://gitee.com/gvp) 全称是码云最有价值开源项目，是码云综合评定出的优秀开源项目
5.  码云官方提供的使用手册 [https://gitee.com/help](https://gitee.com/help)
6.  码云封面人物是一档用来展示码云会员风采的栏目 [https://gitee.com/gitee-stars/](https://gitee.com/gitee-stars/)

<!--
 vue.config.js中的config.devtool可以切换代码的调试方式source-map或eval或cheap-source-map

vue-element-admin 对所有访问的路由进行拦截；
访问路由时会从 Cookie 中获取 Token，判断 Token 是否存在：
如果 Token 存在，将根据用户角色生成动态路由，然后访问路由，生成对应的页面组件。这里有一个特例，即用户访问 /login 时会重定向至 / 路由；
如果 Token 不存在，则会判断路由是否在白名单中，如果在白名单中将直接访问，否则说明该路由需要登录才能访问，此时会将路由生成一个 redirect 参数传入 login 组件，实际访问的路由为：/login?redirect=/xxx。
关于动态路由和权限校验
vue-element-admin 将路由分为：constantRoutes 和 asyncRoutes
用户登录系统时，会动态生成路由，其中 constantRoutes 必然包含，asyncRoutes 会进行过滤；
asyncRoutes 过滤的逻辑是看路由下是否包含 meta 和 meta.roles 属性，如果没有该属性，所以这是一个通用路由，不需要进行权限校验；如果包含 roles 属性则会判断用户的角色是否命中路由中的任意一个权限，如果命中，则将路由保存下来，如果未命中，则直接将该路由舍弃；
asyncRoutes 处理完毕后，会和 constantRoutes 合并为一个新的路由对象，并保存到 vuex 的 permission/routes 中；
用户登录系统后，侧边栏会从 vuex 中获取 state.permission.routes，根据该路由动态渲染用户菜单。




后台
使用express-validator进行参数类型校验
在 router.post 方法中使用 body 方法判断参数类型，并指定出错时的提示信息
使用 const err = validationResult(req) 获取错误信息，err.errors 是一个数组，包含所有错误信息，如果 err.errors 为空则表示校验成功，没有参数错误
如果发现错误我们可以使用 next(boom.badRequest(msg)) 抛出异常，交给我们自定义的异常处理方法进行处理















 -->