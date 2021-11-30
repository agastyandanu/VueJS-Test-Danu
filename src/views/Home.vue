<template>
  <div class="home">    
    <Navbar />
    <div class="container">
      <Hero />

      <div class="row mt-5">
        <div class="col">
          <h2><strong>Movies</strong> Update</h2>
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
// @ is an alias to /src
import axios from 'axios';
import Navbar from '@/components/template/Navbar.vue'
import Hero from '@/components/template/Hero.vue'
import CardMovie from '@/components/CardMovie.vue'

export default {
  name: 'Home',
  components: {
    Navbar,
    Hero,
    CardMovie
  },

  data() {
    return {
      setMovie : []
    }
  },

  methods: {
  },

  mounted() {
    let id = "tt3896198";
    // let type = "movies";
    let key = "6b010a5a";
    axios.get("http://www.omdbapi.com/?apikey="+ key +"&i=" + id)
    .then((response) => {
      this.setMovie = response;
      console.log(response.data.Title);
    } )
    .catch((error) => console.log("Gagal: ", error));
  }
}

</script>
