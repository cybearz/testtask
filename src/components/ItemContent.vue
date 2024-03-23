<script setup lang="ts">
import BaseField from "@/components/BaseField.vue"
import BaseSelect from "@/components/BaseSelect.vue"
import InputSize from "@/components/InputSize.vue"
import type { Product } from "@/types"
import _ from "lodash"
import { reactive, ref, watch } from "vue"

const ATTR_FIELDS_OBJ = {
	color: {
		color: "color",
	},
	size: {
		size: {
			width: 0,
			height: 0,
		},
	},
	weight: {
		weight: 0,
	},
}

const props = defineProps<{
	item: Product
}>()

const type = reactive({
	items: ["color", "size", "weight"],
	selected: "color" as "color" | "size" | "weight",
})
const innerItem = ref<Product | null>(null)

watch(
	() => props.item,
	(item) => {
		innerItem.value = _.cloneDeep(item)
	},
	{ immediate: true, deep: true }
)

const addAttr = () =>
	innerItem.value?.attributes.push({
		code: "new code",
		name: "new field",
		...ATTR_FIELDS_OBJ[type.selected],
	})
</script>

<template>
	<div class="content">
		<h3 class="header">{{ innerItem?.name }}</h3>
		<div
			class="detail"
			v-for="(attr, idx) in innerItem?.attributes"
			:key="`attr.code-${idx}`"
		>
			<BaseField v-model="attr.code" label="code" />

			<BaseField v-model="attr.name" label="name" />

			<BaseField v-if="'color' in attr" v-model="attr.color" label="color" />

			<BaseField v-if="'weight' in attr" v-model="attr.weight" label="weight" />

			<InputSize
				v-if="'size' in attr"
				v-model:width="attr.size.width"
				v-model:height="attr.size.height"
				label="weight"
			/>
		</div>

		<div class="add">
			<BaseSelect v-model="type.selected" :items="type.items" label="type" />
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
.add {
	margin-top: 10px;
	display: flex;
	gap: 10px;
}
</style>
