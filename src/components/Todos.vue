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
        <li class="todo" v-for="todo in filteredTodos"
            :key="todo.name"
            :class="{completed: todo.completed, editing: todo === editing}">
          <div class="view">
            <input type="checkbox" v-model="todo.completed" class="toggle">
            <label @dblclick="editTodo(todo)">{{ todo.name }}</label>
            <button class="destroy" @click.prevent="deleteTodo(todo)"></button>
          </div>
          <input type="text"
                 class="edit"
                 v-focus="todo === editing"
                 @keyup.enter="doneEdit"
                 v-model="todo.name">
        </li>
      </ul>
    </div>
    <footer class="footer" v-show="todos.length > 0">
      <span class="todo-count"><strong>{{ remaining }}</strong> tâches à faire</span>
      <ul class="filters">
        <li><a href="#" :class="{selected: filter === 'all'}" @click.prevent="filter = 'all'">Toutes</a></li>
        <li><a href="#" :class="{selected: filter === 'todo'}" @click.prevent="filter = 'todo'">A faire</a></li>
        <li><a href="#" :class="{selected: filter === 'done'}" @click.prevent="filter = 'done'">Faites</a></li>
      </ul>
      <button class="clear-completed"
              v-show="completed"
              @click.prevent="deleteCompleted">
        Supprimer les tâches finies
      </button>
    </footer>
  </section>
</template>

<script>
export default {
  name: "Todos",
  data() {
    return {
      allDone: true,
      todos: [],
      newTodo: '',
      filter: 'all',
      editing: null
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
    deleteTodo(todo) {
      this.todos = this.todos.filter(e => e !== todo)
    },
    deleteCompleted() {
      this.todos = this.todos.filter(todo => !todo.completed)
    },
    editTodo(todo) {
      this.editing = todo;
    },
    doneEdit() {
      this.editing = null;
    }
  },
  computed: {
    // eslint-disable-next-line vue/no-dupe-keys
    allDone: {
      get() {
        return this.remaining === 0;
      },
      set(value) {
        this.todos.forEach(todo => {
          todo.completed = value;
        })
      }
    },
    completed() {
      return this.getTodosDone.length > 0
    },
    getTodosDone() {
      return this.todos.filter(todo => todo.completed)
    },
    remaining() {
      return this.todos.filter(todo => !todo.completed).length
    },
    filteredTodos() {
      if (this.filter === 'todo') {
        return this.todos.filter(todo => !todo.completed)
      } else if (this.filter === 'done') {
        return this.todos.filter(todo => todo.completed)
      }
      return this.todos
    }
  },
  directives: {
    focus(el, value) {
      if (value) {
        el.focus()
      }

    }
  }
}
</script>

<style src="../Css/todos.css">

</style>
