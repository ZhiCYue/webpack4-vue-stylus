<template>
  <div :class="['todo-item', todo.completed ? 'completed' : '']">
    <input 
      class="toggle"
      v-model="todo.completed"
      type="checkbox"
    >
    <label>{{todo.content}}</label>
    <button class="destory" @click="deleteTodo"></button>
  </div>
</template>

<script>
  export default {
    props: {
      todo: {
        type: Object,
        required: true,
      }
    },
    methods: {
      deleteTodo(){
          this.$emit('del', this.todo.id)
      }
    }

  }
</script>

<style lang="stylus" scoped>

.todo-item{
  position relative
  &:hover {
    .destory:after{
      content: 'x'
    }
  }
}

</style>