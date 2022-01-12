<template>
	<div class="py-8 px-1">
		<div class="grid grid-cols-2 text-4xl">
			<div class="box1">Sample Text with 5 words</div>
			<div class="box">
				<img
					class="border"
					src="~/assets/img/fig-1.png"
					width="400"
					height="400"
				/>
			</div>
			<div class="box2">
				<img
					class="border"
					src="~/assets/img/fig-2.png"
					width="500"
					height="450"
				/>
			</div>
			<div class="box2">Sample Text with 5 words</div>
		</div>

		<div class="p-6 flex items-center justify-center bg-blue-600">
			<div class="bg-white rounded-xl py-6 px-8 w-1/2">
				<button
					class="bttn"
					@click="$router.push($routeUrl.RegisterUrl())"
				>
					<strong>REGISTER</strong>
				</button>
				<button
					class="bttn mt-4"
					@click="$router.push($routeUrl.LoginUrl())"
				>
					<strong>LOGIN</strong>
				</button>
			</div>
		</div>
		<div class="grid grid-cols-2 text-4xl">
			<div class="box2">Sample Text with 5 words</div>
			<div
				class="
					px-8
					flex
					items-center
					justify-center
					border border-border-2-light
					text-center
					bg-white
				"
			>
				<img class="border" src="~/assets/img/fig-3.png" width="300" />
			</div>
			<div class="box">
				<img class="border" src="~/assets/img/fig-4.png" width="650" />
			</div>
			<div class="box1">Sample Text with 5 words</div>
			<div class="box2">Sample Text with 5 words</div>
			<div class="box2">
				<img
					class="border"
					src="~/assets/img/fig-5.png"
					width="200"
					height="200"
				/>
			</div>
			<div class="box1">
				<img
					class="border"
					src="~/assets/img/fig-6.png"
					width="300"
					height="450"
				/>
			</div>
			<div class="box1">Sample Text with 5 words</div>
		</div>

		<div class="p-8 px-12 text-white text-2xl">
			<h2><strong>Contact Us</strong></h2>
			<p>700 Twinridge Lane, South Chester, VA 23235</p>
			<p>700-710-0321 | 700-710-0105 | 700-710-2563 (Fax)</p>
			<span><strong>Business Operations:</strong> 700-710-0328</span>
		</div>
	</div>
</template>

<script lang="ts">
import Vue from 'vue'
export default Vue.extend({
	head() {
		return {
			title: 'panel',
		}
	},
})
</script>
<style lang="postcss" scoped>
.box {
	@apply p-8 flex items-center justify-center border border-border-2-light text-center;
}

.box1 {
	@apply box text-white;
}

.box2 {
	@apply box text-primary bg-white;
}

.bttn {
	@apply rounded-4xl p-4 text-center text-white w-full bg-blue-600;
}
</style>