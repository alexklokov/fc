<template>
	<div class="news-item" @click="showPopup()">
		<div class="news-item__img">
			<img :src="img" :alt="title">
		</div>
		<div class="news-item__title">
			{{ title }}
		</div>
		<div class="news-item__preview">
			{{ preview }}
		</div>
		
	</div>
</template>

<script>
	
	export default {
		data() {
			return {
				text: ''
			}
		},
		props: {
			img: String,
			title: String,
			link: String,
			preview: {
				required: false,
				type: String
			},
			source: String,
		},
		methods: {
			showPopup() {
				const data = {
					title: this.title,
				}
				if(this.text) {
					this.$emit('showPopup', {...data,
						text: this.text
					})
				} else {
					fetch(`${this.source}/api/post_text?url=${this.link}`)
					.then(r => r.text())
					.then(t => {
						this.$emit('showPopup', {
							...data,
							text: t
						})
					})
				}
				
			}
		},
		components: {}
	}
</script>

<style scoped lang="sass">
	.news-item
		display: flex
		flex-direction: column
		max-width: 300px
		border-radius: 6px
		overflow: hidden
		gap: 10px
		transition-duration: .2s
		cursor: pointer
		padding-bottom: 10px
		justify-self: center
		background: white
		
		&__img 
			width: 100%
			max-height: 200px
			overflow: hidden
			
			img
				width: 100%
				object-fit: cover
		
		&__title
			font-size: 18px
			padding: 0 10px
			font-weight: bold
			
		&__preview
			padding: 0 10px
			font-size: 12px
		
		&:hover
			transform: scale(1.05)
			border: solid 3px white
			
		
</style>