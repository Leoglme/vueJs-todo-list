<template>
  <section class="todoapp">
    <header class="header">
      <h1>Todos</h1>
      <input type="text" class="new-todo"
             placeholder="Ajouter une tache"
             @keyup.enter="addTodo"
             v-model="newTodo">
    </header>

    <div class="main">
      <ul class="todo-list">
        <li class="todo" v-for="todo in todos" :key="todo.name">
           <div class="view">
             <input type="checkbox" v-model="todo.completed" class="toggle">
             <label>{{todo.name}}</label>
           </div>
        </li>
      </ul>
    </div>
  </section>
</template>

<script>
export default {
  name: "Todos",
  data () {
    return {
        todos : [{
          name: "Tache de test",
          completed: false
        }],
        newTodo: ''
    }
  },
  methods: {
    addTodo(){
      this.todos.push({
        name: this.newTodo,
        completed: false
      })
      this.newTodo = ''
    }
  }
}
</script>

<style src="../Css/todos.css">

</style>
