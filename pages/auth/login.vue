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
	methods: {},
})
</script>