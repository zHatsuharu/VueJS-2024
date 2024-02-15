<template>
    <div>
        <span>{{ text }}</span>
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