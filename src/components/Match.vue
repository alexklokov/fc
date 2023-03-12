<template>
	<div class="match">
		
		<div class="match__subtitle">
			{{ subtitle }}
		</div>
		<div class="match__teams" v-if="teams.length > 0">
			<div class="match__team">
				<div class="match__team-name">
					{{ teams[0].name }}
				</div>
				<div class="match__team-img">
					<img :src="teams[0].img">
				</div>
				
			</div>
			<div class="match__count">
				{{ teams[0].count }} : {{ teams[1].count }}
			</div>
			<div class="match__team">
				<div class="match__team-img">
					<img :src="teams[1].img">
				</div>
				<div class="match__team-name">
					{{ teams[1].name }}
				</div>
			</div>
		</div>
		<div class="match__title">
			{{ title }}
		</div>
	</div>
</template>

<script>
	export default {
		data() {
			return {
				title: '',
				subtitle: '',
				teams: [],
			}
		},
		mounted() {
			fetch(`${this.source}/api/match`)
				.then(r => r.text())
				.then(t => {
					const data = JSON.parse(t)
					this.title = data.title
					this.subtitle = data.sub_title
					this.teams.push({
						name: data.teams[0].replaceAll('"', ''),
						img: data.imgs[0],
						count: data.counts[0]
					})
					this.teams.push({
						name: data.teams[1].replaceAll('"', ''),
						img: data.imgs[1],
						count: data.counts[1]
					})
				})
		},
		props: {
			source: String,
		}
	}
</script>

<style scoped lang="sass">
	.match
		background: white
		color: #00205b
		border-radius: 6px
		padding: 30px 10px
		text-align: center
		margin: 0 auto
		// max-width: 700px
		
		&__subtitle
			padding: 0 0 20px
			font-weight: bold
			font-size: 30px
		&__title
			font-size: 12px
			color: #535353
			padding-top: 20px
			
		&__teams
			margin: 0 auto
			width: max-content
			display: flex
			align-items: center
			gap: 60px
			
		&__team
			display: flex
			align-items: center
			gap: 20px
			&-img
				height: 80px
				margin-bottom: 10px
				
				img
					height: 100%
			&-name
				font-weight: bold
				font-size: 35px
			
		&__count
			font-size: 50px
			font-weight: bold
		
		@media (max-width: 800px)
			&__team
				&-name
					font-size: 28px
		@media (max-width: 680px)
		
			&__team
				flex-direction: column
			&__team:first-child
				flex-direction: column-reverse
		
		@media (max-width: 480px)
			&__subtitle
				font-size: 20px
				
			&__team
				&-name
					font-size: 20px
					
			&__teams
				gap: 30px
			
			&__count
				font-size: 35px
			
</style>