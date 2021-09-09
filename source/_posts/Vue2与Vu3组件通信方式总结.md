---
title: Vue2与Vu3组件通信方式总结
date: 2021-09-09 10:04:03
tags: Vue
categories: 前端
---
# Vue2组件通信
## 父组件向子组件传值
props:父组件以属性的方式传值给子组件;子组件通过props方式接收数据
在父组件中引入子组件并绑定fatherData自定义属性
```bash
<Son :fatherData="fatherData"></Son>

<script>
import Son from '@/components/son'
  export default{
    name:'Father',
    components:{Son},
    data(){
      return{
        fatherData:'我是父组件向子组件传递的值-props方式'
      }
    }
  }
</script>
```
在子组件中使用 props 接收父组件传递的数据，props 里的名字跟父组件定义的属性名一致
```bash
<template>
  <div>我是父组件的数据：{{fatherData}}</div>
  <div>我是父组件传递修改后的数据：{{mydata}}</div>
</template>
<script>
  export default{
    name:'Son',
    props:{
      fatherData:{
        type:String,
        default:''
      }
    },
    data(){
      mydata:'公众号：贩卖前端仔 '+ this.fatherData
    },
    watch:{
      fatherData(newVal){
        this.mydata='公众号：贩卖前端仔 '+ newVal
      }
    },
  }
</script>
```
因为Vue的单向数据流机制，子组件不能够直接去修改父组件传递的值修改的，否则能改的话那父组件的值就被“污染”了。
但是子组件内想要修改父组件传过来的值却不“污染”父组件的话，可以在子组件内定义一个变量mydata去接收fatherData数据，并使用 watch 监听fatherData数据的变更。
