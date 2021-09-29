<template>
        <li>
            <div class="flip-card">
                <div class="flip-card-inner">

                    <div class="flip-card-front">
                        <img v-if="item.poster_path == null" src="../assets/img/No-Image-Placeholder.png" alt="No-Image-Placeholder" style="width:300px;height:400px;">
                        <img v-else :src="`https://image.tmdb.org/t/p/w342${item.poster_path}`" :alt="item.title || item.name" style="width:300px;height:400px;">
                    </div>

                    <div class="flip-card-back d-flex-column py-4 px-2">

                        <div v-if="item.title || item.name !== item.original_title || item.original_name">
                            <div class="p-2">
                                <span class="fw-bold">Titolo: </span>
                                <span>{{item.title || item.name}}</span>
                            </div>

                            <div class="p-2">
                                <span class="fw-bold">Titolo originale: </span>
                                <span>{{item.original_title || item.original_name}}</span>
                            </div>
                        </div>

                        <div v-else>
                            <span class="fw-bold">Titolo: </span>
                            <span>{{item.title || item.name}}</span>
                        </div>
                        

                        <div class="p-2">
                            <b-form-rating class="rating" v-model="this.starVote">{{ getVote() }}</b-form-rating>
                        </div>

                        <div class="d-flex align-items-center px-2">
                            <span class="fw-bold">Lingua: </span>
                            <span class="flag">
                                <country-flag :country="getFlag(item.original_language)" size='normal'/> 
                            </span>
                        </div>

                        <div>
                            <span class="fw-bold">Genere: </span>
                            <span v-for="genre in genresMovie" :key="genre.id">{{genre}}</span>
                        </div>

                        <div class="p-2">
                            <span class="fw-bold">Overview: </span>
                            <span>{{item.overview}}</span>
                        </div>

                        <div>
                            <b-button v-b-toggle.collapse-2 @click="getActors()" class="m-1">Cast</b-button>
                            <b-collapse id="collapse-2">
                                <b-card v-for="item in SearchActors" :key="item.id">{{ item.name }}</b-card>
                            </b-collapse>
                        </div>
                    </div>
                </div>
            </div>
        </li>
</template>

<script>
import axios from 'axios'
import genreList from '@/assets/data/genreList.js'
export default {
    name: 'Card',
    props: ['item'],
    data() {
        return {
            apiUrl: 'https://api.themoviedb.org/3/',
            apiKey: '1ecf94259141687e2632494ab3f364c1',
            SearchActors: [],
            genresMovie: [],
            starVote: '',
            genreList: genreList,
        }
    },
    methods: {
        // per le bandiere mancanti modifico il dato con quello del country flag icons
        getFlag(language){
            if(language=="en")return "gb"
            if(language=="ja")return "jp"
            if(language=="ko")return "kp"
                return language
        },

        getVote() {
          this.starVote = Math.ceil(this.item.vote_average / 2);
        },
         
        getActors() {
            axios
                .get(this.apiUrl + 'movie/' + this.item.id +'/credits?api_key=' + this.apiKey)
                .then((response) => {
                    console.log(response.data.cast);
                    this.SearchActors = response.data.cast;
                })
        },

        // getGenres() {
        //     if(this.genreList.id == this.item.genre_ids) {
        //       return genresMovie.push(this.genreList.name) 
        //     }
        // }
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

            .rating {
                color: #cda434;
                background-color: black;
                border: none;
            }

            .card {
                border: none;

                .card-body {
                    background-color: $card-color;
                    padding: 5px;
                
                }
            }

            

        }
    } 
}

.flip-card:hover .flip-card-inner {
    transform: rotateY(180deg);
}

</style>