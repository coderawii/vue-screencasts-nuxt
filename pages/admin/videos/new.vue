<template>
<!-- //? **************** /admin/videos/new **************** -->
	<v-container>
		<h1>Video Create Page</h1>
		<VideoEditForm :video="video" :saveVideo="createVideo" buttonText="Create Video" />
	</v-container>
</template>

<script>
import VideoEditForm from '@/components/VideoEditForm.vue'

export default {
	components: {
		VideoEditForm,
	},
	
	data() {
		return {
			video: {}
		}
	},

	methods: {
		async createVideo() {
			let video = await this.$store.dispatch('videos/create', this.video)

			this.$store.dispatch('snackbar/setSnackbar', {text: `You have successfully created a new video, ${video.name}.`})
			this.$router.push(`/admin/videos/${video.id}`);
		}
	},
}
</script>