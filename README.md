# vue-组件之间的传参方式
总结组件之间的传参方式

一，父组件传参给子组件
 * props传参
父组件：
<new-slot propsTitle="父组件传给子组件的值propsTitle"></new-slot>
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
export default {
   methods:{
      add(data){
         console.log(data)
      }
   }
}
 * 通过$children来传参
 在父组件的代码里：
 ```javascript
 export default {
  mounted:function(){
    this.$children[0].add('这是通过$children方式传参')
  }
 }
 ```
 this.$children返回的是所有子组件的实例，如果你知道组件的顺序才可以这么使用，

 


