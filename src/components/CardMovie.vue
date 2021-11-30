<template>

    <div class="card p-2">
        <img class="card-img-top" :src="sendMovie.Poster" alt="Card image cap">
        <div class="card-body">
            <h5 class="card-title"> {{sendMovie.Title}} </h5>
            <p class="card-text"> {{ sendMovie.Country }} </p>
            <router-link :to="{name: 'MovieDetail', params: {id: sendMovie.imdbID} }" class="btn btn-success"> <b-icon-eye></b-icon-eye> Detail</router-link>
        </div>
    </div>

</template>

<script>
    export default {
        name : "CardMovie",
        props: ['sendMovie'],
    }
</script>

<style>

</style>