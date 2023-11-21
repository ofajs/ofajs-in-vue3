# ofajs-in-vue3

在 Vue 项目中使用 ofa.js.

https://github.com/kirakiray/ofa.js/assets/5945154/c6c200bb-6d0b-4ab7-ba0a-ed54d8130877

## 主要步骤

### 1. 在 index.html 中引入 ofa.js

[查看文件](./public/index.html)

```html
  <head>
    ...
    <title><%= htmlWebpackPlugin.options.title %></title>
    <script src="https://cdn.jsdelivr.net/gh/kirakiray/ofa.js/dist/ofa.min.js"></script>
    <style>*:not(:defined){display:none;}</style>
  </head>
  ...
```

### 2. 将自定义组件的标签从名单上去除

[查看文件](./vue.config.js)

```javascript
module.exports = defineConfig({
  chainWebpack: (config) => {
    config.module
      .rule("vue")
      .use("vue-loader")
      .tap((options) => ({
        ...options,
        compilerOptions: {
          isCustomElement: (tag) => {
            // use the l-m and punch-logo component
            return ["l-m", "punch-logo"].includes(tag);
          },
        },
      }));
  },
});
```

### 3. 在 vue 文件中使用组件

基于 ofa.js 开发的组件必须已发布（或者放到本地静态服务器）；如果使用组件有报错，可使用 `eslint-disable-next-line` 解决。

[查看文件](./src/components/HelloWorld.vue)

```html
<l-m src="https://ofajs.github.io/ofa-v4-docs/docs/publics/comps/punch-logo.html"></l-m>

<punch-logo>
    <img
    src="https://ofajs.github.io/ofa-v4-docs/docs/publics/logo.svg"
    logo
    height="90"
    />
    <h2>{{ msg }}</h2>
    <!-- eslint-disable-next-line -->
    <p slot="fly">npm</p>
    <!-- eslint-disable-next-line -->
    <p slot="fly">webpack</p>
    <!-- eslint-disable-next-line -->
    <p slot="fly">nodejs</p>
</punch-logo>
```
