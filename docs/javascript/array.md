---
id:array 
title:Style Guide
---

## map

map() 方法返回一个新数组,顺序依次处理元素。

:::warning

map()不会改变原始数组。

map()当有引用类型时,修改一个数组另一个数组也会变化。

:::

```javascript
const list = [{name: '小明'}, {name: '小李'}]
const newList = list.map(item => item.name) //['小明','小李'] 
```

## push

push() 方法用于在数组的末端添加一个或多个元素，并返回添加新元素后的数组长度。

:::warning

该方法会改变原数组。

:::

```javascript
const list = [1, 2]
const len = list.push(3) //[1,2,3] len=3
```

## some

some() 方法会依次执行数组的每个元素：

1. 如果有一个元素满足条件，则表达式返回true , 剩余的元素不会再执行检测。
1. 如果没有满足条件的元素，则返回false。

:::warning

该方法不会改变原数组。

:::

```javascript
const list = [1, 2, 3, 4, 5]
const flag = list.some(item => item > 3) //true
```

## every

every() 方法使用指定函数检测数组中的所有元素

1. 如果数组中检测到有一个元素不满足，则整个表达式返回 false ，且剩余的元素不会再进行检测。
1. 如果所有元素都满足条件，则返回 true。

:::warning

该方法不会改变原数组。

:::

```js 
const list = [1, 2, 3, 4, 5]
const flag = list.every(item => item > 3) //false
```

## filter

filter() 方法创建一个新的数组，新数组中的元素是通过检查指定数组中符合条件的所有元素。

:::warning

该方法不会改变原数组。

该方法不会对空数组进行检测。

:::

```js
const list = [1, 2, 3, 4, 5]
list.filter(item => item > 3) // [4,5]
```

##  reduce

reduce() 方法接收一个函数作为累加器，数组中的每个值（从左到右）开始缩减，最终计算为一个值。

reduce() 可以作为一个高阶函数，用于函数的 compose。

:::warning

reduce() 对于空数组是不会执行回调函数的。

:::

```js
const list = [1, 2, 3, 4, 5]
list.reduce((previousValue, currentValue, currentIndex, array) => previousValue+currentValue, 0)
//15    
```

|  参数  |   描述       |  
| -------- | --------- | 
| previousValue  | 	必需。初始值, 或者计算结束后的返回值。 | 
| currentValue       | 	必需。当前元素                   |
| currentIndex  | 		可选。当前元素的索引   | 
| array       | 	可选。当前元素所属的数组对象                 |








