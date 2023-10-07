<script setup lang="ts">
import type {ITodoItem} from "@/types/todos.ts";
import {ref} from "vue";

let prop = defineProps<{todo: ITodoItem}>()
const emit = defineEmits<{
  (e: "remove-todo", id: number): void;
  (e: "on-completed", isDone: boolean): void;
}>()
const isDone = ref(prop.todo.completed)

</script>

<template>
  <p
    :class="{done: todo.completed}"
  >
    {{ todo.name }}
    <input
      v-model="isDone"
      type="checkbox"
      @change="emit('on-completed', isDone)"
    >
    <button @click="emit('remove-todo', todo.id)">
      delete
    </button>
  </p>
</template>

<style scoped>
.done {
  text-decoration: line-through;
}
</style>