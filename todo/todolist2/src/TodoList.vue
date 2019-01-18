<template>
  <div>
    <div>
      <h1 v-text="title"></h1>
      <input v-model="inputValue" @keyup.enter="onEnter"/>
    </div>
    <ul>
      <li v-for="item in items" 
        v-bind:class="{finished: item.isFinished}"
        @click="handleclick(item)"
        >{{item.label}}
      </li>
      
    </ul>
    <todo-item></todo-item>
  </div>
</template>

<script>
import Store from './store'
import TodoItem from './components/TodoItem'

export default {
 data () {
   return {
     title: 'this is a todo list',
     items: Store.fetch(),
     inputValue: ''
   }
 },
 components: {
   'todo-item' : TodoItem
 },
 watch: {
   items: {
     handler (items) {
       Store.save(items)
     },
     deep: true
   }
 },
 methods: {
   handleclick (item) {
     item.isFinished = !item.isFinished
   },
   onEnter () {
     this.items.push({
       label: this.inputValue,
       isFinished: false
     })
     this.inputValue = ''
     
   }
 }
}
</script>

<style>
body{
  margin-top:60px;
  display: flex;
  align-items: center;
  justify-content: center;
  height:100%;
}
.finished{
  text-decoration:underline;
}

</style>
