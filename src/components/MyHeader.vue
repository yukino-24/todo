<template>
  <header>
      <input type="text" name="" id="" placeholder="タスクを入力し、ENTERキーを押して下さい"  @keyup.enter="add"/>
  </header>
</template>

<script>
import {nanoid} from 'nanoid';
export default {
   name:'MyHeader',
   methods: {
    add(e){
      // 校验数据
      if(!e.target.value) return 
      // 将用户输入包装成一个todo对象
      const todoObj ={id:nanoid(),title:e.target.value,done:false};
      // 通知app组件去添加一个todo对象
      this.$emit('addTodo',todoObj)
      // 清空输入
      e.target.value="";
    }
  },
}
</script>

<style scoped>
/* header */
header{
  text-align: center;
}
header input{
  font-size: 14px;
  width: calc(100% - 80px);
  height: 30px;
  border: 1px solid purple;
  box-shadow:   6px 6px 5px rgba(0,0,0,0.075);
  border-radius: 4px;
}
header input:focus{
  outline: none;
  border-color: purple;
  
  padding: 4px 7px;
}
</style>