<template>
	<div>
		<MaterialLabel
		:label="label"
		:value="value"
		@click="$emit('click')"
		:invalid="validation.invalid"
		class="textinput"
		:class="{ 'pointer-events-none opacity-75': disabled }"
	>
		<input
			v-if="type == 'text' || type == 'password'"
			:type="type === 'password' ? 'password' : 'text'"
			:name="name"
			class="materiallabel-input"
			:disabled="disabled"
			placeholder=" "
			@input="onChange"
			:value="value"
		/>
		<input
			v-else-if="type === 'number'"
			type="text"
			:min="min"
			:max="max"
			:name="name"
			class="materiallabel-input"
			:disabled="disabled"
			placeholder=" "
			@input="onChange"
			:value="value"
		/>
		<select
			v-else-if="type == 'select'"
			:name="name"
			placeholder=" "
			class="materiallabel-input bg-transparent"
			required
			@change="(e) => $emit('change', e.target.value)"
		>
			<option selected disabled class="hidden" value=""></option>
			<option
				v-for="(option, index) in options"
				:key="index"
				:value="optionValue ? option[optionValue] : option"
				:selected="
					(optionValue ? option[optionValue] : option) == value
				"
			>
				{{ option && (optionName ? option[optionName] : option) }}
			</option>
		</select>
		<div
			v-if="endIcon"
			class="
				textinput-icon
				absolute
				duration-300
				end-0
				top-0
				bottom-0
				pointer-events-none
				flex
				items-center
				justify-center
			"
		>
			<MyIcon :name="endIcon" class="w-8 h-8 me-5" />
		</div>
	</MaterialLabel>
	<div v-if="validation.invalid" class="text-left ml-6 mt-1 text-red text-sm">
		<span>invalid: </span><span>{{validation.error}}</span>
	</div>
	</div>
</template>

<script lang="ts">
import Vue, { PropOptions } from 'vue'
import MaterialLabel from '~/components/utils/MaterialLabel.vue'
import MyIcon, { MyIconNameType } from '~/components/utils/MyIcon.vue'

export default Vue.extend({
	components: {
		MyIcon,
		MaterialLabel,
	},
	model: {
		prop: 'value',
		event: 'change',
	},
	data() {
		return {
			id: null,
			show: false,
		}
	},
	mounted() {
		// @ts-ignore
		this.id = `textinput-${this._uid}`
	},
	props: {
		value: [String, Number],
		name: {
			default: '',
			type: String,
		},
		label: {
			default: '',
			type: String,
		},
		type: {
			default: 'text',
			type: String,
		} as PropOptions<'text' | 'number' | 'select' | 'password'>,
		options: {
			default: null,
			type: Array,
		} as PropOptions<any[]>,
		disabled: {
			type: Boolean,
			default: false,
		},
		endIcon: {
			default: null,
			type: String,
		} as PropOptions<MyIconNameType>,
		optionName: {
			default: null,
			type: [String, Number],
		},
		optionValue: {
			default: null,
			type: [String, Number],
		},
		min: {
			default: 1,
			type: Number,
		},
		max: {
			default: 10,
			type: Number,
		},
		validation: {
			type: Object,
			default: () => ({
				invalid: false,
				error: 'invalid input'
			})
		}
	},
	methods: {
		numberChange(e: any) {},
		persianNumberToEnglish(v: string) {
			let r = []
			for (let i = 0; i < v.length; i++)
				if (v.charCodeAt(i) >= 1776 && v.charCodeAt(i) <= 1785)
					r.push(String.fromCharCode(v.charCodeAt(i) - 1728))
				else r.push(v[i])

			return r.join('')
		},
		onChange(e: any): void {
			const v = (e.target?.value || '') as string
			if (this.type === 'number') {
				const t = this.persianNumberToEnglish(v)
				if (isNaN(Number(t)) || Number(t) > this.max) {
					e.target.value = ''
					return
				}
				this.$emit('input', e)
				this.$emit('change', t)
				return
			}

			const value = e.target.value
			this.$emit('input', e)
			this.$emit('change', value)
		},
	},
})
</script>

<style lang="postcss" scopped>
.textinput .textinput-icon {
	@apply text-black;
}
.textinput:focus-within .textinput-icon {
	@apply text-black;
}
</style>
