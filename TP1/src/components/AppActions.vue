<template>
	<div class="actions-container">
		<AppButton type="button" text="Compléter" @click="$emit('completed')" :disabled="disabled"></AppButton>
		<AppButton type="button" text="Supprimer" @click="$emit('delete')" :disabled="disabled"></AppButton>
	</div>
</template>

<script setup lang="ts">
import AppButton from './AppButton.vue';

	interface Props {
		disabled?: boolean
	}
	const {disabled=true} = defineProps<Props>();

	type Emit = {
        delete: []
		completed: []
    }
    defineEmits<Emit>();
</script>

<style scoped>
.actions-container {
	display: flex;
	flex-direction: row;
	gap: 5px;
}
</style>