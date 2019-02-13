<template>
  <div id="app">
    <Header />
    <AddTodo v-on:add-todo="addTodo" />
    <Todos v-bind:todos="todos" v-on:del-todo="deleteTodo"/>
    <hr />
    <Counter />
    <hr />
    <MonsterSlayer />
  </div>
</template>

<script>
import Header from './components/layout/Header.vue'
import Todos from './components/Todos.vue'
import AddTodo from './components/AddTodo.vue'
import Counter from './components/Counter.vue'
import MonsterSlayer from './components/MonsterSlayer.vue'
import axios from 'axios'

export default {
  name: 'app',
  components: {
    Header,
    Todos,
    AddTodo,
    Counter,
    MonsterSlayer
  },
  data() {
    return {
      todos: []
    }
  },
  methods: {
    deleteTodo(id) {
      this.todos = this.todos.filter(todo => todo.id !== id);
    },
    addTodo(newTodo) {
      const { id, title, completed } = newTodo
      axios.post('https://jsonplaceholder.typicode.com/todos', {
        id,
        title,
        completed
      })
        .then(res => this.todos = [...this.todos, res.data])
        .catch(err => err)
    }
  },
  created() {
    axios.get('https://jsonplaceholder.typicode.com/todos?_limit=5')
      .then(res => this.todos = res.data)
      .catch(err => err)
  }
}
</script>

<style lang="scss">
  #app {
    font-family: 'Avenir', Helvetica, Arial, sans-serif;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    color: #2c3e50;
    margin:  0 auto 60px;

    .btn {
      display: inline-block;
      border: none;
      background: #555;
      color: #fff;
      padding: 8px 20px;
      cursor: pointer;

      &:hover {
        background: #666;
      }
    }
  }
</style>
