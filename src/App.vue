<template>
  <div id="root">
    <div class="container">
    <h2>My Todo List</h2>
    <MyHeader @addTodo="addTodo"/>
    <MyList :todos="todos" :checkTodo="checkTodo" :deleteTodo="deleteTodo"/>
    <MyFooter :todos="todos" @checkAllTodo="checkAllTodo" @clearAllTodo="clearAllTodo"/>
   </div>
  </div>
</template>

<script>
import MyHeader from './components/MyHeader.vue'
import MyList from './components/MyList.vue'
import MyFooter from './components/MyFooter.vue'

export default {
 name:'App',
 components:{
  MyHeader,MyList,MyFooter
 },
 data(){
    return{
      todos:JSON.parse(localStorage.getItem('todos'))||
      []
    }
   },
  methods:{
    // 添加一个todo
    addTodo(todoObj){
     this.todos.unshift(todoObj)
    },
    // 取消勾选一个todo
    checkTodo(id){
      this.todos.forEach((todo)=>{
        if(todo.id === id) todo.done =!todo.done
      })
    },
    // 删除一个todo
    deleteTodo(id){
　　　　this.todos = this.todos.filter(todo => todo.id !== id)
    },
    // 全选or取消全选
    checkAllTodo(done){
      this.todos.forEach((todo)=>{
        todo.done = done
      })
    },
    // 清除所有完成的todo
    clearAllTodo(){
      this.todos= this.todos.filter((todo)=>{
        return !todo.done
      })
    }
  },
  watch:{
    todos:{
      handler(value){
      localStorage.setItem('todos',JSON.stringify(value))
      },
      deep:true
    }
  },
  mounted(){
    this.$bus.$on('checkTodo',this.checkTodo)
    this.$bus.$on('deleteTodo',this.deleteTodo)
  },
  beforeDestroy(){
    this.$bus.$off('checkTodo')
    this.$bus.$off('deleteTodo')
  }
}
</script>

<style>
/* base */
body{
  background: rgb(243, 235, 252);
}
.container{
 margin: 0 auto;
 width: calc(100% - 80px);
  /* border: 1px solid black; */
}

/* title */
#root h2{
  text-align: center;
  color: grey;
}





</style>
