<template>
    <div>
        <input type="checkbox" v-model="selected" :disabled=disabled />
    </div>
</template>

<script setup lang="ts">
    interface Props {
        disabled?: boolean
    }
    const {disabled=false} = defineProps<Props>();
    const selected = defineModel<boolean>();
</script>

<style scoped>

</style>