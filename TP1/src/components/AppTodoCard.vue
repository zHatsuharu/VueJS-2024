<template>
    <div>
        <AppTodoCardTitle :title="todo.title"></AppTodoCardTitle>
        <AppTodoCardContent :text="todo.content"></AppTodoCardContent>
        <AppTodoCardText :text="'Estimated time : ' + todo.time + ' h'"></AppTodoCardText>
        <AppTodoCardText :text="'Assign : ' + todo.user"></AppTodoCardText>
        <AppTodoCardCheck v-model="done"></AppTodoCardCheck>
        <AppButton text="Supprimer" type="button" @click="$emit('delete', todo)"></AppButton>
    </div>
</template>

<script setup lang="ts">
import AppTodoCardTitle from './AppTodoCardTitle.vue';
import type {TodoType} from '../types/todo';
import AppTodoCardContent from './AppTodoCardContent.vue';
import AppTodoCardText from './AppTodoCardText.vue';
import AppTodoCardCheck from './AppTodoCardCheck.vue';
import AppButton from './AppButton.vue';

    const done = defineModel<boolean>()

    interface Props {
        todo: TodoType
    }
    const {todo} = defineProps<Props>()

    type Emit = {
        delete: [todo: TodoType]
    }
    defineEmits<Emit>()
</script>

<style scoped>

</style>