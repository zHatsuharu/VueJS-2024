<script setup lang="ts">
import { reactive, ref } from 'vue';
import AppForm from './components/AppForm.vue';
import { TodoType } from './types/todo';
import AppTodoCard from './components/AppTodoCard.vue';
import AppErrorDisplay from './components/AppErrorDisplay.vue';

const todoList = reactive<TodoType[]>([])
const errorMessage = ref("");

function addTodo(newTodo: TodoType) {
  if (lastValidation(newTodo)) {
    errorMessage.value = ""
    todoList.push(newTodo)
  }
}

function deleteTodo(todoToRemove: TodoType) {
  const index = todoList.indexOf(todoToRemove);
  todoList.splice(index, 1);
}

function editError(message: string) {
  errorMessage.value = message;
}

function lastValidation(newTodo: TodoType): boolean {
  let count = 0;
  let totalTime = newTodo.time;
  todoList.forEach(todo => {
    if (todo.user === newTodo.user) {
      count++;
      totalTime += todo.time
    }
  });
  if (count > 3) {
    errorMessage.value = "La personne possède déjà 3 tâches."
    return false;
  }
  if (totalTime > 10) {
    errorMessage.value = "Le temps depassera 10h pour cette personne."
    return false;
  }
  return true;
}
</script>

<template>
  <div>
    <AppForm @create="addTodo" @error="editError"></AppForm>
    <AppErrorDisplay :message="errorMessage" v-if="errorMessage.length > 0"></AppErrorDisplay>
    <div v-for="(todo, index) in todoList" :key="index">
      <AppTodoCard :todo="todo" v-model="todo.done" @delete="deleteTodo"></AppTodoCard>
    </div>
  </div>
</template>

<style scoped>
</style>
