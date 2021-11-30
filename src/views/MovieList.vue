<template>
    <div>
        <Navbar />
        <div class="container">
            <div class="row">
                <div class="col">
                    <h2>Movie <strong>List</strong></h2>
                </div>
            </div>

            <div class="row mt-5">
                <div class="col">
                    <div class="input-group mb-3">
                        <input v-model="searchKey" type="text" class="form-control" placeholder="Search Movies" @keyup="searchMovie">
                        <div class="input-group-append">
                            <span class="input-group-text" id="basic-addon2"><b-icon-search></b-icon-search></span>
                        </div>
                    </div>
                </div>
            </div>
                    
            <div class="row mt-5">
                <div class="col-md-4 p-2" v-for="datamovie in setMovie" :key="datamovie.imdbID">
                    <CardMovie :sendMovie="datamovie" />
                </div>
            </div>

        </div>
    </div>
</template>

<script>
    import axios from 'axios';
    import Navbar from '@/components/template/Navbar.vue';
    import CardMovie from '@/components/CardMovie.vue';

    export default {
        name : "MovieList",
        components : {
            Navbar,
            CardMovie
        },
    
        data() {
            return {
                setMovie : [],
                searchKey : '',
            }
        },

        methods: {
            searchMovie() {
                let key = "6b010a5a";
                console.log(this.searchKey);
                axios.get("http://www.omdbapi.com/?apikey="+ key +"&s=" + this.searchKey)
                .then((response) => {
                    console.log(response.data);
                    this.setMovie = response.data;
                } )
                .catch((error) => console.log("Gagal: ", error));
            }
        },

        mounted() {
            // let id = "tt3896198";
            // let type = "movies";
            let key = "6b010a5a";
            axios.get("http://www.omdbapi.com/?apikey="+ key +"&s=inception")
            .then((response) => {
                console.log(response.data);
                this.setMovie = response.data;
            } )
            .catch((error) => console.log("Gagal: ", error));
        }

    }

</script>

<style>

</style>