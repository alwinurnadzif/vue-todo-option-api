<template>
  <ul class="list-group">
    <li class="list-group-item" v-for="(todo, index) in todos" :key="todo.id">
      <input type="checkbox" class="form-check-input" :checked="todo.isDone" @change="done(index)">
      <p :class="{ done: todo.isDone }">{{ todo.task }}</p>
      <div class="ms-auto">
        <button class="btn btn-danger btn-sm" @click="remove(index)">x</button>
      </div>
    </li>
  </ul>
</template>

<script>
export default {
  props: {
    todos: {
      type: Array,
      default: []
    }
  },
  emits: ["toggleTodoDone", "removeTodo"],
  methods: {
    done(index) {
      this.$emit("toggleTodoDone", index)
    },
    remove(index) {
      this.$emit("removeTodo", index);
    }
  }
}
</script>

<style scoped>
.list-group-item {
  border: 1px solid #ced4da;
  margin: .2rem 0;
  border-radius: .375rem;
  padding: .5rem;
  display: flex;
  align-items: center;
  gap: .5rem;
}

.list-group-item p {
  margin-bottom: 0;
}

.form-check-input {
  margin-top: 0;
}

.done {
  text-decoration: line-through;
}
</style>
