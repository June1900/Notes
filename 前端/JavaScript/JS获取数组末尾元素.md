##  JavaScript获取Array末尾元素

##  第一种

~~~javascript
//数组的pop用于删除数组末尾元素。pop方法用于删除数组最后一个元素，把数组长度减一，并返回当前元素值；如果数组已经为空，则不改变数组，返回undefined

let array = [1,2,3,4]
let popArr = array.pop();
console.log(array)
console.log(popArr)
~~~

##  第二种

~~~javascript
//数组的length属性

let array = [1,2,3,4]
console.log(array[array.length - 1])
~~~

##  第三种

~~~javascript
//数组的slice方法

let array = [1,2,3,4]
console.log(array.slice(-1))
~~~

