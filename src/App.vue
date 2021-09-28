<template>
  <div id="app">
    <Header @performSearchMovies='GetSearchMovies' @performSearchSeries='GetSearchSeries'/>
    <Main :movies="movies" :series="series"/>
  </div>
</template>

<script>
import axios from 'axios'
import Header from './components/Header.vue';
import Main from './components/Main.vue';

export default {
  name: 'App',
  components: {
    Header,
    Main,
  },
  data() {
    return {
      apiUrl: 'https://api.themoviedb.org/3/search/',
      apiKey: '1ecf94259141687e2632494ab3f364c1',
      movies: [],
      series: [],
      userSearchMovies: '',
      userSearchSeries: '',
    }
  },
  computed: {
  },
  methods: {
    GetSearchMovies(searchMovies) {
      this.userSearchMovies = searchMovies;
      this.getMovies();
    },
    GetSearchSeries(searchSeries) {
      this.userSearchSeries = searchSeries;
      this.getSeries();
    },
      
    getMovies() {
      if(this.userSearchMovies == ''){
        this.movies = [];
      }
      axios
           .get(this.apiUrl + 'movie?api_key=' + this.apiKey + '&query=' + this.userSearchMovies)
           .then((response) => {
              console.log(response.data.results);
              this.movies = response.data.results;
           })
    },
    getSeries() {
      if(this.userSearchSeries == ''){
        this.series = [];
      }
      axios
           .get(this.apiUrl + 'tv?api_key=' + this.apiKey + '&query=' + this.userSearchSeries)
           .then((response) => {
              console.log(response.data.results);
              this.series = response.data.results;
           })
    },
  },
}
</script>

<style lang="scss">
#app {
  width: 100%;
  height: 100%;
}
</style>
