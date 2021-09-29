<template>
    <header class="d-flex justify-content-between align-items-center mt-0 px-2">
        <h1>Boolflix</h1>
        <form class="search d-flex">
            <input type="text" class="input form-control" placeholder="Search" v-model='inputText'>
            <button type="submit" class="btn mx-2" @click.prevent="$emit('performSearchMovies', inputText)">
                Movies
            </button>
            <button type="submit" class="btn" @click.prevent="$emit('performSearchSeries', inputText)">
                Series
            </button>
        </form>
    </header>
</template>

<script>
export default {
    name: 'Header',
    data() {
        return {
            inputText: '',
        }
    },
    methods: {

    }
}
</script>

<style scoped lang="scss">
@import "../styles/vars.scss";

header {
    background-color: $header-color;
    width: 100%;
    height: 60px;
    position: fixed;
    z-index: 999;

    h1 {
        width: 100px;
        color: $logo-color;
        font-weight: bold;
    }

    .search {

        .input {
            margin-left: 20px;
        }
        
        .btn {
            background-color: $logo-color;
            width: 150px;
            color: $title-color;
        }
    }
}
    
</style>