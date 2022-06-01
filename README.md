# uview模版项目

本项目基于uniapp-cli方式运行， `uview: 1.8.6`

```shell
npm config set registry https://registry.npm.taobao.org
npm i 
npm run server
```

## pnpm使用

pnpm可能会造成打包无法使用的情况，所以还是老老实实用npm吧

如果出现以下代码
```text
├─┬ @dcloudio/uni-automator
│ ├── ✕ missing peer adbkit@^2.11.1
│ ├── ✕ missing peer jimp@^0.10.1
│ ├── ✕ missing peer node-simctl@^6.1.0
│ └── ✕ missing peer puppeteer@^3.0.1
├─┬ @dcloudio/vue-cli-plugin-uni
│ └─┬ copy-webpack-plugin
│   └── ✕ missing peer webpack@"^4.0.0 || ^5.0.0"
├─┬ sass-loader
│ └── ✕ missing peer webpack@"^4.36.0 || ^5.0.0"
├─┬ @dcloudio/uni-quickapp-native
│ └─┬ @hap-toolkit/dsl-vue
│   ├─┬ css-loader
│   │ └── ✕ missing peer webpack@^4.0.0
│   ├─┬ mini-css-extract-plugin
│   │ └── ✕ missing peer webpack@^4.4.0
│   ├─┬ url-loader
│   │ └── ✕ missing peer webpack@^4.0.0
│   └─┬ vue-loader
│     └── ✕ missing peer webpack@"^3.0.0 || ^4.1.0 || ^5.0.0-0"
```

在`package.json`中加入以下代码, 官方文档 https://pnpm.io/zh/package_json#pnpmpeerdependencyrulesallowedversions
```json
"pnpm": {
    "peerDependencyRules": {
      "ignoreMissing": ["adbkit","jimp","node-simctl","puppeteer","webpack"],
    }
  }
```

出现以下代码
```text
└─┬ @vue/cli-service
  └─┬ vue-loader
    └── ✕ unmet peer vue@^3.2.13: found 2.6.14
```

在`package.json`中加入以下代码，官方文档 https://pnpm.io/zh/package_json#pnpmneverbuiltdependencies
```json
"pnpm": {
    "peerDependencyRules": {
      "allowedVersions": {
        "vue": "2.6.14"
      }
    }
  }
```


## hbuliderx中运行

1. 拖入hbuliderx中后，需要右键选择"重新识别项目类型"
2. 安装依赖`npm install --registry=https://registry.npm.taobao.org`,必须使用`npm`
4. 测试发现`yarn` 和 `pnpm`可能会有编译问题，详见[https://juejin.cn/post/7077918263954374670#heading-7]()

## 新特性

- [x] rsa加解密
- [x] 增加socket
- [x] 使用uni-simple-router https://github.com/SilurianYang/uni-simple-router
- [ ] 使用luch-request https://www.quanzhan.co/luch-request/
- [x] 热更模块集成 参考https://github.com/zhouwei1994/uni-app-demo/tree/master/uni_modules/zhouWei-APPUpdate
- [ ] 微信小程序分享模块/公众号分享模块 https://github.com/zhouwei1994/uni-app-demo/tree/master/uni_modules/zhouWei-APPshare
- [ ] 增加默认页面【登录，注册，忘记密码，绑定手机号，协议页面，商品海报生成，推广海报生成】
- [ ] 续期jwt，增加request的重试机制，和404等问题转发到指定页面
- [ ] 导航栏到配置，参考 uniappDemo/#/pages/demo/navBarMemo/index
- [ ] 启动界面 manifest.json -> 'App启动界面配置' https://ask.dcloud.net.cn/article/37474
- [ ] 原生协议 https://ask.dcloud.net.cn/article/36937

# 不错的插件

- 模版 https://ext.dcloud.net.cn/plugin?id=2009
- 炫酷的样式、炫酷的动画效果 https://ext.dcloud.net.cn/plugin?id=3685
- mp-html 富文本组件【全端支持，可编辑】 https://ext.dcloud.net.cn/plugin?id=805
- 秋云 ucharts echarts 高性能跨全端图表组件 https://ext.dcloud.net.cn/plugin?id=271
- luch-request https://ext.dcloud.net.cn/plugin?id=392
- 海报画板 https://ext.dcloud.net.cn/plugin?id=2389
- 路由、拦截、最优雅解决方案 uni-simple-router https://ext.dcloud.net.cn/plugin?id=578
- 下拉式筛选菜单 https://ext.dcloud.net.cn/plugin?id=1078
- tree树组件 https://ext.dcloud.net.cn/plugin?id=1000
- lucky-canvas【大转盘｜九宫格｜老虎机】抽奖插件 https://ext.dcloud.net.cn/plugin?id=3499
- APP版本更新、强制更新、静默更新、下载进度（wgt更新） https://ext.dcloud.net.cn/plugin?id=1643
- app版本升级原生弹框和进度提示(包含wgt升级)  https://ext.dcloud.net.cn/plugin?id=1371
- 升级中心 uni-upgrade-center - App https://ext.dcloud.net.cn/plugin?id=4542
- 前端铺子（小程序+H5+公众号+App）多种移动端开发实用模版、功能、样式 https://ext.dcloud.net.cn/plugin?id=5013
- 拖动排序列表 HM-dragSorts https://ext.dcloud.net.cn/plugin?id=1372
- 开箱即用的公共搜索组件（历史记录，app语音输入，搜索推荐） https://ext.dcloud.net.cn/plugin?id=512
- 百度图表 echarts https://ext.dcloud.net.cn/plugin?id=4899
- 蚂蚁图表 antv F2 https://ext.dcloud.net.cn/plugin?id=4613

## eslint

git上传的时候格式化

```json
  "husky": {
"hooks": {
"pre-commit": "lint-staged"
}
},
"lint-staged": {
"src/**/*.{js,vue}": [
"eslint --fix",
"git add"
]
}

```

整个文件范围内禁止规则出现警告, 将/* eslint-disable */放置于文件最顶部

```javascript
/* eslint-disable */
alert('foo');
```

在文件中临时禁止规则出现警告, 将需要忽略的代码块用注释包裹起来

```javascript
/* eslint-disable */
alert('foo');
/* eslint-enable */
```

对指定规则的启用或者禁用警告, 将需要忽略的代码块用注释包裹起来

```javascript
/* eslint-disable no-alert, no-console */
alert('foo');
console.log('bar');
/* eslint-enable no-alert, no-console */
```

对指定行禁用规则警告, 此方法，有两种形式，参见下方。

```javascript
alert('foo'); // eslint-disable-line

// eslint-disable-next-line
alert('foo');
```

在指定行上禁用指定的某个规则

```javascript
alert('foo'); // eslint-disable-line no-alert

// eslint-disable-next-line no-alert
alert('foo');
```

在某个特定的行上禁用多个规则

```javascript
alert('foo'); // eslint-disable-line no-alert, quotes, semi

// eslint-disable-next-line no-alert, quotes, semi
alert('foo');

```