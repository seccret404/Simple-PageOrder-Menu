
<template>
<div>
  
  <b-navbar toggleable="lg" type="dark" variant="info">
    <div class="container">
    <b-navbar-brand href="#">Kulineran</b-navbar-brand>

    <b-navbar-toggle target="nav-collapse"></b-navbar-toggle>

    <b-collapse id="nav-collapse" is-nav>
      <b-navbar-nav>
        <b-nav-item ><router-link to="/" style="color:white;">Home</router-link></b-nav-item>
        <b-nav-item ><router-link to="/food" style="color:white">Food</router-link></b-nav-item>
      </b-navbar-nav>

      <!-- Right aligned nav items -->
      <b-navbar-nav class="ml-auto">
        <li class="nav-item">
          <router-link class="nav-link" to="/keranjang" style="color:white">Keranjang
          <b-icon-bag></b-icon-bag>
          <span class="badge badge-success ml-2">{{updateKeranjang  ? updateKeranjang.length : jumlah_pesanan.length}}</span> 
           </router-link>
        </li>
   
      </b-navbar-nav>
    </b-collapse>
  </div>
  </b-navbar>
</div>

</template>

<script>
import axios from 'axios'
export default {
    // eslint-disable-next-line vue/multi-word-component-names
    name: 'Navbar',
    data(){
      return{
        jumlah_pesanan:[]
      }
    },
    props:['updateKeranjang'], //props digunakan untuk mengoper nilai dari halaman lain

    methods:{
      setJumlah(data){
        this.jumlah_pesanan = data
      }
    },
    mounted(){
      axios
  .get("http://localhost:3000/keranjang") //membuat data masuk kedalam keranjang
  .then((response) => this.setJumlah(response.data))
  .catch((error) => console.log("Gagal",error))
  
    }
}
</script>

<style>

</style>