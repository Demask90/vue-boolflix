<template>
<main class="w-100">

  <section v-if="movies.length !== 0" class="movies">
    <h2>Movies:</h2>
    <ul class="w-100 d-flex flex-wrap justify-content-center col-12 col-sm-6 col-lg-3 col-xl-2 col-xxl-1">
      <Card v-for="item in movies" :key="item.id" class="m-1"  :item="item"/>
    </ul>
  </section>

  <section v-if="series.length !== 0" class="series">
    <h2>Series:</h2>
    <ul class="w-100 d-flex flex-wrap justify-content-center col-12 col-sm-6 col-lg-3 col-xl-2 col-xxl-1">
      <Card v-for="item in series" :key="item.id" class="m-1" :item="item"/>
    </ul>
  </section>

  <section v-if="series.length == 0 && movies.length == 0" class="main-view d-flex justify-content-center">
    <h1 class="col-12 col-sm-12 col-md-10 col-xl-6 col-xxl-6 p-2">Accedi a migliaia di Film e Serie Tv comodamente da casa</h1>
  </section>

</main>
</template>

<script>
import Card from './Card.vue'
export default {

  name: 'Main',
  props: ['series',"movies"],
  components: {
    Card
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
  @import "../styles/vars.scss";
  main {
    background-color: $main-background;
    padding-top: 60px;
    .movies, .series {

      h2 {
        color: $title-color;
        padding: 10px;
      }
      
      ul {
        list-style: none;
        margin-block-start: 0;
        margin-block-end: 0;
        padding-inline-start: 0;
      }

      li{
        background-color: $card-color;  
        color: $title-color;
      }    
    }

    .main-view {
      width: 100%;
      height: calc(100vh - 60px);
      background-image: url('../assets/img/Boolflix_photo.jpg');
      background-position: center;
      background-repeat: no-repeat;
      background-size:contain;

      h1 {
        margin: 10px auto;
        text-align: center;
        color: $title-color;
        text-transform: uppercase;
        font-weight: bold;

      }
    }
    
  }
  

</style>
