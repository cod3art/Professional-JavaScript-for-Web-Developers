## 在 HTML 中使用 JavaScript

####2.1 \<scirpt> 元素
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
> 在上面的例子中，外部文件 example.js 将被加载到当前页面中。外部文件只须包含通常要放在开始的\<script>和结束的\</script>之间的那些JavaScript 代码即可。与解析嵌入式 JavaScript 代码一样，在解析外部 JavaScript 文件（包括下载该文件）时，页面的处理也会暂时停止。

