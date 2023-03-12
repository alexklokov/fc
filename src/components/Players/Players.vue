<template>
	<div class="players">
		<h2 id="players">Команда</h2>
		<div class="nselect">
			<select @change="filterPlayers">
				<option value="" selected> Все </option>
				<option v-for="status in statuses" :value="status">{{ status }}</option>
			</select>
		</div>
		<div class="players__list">
			<Player v-for="player in visiblePlayers" 
				:name="player.name"
				:number="player.num"
				:img="player.img"
				:status="player.status"
			/>
		</div>
	</div>
</template>



<script>
	import Player from '@/components/Players/Player.vue'
	export default {
		data() {
			return {
				statuses: [],
				players: [],
				visiblePlayers: [],
			}
		},
		methods: {
			filterPlayers(e) {
				if(e.target.value === "")
					this.visiblePlayers = this.players
				else 
					this.visiblePlayers = this.players.filter(player => player.status === e.target.value)
			}	
		},
		mounted() {
			fetch(`${this.source}/api/get_team`)
				.then(r => r.text())
				.then(t => {
					this.players = JSON.parse(t)
					this.visiblePlayers = this.players
					this.players.forEach(player => {
						if(this.statuses.indexOf(player.status) === -1)
							this.statuses.push(player.status)
					})
				})
		},
		props: {
			source: String
		},
		components: {
			Player
		}
	}
</script>

<style scoped lang="sass">
	.players__list
		display: grid
		grid-template-columns: repeat(3, 1fr)
		grid-gap: 100px
		
		@media (max-width: 991px) 
			grid-gap: 50px
		@media (max-width: 800px) 
			grid-template-columns: 1fr 1fr
		@media (max-width: 580px)
			grid-template-columns: 1fr
	
	.nselect
		margin: 20px 0
		
	
	
</style>