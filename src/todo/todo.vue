<template>
    <section class="real-app">
      <input
        type="text"
        class="add-input"
        autofocus="autofocus"
        placeholder="接下来要做什么"
        @keyup.enter="addTodo"
      >
      </input>
      <item 
        v-for="todo in filterTodos"
        :key="todo.id"
        @del="deleteTodo"
        :todo="todo"/>
      <tabs 
        @clear="clearCompeleted"
        @toggle="toggleFilter"
        :filter="filter" 
        :todos="todos"/>
    </section>
</template>

<script>
import Item from './item.vue'
import Tabs from './tabs.vue'

let id = 0
export default {
  components: {
    Item,Tabs,
  },
  data() {
    return {
      todos: [],
      filter: 'all'
    }
  },
  methods: {
    addTodo(e){
      this.todos.unshift({
        id: id++,
        content: e.target.value.trim(),
        completed: false
      })
      e.target.value = ''
    },
    deleteTodo(id){
      this.todos.splice(this.todos.findIndex(todo=>todo.id===id), 1)
    },
    clearCompeleted(){
      this.todos = this.todos.filter(v=>( !v.completed))
    },
    toggleFilter(state){
      this.filter = state
    }
  },
  computed: {
    filterTodos(){
      if(this.filter === 'all'){
        return this.todos
      }
      const completed = this.filter === 'completed'
      return this.todos.filter(todo=>todo.completed==completed)
    }
  }
}
</script>

<style lang="stylus" scoped>

.real-app {
  width 600px
  margin 0 auto 
  box-shadow 0 0 5px #666
}

.add-input {
  position relative;
  width 100%
  font-size 20px
  font-family inherit 
  font-weight inherit 
  line-height 1.4em
  border 0
  box-sizing: border-box
  font-smoothing: antialiased 
  box-shadow: inset 0 -2px 1px rgba(0,0,0,0.4)
}

</style>
