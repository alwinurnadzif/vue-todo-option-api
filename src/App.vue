<template>
  <div id="wrapper">
    <div class="container">
      <div class="row justify-content-center">
        <div class="col-12 col-lg-5">
          <div class="card border-0 shadow mt-4">
            <div class="card-body">
              <div class="d-flex">
                <h3>Todo List</h3>
              </div>
              <div class="d-flex gap-2 mb-4">
                <input v-model="inputTodo" type="text" class="form-control" @keyup.enter="addTodo" >
                <button class="btn btn-primary" @click="addTodo">Add</button>
              </div>
              <TodoList @toggleTodoDone="toggleTodoDone" @removeTodo="removeTodo" :todos="todos" />
              <div class="d-flex mt-3 mb-0">
                <span>Total Todo {{ totalTodo }}</span>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
  {{ todos }}
</template>

<script>
import TodoList from "./components/TodoList.vue"

function generateId() {
  return Math.floor(Math.random() * 10_000);
}

export default {
  data() {
    return {
      inputTodo: "",
      todos: []
    }
  },
  components: {
    TodoList
  },
  methods: {
    toggleTodoDone(index) {
      this.todos[index].isDone = !this.todos[index].isDone;
      this.saveTodosToLocalStorage()
    },
    addTodo() {
      const todo = { id: generateId(), task: this.inputTodo, isDone: false }
      this.todos.unshift(todo);
      this.inputTodo = ""
      this.saveTodosToLocalStorage()
    },
    removeTodo(todoIndex) {
      this.todos = this.todos.filter((todo, index) => todoIndex != index)
      this.saveTodosToLocalStorage()
    },
    saveTodosToLocalStorage() {
      localStorage.setItem("todos", JSON.stringify(this.todos));
    }
  },
  computed: {
    totalTodo() {
      return this.todos.length;
    }
  },
  mounted() {
    this.todos = JSON.parse(localStorage.getItem("todos"));
  }
} 
</script>

