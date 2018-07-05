# vue-组件之间的传参方式
总结组件之间的传参方式
一，父组件传参给子组件
*，props传参
父组件：
<new-slot propsTitle="父组件传给子组件的值propsTitle"></new-slot>
子组件接收父组件传过来的值
```javascript
export default {
  props:['propsTitle']
}
```

