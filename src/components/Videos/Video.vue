<template>
	<div class="video" @click="showPopup">
		<div class="video__img">
			<img :src="img">
		</div>
		<div class="video__title">
			{{ title }}
		</div>
	</div>
</template>

<script>
	export default {
		data() {
			return {
				text: '',
			}
		},
		methods: {
			showPopup() {
				const data = {
					title: this.title,
				}
				if(this.text !== '') {
					this.$emit('showPopup', {...data, src: this.text})
				} else {
					fetch(`${this.source}/api/get_video?url=${this.link}`)
						.then(r => r.text())
						.then(t => {
							this.$emit('showPopup', {...data, src: t})
						})
				}
			}
		},
		props: {
			link: String,
			title: String,
			img: String,
			source: String,
		}
	}
</script>

<style lang="sass" scoped>
	.video
		cursor: pointer
		position: relative
		&__img
			img
				width: 100%
		
		&__title
			color: white
			position: absolute
			width: 100%
			height: 100%
			display: flex
			align-items: center
			justify-content: center
			opacity: 0
			left: 0
			top: 0
			transition-duration: .2s
			background: black
			padding: 10px
			text-align: center
			
			
		&:hover 
			.video__title
				opacity: .9

			
</style>