<template>
  <div>
        <div>Titolo<h3 class="item-title">{{item.title}}</h3></div>
        <div>Titolo originale<h3 class="item-originalTitle">{{item.original_title}}</h3></div>
        <div>Lingua<h3 class="item-language">{{item.original_language}}</h3></div>
        <div>Voto<h3 class="item-vote">{{item.vote_average}}</h3></div>
  </div>
</template>

<script>
export default {
    name: 'VideoCard',
    components: {
    },
    props: ['item'],
    data() {
        return {
        }
    },
}
</script>

<style lang="scss" scoped>
div{
    margin: 5px;
}
</style>