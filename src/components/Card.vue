<template>
        <li>
            <div class="flip-card">
                <div class="flip-card-inner">

                    <div class="flip-card-front">
                        <img :src="`https://image.tmdb.org/t/p/w342${item.poster_path}`" :alt="item.title || item.name" style="width:300px;height:400px;">
                    </div>

                    <div class="flip-card-back d-flex-column py-4 px-2">

                        <div class="p-2">
                            <span class="fw-bold">Titolo: </span>
                            <span>{{item.title || item.name}}</span>
                        </div>

                        <div class="p-2">
                            <span class="fw-bold">Titolo originale: </span>
                            <span>{{item.original_title || item.original_name}}</span>
                        </div>

                        <div class="p-2">
                            <span class="fw-bold">Voto: </span>
                            <i v-for=" n in 5" :key="n" class="fa-star" style="color: yellow" :class="(n <= getVote()) ? 'fas' : 'far' "></i>
                        </div>

                        <div class="d-flex align-items-center px-2">
                            <span class="fw-bold">Lingua: </span>
                            <span class="flag">
                                <country-flag :country="getFlag(item.original_language)" size='normal'/> 
                            </span>
                        </div>

                        <div class="p-2">
                            <span class="fw-bold">Overview: </span>
                            <span>{{item.overview}}</span>
                        </div>

                    </div>
                </div>
            </div>
        </li>
</template>

<script>
export default {
    name: 'Card',
    props: ['item'],
    data() {
    return {
        StarVote: '',
    }
  },
    methods: {
        getFlag(language){
            if(language=="en")return "gb"
            if(language=="ja")return "jp"
            if(language=="ko")return "kp"
                return language
        },
        getVote() {
           return Math.ceil(this.item.vote_average / 2);

        }
    }
}
</script>

<style lang="scss" scoped>
@import "../styles/vars.scss";

.flip-card {
    width: 300px;
    height: 400px;
    background-color: transparent;
    perspective: 1000px;

    .flip-card-inner {
        width: 100%;
        height: 100%;
        position: relative;
        transition: transform 0.6s;
        transform-style: preserve-3d;

        .flip-card-front {
            position: absolute;
            -webkit-backface-visibility: hidden;
            backface-visibility: hidden;
        }

        .flip-card-back {
            width: 100%;
            height: 100%;
            background-color: $card-color;
            color: $title-color;
            transform: rotateY(180deg);
            position: absolute;
            -webkit-backface-visibility: hidden;
            backface-visibility: hidden;
            overflow: auto;

        }
    } 
}

.flip-card:hover .flip-card-inner {
    transform: rotateY(180deg);
}

</style>