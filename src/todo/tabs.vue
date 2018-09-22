<template>
  <div class="helper">
    <span class="left">left:{{unFinishedTodoLength}}</span>
    <span class="tabs">
      <span 
        v-for="state in states"
        :key="state"
        :class="[state, filter === state ? 'actived' : '']"
        @click="toggleFilter(state)"
      >
        {{state}}
      </span>
    </span>
    <span class="clear" @click="clearAllCompleted">Clear completed.</span>
  </div>
</template>

<script>
  export default {
    props: {
      filter: {
        type: String,
        required: true
      },
      todos: {
        type: Array,
        required: true
      }
    },
    data(){
      return {
        states: ['all', 'active', 'completed']
      }
    },
    computed: {
      unFinishedTodoLength(){
        return this.todos.filter(todo=>!todo.completed).length
      }
    },
    methods: {
      clearAllCompleted(){
        this.$emit('clear')
      },
      toggleFilter(state){
        this.$emit('toggle', state)
      }
    }
  }
</script>

<style lang="stylus" scoped>

.actived {
  color yellow
}

</style>