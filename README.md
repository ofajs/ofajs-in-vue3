# ofajs-in-vue3

Using ofa.js in a Vue project.

[中文教程](./README-CN.md)

## Main Steps

### 1. Include ofa.js in index.html

[View File](./public/index.html)

```html
  <head>
    ...
    <title><%= htmlWebpackPlugin.options.title %></title>
    <script src="https://cdn.jsdelivr.net/gh/kirakiray/ofa.js/dist/ofa.min.js"></script>
    <style>*:not(:defined){display:none;}</style>
  </head>
  ...
```

### 2. Exclude Custom Component Tags from the Whitelist

[View File](./vue.config.js)

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

### 3. Use Components in Vue Files

Components developed based on ofa.js must be published (or hosted on a local static server). If there are errors when using components, you can use `eslint-disable-next-line` to resolve them.

[View File](./src/components/HelloWorld.vue)

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