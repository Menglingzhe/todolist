<template>
  <div class="todo-header">
    <input type="text" placeholder="请输入你的任务名称，按回车键确认" v-model="title" @keyup.enter="add"/>
  </div>
</template>

<script>
import {nanoid} from 'nanoid'
export default {
  name: "MyHeader",
  //props传值
  props:['addTodo'],
  data(){
    return{
      //收集用户输入
       title:''
    }
  },
  methods:{//一定要加s
    add(){
      // console.log('调用')
      if(!this.title.trim()) return alert('请输入内容') 
      //输入转为可用对象
      const todoObj = {id:nanoid(),title:this.title,done:false}
      //调用props函数传值给app
      this.addTodo(todoObj)
      this.title=''
    }
  },
 
}
</script>

<style scoped>
/*header*/
.todo-header input {
  width: 560px;
  height: 28px;
  font-size: 14px;
  border: 1px solid #ccc;
  border-radius: 4px;
  padding: 4px 7px;
}

.todo-header input:focus {
  outline: none;
  border-color: rgba(82, 168, 236, 0.8);
  box-shadow: inset 0 1px 1px rgba(0, 0, 0, 0.075),
    0 0 8px rgba(82, 168, 236, 0.6);
}
</style>