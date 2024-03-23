<script setup lang="ts">
const emit = defineEmits(["update:modelValue"])
defineProps<{
	modelValue?: string | number
	items: string[]
	label?: string
}>()
</script>

<template>
	<div class="field">
		<label v-if="label" class="label">{{ label }}:</label>
		<select :value="modelValue" @change="emit('update:modelValue')">
			<option v-for="(item, idx) in items" :key="idx">
				{{ item }}
			</option>
		</select>
	</div>
</template>

<style scoped lang="css">
.field {
	display: flex;
	gap: 5px;
}
.label {
	width: 60px;
}
</style>
