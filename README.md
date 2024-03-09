# tpl-micro-frontends
微前端技术方案主要分为跳转式微前端和请求式微前端。升级方向主要包括应用容器搭建、共享包开发、公用设计系统搭建和monorepo本地开发。
### 跳转式
跳转式微前端的技术主要包括URL和iframe。URL最简单，但有页面刷新。iframe开发体验最好，但频繁的文档创建，导致浏览器性能消耗大，而且破坏了文档的完整性，导致语义化，SEO不友好。所以，此类方案常用于中后台微前端建设。
### 请求式
请求式微前端的技术主要包括客户端渲染和服务端拼装。ajax + nginx(前端代理)、ajax + nginx + ssi 分别是实现客户端渲染、服务端拼装的最简单方式，而且渲染的文档完整，很适合客户端微前端。但要做好隔离和延迟风险的规避。
### 应用容器
应用容器可实现统一的单页应用。web Component + Shadow DOM + history路由，可以搭建应用容器，其中包括微前端生命周期、通信、隔离、上下文、路由等基本要素，是应用容器的基本原型。但是旧浏览器不支持，多应用于新客户端，建议在single.js这个元框架上做二次开发。
### 共享包
基于webpack的vender bundle、模块联邦、rollup动态导入，都可以实现公用框架的抽离，减少代码冗余。
### 公用设计系统
基于样式库、UI风格搭建的系统，统一研发的风格和交互，提升用户体验，利于品牌打造。
### 本地开发
通过monorepo或则片段模拟的方式进行本地协作和开发调试。

# mf_ajax_router
通过ajax请求，nginx根据请求按路由拉取资源
```javascript
(function() {
  const element = document.querySelector(".decide_recos");
  const url = element.getAttribute("data-fragment");

  window
    .fetch(url)
    .then(res => res.text())
    .then(html => {
      element.innerHTML = html;
    });
})();
```

# mf_web_component mf_single_spa
mf_web_component是应用容器原型，single.js是应用容器元框架，可以基于single.js的动态注册微前端，（vue\react\svelte）的适配器做二次开发。

# mf_shared_vendor
共享包，统一框架，统一引入公用框架，减少代码冗余