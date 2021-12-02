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
                <div class="col-md-6 m-auto">
                    <input v-model="searchKey" @keyup="searchMovie" placeholder="Search Movies" type="text" class="form-control text-right">
                </div>
            </div>
                    
            <div class="row mt-5">
                <div class="col-md-3 p-2" v-for="datamovie in setMovie" :key="datamovie.imdbID">
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
                const key = "6b010a5a";
                const search = this.searchKey;
                axios.get("http://www.omdbapi.com/?apikey="+ key +"&s=" + search)
                .then((result) => {
                    if (result.data.Response == "True") {
                        this.setMovie = result.data.Search;
                    } else {
                        // alert("Something Went Wrong");
                    }
                })
                .catch((error) => console.log("Gagal: ", error));
            }
        },

        mounted() {
            const key = "6b010a5a";
            const search = "harry";
            axios.get("http://www.omdbapi.com/?apikey="+ key +"&s=" + search)
            .then((result) => {
                if (result.data.Response == "True") {
                    this.setMovie = result.data.Search;
                } else {
                    // alert("Something Went Wrong");
                    this.setMovie = "Movie Not Found";
                }      
            }) 
            .catch((error) => console.log("Gagal: ", error));
        }

    }

</script>

<style>

</style>