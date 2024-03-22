<script setup lang="ts">
import { ref } from "vue"
import ItemContent from "@/components/ItemContent.vue"
import ItemList from "@/components/ItemList.vue"
import Data from "@/api/mockData"
import type { Product } from "@/types"

const data = ref(Data)

const selectedItem = ref<Product | null>(null)
</script>

<template>
	<div class="main">
		<item-list v-model="selectedItem" :items="data" class="sidebar" />
		<item-content v-if="selectedItem" :item="selectedItem" />
	</div>
</template>

<style scoped lang="css">
.main {
	display: flex;
	gap: 20px;
}
.sidebar {
	width: auto;
}
</style>
