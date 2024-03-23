<script setup lang="ts">
const emit = defineEmits(["update:width", "update:height"])
defineProps<{
	width: number
	height: number
}>()
</script>

<template>
	<div class="field">
		<label class="label">size:</label>
		<input
			:value="width"
			@input="({ target }) => emit('update:width', Number((target as HTMLInputElement).value))"
			type="number"
		/>
		x
		<input
			:value="height"
			@input="({ target }) => emit('update:height', Number((target as HTMLInputElement).value))"
			type="number"
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
