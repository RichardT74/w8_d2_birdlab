<template>
  <div id="app">
    <sightings-form />
    <sightings-grid :sightings="sightings" />
    <!-- above is expecting sightings from the prop -->
  </div>
</template>

<script>
import SightingsForm from './components/SightingsForm'; //going out
import SightingsGrid from './components/SightingsGrid';
import { eventBus } from './main';

export default {
  name: 'app',
  data () {
    return {
      sightings: []//from the fetch below, can now start rendering
    }
  },
  components: {
    'sightings-form': SightingsForm, //see stuff in above
    'sightings-grid': SightingsGrid
  },
  mounted(){
    this.fetchData();
  },
  methods: {
    fetchData(){
      fetch("http://localhost:3000/api/sightings")
        .then(res => res.json())
        .then(sightings => this.sightings = sightings);
    }
  }
}
</script>

<style>
html {
  height: 100%;
}

body {
  background: url('./assets/birds-background.jpg') no-repeat;
  height: 100%;
  background-position: center;
  background-repeat: no-repeat;
  background-size: cover;

}
</style>
