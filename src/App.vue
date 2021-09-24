<template>
  <div id="app">
    <Header @performSearch='GetSearch'/>
    <Main :movies="movies"/>
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
      userSearch: 'All',
      loading: true
    }
  },
  computed: {

  },
  methods: {
    GetSearch(search) {
        this.userSearch = search;
        this.getMovies()
      },
      
    getMovies() {
      if(this.userSearch == ''){
        this.movies = []
      }
      axios
           .get(this.apiUrl + 'movie?api_key=' + this.apiKey + '&query=' + this.userSearch)
           .then((response) => {
              console.log(response.data.results);
              this.movies = response.data.results;
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
