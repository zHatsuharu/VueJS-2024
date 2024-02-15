<template>
    <div>
        <input type="checkbox" v-model="done" />
    </div>
</template>

<script setup lang="ts">
    const done = defineModel<boolean>();
</script>

<style scoped>

</style>