<script setup lang="ts">
const emit = defineEmits(["update:modelValue"])
defineProps<{
	modelValue?: string | number
	label?: string
}>()
</script>

<template>
	<div class="field">
		<label v-if="label" class="label">{{ label }}:</label>
		<input
			:value="modelValue"
			@input="({ target }) => emit('update:modelValue', (target as HTMLInputElement).value)"
		/>
	</div>
</template>

<style scoped lang="css">
.field {
	display: flex;
	gap: 5px;
}
.label {
	font-weight: bold;
	width: 60px;
}
</style>
