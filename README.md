[合集 \- 2024/11(16\)](https://github.com)[1\.Nuxt.js 应用中的 nitro：config 事件钩子详解11\-02](https://github.com/Amd794/p/18522042)[2\.Nuxt.js 应用中的 nitro：init 事件钩子详解11\-03](https://github.com/Amd794/p/18523216)[3\.Nuxt.js 应用中的 nitro：build：before 事件钩子详解11\-04](https://github.com/Amd794/p/18525081)[4\.Nuxt.js 应用中的 nitro：build：public\-assets 事件钩子详解11\-05](https://github.com/Amd794/p/18527699)[5\.Nuxt.js 应用中的 components：extend 事件钩子详解11\-01](https://github.com/Amd794/p/18519888)[6\.Nuxt.js 应用中的 prerender：routes 事件钩子详解11\-06](https://github.com/Amd794/p/18530333)[7\.Nuxt.js 应用中的 build：error 事件钩子详解11\-07](https://github.com/Amd794/p/18532261)[8\.Nuxt.js 应用中的 prepare：types 事件钩子详解11\-08](https://github.com/Amd794/p/18535141)[9\.Nuxt.js 应用中的 listen 事件钩子详解11\-09](https://github.com/Amd794/p/18536816)[10\.Nuxt.js 应用中的 schema：extend事件钩子详解11\-10](https://github.com/Amd794/p/18538315)[11\.Nuxt.js 应用中的 vite：extend 事件钩子详解11\-11](https://github.com/Amd794/p/18539720)[12\.Nuxt.js 应用中的 vite：extendConfig 事件钩子详解11\-12](https://github.com/Amd794/p/18541898)[13\.Nuxt.js 应用中的 schema：resolved 事件钩子详解11\-13](https://github.com/Amd794/p/18543356)[14\.Nuxt.js 应用中的 schema：beforeWrite 事件钩子详解11\-14](https://github.com/Amd794/p/18545946)[15\.Nuxt.js 应用中的 schema：written 事件钩子详解11\-15](https://github.com/Amd794/p/18548046)16\.Nuxt.js 应用中的 vite：extendConfig 事件钩子详解11\-16收起


---


title: Nuxt.js 应用中的 vite：extendConfig 事件钩子
date: 2024/11/16
updated: 2024/11/16
author:  [cmdragon](https://github.com) 


excerpt:
通过合理使用 vite:extendConfig 钩子，开发者可以极大地增强 Nuxt 3 项目的灵活性和功能性，为不同的项目需求量身定制 Vite 配置。无论是添加插件、调整构建选项还是配置开发服务器，这些扩展可以有效提升开发体验和应用性能。


categories:


* 前端开发


tags:


* Nuxt
* Vite
* 配置
* 钩子
* 插件
* 构建
* 环境




---


![image](https://img2024.cnblogs.com/blog/1546022/202411/1546022-20241116152738668-614483605.png)


![image](https://img2024.cnblogs.com/blog/1546022/202411/1546022-20241116152759171-8750132.png)


扫描[二维码](https://github.com)关注或者微信搜一搜：`编程智域 前端至全栈交流与成长`


在 Nuxt 3 中，`vite:extendConfig` 钩子允许开发者扩展默认的 Vite 配置。这意味着你可以在 Nuxt 项目中根据需求自定义 Vite 的配置，包括添加插件、修改构建选项、调整开发服务器设置等。


## 文章大纲


1. [定义与作用](https://github.com)
2. [调用时机](https://github.com)
3. [参数说明](https://github.com)
4. [示例用法](https://github.com)
5. [应用场景](https://github.com)
	* [5\.1 添加 Vite 插件](https://github.com)
	* [5\.2 调整构建配置](https://github.com)
	* [5\.3 自定义开发服务器设置](https://github.com)
	* [5\.4 根据环境动态调整配置](https://github.com)
6. [注意事项](https://github.com)
7. [总结](https://github.com)


## 1\. 定义与作用


* **`vite:extendConfig`** 是一个事件钩子，提供了机会来修改 Vite 的配置对象。
* 通过该钩子，你可以将额外的 Vite 插件、构建选项、开发服务器设置等添加到项目中。


## 2\. 调用时机


`vite:extendConfig` 钩子在 Nuxt 3 启动时进行 Vite 配置的构建阶段被调用，此时你可以访问到 `viteInlineConfig` 和环境变量 `env`。


## 3\. 参数说明


钩子接收两个参数：


1. **`viteInlineConfig`**: 当前 Vite 的配置对象。你可以直接修改这个对象的属性。
2. **`env`**: 当前的环境变量。可以根据不同环境配置。


## 4\. 示例用法


下面是如何使用 `vite:extendConfig` 钩子的基本示例，展示了如何扩展 Vite 的默认配置。


### 在 `plugins/viteExtendConfig.js` 文件中的实现



```
// plugins/viteExtendConfig.js

export default defineNuxtPlugin((nuxtApp) => {
  nuxtApp.hooks('vite:extendConfig', (viteInlineConfig, env) => {
    // 添加自定义的 Vite 插件，例如 React 支持
    viteInlineConfig.plugins.push(require('@vitejs/plugin-react')());

    // 根据环境动态调整构建选项
    viteInlineConfig.build = {
      ...viteInlineConfig.build,
      sourcemap: env.NODE_ENV === 'development', // 仅在开发模式下开启 sourcemap
    };

    // 修改开发服务器设置
    viteInlineConfig.server = {
      ...viteInlineConfig.server,
      port: 3001, // 将开发服务器的端口修改为 3001
    };
  });
});

```

## 5\. 应用场景


### 5\.1 添加 Vite 插件


在涉及到使用特定功能的情况下，例如使用 React，你可以在 `vite:extendConfig` 中添加 Vite 插件：



```
// plugins/viteExtendConfig.js
viteInlineConfig.plugins.push(require('@vitejs/plugin-react')());

```

### 5\.2 调整构建配置


在不同的环境中，可能需要不同的构建选项。例如，调试开发环境可以开启源码映射：



```
// 根据环境动态调整构建选项
viteInlineConfig.build = {
  ...viteInlineConfig.build,
  sourcemap: env.NODE_ENV === 'development', // 开发环境开启 sourcemap
};

```

### 5\.3 自定义开发服务器设置


如果你需要指定开发服务器的端口，可以这样做：



```
// 修改开发服务器设置
viteInlineConfig.server = {
  ...viteInlineConfig.server,
  port: 3001, // 设置开发服务器端口
};

```

### 5\.4 根据环境动态调整配置


使用 `env` 参数，可以在生产环境和开发环境中使用不同的配置。这使得你的应用更加灵活：



```
if (env.NODE_ENV === 'production') {
  viteInlineConfig.base = '/my-production-base/';
} else {
  viteInlineConfig.base = '/';
}

```

## 6\. 注意事项


* **性能影响**: 添加过多插件或配置可能会影响构建性能，需谨慎选择。
* **兼容性**: 确保你所添加的插件与 Vite 及其他 Nuxt 插件兼容，以避免运行时错误。


## 7\. 总结


通过合理使用 `vite:extendConfig` 钩子，开发者可以极大地增强 Nuxt 3 项目的灵活性和功能性，为不同的项目需求量身定制 Vite 配置。无论是添加插件、调整构建选项还是配置开发服务器，这些扩展可以有效提升开发体验和应用性能。


余下文章内容请点击跳转至 个人博客页面 或者 扫码关注或者微信搜一搜：`编程智域 前端至全栈交流与成长`，阅读完整的文章：
[Nuxt.js 应用中的 vite：extendConfig 事件钩子 \| cmdragon's Blog](https://github.com)


## 往期文章归档：


* [Nuxt.js 应用中的 schema：written 事件钩子详解 \| cmdragon's Blog](https://github.com)
* [Nuxt.js 应用中的 schema：beforeWrite 事件钩子详解 \| cmdragon's Blog](https://github.com)
* [Nuxt.js 应用中的 schema：resolved 事件钩子详解 \| cmdragon's Blog](https://github.com)
* [Nuxt.js 应用中的 vite：extendConfig 事件钩子详解 \| cmdragon's Blog](https://github.com)
* [Nuxt.js 应用中的 vite：extend 事件钩子详解 \| cmdragon's Blog](https://github.com)
* [Nuxt.js 应用中的 schema：extend事件钩子详解 \| cmdragon's Blog](https://github.com)
* [Nuxt.js 应用中的 listen 事件钩子详解 \| cmdragon's Blog](https://github.com)
* [Nuxt.js 应用中的 prepare：types 事件钩子详解 \| cmdragon's Blog](https://github.com)
* [Nuxt.js 应用中的 build：error 事件钩子详解 \| cmdragon's Blog](https://github.com)
* [Nuxt.js 应用中的 prerender：routes 事件钩子详解 \| cmdragon's Blog](https://github.com)
* [Nuxt.js 应用中的 nitro：build：public\-assets 事件钩子详解 \| cmdragon's Blog](https://github.com):[FlowerCloud机场](https://yunbeijia.com)
* [Nuxt.js 应用中的 nitro：build：before 事件钩子详解 \| cmdragon's Blog](https://github.com)
* [Nuxt.js 应用中的 nitro：init 事件钩子详解 \| cmdragon's Blog](https://github.com)
* [Nuxt.js 应用中的 nitro：config 事件钩子详解 \| cmdragon's Blog](https://github.com)
* [Nuxt.js 应用中的 components：extend 事件钩子详解 \| cmdragon's Blog](https://github.com)
* [Nuxt.js 应用中的 components：dirs 事件钩子详解 \| cmdragon's Blog](https://github.com)
* [Nuxt.js 应用中的 imports：dirs 事件钩子详解 \| cmdragon's Blog](https://github.com)
* [Nuxt.js 应用中的 imports：context 事件钩子详解 \| cmdragon's Blog](https://github.com)
* [Nuxt.js 应用中的 imports：extend 事件钩子详解 \| cmdragon's Blog](https://github.com)
* [Nuxt.js 应用中的 imports：sources 事件钩子详解 \| cmdragon's Blog](https://github.com)
* [Nuxt.js 应用中的 server：devHandler 事件钩子详解 \| cmdragon's Blog](https://github.com)
* [Nuxt.js 应用中的 pages：extend 事件钩子详解 \| cmdragon's Blog](https://github.com)
* [Nuxt.js 应用中的 builder：watch 事件钩子详解 \| cmdragon's Blog](https://github.com)
* [Nuxt.js 应用中的 builder：generateApp 事件钩子详解 \| cmdragon's Blog](https://github.com)
* [Nuxt.js 应用中的 build：manifest 事件钩子详解 \| cmdragon's Blog](https://github.com)
* [Nuxt.js 应用中的 build：done 事件钩子详解 \| cmdragon's Blog](https://github.com)
* [Nuxt.js 应用中的 build：before 事件钩子详解 \| cmdragon's Blog](https://github.com)
* [Nuxt.js 应用中的 app：templatesGenerated 事件钩子详解 \| cmdragon's Blog](https://github.com)
* [Nuxt.js 应用中的 app：templates 事件钩子详解 \| cmdragon's Blog](https://github.com)
* [Nuxt.js 应用中的 app：resolve 事件钩子详解 \| cmdragon's Blog](https://github.com)
* [Nuxt.js 应用中的 modules：done 事件钩子详解 \| cmdragon's Blog](https://github.com)
* 


  * [文章大纲](#%E6%96%87%E7%AB%A0%E5%A4%A7%E7%BA%B2)
* [1\. 定义与作用](#tid-4YEjRH)
* [2\. 调用时机](#tid-nZeYZi)
* [3\. 参数说明](#tid-XjJn7P)
* [4\. 示例用法](#tid-SnMxAe)
* [在 plugins/viteExtendConfig.js 文件中的实现](#%E5%9C%A8-pluginsviteextendconfigjs-%E6%96%87%E4%BB%B6%E4%B8%AD%E7%9A%84%E5%AE%9E%E7%8E%B0)
* [5\. 应用场景](#tid-eGAZDA)
* [5\.1 添加 Vite 插件](#tid-TZsXFj)
* [5\.2 调整构建配置](#tid-wGr5wc)
* [5\.3 自定义开发服务器设置](#tid-CQnytZ)
* [5\.4 根据环境动态调整配置](#tid-TWzknd)
* [6\. 注意事项](#tid-3wdsSj)
* [7\. 总结](#tid-8sZsbm)
* [往期文章归档：](#%E5%BE%80%E6%9C%9F%E6%96%87%E7%AB%A0%E5%BD%92%E6%A1%A3)

   \_\_EOF\_\_

       - **本文作者：** [Amd794](https://github.com)
 - **本文链接：** [https://github.com/Amd794/p/18549395](https://github.com)
 - **关于博主：** 评论和私信会在第一时间回复。或者[直接私信](https://github.com)我。
 - **版权声明：** 本博客所有文章除特别声明外，均采用 [BY\-NC\-SA](https://github.com "BY-NC-SA") 许可协议。转载请注明出处！
 - **声援博主：** 如果您觉得文章对您有帮助，可以点击文章右下角**【[推荐](javascript:void(0);)】**一下。
     
