<script lang="ts" setup>
import {ref} from "vue";
import type {ITodoItem} from "@/types/todos.ts";
import TodoList from "@/components/TodoList.vue";

let id = 3
let todos = ref<ITodoItem[]>([
  {
    id: 1,
    name: "Learn Vue",
    completed: false,
  },
  {
    id: 2,
    name: "Learn TypeScript",
    completed: true,
  },
  {
    id: 3,
    name: "Learn JavaScript",
    completed: true,
  }
])
let newTodo = ref("")

function addTodo() {
  if (newTodo.value === "") return

  todos.value.push({
    id: id++,
    name: newTodo.value,
    completed: false,
  })
  newTodo.value = ""
}

function removeTodo(todoId: number) {
  todos.value = todos.value.filter((todo) => todo.id !== todoId)
}
</script>

<template>
  <div>
    <div>
      <input v-model="newTodo">
      <button @click="addTodo">
        add todo
      </button>
    </div>
    <TodoList
      :todos="todos"
      @remove-todo="removeTodo"
    />
  </div>
</template>

<style>

</style>
