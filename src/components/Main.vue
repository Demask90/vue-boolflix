<template>
  <ul>
    <li v-for="(item, index) in movies" :key="index">
      <MovieCard :item="item"/>
    </li>
    
  </ul>
</template>

<script>
import MovieCard from './MovieCard.vue'
export default {

  name: 'Main',
  props: ['movies'],
  components: {
    MovieCard
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
  @import "../styles/vars.scss";
  main {
    widows: 100%;
    height: 100%;
    background-color: $main-background;

    
  }
  ul {
    width: 100%;
    margin: 0;
    list-style: none;
    display: flex;
    flex-wrap: wrap;
    justify-content: center;
    margin-block-start: 0;
    margin-block-end: 0;
    padding-inline-start: 0;
}

    li{
        width: calc(100% / 6 - 20px);
        margin: 10px;
        text-align: center;
        background-color: $card-color;
        color: $title-color;


    }    

</style>
