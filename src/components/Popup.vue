<template>
	
	<div class="news-popup" :class="visible ? 'visible' : '' " @click="closePopup">
		<div class="news-popup__window">
			<div class="news-popup__title">
				{{title}}
				<div class="news-popup__close"></div>
			</div>
			<div class="news-popup__text" v-html="text">
				
			</div>
		</div>
	</div>
</template>

<script>
	export default {
		methods: {
			closePopup() {
				this.$emit('closePopup')
			}
		},
		props: {
			title: String,
			text: String,
			visible: Boolean
		}
	}
</script>

<style scoped lang="sass">
	.news-popup
		display: none
		position: fixed
		z-index: 200
		width: 100%
		height: 100%
		background: rgba(0, 0, 0, .7)
		align-items: center
		justify-content: center
		top: 0
		left: 0
		
		
		&.visible
			display: flex
		
		&__window
			border-radius: 6px
			display: flex
			gap: 20px
			display: flex
			flex-direction: column
			background: white
			max-width: 700px
			overflow: hidden
			
		&__title
			padding: 10px 20px
			font-size: 18px
			background: #00205b
			color: white
			
		
				
		&__text
			padding: 0 20px 20px
			overflow: scroll
			max-height: 500px
</style>