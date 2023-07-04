<template>
    <div class="pesanan-sukses">
  <Navbar/>
  <div class="container">
    <div class="row justify-content-center mt-5 mb-5">
        <div class="col text-center">
            <img src="../assets/image/menunggu.png" width="300px" alt="">
            <h2><strong>Berhasil</strong></h2>
            <h4>Pesanan Anda sedang di sajikan, Mohon menunggu sebentar ya!</h4>
        </div>
        
    </div>
  </div>
  </div>
</template>

<script>
import Navbar from '@/components/Navbar.vue'
export default {
    // eslint-disable-next-line vue/multi-word-component-names
    name: 'Pesanan',
    components:{
        Navbar
    }

}
</script>

<style>

</style>