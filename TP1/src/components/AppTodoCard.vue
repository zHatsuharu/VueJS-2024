<template>
    <div class="card" :class="{'card-done' : todo.done}">
        <AppTodoCardCheck v-model="selected" :disabled="todo.done"></AppTodoCardCheck>
        <AppTodoCardTitle :title="todo.title"></AppTodoCardTitle>
        <AppTodoCardContent :text="todo.content"></AppTodoCardContent>
        <AppTodoCardText :text="'Estimated time : ' + todo.time + ' h'"></AppTodoCardText>
        <AppTodoCardText :text="'Assign : ' + todo.user"></AppTodoCardText>
        <AppButton v-if="!todo.done" text="Modifier" type="button"></AppButton>
    </div>
</template>

<script setup lang="ts">
import AppTodoCardTitle from './AppTodoCardTitle.vue';
import type {TodoType} from '../types/todo';
import AppTodoCardContent from './AppTodoCardContent.vue';
import AppTodoCardText from './AppTodoCardText.vue';
import AppTodoCardCheck from './AppTodoCardCheck.vue';
import AppButton from './AppButton.vue';

    const selected = defineModel<boolean>()

    interface Props {
        todo: TodoType
    }
    const {todo} = defineProps<Props>()
</script>

<style scoped>
.card {
    box-shadow: 0px 0px 10px 4px rgba(0,0,0,0.3);
    -webkit-box-shadow: 0px 0px 10px 4px rgba(0,0,0,0.3);
    -moz-box-shadow: 0px 0px 10px 4px rgba(0,0,0,0.3);
    border: 2px solid #b4b4b4;
    border-radius: 20px;
    padding: 15px;
}
.card-done {
    border: 2px solid #62eb3c !important;
}
</style>