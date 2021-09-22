<template>
  <Todos v-model="todos"/>
</template>

<script>
import Todos from "@/components/Todos";
export default {
  name: 'App',
  components: {
    Todos
  },
  data() {
    return {
      todos: [{
        name: 'Demo',
        completed: true
      }]
    }
  },
  methods: {
    addTodo(){
       this.todos.push({
         name: 'Jean',
         completed: false
       })
    }
  }
}
</script>

<style>
</style>
