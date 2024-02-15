<template>
    <div>
        <button :type="type" :disabled=disabled>{{ text }}</button>
    </div>
</template>

<script setup lang="ts">
    interface Props {
        text: string,
        type?: "button" | "submit" | "reset" | undefined,
        disabled?: boolean
    }
    const {text, type="button", disabled=false} = defineProps<Props>()
</script>

<style scoped>

</style>