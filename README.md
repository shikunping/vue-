# vue组件之间的传参方式
总结组件之间的传参方式

一，父组件传参给子组件
 * props传参
父组件：
```javascript
<new-slot propsTitle="父组件传给子组件的值propsTitle"></new-slot>
```
子组件接收父组件传过来的值
```javascript
export default {
  props:['propsTitle']
}
```
子组件获取到的参数可以用this.propsTitle直接访问

* 通过ref传参
```javascript     
<new-slot rel='newSlot'></new-slot>
export default {
   mounted:function(){
      this.$refs.newSlot.add('这是通过ref传参方式');//add是子组件的函数
   }
}
```
子组件
```javascript
export default {
   methods:{
      add(data){
         console.log(data)
      }
   }
}
```
 * 通过$children来传参
 在父组件的代码里：
 ```javascript
 export default {
  mounted:function(){
    this.$children[0].add('这是通过$children方式传参')
  }
 }
 ```
 this.$children返回的是所有子组件的实例，如果你知道组件的顺序才可以这么使用
 * 通过resolve和inject来传参
  父组件
 ```javascript
 export default {
   provide: function () {
    return {
      getMap: this.msg
    }
  },
    data () {
    return {
      msg: 'Welcome to Your Vue.js App'
    }
  }
 }
 ```
  子组件
  ```javascript
  export default {
    inject: ['getMap']
  }
  ```
  这种方式跟props很相似，但是依赖注入这种方式不是响应式的，如果我在父组件里修改了msg的值是不会反应到子组件里
 
 二，子组件给父组件传参
  * $emit触发父组件自定义事件
  子组件
  ```javascript
  export default {
    methods:{
      clickEmit(){
        this.$emit('emitTap','子组件传给父组件的参数$emit');
      }//点击执行这个函数
    }
  }
  ```
  父组件
  ```javascript
  <new-slot v-on:emitTap="faEmit"></new-slot>
  export default {
    methods:{
      faEmit(msg){
        console.log(msg);//这里的msg就是子组件传过来的参数
      }
    }
  }
  ```
  * this.$parent传参
父组件
```javascript
export default {
  methods：{
    faParent(msg){
      console.log(msg);//这里的msg就是子组件传过来的参数
    }
  }
}
```
子组件
```javascript
export default {
  methods:{
    clickParent(){
      this.$parent.faParent('通过$parent传参')
    }
  }
}
```
* 如果子组件想要访问根属性可通过this.$root访问
根实例
```javascript
new Vue({
  el: '#app',
  data () {
    return {
      msg: '根组件'
    }
  }
})
```
子组件
```javascript
export default {
  methods:{
    clickRoot(){
      console.log(this.$root.msg)
    }
  }
}
```
 


