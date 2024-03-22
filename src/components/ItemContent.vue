<script setup lang="ts">
import type { Product } from "@/types"
import { defineProps, ref, watch } from "vue"

const props = defineProps<{
	item: Product
}>()

//todo типизировать
const selectType = ref("color")

const innerItem = ref<Product | null>(null)

watch(
	() => props.item,
	(item) => {
		innerItem.value = {
			...item,
			attributes: [...item.attributes],
		}
	},
	{ immediate: true, deep: true }
)

const addAttr = () => {
	const type = selectType.value
	console.log("type", type)
	switch (type) {
		case "color": {
			innerItem.value?.attributes.push({
				code: "new code",
				name: "new field",
				color: "color",
			})
			break
		}
		case "size": {
			innerItem.value?.attributes.push({
				code: "new code",
				name: "new field",
				size: {
					width: 0,
					height: 0,
				},
			})
			break
		}
		case "weight": {
			innerItem.value?.attributes.push({
				code: "new code",
				name: "new field",
				weight: 0,
			})
			break
		}
	}
}
</script>

<template>
	<div class="content">
		<span class="header"> {{ item.name }}</span>

		<div
			class="detail"
			v-for="(attr, idx) in innerItem?.attributes"
			:key="`attr.code-${idx}`"
		>
			<div class="field">
				<span class="title">code:</span>
				<input :value="attr.code" />
			</div>

			<div class="field">
				<span class="title">name:</span>
				<input :value="attr.name" />
			</div>

			<div v-if="'color' in attr" class="field">
				<span class="title">color:</span>
				<input :value="attr.color" />
			</div>

			<div v-if="'size' in attr" class="field">
				<span class="title">size:</span>
				<span>
					<input :value="attr.size.width" type="number" /> x
					<input :value="attr.size.height" type="number" />
				</span>
			</div>

			<div v-if="'weight' in attr" class="field">
				<span class="title">weight:</span>
				<input :value="attr.weight" type="number" />
			</div>
		</div>

		<div class="add">
			<label for="select">type</label>
			<select id="select" v-model="selectType">
				<option>color</option>
				<option>size</option>
				<option>weight</option>
			</select>

			<button @click="addAttr">Add</button>
		</div>
	</div>
</template>

<style scoped lang="css">
.header {
	font-weight: bold;
}
.content {
	display: flex;
	flex-direction: column;
	padding: 20px;
	gap: 20px;
}
.detail {
	padding: 10px;
	display: flex;
	flex-direction: column;
	gap: 10px;
}
.field {
	display: flex;
	gap: 5px;
}
.title {
	font-weight: bold;
}
.add {
	display: flex;
	gap: 10px;
}
</style>
