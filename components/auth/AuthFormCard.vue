<template>
	<div class="bg-white p-8 rounded-lg text-center min-w-100">
		<MyIcon
			v-if="showBack"
			name="arrow-left"
			class="w-8 h-8 cursor-pointer -ms-6"
			@click="$emit('back')"
		/>
		<div class="font-bold text-2xl">{{ title }}</div>
		<div class="mt-8 flex flex-col">
			<TextInput
				v-if="showUsername"
				type="text"
				label="username"
				:value="data.username"
				@change="(v) => changeData('username', { username: v })"
				:validation="getValidation('username')"
			/>
			<TextInput
				v-if="showEmail"
				type="text"
				label="email"
				class="mt-4"
				v-model="data.email"
				@change="(v) => changeData('email', { email: v })"
				:validation="getValidation('email')"
			/>
			<TextInput
				v-if="showPassword"
				type="password"
				label="password"
				class="mt-4"
				:value="data.password"
				@change="(v) => changeData('password', { password: v })"
				:validation="getValidation('password')"
			/>
			<TextInput
				v-if="showRePassword"
				type="password"
				label="confirm password"
				class="mt-4"
				:value="data.rePassword"
				@change="(v) => changeData('repassword', { rePassword: v })"
				:validation="getValidation('repassword')"
			/>
			<hr v-if="showLine" class="w-full mt-4" />
			<TextInput
				v-if="showSocialSecurity"
				type="text"
				label="Social Security number"
				class="mt-4"
				:value="data.SSN"
				@change="(v) => changeData('security', { SSN: v })"
				:validation="getValidation('security')"
			/>
			<TextInput
				v-if="showMobile"
				type="number"
				label="Mobile number"
				class="mt-4"
				:min="1"
				:max="99999999999"
				:value="data.mobile"
				@change="(v) => changeData('mobile', { mobile: v })"
				:validation="getValidation('mobile')"
			/>
			<hr v-if="showLine" class="w-full mt-4" />
			<div v-if="showCode" class="mt-4">
				<label>Please Enter Your Verification Code Here:</label>
				<TextInput
					type="text"
					label="verification code"
					class="mt-4"
					:value="data.code"
					@change="(v) => changeData('code', { code: v })"
					:validation="getValidation('code')"
				/>
			</div>
		</div>
		<button class="mt-6 btn w-full p-3" @click="submit">
			{{ btnTitle }}
		</button>
		<div v-if="showSubtitle" class="mt-3 text-sm">
			<nuxt-link :to="subTitleLink">{{ subTitle }}</nuxt-link>
		</div>
	</div>
</template>

<script lang="ts">
import Vue from 'vue'
import TextInput from '~/components/utils/TextInput.vue'
import MyIcon from '~/components/utils/MyIcon.vue'

export const emptyData = {
	username: '',
	email: '',
	password: '',
	rePassword: '',
	captcha: '',
	captchaKey: '',
	code: '',
	mobile: '',
	SSN: '',
}

export default Vue.extend({
	model: {
		prop: 'data',
		event: 'change',
	},
	components: {
		TextInput,
		MyIcon,
	},
	data() {
		return {
			validations: {} as any,
		}
	},
	props: {
		data: Object,
		title: {
			type: String,
			default: 'Log in',
		},
		btnTitle: {
			type: String,
			default: 'Log in',
		},
		showBack: {
			type: Boolean,
			default: false,
		},
		showUsername: {
			type: Boolean,
			default: false,
		},
		showEmail: {
			type: Boolean,
			default: false,
		},
		showPassword: {
			type: Boolean,
			default: false,
		},
		showRePassword: {
			type: Boolean,
			default: false,
		},
		showLine: {
			type: Boolean,
			default: false,
		},
		showSocialSecurity: {
			type: Boolean,
			default: false,
		},
		showMobile: {
			type: Boolean,
			default: false,
		},
		showCode: {
			type: Boolean,
			default: false,
		},
		showSubtitle: {
			type: Boolean,
			default: false,
		},
		subTitle: {
			type: String,
			default: '',
		},
		subTitleLink: {
			type: String,
			default: null,
		},
		showForgetPassword: {
			type: Boolean,
			default: false,
		},
		secondValidations: {
			type: Object,
			default: () => {},
		},
	},
	methods: {
		changedMobile( d: typeof emptyData | any){
			// this.changeData('mobile', { mobile: v })
		},
		changeData(id: any, d: typeof emptyData | any) {
			this.$emit('change', {
				...this.data,
				...d,
			})
			if (this.validations[id] && this.validations[id].invalid)
				Vue.set(this.validations, id, { invalid: false, error: '' })
		},
		getValidation(id: any) {
			return (
				this.validations[id] ||
				this.secondValidations[id] || {
					invalid: false,
					error: '',
				}
			)
		},
		validate(): boolean {
			let v = true
			if (
				this.showUsername &&
				(!this.data.username || this.data.username.length < 4)
			) {
				v = false
				Vue.set(this.validations, 'username', {
					invalid: true,
					error: 'username length must be more than 4',
				})
			}
			const re = /^.+@.+\..+$/gm
			if (
				this.showEmail &&
				(!this.data.email || re.exec(this.data.email) === null)
			) {
				v = false
				Vue.set(this.validations, 'email', {
					invalid: true,
					error: 'invalid email',
				})
			}
			if (
				this.showPassword &&
				(!this.data.password || this.data.password.length < 6)
			) {
				v = false
				Vue.set(this.validations, 'password', {
					invalid: true,
					error: 'length must 6 or more',
				})
			}
			if (
				this.showRePassword &&
				(!this.data.rePassword ||
					this.data.password !== this.data.rePassword)
			) {
				v = false
				Vue.set(this.validations, 'repassword', {
					invalid: true,
					error: 'must be equal to password',
				})
			}
			if (this.showSocialSecurity && !this.data.SSN) {
				v = false
				Vue.set(this.validations, 'security', {
					invalid: true,
					error: 'security must not be empty',
				})
			}
			if (
				this.showMobile &&
				(!this.data.mobile || this.data.mobile.length !== 11)
			) {
				v = false
				Vue.set(this.validations, 'mobile', {
					invalid: true,
					error: 'mobile length must be 11',
				})
			}
			if (this.showCode && !this.data.code) {
				v = false
				Vue.set(this.validations, 'code', {
					invalid: true,
					error: 'code must not be empty',
				})
			}
			return v
		},
		submit() {
			if (!this.validate()) return
			this.$emit('submit')
		},
	},
})
</script>

<style scoped>
.min-w-100 {
	min-width: 500px;
}
</style>