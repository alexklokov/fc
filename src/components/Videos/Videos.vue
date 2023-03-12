<template>
	<div class="videos">
		<h2 id="videos">Видео</h2>
		<div class="video__list">
			<Video v-for="video in videos" 
				:img="video.img"
				:link="video.link"
				:title="video.title"
				:source="source"
				@showPopup="showPopup($event)"
			/>
		</div>
	</div>
	<Popup 
		:visible="visiblePopup"
		:title="popupTitle"
		:text="popupText"
		@closePopup="closePopup()"
	/>
</template>

<script>
	import Video from '@/components/Videos/Video.vue'
	import Popup from '@/components/Popup.vue'
	
	export default {
		data() {
			return {
				videos: [],
				visiblePopup: false,
				popupTitle: '',
				popupText: ''
			}
		},
		methods: {
			closePopup() {
				this.visiblePopup = false
				this.popupText = ""
			},
			showPopup(data) {
				this.popupTitle = data.title
				this.popupText = `<iframe src="${data.src}" height=400 width=600 allowfullscreen/>`
				this.visiblePopup = true	
			}
		},
		mounted() {
			fetch(`${this.source}/api/get_videos`)
				.then(r => r.text())
				.then(t => {
					this.videos = JSON.parse(t)
				})
		},
		props: {
			source: String
		},
		components: {
			Video, Popup
		}
	}
</script>

<style lang="sass" scoped>
	.video__list
		display: grid
		grid-template-columns: repeat(4, 1fr)
		grid-template-rows: repeat(4, 1fr)
		grid-gap: 10px
		
		.video:nth-child(1)
			grid-column-start: 1
			grid-column-end: 4
			grid-row-start: 1
			grid-row-end: 4
			
			
</style>