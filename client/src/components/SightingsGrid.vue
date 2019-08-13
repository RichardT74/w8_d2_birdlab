<template lang="html">
	<div id="sightingsGrid">
		<div class="sighting" v-for="(sighting, index) in sightings" :key='index' :value='sighting'>
			<h2>{{ sighting.species }}</h2>
			<p>{{ sighting.location }} on {{ sighting.date|format }}</p>
<!-- this is all a looop for each sighting in sightings -->
			<button type="button" class="delete-btn" v-on:click="deleteSighting">Delete Sighting</button>
		</div>
	</div>
</template>

<script>
import { eventBus } from '../main';
import BirdsService from '@/services/BirdsService.js';

// below is tlabe for the component that will be used in app .vew []
export default {
	name: "sightings-grid",
	props: ["sightings"], // exexping sightings from app.vue
	filters: {
		format(value){
			return new Date(value).toLocaleString().substring(0, 10);
		}
	},
	methods: {
		deleteSighting(){
			BirdsService.deleteSighting(this.sighting._id)
			.then(() => eventBus.$emit( 'sighting-deleted', this.dighting._id ))
		}
	}
}
</script>

<style lang="css" scoped>
#sightingsGrid {
	display: flex;
	flex-wrap: wrap;
	justify-content: space-evenly;
}

h2 {
	padding: 0;
	margin: 0;
}

.sighting {
	width: 30%;
	background: rgba(255, 255, 255, 0.7);
	margin-bottom: 20px;
	padding: 25px;
}

button {
	color: #fff;
	border: none;
	font-size: 18px;
	padding: 10px;
	margin-top: 10px;
	background: #F55536;
}
</style>
