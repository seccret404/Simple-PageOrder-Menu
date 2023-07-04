<template>
  <div class="container">
 <!--dekstop-->
 <div class="d-none d-md-block">
  <div class="row mt-4">
    <div class="col-md-6">
        <div class="d-flex h-100">
            <div class="justify-content-center align-selft-center">
                <h2><strong>Delicious Food Menu</strong> in Your Menu</h2>
                <p>Segera lakukan pemesanan makanan</p>
                <router-link to="/food" class="btn btn-success"><b-icon-arrow-right></b-icon-arrow-right> Pesan </router-link>
                
            </div>
        </div>
    </div>
    <div class="col-md-6">
        <img src="../assets/image/hero.png" width="100%" alt="">
    </div>
  </div>
 </div>

 <!--mobile-->
 <div class="row mt-4 d-md-none d-sm-block">
  <div class="col-md-6">
        <img src="../assets/image/hero.png" width="100%" alt="">
    </div>
    <div class="col-md-6">
        <div class="d-flex h-100">
            <div class="justify-content-center align-selft-center">
                <h2><strong>Delicious Food Menu</strong> in Your Menu</h2>
                <p>Segera lakukan pemesanan makanan</p>
                <router-link to="/food" class="btn btn-success"><b-icon-arrow-right></b-icon-arrow-right> Pesan </router-link>
                
            </div>
        </div>
    </div>
    
  </div>
</div>
</template>

<script>
export default {
 // eslint-disable-next-line vue/multi-word-component-names
 name : 'Hero'
 }
</script>

<style>

</style>