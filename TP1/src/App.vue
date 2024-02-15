<script setup lang="ts">
import { computed, reactive, ref } from 'vue';
import AppForm from './components/AppForm.vue';
import { TodoType } from './types/todo';
import AppTodoCard from './components/AppTodoCard.vue';
import AppErrorDisplay from './components/AppErrorDisplay.vue';
import AppActions from './components/AppActions.vue';

const todoList = reactive<TodoType[]>([])
const errorMessage = ref("");

function addTodo(newTodo: TodoType) {
  if (lastValidation(newTodo)) {
    errorMessage.value = ""
    todoList.push(newTodo)
  }
}

function deleteTodos() {
  for (let i = todoList.length-1; i >= 0; i--) {
    if (todoList[i].selected) {
      todoList.splice(i, 1)
    }
  }
}

function completeTodos() {
  todoList.forEach(todo => {
    if (todo.selected) {
      todo.done = true;
      todo.selected = false;
    }
  });
}

function editError(message: string) {
  errorMessage.value = message;
}

function lastValidation(newTodo: TodoType): boolean {
  let count = 0;
  let totalTime = newTodo.time;
  todoList.forEach(todo => {
    if (todo.user === newTodo.user && !todo.done) {
      count++;
      totalTime += todo.time
    }
  });
  if (count >= 3) {
    errorMessage.value = "La personne possède déjà 3 tâches."
    return false;
  }
  if (totalTime > 10) {
    errorMessage.value = "Le temps depassera 10h pour cette personne."
    return false;
  }
  return true;
}

const actionsDisabled = computed(() => !todoList.some(todo => todo.selected));
</script>

<template>
  <div>
    <AppForm @create="addTodo" @error="editError"></AppForm>
    <AppActions :disabled="actionsDisabled" @delete="deleteTodos" @completed="completeTodos"></AppActions>
    <AppErrorDisplay :message="errorMessage" v-if="errorMessage.length > 0"></AppErrorDisplay>
    <div class="card-container">
      <AppTodoCard v-for="(todo, index) in todoList"
        :key="index"
        :todo="todo"
        v-model="todo.selected"
        @delete="deleteTodos"
      ></AppTodoCard>
    </div>
  </div>
</template>

<style scoped>
.card-container {
  display: flex;
  gap: 20px;
  margin: 30px;
}
</style>
