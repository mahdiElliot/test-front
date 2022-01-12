<template>
	<div
		class="
			materiallabel
			text-sm
			bg-white
			block
			border-2
			focus-within:border-primary focus-within:text-primary
			relative
			duration-300
			rounded-3xl
			min-h-56
		"
		:class="[
			focus
				? 'text-text-primary-dark border-primary'
				: 'text-text-hint-dark',
			invalid ? 'border-red' : 'border-border-2-light',
		]"
	>
		<slot></slot>
		<div
			class="
				materiallabel-ctr
				origin-start
				absolute
				duration-300
				ps-3
				start-0
				top-0
				pointer-events-none
				flex
				items-center
				justify-start
				font-bold
				min-h-58
			"
			:class="{
				'materiallabel-ctr-focus': !isBlank || focus,
			}"
		>
			<span
				class="
					materiallabel-label
					origin-start
					bg-white bg-opacity-0
					px-4
					py-px
					transition-all
					duration-300
					rounded-3xl
				"
				:class="{
					'materiallabel-label-focus': !isBlank || focus,
					'text-primary': focus,
				}"
			>
				<label class="mb-0">
					{{ label }}
				</label>
			</span>
		</div>
	</div>
</template>

<script lang="ts">
import Vue from 'vue'
export default Vue.extend({
	props: {
		value: [String, Number, Boolean],
		label: {
			default: '',
			type: String,
		},
		focus: {
			default: false,
			type: Boolean,
		},
		invalid: {
			default: false,
			type: Boolean,
		},
	},
	computed: {
		isBlank(): boolean {
			return !this.value && this.value !== 0
		},
	},
})
</script>

<style lang="postcss">
.materiallabel:focus-within .materiallabel-ctr,
.materiallabel-ctr-focus {
	transform: translateY(calc(-46px / 2 - 2px)) scale(0.75) !important;
}

.materiallabel:focus-within .materiallabel-label {
	@apply text-primary;
}

.materiallabel:focus-within .materiallabel-label,
.materiallabel-label-focus {
	@apply z-0 font-normal bg-opacity-100;
}

.materiallabel:focus-within .materiallabel-focus {
	@apply border-primary text-primary duration-300;
}

.materiallabel-input {
	@apply px-5 py-2 w-full bg-light-1 outline-none font-bold rounded-3xl text-text-primary-dark flex appearance-none border-0;
	min-height: 46px;
}

.materiallabel-input-height {
	min-height: 46px;
}
.min-h-56 {
	min-height: 44px;
}
.min-h-58 {
	min-height: 46px;
}
</style>
