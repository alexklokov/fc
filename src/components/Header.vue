<template>
	<header class="header">
		<div class="header__logo">
			<img src="http://fc-tambov.ru/upfiles/championat/team_logos/1.png">
		</div>
		<div class="header__menu-toggle" @click="toggleMenu" :class="menuVisible ? 'opened' : ''">
			<span></span>
			<span></span>
			<span></span>
		</div>
		<div class="header__menu" :class="menuVisible ? 'visible' : '' ">
			<a href="#match-table">Турнирная таблица</a>
			<a href="#players">Команда</a>
			<a href="#news">Новости</a>
			<a href="#videos">Видео</a>
			
		</div>
	</header>
</template>

<script>
	export default {
		data() {
			return {
				menuVisible: false
			}
		},
		methods: {
			toggleMenu() {
				this.menuVisible = !this.menuVisible
			}
		}
	}
</script>

<style scoped lang="sass">
	
	.header
		position: fixed
		top: 0
		left: 0
		width: 100%
		background: rgba(255, 255, 255, .9)
		padding: 0 20px
		box-sizing: border-box
		display: flex
		align-items: center
		justify-content: space-between
		z-index: 1000
		
		&__menu-toggle
			display: none
			flex-direction: column
			justify-content: center
			gap: 5px
			width: 50px
			height: 50px
			align-items: center
			background: rgba(0, 32, 91, .1)
			border-radius: 50%
			cursor: pointer
			position: relative
			span
				width: 20px
				height: 2px
				background: #00205b
				transition-duration: .2s
				
			&.opened
				span
					position: absolute
					top: 50%
				span:nth-child(2)
					opacity: 0
				
				span:nth-child(1)
					
					transform: rotate(45deg)
				span:nth-child(3)
					transform: rotate(-45deg)
				
				
			
		&__logo
			max-width: 50px
			img
				width: 100%
				
		&__menu
			display: flex
			gap: 20px
			width: 50%
			justify-content: space-between

			a
				color: #00205b
				text-decoration: none
				position: relative
				padding-bottom: 5px
				
				&::before
					content: ''
					position: absolute
					top: 100%
					left: 50%
					width: 0
					height: 1px
					background: #00205b
					transition-duration: .2s
					
				
				&:hover::before
					width: 100%
					left: 0
		
		@media (max-width: 1400px)
			&__menu
				width: 70%
				
		@media (max-width: 991px)
			&__menu
				width: 90%
			
		@media (max-width: 768px)
			&__menu
				width: 0
				padding: 20px 0
				position: fixed
				left: 100%
				flex-direction: column
				align-items: flex-start
				top: 66px
				height: 100vh
				width: 260px
				background: white
				justify-content: flex-start
				overflow: hidden
				
				
				&.visible
					padding: 20px
					display: flex
					left: 80%
					width: 300px
					right: 0
					left: unset
					transition-duration: .3s
					
					
					
			&__menu-toggle
				display: flex
</style>