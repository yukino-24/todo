<template>
 <li>
        <label for="">
        <input type="checkbox" :checked="todo.done" @click="handleCheck(todo.id)">
        <span  @click="handleCheck(todo.id)">{{todo.title}}</span>
        </label>
        
        <div>
        <button  @click="handleDelete(todo.id)">削除</button>
        <!-- <button  @click="handleEdit(todo)">削除</button> -->
      </div>
  </li>
     
</template>

<script>
export default {
   name:'MyItem',
   props:['todo'],
   methods: {
    // 勾选
    handleCheck(id){
    //  通知App组件将对应的done值取反
    this.$bus.$emit('checkTodo',id)
    },
    // 删除
    handleDelete(id){
    　if(confirm('Are you sure?')){
      this.$bus.$emit('deleteTodo',id)
    }
    },
    //编辑
    handleEdit(todo){
     todo.isEdit = true
    }
   },

}
</script>
<style scoped>
/* item */
li{
  list-style: none;
  height: 36px;
  line-height: 36px;
  padding: 0 5px;
  border-bottom: 1px solid rgb(135, 132, 132);
  display: flex;
  justify-content: space-between;
}
div{
  width: 80px;
  display: flex;
  justify-content: space-between;
}
li input:hover{
  transform: scale(1.1);
}
li label{
  cursor: pointer;
}
li input{
  vertical-align: middle;
  margin-right: 6px;
 
}
li button{
  margin-top: 3px;
  height: 30px;
  border: none;
  background-image: linear-gradient(48deg, #659de6, #f4a1f7);
  color: #eee;
  cursor: pointer;
  border-radius: 4px;
  display: none;
}
li .edit{
  padding-left: 5px;
}

li:before{
  content:inherit;
}
li:hover{
  color: rgb(15, 14, 15,.3);
}
li:hover button{
  display: block;
}
</style>

