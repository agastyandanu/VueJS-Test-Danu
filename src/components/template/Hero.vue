<template>

  <div class="hero">

    <!-- Desktop -->
    <div class="d-sm-none d-md-block">
        <div class="row mt-4">
            <div class="col-md-6">
                <div class="d-flex h-100">
                    <div class="justify-content-center align-self-center">
                        <h2><strong>Unlimited Movies</strong> <br> from Your Gadget</h2>
                        <p>Wherever and whenever You Are</p>
                        <router-link to="/movie-list" class="btn btn-lg btn-success">Get Started <b-icon-arrow-right></b-icon-arrow-right> </router-link>
                    </div>
                </div>            
            </div>
            <div class="col-md-6">
                <img src="../../assets/img/hero.png" width="100%" alt="">
            </div>
        </div>
    </div>      

  </div>    

</template>

<script>
export default {
    name : 'Hero'
}
</script>

<style>

</style>