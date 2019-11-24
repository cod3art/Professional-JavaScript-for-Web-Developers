## 在 HTML 中使用 JavaScript

#### 2.1 \<scirpt> 元素
> 向 HTML 页面中插入 JavaScript 的主要方法，就是使用\<script>元素。这个元素由 Netscape 创造，并在 Netscape Navigator 2 中首先实现。后来，这个元素被加入到正式的 HTML 规范中。HTML 4.01 为\<script>定义了下列6个属性。
- async：可选。表示应该立即下载脚本，但不应妨碍页面中的其他操作，比如下载其他资源或等待加载其他脚本。只对外部脚本文件有效。
- charset：可选。表示通过 src 属性指定的代码字符集。
- defer：可选。表示脚本可以延迟到文档完全被解析和现实之后再执行。只对外部脚本文件有效。
- language：已废弃。原来用于表示编写代码使用的脚本语言。
- src：可选。表示包含要执行代码的外部文件。
- type：可选。可以看成 language 的替代属性；表示编写代码使用的脚本语言的内容类型（也称为 MIME 类型）。虽然 text/javascript 和 text/ecmascript 都已经不被推荐使用，但人们一直以来使用的都还是 text/javascript。不过，这个属性并不是必需的，如果没有指定这个属性，则其默认值仍为 text/javascript。
  
###### 使用\<script>元素的两种方式
> 直接在页面中嵌入 JavaScript 代码和包含外部 JavaScript 文件。
- 在使用\<script>元素嵌入 JavaScript 代码时，只须为\<script>指定type属性。然后像下面这样把 JavaScript 代码直接放在元素内部即可。
```javascript
    <script type="text/javascript">
        function sayHi() {
            alert("Hi!");
        }
    </script>
```
> 包含在\<script>元素内部的代码将被从上至下一次解释。拿上面的例子来说，解释器会解释一个函数的定义，然后将该定义保存在自己的环境当中。在解释器对\<script>元素内部的所有代码求值完毕以前，页面中的其余内容都不会被浏览器加载或显示。
- 如果要通过\<script>元素来包含外部 JavaScript 文件，那么 src 属性就是必需的。这个属性的值是一个指向外部 JavaScript 文件的链接，例如：
```javascript
    <script type="text/javascript" src="example.js"></script>
```
> 在上面的例子中，外部文件 example.js 将被加载到当前页面中。外部文件只须包含通常要放在开始的\<script>和结束的\</script>之间的那些JavaScript 代码即可。与解析嵌入式 JavaScript 代码一样，在解析外部 JavaScript 文件（包括下载该文件）时，页面的处理也会暂时停止。如果在带有 src 属性的 \<script> 和 \</script> 标签之间嵌入了额外的 JavaScript 代码，则只会下载并执行外部的脚本文件，嵌入的代码会被忽略。
> 无论如何包含代码，只要不存在 defer 和 async 属性，浏览器都会按照\<script>元素在页面中出现的先后顺序对它们依次进行解析。

#### 2.1.1 标签的位置
> 按照传统的做法，所有的\<script>元素都应该放在页面的\<head>元素中，例如：
```javascript
<!DOCTYPE html>
<html>
    <head>
	    <title>Example HTML Page</title>
	    <script type="text/javascript" src="example1.js"></script>
	    <script type="text/javascript" src="example2.js"></script>
    </head>
<body>
    <!-- 这里放内容 -->
</body>
</html>
```
> 这种做法的目的是把所有外部文件的饮用都放在相同的地方。可是，在文档的\<head>元素中包含所有的 JavaScript 文件，必需等到全部 JavaScript 代码都被下载、解析和执行完成以后，才能开始呈现页面的内容（浏览器在遇到\<body>标签时才开始呈现内容）。对于那些需要很多 JavaScript 代码的页面来说，无疑会导致浏览器在呈现页面时出现明显的延迟、延迟期间的浏览器窗口中将是一片空白。为了避免这个问题，现代Web应用程序一般都把全部的 JavaScript 引用放在 \<body> 元素中页面内容的后面，如下所示：
```javascript
<!DOCTYPE html>
<html>
    <head>
	    <title>Example HTML Page</title>
    </head>
<body>
    <!-- 这里放内容 -->
    <script type="text/javascript" src="example1.js"></script>
    <script type="text/javascript" src="example2.js"></script>
</body>
</html>
```
#### 2.1.2 延迟脚本
> HTML4.01 为\<script>标签定义了defer属性。这个属性的用途是表明脚本在执行时不会影响页面的构造。在\<script>元素中设置了 defer 属性，相当于告诉浏览器**立即下载**，但延迟执行。按照HTML5 规范要求脚本按照它们出现的先后顺序执行，但在现实当中，延迟脚本并不一定会按照顺序执行，也不一定会在 DOMContentLoaded 事件触发前执行，**因此最好只包含一个延迟脚本**
```javascript
<!DOCTYPE html>
<html>
    <head>
	    <title>Example HTML Page</title>
        <script type="text/javascript" defer="defer" src="example1.js"></script>
        <script type="text/javascript" defer="defer" src="example2.js"></script>
    </head>
<body>
    <!-- 这里放内容 -->
</body>
</html>
```
#### 2.1.3 异步脚本
> 与 defer 类似，async 只适用于外部脚本文件，并告诉浏览器立即下载文件。指定 async 属性的目的是不让页面等待两个脚本下载和执行，从而也不加载页面其他内容。为此，**建议异步脚本不要在加载期间修改DOM**，异步脚本一定会在页面的 load 事件之前执行，但可能会在 DOMContentLoaded 事件出发之前或之后执行。
 ```javascript
<!DOCTYPE html>
<html>
    <head>
	    <title>Example HTML Page</title>
        <script type="text/javascript" async="async" src="example1.js"></script>
        <script type="text/javascript" async="async" src="example2.js"></script>
    </head>
<body>
    <!-- 这里放内容 -->
</body>
</html>
```
#### 2.4 \<noscript>元素
> 早起浏览器都会面临一个特殊的问题，即当浏览器不支持 JavaScript 时如何让页面平稳地退化。最终解决方案就是创造一个\<noscript>元素。这个元素可以包含能够出现在文档\<body>中的任何 HTML 元素————\<script>元素除外。包含在\<noscript>元素汇总的内容只有在下列情况下才会显示出来：
- 浏览器不支持脚本；
- 浏览器支持脚本，但脚本被禁用。
```javascript
<!DOCTYPE html>
<html>
    <head>
	    <title>Example HTML Page</title>
        <script type="text/javascript" defer="defer" src="example1.js"></script>
        <script type="text/javascript" defer="defer" src="example2.js"></script>
    </head>
<body>
    <!-- 这里放内容 -->
    <noscript>
        <p>本页面需要浏览器支持（启用）JavaScript。</p>
    </noscript>    
</body>
</html>
```