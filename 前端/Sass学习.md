#  Sass简介

* 世界上最成熟、最稳定、最强大的专业级CSS扩展语言
* 特点：
  * 兼容CSS：Sass完全兼容所有版本的CSS
  * 特性丰富：Sass拥有比其他任何CSS扩展语言更多的功能和特性
  * 成熟：Sass已经经过核心团队超过8年的精心打造
  * 行业认可
  * 社区庞大
  * 框架：有无数的框架使用Sass构建。比如compass，Bourbon，Susy

#  快速入门

##  使用变量

* 变量申明

  `sass`变量的声明和`css`属性的声明很像：

  ```
  $highlight-color: #F90;
  ```

  这意味着变量`$highlight-color`现在的值是`#F90`。任何可以用作`css`属性值的赋值都 可以用作`sass`的变量值，甚至是以空格分割的多个属性值，如`$basic-border: 1px solid black;`，或以逗号分割的多个属性值，如`$plain-font: "Myriad Pro"、Myriad、"Helvetica Neue"、Helvetica、"Liberation Sans"、Arial和sans-serif; sans-serif;`。这时变 量还没有生效，除非你引用这个变量——我们很快就会了解如何引用。

  与`CSS`属性不同，变量可以在`css`规则块定义之外存在。当变量定义在`css`规则块内，那么该变量只能在此规则块内使用。如果它们出现在任何形式的`{...}`块中（如`@media`或者`@font-face`块），情况也是如此：

  ```
  $nav-color: #F90;
  nav {
    $width: 100px;
    width: $width;
    color: $nav-color;
  }
  //编译后
  nav {
    width: 100px;  
    color: #F90;
  }
  ```

* 变量引用

  凡是`css`属性的标准值（比如说1px或者bold）可存在的地方，变量就可以使用。`css`生成时，变量会被它们的值所替代。之后，如果你需要一个不同的值，只需要改变这个变量的值，则所有引用此变量的地方生成的值都会随之改变。

  ~~~
  $highlight-color: #F90;
  .selected {
    border: 1px solid $highlight-color;
  }
  //编译后
  .selected {
    border: 1px solid #F90;
  }
  ~~~

* 变量中用中划线还是下划线分割

  `sass`的变量名可以与`css`中的属性名和选择器名称相同，包括中划线和下划线。这完全取决于个人的喜好，有些人喜欢使用中划线来分隔变量中的多个词（如`$highlight-color`），而有些人喜欢使用下划线（如`$highlight_color`）。使用中划线的方式更为普遍，这也是`compass`和本文都用的方式。

  不过，`sass`并不想强迫任何人一定使用中划线或下划线，所以这两种用法相互兼容。用中划线声明的变量可以使用下划线的方式引用，反之亦然。这意味着即使`compass`选择用中划线的命名方式，这并不影响你在使用`compass`的样式中用下划线的命名方式进行引用：

  ```
  $link-color: blue;
  a {
    color: $link_color;
  }
  //编译后
  a {
    color: blue;
  }
  ```

##  嵌套CSS 规则

`css`中重复写选择器是非常恼人的。如果要写一大串指向页面中同一块的样式时，往往需要 一遍又一遍地写同一个`ID`：

~~~
#content article h1 { color: #333 }
#content article p { margin-bottom: 1.4em }
#content aside { background-color: #EEE }
~~~

像这种情况，`sass`可以让你只写一遍，且使样式可读性更高。在Sass中，你可以像俄罗斯套娃那样在规则块中嵌套规则块。`sass`在输出`css`时会帮你把这些嵌套规则处理好，避免你的重复书写。

~~~
#content {
  article {
    h1 { color: #333 }
    p { margin-bottom: 1.4em }
  }
  aside { background-color: #EEE }
}
/* 编译后*/
#content article h1 { color: #333 }
#content article p { margin-bottom: 1.4em }
#content aside { background-color: #EEE }
~~~

* 父选择器的标识符&

  一般情况下，`sass`在解开一个嵌套规则时就会把父选择器（`#content`）通过一个空格连接到子选择器的前边（`article`和`aside`）形成（`#content article`和`#content aside`）。这种在CSS里边被称为后代选择器，因为它选择ID为`content`的元素内所有命中选择器`article`和`aside`的元素。但在有些情况下你却不会希望`sass`使用这种后代选择器的方式生成这种连接。

  最常见的一种情况是当你为链接之类的元素写`：hover`这种伪类时，你并不希望以后代选择器的方式连接。比如说，下面这种情况`sass`就无法正常工作

  ~~~
  article a {
    color: blue;
    :hover { color: red }
  }
  ~~~

  这意味着`color: red`这条规则将会被应用到选择器`article a :hover`，`article`元素内链接的所有子元素在被`hover`时都会变成红色。这是不正确的！你想把这条规则应用到超链接自身，而后代选择器的方式无法帮你实现。

  解决之道为使用一个特殊的`sass`选择器，即父选择器。在使用嵌套规则时，父选择器能对于嵌套规则如何解开提供更好的控制。它就是一个简单的`&`符号，且可以放在任何一个选择器可出现的地方，比如`h1`放在哪，它就可以放在哪。

  ~~~
  article a {
    color: blue;
    &:hover { color: red }
  }
  ~~~

* 群组选择器的嵌套

  在`CSS`里边，选择器`h1``h2`和`h3`会同时命中h1元素、h2元素和h3元素。与此类似，`.button` `button`会命中button元素和类名为.button的元素。这种选择器称为群组选择器。群组选择器 的规则会对命中群组中任何一个选择器的元素生效。

  ~~~
  .button, button {
    margin: 0;
  }
  ~~~

  当看到上边这段代码时，你可能还没意识到会有重复性的工作。但会很快发现：如果你需要在一个特定的容器元素内对这样一个群组选择器进行修饰，情况就不同了。`css`的写法会让你在群组选择器中的每一个选择器前都重复一遍容器元素的选择器。

  ~~~
  .container h1, .container h2, .container h3 { margin-bottom: .8em }
  ~~~

  非常幸运，`sass`的嵌套特性在这种场景下也非常有用。当`sass`解开一个群组选择器规则内嵌的规则时，它会把每一个内嵌选择器的规则都正确地解出来：

  ```
  .container {
    h1, h2, h3 {margin-bottom: .8em}
  }
  ```

* 子组合选择器和同层组合选择器：>,+和~

  你可以用子组合选择器>选择一个元素的直接子元素。上例中，第一个选择器会选择article下的所有命中section选择器的元素

  ~~~
  article > section { border: 1px solid #ccc }
  ~~~

  你可以用同层相邻组合选择器`+`选择`header`元素后紧跟的`p`元素

  ~~~
  header + p { font-size: 1.1em }
  ~~~

  你也可以用同层全体组合选择器`~`，选择所有跟在`article`后的同层`article`元素，不管它们之间隔了多少其他元素

  ~~~
  article ~ article { border-top: 1px dashed #ccc }
  ~~~

  这些组合选择器可以毫不费力地应用到`sass`的规则嵌套中。可以把它们放在外层选择器后边，或里层选择器前边

  ~~~
  article {
    ~ article { border-top: 1px dashed #ccc }
    > section { background: #eee }
    dl > {
      dt { color: #333 }
      dd { color: #555 }
    }
    nav + & { margin-top: 0 }
  }
  ~~~

* 嵌套属性

  在`sass`中，除了CSS选择器，属性也可以进行嵌套。尽管编写属性涉及的重复不像编写选择器那么糟糕，但是要反复写`border-style``border-width``border-color`以及`border-*`等也是非常烦人的。在`sass`中，你只需敲写一遍`border`：

  ~~~
  nav {
    border: {
    style: solid;
    width: 1px;
    color: #ccc;
    }
  }
  ~~~

##  导入SASS文件

`css`有一个特别不常用的特性，即`@import`规则，它允许在一个`css`文件中导入其他`css`文件。然而，后果是只有执行到`@import`时，浏览器才会去下载其他`css`文件，这导致页面加载起来特别慢。

`sass`也有一个`@import`规则，但不同的是，`sass`的`@import`规则在生成`css`文件时就把相关文件导入进来。这意味着所有相关的样式被归纳到了同一个`css`文件中，而无需发起额外的下载请求。

* 使用SASS部分文件

  当通过`@import`把`sass`样式分散到多个文件时，你通常只想生成少数几个`css`文件。那些专门为`@import`命令而编写的`sass`文件，并不需要生成对应的独立`css`文件，这样的`sass`文件称为局部文件。对此，`sass`有一个特殊的约定来命名这些文件。

  此约定即，`sass`局部文件的文件名以下划线开头。这样，`sass`就不会在编译时单独编译这个文件输出`css`，而只把这个文件用作导入。当你`@import`一个局部文件时，还可以不写文件的全名，即省略文件名开头的下划线。举例来说，你想导入`themes/_night-sky.scss`这个局部文件里的变量，你只需在样式表中写`@import` `"themes/night-sky";`。

  局部文件可以被多个不同的文件引用。当一些样式需要在多个页面甚至多个项目中使用时，这非常有用。在这种情况下，有时需要在你的样式表中对导入的样式稍作修改，`sass`有一个功能刚好可以解决这个问题，即默认变量值。

* 默认变量值

  一般情况下，你反复声明一个变量，只有最后一处声明有效且它会覆盖前边的值。

  ~~~
  $link-color: blue;
  $link-color: red;
  a {
  	color: $link-color;
  }
  ~~~

* 嵌套导入

  跟原生的`css`不同，`sass`允许`@import`命令写在`css`规则内。这种导入方式下，生成对应的`css`文件时，局部文件会被直接插入到`css`规则内导入它的地方。

  ~~~
  .blue-theme {@import "blue-theme"}
  
  //生成的结果跟你直接在.blue-theme选择器内写_blue-theme.scss文件的内容完全一样。
  
  .blue-theme {
    aside {
      background: blue;
      color: #fff;
    }
  }
  ~~~

* 原生的CSS导入

  由于`sass`兼容原生的`css`，所以它也支持原生的`CSS@import`。尽管通常在`sass`中使用`@import`时，`sass`会尝试找到对应的`sass`文件并导入进来，但在下列三种情况下会生成原生的`CSS@import`，尽管这会造成浏览器解析`css`时的额外下载：

  - 被导入文件的名字以`.css`结尾；
  - 被导入文件的名字是一个URL地址（比如http://www.sass.hk/css/css.css），由此可用谷歌字体API提供的相应服务；
  - 被导入文件的名字是`CSS`的url()值。

  这就是说，你不能用`sass`的`@import`直接导入一个原始的`css`文件，因为`sass`会认为你想用`css`原生的`@import`。但是，因为`sass`的语法完全兼容`css`，所以你可以把原始的`css`文件改名为`.scss`后缀，即可直接导入了。

  文件导入是保证`sass`的代码可维护性和可读性的重要一环。次之但亦非常重要的就是注释了。注释可以帮助样式作者记录写`sass`的过程中的想法。在原生的`css`中，注释对于其他人是直接可见的，但`sass`提供了一种方式可在生成的`css`文件中按需抹掉相应的注释。

##  静默注释

`css`中注释的作用包括帮助你组织样式、以后你看自己的代码时明白为什么这样写，以及简单的样式说明。但是，你并不希望每个浏览网站源码的人都能看到所有注释。

`sass`另外提供了一种不同于`css`标准注释格式`/* ... */`的注释语法，即静默注释，其内容不会出现在生成的`css`文件中。静默注释的语法跟`JavaScript``Java`等类`C`的语言中单行注释的语法相同，它们以`//`开头，注释内容直到行末。

~~~
body {
  color: #333; // 这种注释内容不会出现在生成的css文件中
  padding: 0; /* 这种注释内容会出现在生成的css文件中 */
}
~~~

实际上，`css`的标准注释格式`/* ... */`内的注释内容亦可在生成的`css`文件中抹去。当注释出现在原生`css`不允许的地方，如在`css`属性或选择器中，`sass`将不知如何将其生成到对应`css`文件中的相应位置，于是这些注释被抹掉。

```
body {
  color /* 这块注释内容不会出现在生成的css中 */: #333;
  padding: 1; /* 这块注释内容也不会出现在生成的css中 */ 0;
}
```

##  混合器

混合器使用`@mixin`标识符定义。看上去很像其他的`CSS @`标识符，比如说`@media`或者`@font-face`。这个标识符给一大段样式赋予一个名字，这样你就可以轻易地通过引用这个名字重用这段样式。下边的这段`sass`代码，定义了一个非常简单的混合器，目的是添加跨浏览器的圆角边框。

~~~
@mixin rounded-corners {
  -moz-border-radius: 5px;
  -webkit-border-radius: 5px;
  border-radius: 5px;
}
~~~

然后就可以在你的样式表中通过`@include`来使用这个混合器，放在你希望的任何地方。`@include`调用会把混合器中的所有样式提取出来放在`@include`被调用的地方。如果像下边这样写：

~~~
notice {
  background-color: green;
  border: 2px solid #00aa00;
  @include rounded-corners;
}
//sass最终生成：
.notice {
  background-color: green;
  border: 2px solid #00aa00;
  -moz-border-radius: 5px;
  -webkit-border-radius: 5px;
  border-radius: 5px;
}
~~~

* 何时使用混合器

  判断一组属性是否应该组合成一个混合器，一条经验法则就是你能否为这个混合器想出一个好的名字。

* 混合器中的CSS规则

  混合器中不仅可以包含属性，也可以包含`css`规则，包含选择器和选择器中的属性，如下代码:

  ~~~
  @mixin no-bullets {
    list-style: none;
    li {
      list-style-image: none;
      list-style-type: none;
      margin-left: 0px;
    }
  }
  ~~~

  当一个包含`css`规则的混合器通过`@include`包含在一个父规则中时，在混合器中的规则最终会生成父规则中的嵌套规则。举个例子，看看下边的`sass`代码，这个例子中使用了`no-bullets`这个混合器：

  ~~~
  ul.plain {
    color: #444;
    @include no-bullets;
  }
  ~~~

* 给混合器传参

  混合器并不一定总得生成相同的样式。可以通过在`@include`混合器时给混合器传参，来定制混合器生成的精确样式。当`@include`混合器时，参数其实就是可以赋值给`css`属性值的变量。如果你写过`JavaScript`，这种方式跟`JavaScript`的`function`很像：

  ~~~
  @mixin link-colors($normal, $hover, $visited) {
    color: $normal;
    &:hover { color: $hover; }
    &:visited { color: $visited; }
  }
  ~~~

  当混合器被`@include`时，你可以把它当作一个`css`函数来传参。如果你像下边这样写：

  ~~~
  a {
    @include link-colors(blue, red, green);
  }
  //Sass最终生成的是：
  a { color: blue; }
  a:hover { color: red; }
  a:visited { color: green; }
  ~~~

* 默认参数值

  为了在`@include`混合器时不必传入所有的参数，我们可以给参数指定一个默认值。参数默认值使用`$name: default-value`的声明形式，默认值可以是任何有效的`css`属性值，甚至是其他参数的引用，如下代码：

  ~~~
  @mixin link-colors(
      $normal,
      $hover: $normal,
      $visited: $normal
    )
  {
    color: $normal;
    &:hover { color: $hover; }
    &:visited { color: $visited; }
  }
  ~~~

##  使用选择器继承来精简CSS

* 何时使用继承

  继承是基于类的（有时是基于其他类型的选择器），所以继承应该是建立在语义化的关系上。

* 继承的高级用法

  最常用的一种高级用法是继承一个`html`元素的样式

  ~~~
  .disabled {
    color: gray;
    @extend a;
  }
  ~~~

* 继承的工作细节

  混合器本身不会引起`css`层叠的问题，因为混合器把样式直接放到了`css`规则中，而继承存在样式层叠的问题。被继承的样式会保持原有定义位置和选择器权重不变。

* 使用继承的最佳实践

  通常使用继承会让你的`css`美观、整洁。因为继承只会在生成`css`时复制选择器，而不会复制大段的`css`属性。但是如果你不小心，可能会让生成的`css`中包含大量的选择器复制。

  避免这种情况出现的最好方法就是不要在`css`规则中使用后代选择器（比如`.foo .bar`）去继承`css`规则。如果你这么做，同时被继承的`css`规则有通过后代选择器修饰的样式，生成`css`中的选择器的数量很快就会失控：

  ~~~
  .foo .bar { @extend .baz; }
  .bip .baz { a: b; }
  ~~~

