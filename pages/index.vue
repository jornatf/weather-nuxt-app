<template>
	<div class="container">
		<div class="header">
            <h1>Get weather in realtime !</h1>
        </div>
		<WeatherCard v-if="!loader" :items="weatherDatas" />
		<div class="loading" v-else>Loading...</div>
		<div class="footer">
			<div class="last-update">Last update {{ lastDate }}</div>
			<div>
				<Button @handleClick="refreshDatas">Refresh</Button>
			</div>
		</div>
	</div>
</template>

<style scoped>
	.container {
		display: flex;
		flex-direction: column;
		justify-content: center;
		align-items: center;
		height: 100vh;
		width: 100vw;
		padding: 20px;
	}

	.header {
		padding: 0 15px;
		text-align: center;
		opacity: .4;
		color: #F9F9F9;
	}

	.header h1 {
		font-size: 30px;
		font-weight: 200;
		padding-bottom: 10px;
		margin: 0;
	}

	.footer {
		width: 100%;
		max-width: 550px;
		display: flex;
		justify-content: space-between;
		align-items: center;
		padding: 0 30px;
	}

	.loading {
		color: #F9F9F9;
		text-transform: uppercase;
		font-size: 9px;
		letter-spacing: .1em;
		display: flex;
        justify-content: space-between;
        align-items: center;
		height: 125px;
	}

	.last-update {
		color: #f9f9f9;
		font-size: 9px;
		font-weight: 400;
		opacity: .6;
		text-transform: uppercase;
	}
</style>

<script>
export default {
	name: 'IndexPage',
	data() {
		return {
			loader: true,
			weatherDatas: [],
			lastDate: new Date().toLocaleString()
		}
	},
	created() {
		this.refreshDatas()
	},
	mounted() {
		// refresh datas without new geolocation
		setInterval(() => this.fetchDatas(), 5*60*1000)
	},
	methods: {
		refreshDatas() {
			this.initDatas()
		},
		initDatas() {
			this.$getLocation().then(coords => {
				this.fetchDatas(coords)
			})
		},
		async fetchDatas(coords) {
			const urlParams = {
				params: {
					aqi: 'no',
					key: process.env.NUXT_ENV_API_KEY,
					q: `${coords.lat},${coords.lng}`
				}
			}
			const res = await this.$axios.get('https://api.weatherapi.com/v1/current.json', urlParams)
			this.weatherDatas = res.data
			this.lastDate = new Date().toLocaleString()
			this.loader = false
		}
	}
}
</script>
