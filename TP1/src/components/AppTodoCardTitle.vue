<template>
    <div>
        <h1>{{ title }}</h1>
    </div>
</template>

<script setup lang="ts">
    interface Props {
        title: string
    }
    const {title} = defineProps<Props>()
</script>

<style scoped>

</style>