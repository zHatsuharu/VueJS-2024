<template>
    <div>
        <input type="number" min="0" max="10" v-model="time" :required="req" />
    </div>
</template>

<script setup lang="ts">
    interface Props {
        req: boolean
    }
    const {req} = defineProps<Props>();
    const time = defineModel();
</script>

<style scoped>

</style>