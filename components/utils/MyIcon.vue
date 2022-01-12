<template>
	<client-only>
		<component :is="'my-' + name" @click="(e) => $emit('click', e)" />
	</client-only>
</template>

<script lang="ts">
import Vue from 'vue'

export type MyIconNameType = 'close' | 'search'

export default Vue.extend({
	components: {
        'my-arrow-left': () => import('~/assets/img/icons/ic_arrow_left.svg')
	},
	props: {
		name: {
			type: String,
			default: () => 'grid',
		},
	},
})
</script>

<style></style>
