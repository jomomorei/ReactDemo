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
**胖哥的视频里对antd的按需加载进行了一系列设置，ant4.0以后的版本已经默认按需加载，不需要额外配置，需要注意下。配置后反而会出现问题**

**在之后的视频里对Icon的引入，新版本也发生了变化，需要注意，具体使用参考文档**
