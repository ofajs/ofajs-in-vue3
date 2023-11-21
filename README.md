# ofajs-in-vue3

在 Vue 项目中使用 ofa.js.

## 主要步骤

### 1. 在 index.html 中引入 ofa.js

[查看文件](./public/index.html)

```html
  <head>
    ...
    <title><%= htmlWebpackPlugin.options.title %></title>
    <script src="https://cdn.jsdelivr.net/gh/kirakiray/ofa.js/dist/ofa.min.js"></script>
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

### 3. 在页面内使用发布好的组件

[查看文件](./src/components/HelloWorld.vue)

```html
<l-m
    src="https://ofajs.github.io/ofa-v4-docs/docs/publics/comps/punch-logo.html"
></l-m>

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
