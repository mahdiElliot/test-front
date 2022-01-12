<template>
	<div class="w-full h-full flex justify-center items-center p-8 mt-16">
		<img src="~/assets/img/light.png" class="mr-6" />
		<slot></slot>
	</div>
</template>

<script lang="ts">
import Vue from 'vue'
export default Vue.extend({
	head(){
		return {
			title: 'auth'
		}
	}
})
</script>