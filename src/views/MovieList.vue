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
                <div class="card p-2">
                    <img class="card-img-top" v-b-modal="'modalDetail'" :src="datamovie.Poster" alt="Card image cap" @click="showImage(datamovie)">
                    <div class="card-body">
                        <h5 class="card-title text-center"> {{datamovie.Title}} ({{ datamovie.Year}}) </h5>
                        <router-link :to="{name: 'MovieDetail', params: {id: datamovie.imdbID} }">
                            <button variant="outline-primary" class="btn btn-outline-primary btn-block mt-2">Detail</button>                
                        </router-link> 
                    </div>
                </div>
                </div>
            </div>

            <b-modal id="modalDetail" size="lg" hide-footer>
                <div class="d-block text-center">
                    <img :src="imageData.poster" alt="">
                </div>
            </b-modal>

        </div>
    </div>
</template>

<script>
    import axios from 'axios';
    import Navbar from '@/components/template/Navbar.vue';

    export default {
        name : "MovieList",
        components : {
            Navbar
        },
    
        data() {
            return {
                setMovie : [],
                searchKey : '',
                imageData : {
                    poster: ''
                }
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
                        alert("Data Not Found");
                    }
                })
                .catch((error) => console.log("Gagal: ", error));
            },

            showImage(datamovie) {
                this.imageData.poster = datamovie.Poster;
            }
        },

        mounted() {
            const key = "6b010a5a";
            const search = "train";
            axios.get("http://www.omdbapi.com/?apikey="+ key +"&s=" + search)
            .then((result) => {
                if (result.data.Response == "True") {
                    this.setMovie = result.data.Search;
                } else {
                    alert("Data Not Found");
                }      
            }) 
            .catch((error) => console.log("Gagal: ", error));
        }

    }

</script>

<style>

</style>