# ReactDemo
使用技术：React+Redux+Next+Antd

根据胖哥教程制作react博客项目，对重点进行笔记。胖哥视频教程地址 http://bilibili.com/video/BV1CJ411377B


### 1.利用脚手架工具创建项目
使用Next.js脚手架create-next-app生成项目。

create-next-app的安装

```
$ npm install -g create-next-app
```

生成项目
```
$ npx create-next-app blog
```
启动命令

```
cd blog
yarn dev
```

启动地址：http://localhost:3000/

### 2.外部CSS导入设置
Next默认是不支持外部CSS导入，需要进行配置
```
yarn add @zeit/next-css
```
之后在blog根目录下，新建一个next.config.js，添加如下代码
```
const withCss = require('@zeit/next-css')

if(typeof require !== 'undefined'){
    require.extensions['.css']=file=>{}
}

module.exports = withCss({})
```
### 3.安装ant design
选用阿里的Ant Desgin来作为UI交互库，支持国际化语言设置
```
yarn add antd 
```
胖哥的视频里对antd的按需加载进行了一系列设置，ant4.0以后的版本已经默认按需加载，正常不需要再设置，但是我在未配置的情况下F12的控制台出现了以下警告，还是参照了胖哥的配置
```
You are using a whole package of antd, please use https://www.npmjs.com/package/babel-plugin-import to reduce app bundle size.
```
由于前端框架和插件的更新非常快速，在配置环节经常会遇到问题，最好的方法是按视频中使用的版本进行下载。如果下载最新版本，需要特别小心版本之间的差异带来的配置问题。

**另外ANTD新版本发生了变化，在之后的视频里对Icon的引入需要变化，具体使用参考文档**

安装babel-plugin-import
```
yarn add babel-plugin-import
```
在项目根目录建立.babelrc文件，写入如下代码
```
{
    "presets":["next/babel"],  //Next.js的总配置文件，相当于继承了它本身的所有配置
    "plugins":[     //增加新的插件，这个插件就是让antd可以按需引入，包括CSS
        [
            "import",
            {
                "libraryName":"antd"
            }
        ]
    ]
}
```
在pages目录下，有一个_app.js文件，添加
```
import 'antd/dist/antd.css'
```
实现全局引入。

胖哥视频里的初始项目是不存在_app.js文件的，需要新建，我的项目里已存在，只需要添加以上一条命令即可。

**注意**我的项目里不允许在组件里导入css文件，需要在_app.js里全局导入。
如下
```
import '../styles/globals.css'
import 'antd/dist/antd.css'
import '../styles/pages/comm.css'
import '../styles/components/header.css'
function MyApp({ Component, pageProps }) {
  return <Component {...pageProps} />
}

export default MyApp
```
