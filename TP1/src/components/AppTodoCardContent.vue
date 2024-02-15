<template>
    <div>
        <p>{{ text }}</p>
    </div>
</template>

<script setup lang="ts">
interface Props {
    text: string
}
const {text} = defineProps<Props>()
</script>

<style scoped>

</style>