<script setup lang="ts">
import {ref} from "vue";

let todos = ref(['todo 1', 'todo 2', 'todo 3'])
let newTodo = ref("")

function addTodo() {
  if (newTodo.value === "") return
  todos.value.push(newTodo.value)
}
</script>

<template>
  <div>
    <div>
      <input v-model="newTodo"/>
      <button @click="addTodo">add todo</button>
    </div>
    <div>
      <p :key="todo" v-for="todo in todos">{{ todo }}</p>
    </div>
  </div>

</template>

<style scoped>

</style>
