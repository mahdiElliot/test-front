<template>
	<AuthContainer>
		<AuthFormCard
			title="Register"
			btnTitle="Register with email"
			showSubtitle
			subTitle="login"
			:subTitleLink="$routeUrl.LoginUrl()"
			showUsername
			showEmail
			showPassword
			showRePassword
			showLine
			showSocialSecurity
			showMobile
			showCode
			v-model="data"
			@submit="submit"
			:secondValidations="{}"
		/>
	</AuthContainer>
</template>

<script lang="ts">
import Vue from 'vue'
import AuthContainer from '~/components/auth/AuthContainer.vue'
import AuthFormCard from '~/components/auth/AuthFormCard.vue'
import TextInput from '~/components/utils/TextInput.vue'

export default Vue.extend({
	components: {
		AuthContainer,
		AuthFormCard,
		TextInput,
	},
	data() {
		return {
			data: {} as any,
		}
	},
	methods: {
		submit() {
			this.$axios
				.post(this.$apiUrl.UsersUrl(), this.data)
				.then((response) => {
					this.$toast.success(
						`${response.data.username} saved successfully`,
						'',
						{} as any
					)
				}).catch(e => {
					this.$toastErrors(this, e)
				})
		},
	},
})
</script>