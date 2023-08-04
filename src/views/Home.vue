<template>
	<PageContainer>
		<VCard class="pa-8">
			<h2 class="text-h6 font-weight-bold primary--text mb-4">
				{{ $t('views.home.title') }}
			</h2>

			<p>{{ $t('views.home.description.block1') }}</p>

			<p>{{ $t('views.home.description.block2') }}</p>

			<RouterLink
				:to=" {
					name: 'about'
				}"
				data-cy="aboutLink"
			>
				{{ $t('views.home.about.label') }}
			</RouterLink>

			<VSpacer />

			<VBtn
				color="accent"
				outlined
				height="auto"
				min-height="36px"
				class="text-wrap mt-8"
				data-cy="sendNotification"
				@click="sendNotification"
			>
				{{ $t('views.home.sendNotification') }}
			</VBtn>
		</VCard>
	</PageContainer>
</template>

<script lang="ts">
	import Vue from 'vue';
	import Component from 'vue-class-component';

	import { Meta, MetaInfo } from '@/decorators';

	import { mapActions } from 'vuex';

	@Component({
		// Vuex bindings
		methods: mapActions('notification', ['addNotification'])
	})
	export default class Home extends Vue {
		/* istanbul ignore next */
		sendNotification(): void {
			this.addNotification({
				type: 'success',
				message: 'Exemple de notification'
			});
		}

		/* istanbul ignore next */
		@Meta
		metaInfo(): MetaInfo {
			return {
				title: this.$t('views.home.meta.title') as string,
				meta: [
					{
						name: 'description',
						vmid: 'description',
						content: this.$t('views.home.meta.description') as string
					}
				]
			};
		}
	}
</script>
