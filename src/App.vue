<template>
  <div id="app">
    <img src="https://alejandro-fajardo.github.io/platzimusic/assets/logo.png">
    <h1>Platzi Music</h1>
    <Spinner v-show="loading"></Spinner>
    <select v-model="country" >
      <option value="argentina">Argentina</option>
      <option value="colombia">Colombia</option>
      <option value="spain">España</option>
    </select>
    <ul>
        <Artist v-for="artist in artists" v-bind:key="artist.name" :artist="artist"></Artist>
        <!-- {{artist.name}} -->
    </ul>
  </div>
</template>

<script>
import getArtists from './api'
import Artist from './components/Artist.vue'
import Spinner from './components/Spinner.vue'

export default {
  name: 'app',
  data () {
    return {
      msg: 'Welcome to Your Vue.js App',
      artists: [],
      country: 'spain',
      loading: false
    }
  },
  components: {
    Artist,
    Spinner
  },
  mounted: function () {
    this.changeCountry()
  },
  watch:{
    country:function (){
      this.changeCountry()
    }
  },
  methods:{
    changeCountry: function (){
      console.log(this.country)
      const self = this;
      self.loading =true;
      getArtists(this.country)
      .then(function (artists) {
        self.artists = artists
        self.loading =false;
      })
    }
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

h1, h2 {
  font-weight: normal;
}

ul {
  list-style-type: none;
  padding: 0;
}

li {
  display: inline-block;
  margin: 0 10px;
}

a {
  color: #42b983;
}
</style>
