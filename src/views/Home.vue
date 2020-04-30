<template>
  <div class="container">
    <div class="row">
      <div class="col-12 py-5">
        <h1>{{ listName }}</h1>
      </div>
    </div>
    <div class="row mb-3">
      <create-todo @on-new-todo="addTodo($event)"></create-todo>
    </div>
    <div class="row">
      <div class="col-12 col-sm-10 col-lg-6">
        <ul class="list-group">
          <todo
            v-for="(todo, index) in todos"
            :key="index"
            :description="todo.description"
            :completed="todo.completed"
            @on-toggle="toggleTodo(todo)"
            @on-delete="deleteTodo(todo)"
            @on-edit="editTodo(todo, $event)"
          />
        </ul>
      </div>
    </div>
  </div>
</template>

<script>
// @ is an alias to /src
import CreateTodo from '@/components/CreateTodo.vue'
import Todo from '@/components/Todo.vue'

export default {
  name: 'Home',
  props: {
    listName: String
  },
  data() {
    return {
      todos: [
        {
          description: "我和你网站搜索功能",
          completed: true
        },
        {
          description: "我和你网站公司介绍",
          completed: false
        },
        {
          description: "资天风水内容添加",
          completed: false
        }
      ]
    };
  },
  components: {
    CreateTodo,
    Todo
  },
  methods: {
    addTodo(newTodo) {
      this.todos.push({ description: newTodo, completed: false });
    },
    toggleTodo(todo) {
      todo.completed = !todo.completed;
    },
    deleteTodo(deletedTodo) {
      this.todos = this.todos.filter(todo => {
        todo !== deletedTodo
      });
    },
    editTodo(todo, newTodoDescription) {
      todo.description = newTodoDescription;
    }
  }
}
</script>
