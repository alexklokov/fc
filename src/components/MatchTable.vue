<template>
	<div class="match-table">
		<h2 id="match-table">Турнирная таблица</h2>
		<table>
			<thead>
				<tr>
					<th>№</th>
					<th colspan="2">Команда</th>
					<th>Игры</th>
					<th>Очки</th>
				</tr>
			</thead>
			<tbody>
				<tr v-for="(team, i) in teams" :class="i > 10 && !showAll ? 'hidden' : '' ">
					<td>{{ i + 1}}</td>
					<td> 
						<img :src="team.img" :alt="team.name">
					</td>
					<td>
						{{ team.name }}
					</td>
					<td>
						{{ team.games }}
					</td>
					<td>
						{{ team.count }}
					</td>
				</tr>
			</tbody>
		</table>
		
		<div class="nbutton" @click="toggleShowAll()"> {{ showAll ? 'Скрыть' : 'Показать все' }} </div>
	</div>
</template>


<script>
	export default {
		data() {
			return {
				showAll: false,
				teams: []
			}
		},
		methods: {
			toggleShowAll() {
				this.showAll = !this.showAll
			}
		},
		mounted() {
			fetch(`${this.source}/api/match_table`)
				.then(r => r.text())
				.then(t => {
					const data = JSON.parse(t)
					this.teams = data
				})
		},
		props: {
			source: String
		}
	}
</script>

<style scoped lang="sass">
	table
		background: white
		border-collapse: collapse
		border-radius: 6px
		overflow: hidden
		width: 100%
		
		
		
		th
			text-align: left
			padding: 20px
			border: solid 1px #e3e3e3
			
		td
			padding: 5px 20px
			border: solid 1px #e3e3e3
		td 
			img
				height: 20px
		tr
			td:nth-child(3) 
				width: 50%
			td:nth-child(4), td:nth-child(5),
			th:nth-child(3), th:nth-child(4)
				text-align: center 

			&.hidden
				display: none
	
	.nbutton
		margin: 30px auto
		
</style>