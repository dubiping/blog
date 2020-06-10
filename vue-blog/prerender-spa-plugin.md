## 安装使用
1、安装插件
```javascript
  yarn add prerender-spa-plugin --dev
  // 依赖包
  yarn add puppeteer --dev
```
2、vue.config.js配置
```javascript
const PrerenderSPAPlugin = require("prerender-spa-plugin");
const Renderer = PrerenderSPAPlugin.PuppeteerRenderer;

module.exports = {
  configureWebpack: config => {
    const opt = {};
    if (process.env.NODE_ENV === "production") {
      // 为生产环境修改配置...
      opt.mode = "production";
      opt.plugins = [
        new PrerenderSPAPlugin({
          // 生成文件的路径，也可以与webpakc打包的一致。
          // 下面这句话非常重要！！！
          // 这个目录只能有一级，如果目录层次大于一级，在生成的时候不会有任何错误提示，在预渲染的时候只会卡着不动。
          staticDir: path.join(__dirname, "dist"),
          // 对应自己的路由文件，比如a有参数，就需要写成 /a/param1。
          routes: ["/home", "/problem", "/about"],
          // 这个很重要，如果没有配置这段，也不会进行预编译
          renderer: new Renderer({
            inject: {
              // foo: "bar"
            },
            headless: false,
            // 在 main.js 中 document.dispatchEvent(new Event('render-event'))，两者的事件名称要对应上。
            renderAfterDocumentEvent: "render-event"
            // executablePath: ""
          })
        })
      ];
    } else {
      // 为开发环境修改配置...
      opt.mode = "development";
    }
    // 这里使用Object.assign(config, {resolve: {}}) 会报错
    return {
      ...opt,
      resolve: {
        alias: {
          "@": path.resolve(__dirname, "./src"),
          "@c": path.resolve(__dirname, "./src/components")
        }
      }
    };
  },
}
```
3、在main.ts配置
```javascript
new Vue({
  router,
  store,
  render: h => h(App),
  mounted() {
    document.dispatchEvent(new Event('render-event'))
  }
}).$mount("#app");
```
## 报错
```javascript
[prerender-spa-plugin] Unable to prerender all routes!
```
> 这个问题莫名其妙，刚开始一直报错，后面莫名其妙好了，诶。。。。
* 替换了\node_modules\puppeteer\.local-chromium\ 下的chromium.app
* 清除了浏览器缓存, 重新打开了vscode
[chromium下载地址](https://npm.taobao.org/mirrors/chromium-browser-snapshots)