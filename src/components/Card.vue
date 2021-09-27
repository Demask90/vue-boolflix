<template>
        <div>
            <div class="flip-card">
                <div class="flip-card-inner">
                <div class="flip-card-front">
                <img :src="`https://image.tmdb.org/t/p/w342${item.poster_path}`" :alt="item.title" style="width:300px;height:400px;">
            </div>
            <div class="flip-card-back d-flex-column py-4 px-2">
                <div><span class="fw-bold">Titolo: </span><span>{{item.title || item.name}}</span></div>
                <div><span class="fw-bold">Titolo originale: </span><span>{{item.original_title || item.original_name}}</span></div>
                <div><span class="fw-bold">Voto: </span><span>{{item.vote_average}}</span></div>
                <div><span class="fw-bold">Lingua: </span><span><flag :iso="item.original_language"/></span></div>
                <div><span class="fw-bold">Overview: </span><span>{{item.overview}}</span></div>
            </div>
        </div>
    </div>
</div>
</template>

<script>
export default {
    name: 'Card',
    components: {
    },
    props: ['item'],
    data() {
        return {
            Star: '',
        }
    },methods: {
        getStar() {
            this.Star = (item.vote_avarge / 2),
            console.log(this.Star)
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
            overflow-y: scroll;
        }
    } 
}

.flip-card:hover .flip-card-inner {
    transform: rotateY(180deg);
}

</style>