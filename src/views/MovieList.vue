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
                        <input v-model="searchKey" type="text" class="form-control" placeholder="Search Menu" @keyup="searchMovie">
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
                // axios.get('http://127.0.0.1:8000/api/v1/post/search-data/'+this.searchKey)
                let key = "6b010a5a";
                axios.get("http://www.omdbapi.com/?apikey="+ key +"&s=" + this.searchKey)
                .then((response) => {
                    this.setMovie = response.data;
                } )
                .catch((error) => console.log("Gagal: ", error));
            }
        },

        mounted() {
            let id = "tt3896198";
            let key = "6b010a5a";
            axios.get("http://www.omdbapi.com/?apikey="+ key +"&i=" + id)
            .then((response) => {
                this.setMovie = response.data;
            } )
            .catch((error) => console.log("Gagal: ", error));
        }

    }

</script>

<style>

</style>