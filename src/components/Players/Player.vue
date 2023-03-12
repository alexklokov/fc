<template>
	<div class="player">
		<div class="player__img">
			<img :src="img" :alt="name">
		</div>
		<div class="player__info">
			<div class="player__last-name">
				{{ name.split(" ")[0] }} 
			</div>
			<div class="player__first-name">
				{{ name.split(" ")[1] }} 
			</div>
			<div class="player__status">
				{{ status }}
			</div>
			
		</div>
	</div>
</template>

<script>
	export default {
		props: {
			name: String,
			number: String,
			img: String,
			status: String,
		}
	}
</script>

<style scoped lang="sass">
	.player
		position: relative
		overflow: hidden
		justify-self: center
		
		&__img
			position: relative
			
			img 
				width: 100%
			
			&::after
				content: ''
				position: absolute
				width: 100%
				bottom: 0
				height: 100%
				left: 0
				background: linear-gradient(180deg, rgba(0, 0, 0, 0) 0%, rgba(0,27,78,1) 90%)
		
		&__info
			color: white
			text-align: center
			top: -30px
			z-index: 10
			position: relative
			
		&__last-name
			font-size: 45px
			font-weight: bold
			line-height: 1
			
		&__first-name
			font-size: 28px
			font-weight: bold
			
		&__status
			padding-top: 10px
			color: #a3a3a3
			font-size: 14px
</style>