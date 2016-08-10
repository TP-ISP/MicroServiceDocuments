# server-to-go
Provide  information to the frontend with JSON.

This project is just an simple example of the depart-development .

## 前后分离



![前后分离](http://ww3.sinaimg.cn/mw690/63918611gw1efj2vvjwtfj20ge0gzab9.jpg)

**前后分离拓扑**

在classaide的项目中，为了能够实践我在博客中阐述的开发准则，我将前端，后端，可选的中间件，数据库schema都单独进行开发，然后针对一个应用，设计一套schema，对界面进行适当的定制，即可实现敏捷开发。

在拓扑中，前端采用Vue.js进行开发，使用vue-resource获取数据，Koa作为中间层，提供Restful风格的API，然后Nodejs负责业务逻辑，与数据库进行交互，图中是使用Spring进行业务处理。



## 设计准则

要实现在解耦的情况下的高可用，需要有一套行之有效的规范接口准则。目前，对我我设计的前后分离实践，需要遵循一下几个原则：

1. 数据传输全部使用标准的JSON。
2. 数据库表中，关系型数据库不允许出现外键，有业务逻辑交叉的表相互独立，其业务上的联系在代码中处理。
3. 所有API都要按照Restful方式提供。
4. 中间层的和业务处理之间不能混砸，不能直接在路由函数中处理逻辑。所有业务处理逻辑需要遵循统一的命名空间。
5. 必须要有单独的用户管理模块，所有需要登录的，Auth相关的，全部交给这个模块，之后新增的业务遵循SSO方式处理。
6. 前端不使用后端模板引擎来渲染。
7. 在后端提供的API中，必须有一个接口，能够返回前端所能请求的所有接口的信息。