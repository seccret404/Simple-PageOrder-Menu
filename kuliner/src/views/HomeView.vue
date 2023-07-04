<template>
  <div class="home">
   <Navbar/>
   <div class="container">
   <Hero/>
   <div class="row mt-4">
    <div class="col" id="mark">
      Best <strong>Food!</strong>
    </div>
    <div class="col">
      <router-link to="/food" class="btn btn-success float-right"><b-icon-eye></b-icon-eye> Lihat semua</router-link>
    </div>
   </div>
  
  <div class="row mb-3">
    <!--untuk mengaliaskan data produk kedalam produks dari database-->
    <!--v-for="product in products" :key="product.id"-->
    <div class="col-md-3 mt-4" v-for="product in product" :key="product.id">
       <Card :product="product"/>
    </div>
  </div>


</div>
</div>
</template>

<script>
// @ is an alias to /src
import Navbar from '@/components/Navbar.vue'
import Hero from '../components/Hero.vue'
import Card from '../components/Card.vue'
import axios from "axios"
export default {
  name: 'HomeView',
  components: {
    Navbar,
    Hero,
    Card,
    
   
  },
  data(){
    return{
      product:[]
    }
  },
  methods:{
    setProducts(data){
      this.product = data;
    }
  },
  mounted(){
    axios
  .get("http://localhost:3000/best-product")
  .then((response) => this.setProducts(response.data))
  .catch((error) => console.log("Gagal",error))
  
  }
};
</script>
<style>
  #mark{
    font-size: 20px;
   
    
    
  }
</style>