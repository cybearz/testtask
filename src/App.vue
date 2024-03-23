<script setup lang="ts">
import Data from "@/api/mockData"
import ItemContent from "@/components/ItemContent.vue"
import ItemList from "@/components/ItemList.vue"
import type { Product } from "@/types"
import { ref } from "vue"

const data = ref(Data)

const selectedItem = ref<Product | null>(null)
</script>

<template>
	<main>
		<item-list v-model="selectedItem" :items="data" class="sidebar" />
		<item-content v-if="selectedItem" :item="selectedItem" class="content" />
	</main>
</template>

<style scoped lang="css">
main {
	display: flex;
	gap: 20px;
	height: 100vh;
}
.sidebar {
	width: auto;
	height: 100%;
}
.content {
	overflow-y: auto;
	width: 100%;
}
</style>
