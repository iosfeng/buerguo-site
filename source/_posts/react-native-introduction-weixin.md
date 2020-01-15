---
title: react-native入门实战小结
date: 2019-11-02
categories: App
---

## 唠叨两句

在公司提效的大背景下，今年6月初，部门的国际化新项目我们通过多方面的对比，技术选型采用react-native为最终的方案，之所以没有采用目前比较火的Flutter。其中的原因我会在以下小节有个简要的说明。项目第一版已接近尾声，到了最后的细节调整阶段。正好借此机会记录下这段时间入坑RN的一些心得体会。
<!-- more -->
## 心得体会

入坑3月有余，幸而有我们前端同学的加持，使我们在第一次使用新技术栈的同时开发如此大规模的项目，得以保证开发进度的顺利进行。

在整个项目中使用到的语言包括TypeScript/JavaScript/Objective-C/Java，项目管理、打包、构建工具包括npm/cocoapods/gradle/webpack，至于开发工具方面我更喜欢WebStorm+AndroidStudio+AppCode组合，可以保证开发体验高度一致，开发速度会更快，当然Xcode必不可少。而前端同学更喜欢VSCode，都是可以的。

react-native来实现项目中所有的业务逻辑，开发速度自然快了许多，使我这个同时开发过iOS和Android项目的人深深体会到了跨平台的好处，再也不会出现同样的功能在iOS侧和Android侧实现两遍而且实现思路还不一样的尴尬场面，在维护时的痛苦不言而喻。

由于项目中会用到前端及移动端等需要不同路线的、独立的技术栈，有幸我们小组同时具有各自领域擅长的同学，得以在整个开发过程中都能hold住各个模块，为了让前端同学在不需要了解移动端很多知识的前提下可以正常、稳定的运行、调试项目，我们在项目初期编写了大量的npm脚本命令来实现一键自动化功能，比如启动react-native服务，运行、构建、打包、安装iOS和Android App等命令。使前端同学可以快速地专注于开发、调试。打包提测速度也有很大的改善。

## 技术选型

都9102年了，为什么还选react-native？当时5、6月份做选型的时候，也做了很多方面的对比。当然，最后对比主要还是关注在react-native和Flutter的选择上。由于项目大，人员又比较少，所以想通过跨平台的技术来提效是一个大前提，很多能达到跨平台效果的框架我们都做了整体的调研，比如ionic、weex、hybrid等等，不过为了追求原生般的用户体验，这些方案都被pass掉了。至于react-native和Flutter的选择，前端之巅公众号在8月中旬发布这篇文章[《为什么Flutter还不是最成熟的跨端框架》](https://mp.weixin.qq.com/s/DlzY6qxFC8UnmvnJJtMXTQ)里面的观点很入我的法眼。

重点关注以下几点：

1. 开发语言：JS or Dart？ 由于本次项目比较急，排期又是倒排，为了保证项目的进度，选择团队中熟悉的技术语言JS会更可靠。
2. 成熟度：很明显react-native的生态要比Flutter要好得多、成熟得多，单从issue来看，框架本身react-native也要稳定很多，而且第三方库也要多很多。
3. 热更新支持：目前Flutter官方还是不支持热更新，而且也没有相关的计划表。
4. WEB平台支持：Flutter在5月初的1.5版本刚支持到WEB平台，还不够成熟，无法在生产环境中使用。

以上几点是保证项目能顺利上线的优先考虑点，至于Flutter的优势、趋势及未来发展倒不是本次选型的关键和重点。

## 环境搭建

[官方的环境搭建文档](https://facebook.github.io/react-native/docs/getting-started)已经有详细的说明，这里不再重复。大家可以看下我本地的环境配置版本，目前整个项目运行稳定，可以借鉴。

```sh
$ react-native info
info 
  React Native Environment Info:
    System:
      OS: macOS 10.14.6
      CPU: (8) x64 Intel(R) Core(TM) i7-7700HQ CPU @ 2.80GHz
      Memory: 259.21 MB / 16.00 GB
      Shell: 3.2.57 - /bin/bash
    Binaries:
      Node: 8.11.1 - /usr/local/bin/node
      Yarn: 1.12.3 - /usr/local/bin/yarn
      npm: 6.10.3 - /usr/local/bin/npm
      Watchman: 4.9.0 - /usr/local/bin/watchman
    SDKs:
      iOS SDK:
        Platforms: iOS 12.4, macOS 10.14, tvOS 12.4, watchOS 5.3
      Android SDK:
        API Levels: 22, 23, 24, 25, 26, 27, 28
        Build Tools: 19.1.0, 20.0.0, 21.1.2, 22.0.1, 23.0.1, 23.0.2, 23.0.3, 24.0.0, 24.0.1, 24.0.2, 24.0.3, 25.0.0, 25.0.1, 25.0.2, 25.0.3, 26.0.0, 26.0.1, 26.0.2, 26.0.3, 27.0.0, 27.0.1, 27.0.2, 27.0.3, 28.0.0, 28.0.0, 28.0.2, 28.0.3
        System Images: android-28 | Google Play Intel x86 Atom
    IDEs:
      Android Studio: 3.4 AI-183.6156.11.34.5692245
      Xcode: 10.3/10G8 - /usr/bin/xcodebuild
    npmPackages:
      react: 16.8.3 => 16.8.3 
      react-native: 0.59.10 => 0.59.10 
    npmGlobalPackages:
      react-native-cli: 2.0.1
      react-native-git-upgrade: 0.2.7
```

值得一说的是，react-native库使用的是0.59.10，0.59的最后一个版本，相信0.60版本后Android侧引入的新JS引擎，对App的性能有更多的提升。我们后续在适当的机会也会做相应的升级。还有，每个开发的cocoapods包管理工具最好也要保持一致，目前我们统一使用`1.7.2`版本，否则，每次`pod install`都会引起Podfile.lock文件的变化，容易代码冲突。

另外，本项目采用的开发语言为TypeScript，并没有采用JavaScript。TypeScript中增加了静态类型、类、模块、接口和类型注解等等，对我们移动开发者常用的面向对象语言OC/Java都很友好，上手更加容易、更易理解，而且其面向对象编程语言的结构保持了代码的清洁、一致和简单的调试，在应对大型开发项目时，使用TypeScript更加合适。

## 常用组件&第三方库

常用的官方组件我这里不一一介绍，大家可以直接看[官方文档](https://facebook.github.io/react-native/docs/activityindicator)，官方文档永远是最新最可靠的。

以下所列是我们项目中目前使用到的第三方库，能帮助我们更好、更快地开发和构建项目。有兴趣的同学可以点开了解一下，相信有很多库都是大多数项目中离不开的，比如导航库react-navigation、状态管理库mobx/redux等等。

- [react-navigation](https://reactnavigation.org/zh-Hans/)
- [mobx](https://github.com/mobxjs/mobx)
- [react-native-localize](https://github.com/react-native-community/react-native-localize)
- [react-native-default-preference](https://github.com/kevinresol/react-native-default-preference)
- [react-native-deep-link](https://github.com/Starotitorov/react-native-deep-link)
- [react-native-push-notification](https://github.com/zo0r/react-native-push-notification)
- [react-native-linear-gradient](https://github.com/react-native-community/react-native-linear-gradient)
- [react-native-cameraroll](https://github.com/react-native-community/react-native-cameraroll)
- [react-native-easy-grid](https://github.com/GeekyAnts/react-native-easy-grid)
- [react-native-device-info](https://github.com/react-native-community/react-native-device-info)
- [react-native-iphone-x-helper](https://github.com/ptelad/react-native-iphone-x-helper)
- [react-native-webview](https://github.com/react-native-community/react-native-webview)
- [react-native-cookies](https://github.com/joeferraro/react-native-cookies)  这个库不好用，自己实现
- [react-native-fs](https://github.com/itinance/react-native-fs)
- [react-native-qrcode-svg](https://github.com/awesomejerry/react-native-qrcode-svg)
- [react-native-splash-screen](https://github.com/crazycodeboy/react-native-splash-screen)
- [react-native-keyboard-aware-scroll-view](https://github.com/APSL/react-native-keyboard-aware-scroll-view)
- [react-native-image-picker](https://github.com/react-native-community/react-native-image-picker)
- [react-native-root-toast](https://github.com/magicismight/react-native-root-toast)
- [react-native-web](https://github.com/necolas/react-native-web)
- [react-native-view-shot](https://github.com/gre/react-native-view-shot)

## 代码规范

这点比较有意思的是，我们前端同学以前更多了解的是JS，而我们这次选用的开发语言是TS，其实还是有很多不同的。比如最简单的类型定义，习惯了OC/Java的同学自然是对JS那种无类型的语言深恶痛绝，而JS那种无类型的写法也不是TS的最佳实践，所以坦白来讲，我们小组基本没有什么经验来规范TS如何写才是最优雅的。

这次选用TS的一个核心诉求也是为了其静态类型化功能，能帮助我们编写更健壮的代码、更好的协作。既然自己没有经验，不如拿来主义，以下两个是比较官方的两例。觉得不错，可以先试用之。

- [Google TypeScript Style](https://github.com/google/gts)
- [Airbnb React/JSX Style Guide](https://github.com/airbnb/javascript/tree/master/react)

## react-native项目中需要掌握的技术栈

以下的知识点是我个人从移动端开发到react-native开发，入门时学过和参考过的一些文档和资料。供大家入坑参考。

- iOS/Android - Objective-C/Swift/Java/Kotlin
    - 原生开发基础，涉及太多知识，这里暂不列举

- JS/TS - ES2015/ES6
    - [ECMAScript6入门教程](http://es6.ruanyifeng.com/#docs/object)
    - [JavaScript教程](http://www.runoob.com/js/js-tutorial.html)
    - [React/React Native的ES5 ES6写法对照表](http://bbs.reactnative.cn/topic/15/react-react-native-的es5-es6写法对照表)
    - [ES6的十大特性](http://geek.csdn.net/news/detail/239352)
    - [TS官网](https://www.typescriptlang.org/)    

- React - JavaScript/JSX语法/HTML/CSS
    - [React入门实例教程](http://www.ruanyifeng.com/blog/2015/03/react.html)
    - [React官方教程](https://reactjs.org/)
    - [React与webpack](https://typescript.bootcss.com/tutorials/react-&-webpack.html)

- ReactNative - React
    - [ReactNative官方文档](http://facebook.github.io/react-native/docs/getting-started.html)
    - [ReactNative中文文档](https://reactnative.cn)
    - [react-native-guide](https://github.com/reactnativecn/react-native-guide)

- 【进阶】MobX/Redux - 状态管理、组件间的通信
    - [mobx](https://github.com/mobxjs/mobx)
    - [Redux入门教程](http://www.ruanyifeng.com/blog/2016/09/redux_tutorial_part_one_basic_usages.html)
    - [Redux中文教程](http://www.redux.org.cn/docs/basics/index.html)

- Node/NPM - 项目、包管理
    - [暂无]()

- 热更新
    - [CodePush](http://microsoft.github.io/code-push/index.html#getting_started)

- 其他
    - [React Native专题文章](http://www.hangge.com/blog/cache/category_76_1.html)
    - [React Native - Text组件使用详解（样式、属性、方法）](http://www.hangge.com/blog/cache/detail_1486.html)
    - [React Native布局详细指南](http://blog.csdn.net/quanqinyang/article/details/52215641)

## 小结

从目前来看，react-native的成熟、稳定完全可以支撑起一个商业型的项目，开发期间虽然经历了各种各样的坑和奇怪的问题，但是在官方文档、stackoverflow以及对具体问题的分析，最后都能得到可行的解决方案。借用公众号那句话，目前阶段，react-native才是业内最成熟的跨端框架。欢迎大家一起入坑学习~