<template>
<!-- //? **************** /tags/88 **************** -->
	<v-container>
	<!-- **************** /tags/5 **************** -->
		<h1 class="display-3 ma-4 d-flex justify-center">Videos with Tag "{{ tag.name }}" </h1>

		<VideoTable :videos="videosOnTag" :headers="headers" />

		<!-- <div class="d-flex flex-wrap justify-center">
			<div v-for="video in videosOnTag" :key="video.id">
				<VideoListVideo :video="video" :tags="tags"></VideoListVideo>
			</div>
		</div> -->
	</v-container>
</template>

<script>
// import VideoListVideo from '@/components/VideoListVideo'
import VideoTable from '@/components/VideoTable'
import { mapState } from 'vuex'

export default {
	components: { 
		// VideoListVideo,
		VideoTable
	},

	// async fetch({store, params, from}) { // ovo from nam kazuje koja je ruta s koje dolazimo
	// // debugger
	// 	console.log(from)
	// 	let isInitialPageLoad = !from
	// 	console.log(isInitialPageLoad) // ovo je ugl false

	// 	if(isInitialPageLoad) { // sad se mnoooogo brze ucitava sve, tj valjda se koristi vec uctiano kada koristimo iste pdoatke, ne razumem, dakle ako page s koje dolazimo na ovu komponentu nije insta kao ova, onda ucitavamo opet videe i tagove ili sta
	// 		await store.dispatch('loadAllVideos')
	// 		await store.dispatch('loadAllTags')
	// 	}
	// 	// await store.dispatch('loadTagAndRelationships', { tagID: params.id })




	// 	// let response = await $axios.get(`/tags/${params.id}`)

	// 	// let tag = response.data.data
	// 	// tag.attributes.id = tag.id

	// 	// let videosOnTag = response.data.included.filter(i => i.type === 'video') // ovo ce da vrati nekoliko videa. svakom tom videu ce trebati tag_ids niz koji bi im trebalo dodati bas kao u home page (pages/index.vue):
	// 	// videosOnTag.forEach(v => {
	// 	// 	v.attributes.tag_ids = v.relationships.tags.data.map(t => t.id)
	// 	// })

	// 	// let tags = response.data.included.filter(i => i.type === 'tag')
	// 	// tags.forEach(t => {
	// 	// 	t.attributes.id = t.id
	// 	// })

		
	// 	// // debugger
	// 	// return {
	// 	// 	tag: tag.attributes,
	// 	// 	videosOnTag: videosOnTag.map(vot => vot.attributes),
	// 	// 	tags: tags.map(t => t.attributes) // ovi attributes nemaju id included kao video pa smo im zato morali da dodeliti id sa tags.forEach
	// 	// }
	// },

	computed: {
		...mapState({
			tags: state => state.tags.tags,
			videos: state => state.videos.videos
		}),

		videosOnTag() {
			return this.videos.filter(vot => {
				return this.tag.video_ids.includes(vot.id.toString()) // dakle vrati sve videe koji u sebi sadrze tagove koji u sebi imaju id odredjenih videa
			})
		},

		tag() {
			return this.tags.find(t => t.id == this.$route.params.id)
		},

		headers() {
			return [
				{text: 'Played', value: 'played', sortable: false, width: "70px"},
				{text: 'Name', value: 'name'},
				// {text: 'Date', value: 'published_at'},
				{text: 'Date', value: 'sortable_published_at'},
				{text: 'Duration', value: 'duration'},
				{text: 'Tags', value: 'tags', sortable: false},
			]
		},
	},
}
</script>