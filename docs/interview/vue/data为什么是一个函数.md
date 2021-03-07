---

id:vue0 

title:为什么vue中data是一个函数?

---
首先要知道data为什么是一个函数,先要了解是什么vue组件:

## 什么是组件

组件是可复用的 Vue 实例，且带有一个名字。 --[Vue官网](https://cn.vuejs.org/v2/guide/components.html?#%E5%9F%BA%E6%9C%AC%E7%A4%BA%E4%BE%8B)

vue的data数据其实是vue原型上的属性，数据存在于内存当中。

vue为了保证每个实例上的data数据的独立性，规定了必须使用函数，而不是对象。

而在单文件中只有一个new Vue实例,所以在普通js中 new Vue() 可以是一个对象。<span style={{color:'#f08d49'}}>(会有多个不同的vue实例)</span>

## 当vue.data是一个对象

```js
const myComponent = function () {
    //...code
}
myComponent.prototype.data = {
    sex: '女',
    height: '165'
}
const xiaoming = new myComponent()
const xiaohong = new myComponent()
console.log(`${xiaohong.data.sex === xiaoming.data.sex}`)//true
xiaoming.data.sex = '男'
console.log(xiaohong.data.sex) //男 被xiaoming给影响了

```

## 当vue.data是一个函数
```js

const myComponent = function () {
    //...code
    this.data = this.data() //在new的时候保存初始值
}
myComponent.prototype.data = function (){
   return{
       sex: '女',
       height: '165'
   }
}
const xiaoming = new myComponent()
const xiaohong = new myComponent()
console.log(`${xiaohong.data.sex === xiaoming.data.sex}`)//true
xiaoming.data.sex = '男'
console.log(xiaohong.data.sex) //女 值不是同的 在new是时候被赋予的并没有改变
```




    

