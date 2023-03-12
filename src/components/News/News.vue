<template>
	<h2 id="news">Новости</h2>
	<div class="news-list">
	<NewsItem v-for="newsItem in news" 
		:title="newsItem.title" 
		:preview="newsItem.preview_text" 
		:img="newsItem.img"
		:source="source"
		:link="newsItem.link"
		@showPopup="showPopup($event)"	
	/>
		
	<Popup 
		:visible="visiblePopup"
		:title="popupTitle"
		:text="popupText"
		@closePopup="closePopup()"
	/>
	</div>
</template>

<script>
	import NewsItem from "@/components/News/NewsItem.vue"
	import Popup from '@/components/Popup.vue'
	
	export default {
		data() {
			return {
				news: [],
				visiblePopup: false,
				popupTitle: '',
				popupText: ''
			}
		},
		methods: {
			closePopup() {
				this.visiblePopup = false
			},
			showPopup(data) {
				this.popupTitle = data.title
				this.popupText = data.text
				this.visiblePopup = true	
			}
		},
		mounted() {
			fetch(`${this.source}/api/posts`)
				.then(r => r.text())
				.then(t => {
					const news = JSON.parse(t.trim())
					this.news = news
				})
		},
		props: {
			source: String	
		},
		components: {
			NewsItem, Popup
		}
	}
</script>


<style lang="sass" scoped>
	.news-list
		display: grid
		grid-template-columns: repeat(4, 1fr)
		grid-column-gap: 20px
		grid-row-gap: 40px
	
		@media (max-width: 1024px)
			grid-template-columns: repeat(3, 1fr)
		
		@media (max-width: 800px)
			grid-template-columns: 1fr 1fr
			
		@media (max-width: 540px)
			grid-template-columns: 1fr
</style>