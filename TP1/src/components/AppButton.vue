<template>
    <div>
        <button :type="type">{{ text }}</button>
    </div>
</template>

<script setup lang="ts">
    interface Props {
        text: string,
        type: "button" | "submit" | "reset" | undefined,
    }
    const {text, type} = defineProps<Props>()
</script>

<style scoped>

</style>