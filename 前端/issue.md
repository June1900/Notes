###  场景1:html+css截取字符串

* 单行省略

  * ```css
    overflow: hidden;
    text-overflow:ellipsis;
    white-space: nowrap;
    ```

* 多行省略

  * 使用WebKit的CSS扩展属性，该方法适用于WebKit浏览器及移动端

  ```css
  display: -webkit-box;
  -webkit-box-orient: vertical;
  -webkit-line-clamp: 3;
  overflow: hidden;
  ```

* 多行省略

  * ```css
    p{position: relative; line-height: 20px; max-height: 40px;overflow: hidden;}
    p::after{content: "..."; position: absolute; bottom: 0; right: 0; padding-left: 40px;
    background: -webkit-linear-gradient(left, transparent, #fff 55%);
    background: -o-linear-gradient(right, transparent, #fff 55%);
    background: -moz-linear-gradient(right, transparent, #fff 55%);
    background: linear-gradient(to right, transparent, #fff 55%);
    }
    ```

  * 方法适用范围广，但文字未超出行的情况下也会出现省略号,可结合js优化该方法

    * 将height设置为line-height的整数倍，防止超出的文字露出。
    * 给p::after添加渐变背景可避免文字只显示一半。
    * 由于ie6-7不显示content内容，所以要添加标签兼容ie6-7（如：<span>…<span/>）；兼容ie8需要将::after替换成:after。

###  场景2：

