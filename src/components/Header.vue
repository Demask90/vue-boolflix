<template>
    <header class="d-flex justify-content-between align-items-center mt-0 px-2">
        <img src="../assets/img/Netflix-Logo.wine.png" alt="">
        <form class="d-flex">
            
            <div>
                <input type="text" class="form-control"  placeholder="Search Movie" v-model='inputText' @keyup.enter="$emit('performSearch', inputText)" >
            </div>

            <div>
                <button type="submit" class="btn btn-danger" @click.prevent="$emit('performSearch', inputText)">
                    Search
                </button>
            </div>
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
    img {
        width: 100px;
    }
}
    
</style>