<template>
<!-- //? **************** /admin/videos **************** -->
	<v-container grid-list-xs>
		<h1>Video List</h1>
		<v-btn text to="/admin/videos/new" color="#00c58e">Add Video</v-btn>

		<VideoTable 
			:videos="videos"
			:headers="headers"
			:customClickAction="goToVideoShow"
			:dense="true"
			:itemsPerPage="20"
		 />



	<!-- //? PRE VIDEOTABLE KOMPONENTE -->
		<!-- <div class="flex-table">
			<div>Name</div>
			<div>Description</div>
			<div>Actions</div>
		</div>

		<div v-for="video in videos" :key="video.id" class="flex-table">
			<div>{{ video.name }}</div>
			<div>{{ video.description | abbreviate}}</div>
			<div class="actions">
				<router-link :to="`/watch/${video.id}`">Watch</router-link> 
				<router-link :to="`/admin/videos/${video.id}`">Show</router-link>
				<router-link :to="`/admin/videos/${video.id}/edit`">Edit</router-link>
				<v-btn @click="deleteVideo(video)" x-small color="red white--text">Delete</v-btn>
			</div>
		</div> -->
	</v-container>
</template>

<script>
import { mapState } from 'vuex'
import VideoTable from "@/components/VideoTable";
export default {
	name: 'AdminVideoList',
	components: {
		VideoTable,
	},

	computed: {
		...mapState({
			videos: s => s.videos.videos
		}),

		headers() {
			return [
				{text: 'Name', value: 'name'},
				{text: 'Date', value: 'sortable_published_at'},
				{text: 'Duration', value: 'duration'},
				{text: 'Tags', value: 'tags', sortable: false},
				{text: 'Actions', value: 'actions', sortable: false, width: "300px"}, //! i s obzirom na to da u videos (iliti items) nemamo ovaj property actions, moramo kreirati slot za ovo u VideoTable.vue
			]
		},
		
	},

	// filters: {
	// 	abbreviate(text) {
	// 		if(text) {
	// 			text = text.replace('<p>', '');
	// 			// return text && text.slice(0, 50)
	// 			return text.slice(0, 50)
	// 		}
	// 	}
	// },

	methods: {
		// deleteVideo(video) {
		// 	let response = confirm(`Are you sure you want to delete "${video.name}"?`)

		// 	if(response) {
		// 		this.$store.dispatch('videos/delete', video)
		// 		this.$store.dispatch('snackbar/setSnackbar', { text: `You have successfully deleted your video, "${video.name}" ` })
		// 	}
		goToVideoShow(video) {
			this.$router.push(`/admin/videos/${video.id}`)
		}
	}
}
</script>

<style scoped>
.flex-table {
	display: grid;
	grid-template-columns: repeat(auto-fill, 33%);
	padding: 10px;
	/* border-bottom: 1px solid silver; */
}

.flex-table:nth-of-type(2n) {
	background-color: #dedede;
}

.actions * {
	margin: 0 5px;
}
</style>