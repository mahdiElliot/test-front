<template>
	<container>
		<AuthContainer>
			<AuthFormCard
				title="Log in"
				btnTitle="Log in"
				showSubtitle
				showForgetPassword
				subTitle="no account? register"
				:subTitleLink="$routeUrl.RegisterUrl()"
				showEmail
				showPassword
				v-model="data"
				@submit="submit"
				:secondValidations="{}"
			/>
		</AuthContainer>
	</container>
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
		submit(){
			this.$axios
				.post(this.$apiUrl.LoginUrl(), this.data)
				.then((response) => {
					this.$toast.success(
						`${response.data.username} signed in successfully`,
						'',
						{} as any
					)
					this.$router.replace(this.$routeUrl.PanelUrl())
				}).catch(e => {
					this.$toastErrors(this, e)
				})
		}
	},
})
</script>