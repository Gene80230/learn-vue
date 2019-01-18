<template>
  <div>
    <div>
      <h1 v-text="title"></h1>
      <input v-model="inputValue"/>
      <button @click="handleSubmit">提交</button>
    </div>
    <ul>
     <todo-item 
      v-for="(item, index) of list"
      :key="index"
      :content="item"
      :index="index"
      @delete="handleDelete"
     ></todo-item>
    </ul>
  </div>
</template>

<script>
import TodoItem from './components/TodoItem' 
export default {
  components:{
    'todo-item' : TodoItem
  },
 data () {
   return {
     title:'This is a todo list',
     inputValue: '',
     list: []
   }
 },
 methods: {
   handleSubmit () {
     this.list.push(this.inputValue)
     this.inputValue = ''
   },
   handleDelete (index) {
     this.list.splice(index, 1)
   }
 }
}
</script>

<style>
body{
  margin-top:80px;
  display:flex;
  align-items:center;
  justify-content:center;
}
</style>
