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
      <input type="checkbox" class="toggle-all" id="toggle-all" v-model="allDone">
      <label for="toggle-all"></label>
      <ul class="todo-list">
        <li class="todo" v-for="todo in filteredTodos" :key="todo.name" :class="{completed: todo.completed}">
          <div class="view">
            <input type="checkbox" v-model="todo.completed" class="toggle">
            <label>{{ todo.name }}</label>
          </div>
        </li>
      </ul>
    </div>
    <footer class="footer">
      <span class="todo-count"><strong>{{remaining}}</strong> tâches à faire</span>
      <ul class="filters">
        <li><a href="#" :class="{selected: filter === 'all'}" @click.prevent="filter = 'all'">Toutes</a></li>
        <li><a href="#" :class="{selected: filter === 'todo'}" @click.prevent="filter = 'todo'">A faire</a></li>
        <li><a href="#" :class="{selected: filter === 'done'}" @click.prevent="filter = 'done'">Faites</a></li>
      </ul>
    </footer>
  </section>
</template>

<script>
export default {
  name: "Todos",
  data() {
    return {
      allDone: true,
      todos: [{
        name: "Tache de test",
        completed: true
      }],
      newTodo: '',
      filter: 'all'
    }
  },
  methods: {
    addTodo() {
      this.todos.push({
        name: this.newTodo,
        completed: false
      })
      this.newTodo = ''
    },
  },
  computed: {
    // eslint-disable-next-line vue/no-dupe-keys
    allDone: {
      get(){
        return null
      },
      set(value){
        this.todos.forEach(todo => {
          todo.completed = value;
        })
      }
    },
    remaining(){
      return this.todos.filter(todo => !todo.completed).length
    },
    filteredTodos(){
      if (this.filter === 'todo'){
        return this.todos.filter(todo => !todo.completed)
      }else if (this.filter === 'done'){
        return this.todos.filter(todo => todo.completed)
      }
      return this.todos
    }
  }
}
</script>

<style src="../Css/todos.css">

</style>
