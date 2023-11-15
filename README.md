<div align="center">
 
  <a href="https://github.com/webpack/webpack">
    <img width="200" height="200"
      src="https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/b148304186f0459db30bb54f39de44ab~tplv-k3u1fbpfcp-zoom-1.image">
  </a>
  <h1>Auto Publish Plugin</h1>
  <p>Webpack plugin that supports automatic publishing of NPM packages.</p>
</div>

<h2 align="center">安装</h2>

```bash
  npm i --save-dev @comkit/auto-publish-plugin
```

```bash
  yarn add --dev @comkit/auto-publish-plugin
```

<h2 align="center">使用</h2>

`auto-publish-plugin`支持自动发布 npm 包。

**webpack.config.js**

```js
const path = require('path');
const AutoPublishWebpackPlugin = require('auto-publish-plugin').default;

module.exports = {
  entry: './index.js',
  plugins: [
    new AutoPublishWebpackPlugin({
      name: 'vue',
      output: path.resolve(__dirname, './dist'),
      registry: 'http://registry.npmjs.org/',
    }),
  ],
  output: {
    filename: 'name.js',
    path: path.resolve(__dirname, 'dist'),
  },
};
```

<h2 align="center">参数</h2>

|   Name   |  Type  |           Default            | Description                    |
| :------: | :----: | :--------------------------: | :----------------------------- |
|   name   | string |          `required`          | 生成的`package.json`中的包名称 |
| rootDir  | string |          `required`          | 当前项目跟路径                 |
|  output  | string |          `required`          | 打包后生成内容的文件夹路径     |
| registry | string | `http://registry.npmjs.org/` | `npm`源                        |

> prerelease 下推送会自动在根目录提交并推送文件变成，并且生成对应 alpha 版本 Tag 同时自动提交。

<h2 align="center">环境变量</h2>

`auto-publish-plugin`还支持通过环境变量注入的方式更新包版本。

- `__version__plugin__mode=patch`
- `__version__plugin__mode=minor`
- `__version__plugin__mode=major`
- `__version__plugin__mode=auto`

当传递`patch`、`minor`、`major`时，会根据对应的值直接进行版本号修改跳过询问步骤。

当传递`auto`时，会进入版本号询问环节，支持上述三种定义以及输入自定义版本号。

默认不传递`__version__plugin__mode`时，开启询问模式。
