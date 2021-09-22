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
        <li class="todo" v-for="todo in todos" :key="todo.name" :class="{completed: todo.completed}">
          <div class="view">
            <input type="checkbox" v-model="todo.completed" class="toggle">
            <label>{{ todo.name }}</label>
          </div>
        </li>
      </ul>
    </div>
    <footer class="footer">
      <span class="todo-count"><strong>{{remaining}}</strong> tâches à faire</span>
    </footer>
  </section>
</template>

<script>
export default {
  name: "Todos",
  data() {
    return {
      todos: [{
        name: "Tache de test",
        completed: true
      }],
      newTodo: ''
    }
  },
  methods: {
    addTodo() {
      this.todos.push({
        name: this.newTodo,
        completed: false
      })
      this.newTodo = ''
    }
  },
  computed: {
    remaining(){
      return this.todos.filter(todo => !todo.completed).length
    }
  }
}
</script>

<style src="../Css/todos.css">

</style>
