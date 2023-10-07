<script lang="ts" setup>
import {computed, ref} from "vue";
import TodoItem from "@/components/TodoItem.vue";
import type {ITodoItem} from "@/types/todos";


let selected = ref("all");
let prop = defineProps<{ todos: ITodoItem[] }>()
let emit = defineEmits<{
  (e: "remove-todo", id: number): void;
}>()
let showingTodos = computed(() => {
  if (selected.value === "all") {
    return prop.todos;
  }
  return prop.todos.filter((todo) => todo.completed);
})
</script>

<template>
  <div>
    <div>
      <select v-model="selected">
        <option value="all">
          All
        </option>
        <option value="completed">
          Completed
        </option>
      </select>
    </div>
    <div>
      <TodoItem
        v-for="todo in showingTodos"
        :key="todo.id"
        :todo="todo"
        @on-completed="todo.completed = $event"
        @remove-todo="emit('remove-todo', todo.id)"
      />
    </div>
  </div>
</template>