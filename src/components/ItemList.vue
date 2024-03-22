<script setup lang="ts">
import { defineEmits, defineProps } from "vue"
import type { Product } from "@/types"

const emit = defineEmits(["update:modelValue"])
defineProps<{
	modelValue: Product | null
	items: Product[]
}>()
</script>

<template>
	<div class="list">
		<span
			v-for="item in items"
			:key="item.id"
			class="item"
			:class="{ itemSelected: item.id === modelValue?.id }"
			@click="emit('update:modelValue', item)"
		>
			{{ item.name }}
		</span>
	</div>
</template>

<style lang="css">
.list {
	display: flex;
	flex-direction: column;
	border: 1px solid lightblue;
}

.item {
	padding: 10px;
	cursor: pointer;
	font-size: 20px;
	font-weight: bold;
	min-width: 250px;
}

.itemSelected {
	padding: 10px;
	cursor: pointer;
	font-size: 20px;
	font-weight: bold;
	min-width: 250px;
	background: lightskyblue;
}

.item:hover {
	background: #f0f0ff;
}
</style>
