<template>
    <footer v-show="todos.length">
      <label for="" >
      <input type="checkbox" :checked="isAll" @change="checkAll">
      <span>済み{{doneTotal}}</span> /全部{{todos.length}}
      </label>
      <button @click="clearAll">全てのリストを削除</button>
    </footer>
</template>

<script>
export default {
   name:'MyFooter',
   props:['todos'],
   computed:{
    doneTotal(){
      return this.todos.reduce((pre,todo)=>pre+(todo.done?1:0),0)
    },
    isAll(){
      return this.doneTotal === this.todos.length && this.doneTotal>0
    }
   },
   methods:{
    checkAll(e){
　　　　this.$emit('checkAllTodo',value)
    },
    clearAll(){
      　if(confirm('Are you sure?')){
      this.$emit('clearAllTodo')
      }
      }
    }
   }

</script>

<style scoped>
/* footer */
footer{
 
  height: 40px;
  line-height: 40px;
  padding-left:15px;
  margin-top: 15px;
  display: flex;
  justify-content: space-between;
}
footer input{
  /* margin-right: 15px; */
  transform: scale(1.1);
}
footer input:hover{
  transform: scale(1.2);
}
footer button{
  /* display: none; */
  margin-top: 5px;
  margin-right: 10px;
  height: 30px;
  border: none;
  background-image: linear-gradient(48deg, #659de6, #f4a1f7);
  border-radius: 4px;
  color: #eee;
  cursor: pointer;

}
</style>