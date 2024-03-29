## 第 1 章 JavaScript 简介

#### 1.1 JavaScript 历史回顾

- 诞生背景：1995年，绝大多数的因特网用户都使用速度仅为 28.8kbit/s 的“猫”（调制解调器）上网，但网页的大小和复杂性却不断增加。为了完成简单的表单验证而频繁的与服务器进行交换数据只会加重用户的负担。
- 场景描述：当用户填写完一个表单，单击“提交”按钮，然后等待 30 秒钟，最终服务器返回消息说有一个必填字段没有填好......
- 就职于 Netscape 公司的布兰登·艾奇（Brendan Eich），为计划于1995年2月发布的 Netscape Navigator 2 开发一种名为 LiveScript 的脚本语言。发布前夕，Netscape 公司为了搭上媒体热炒 Java 的顺风车，临时把 LiveScript 改名为 JavaScript。
- 1997年，以 JavaScript 1.1 为蓝本的的建议被提交给欧洲计算机制造商协会（ECMA，European Computer Manufacturers Association）。该协会指定39号技术委员会（负责“标准化一种通用、跨平台、供应商中立的脚本语言的语法和语义”），他们经过数月的努力完成了 ECMA-262————定义一种名为 ECMAScript（发音为 “ek-ma-script”）的新脚本语言的标准。
- 第二年，ISO/IEC（国际标准化组织和国际电工委员会）也采用了 ECMAScript 作为标准。自此以后，浏览器开发商就开始致力于将 ECMAScript 作为各自 JavaScript 实现的基础。

### 1.2 JavaScript 实现

> 虽然 JavaScript 和 ECMAScript 通常被人们用来表达相同的含义，但 JavaScript 的含义却比 ECMA-262 中规定的要多得多。一个完整的 JavaScript 实现由一下三个不同的部分组成。
- 核心（ECMAScript）
- 文档对象模型（DOM，Document Object Model）
    *是 HTML 和 XML 的应用程序接口（API）。DOM 将把整个页面规划成由节点层级构成的文档。HTML或XML页面中的每个组成部分都是某种类型的节点，这些节点又包含着不同类型的数据。*
- 浏览器对象模型（BOM，Browser Object Model）
    *IE 3.0 和 Netscape Navigator 3.0 提供了一种特性 - BOM（浏览器对象模型），可以对浏览器窗口进行访问和操作。使用 BOM，开发者可以移动窗口、改变状态栏中的文本以及执行其他与页面内容不直接相关的操作。*

### 小结
> JavaScript 是一种专为与网页交互而设计的脚本语言，由下列三个不同的部分组成。
- ECMAScript，由 ECMA-262 定义，提供核心语言功能；
- 文档对象模型（DOM）,提供访问和操作网页内容的方法和接口；
- 浏览器对象模型（BOM），提供与浏览器交互的方法和接口。  
