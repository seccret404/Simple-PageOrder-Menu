<template>
  <div>
    <Navbar />
    <div class="container">
      <div class="row mt-4">
        <div class="col">
          <h1>Daftar <strong>Makanan</strong></h1>

        </div>
      </div>
      <div class="row mt-3">
        <div class="col">
          <div class="input-group mb-3">
<!--v-model kita gunakan untuk variable search -->
            <input v-model="search"
             type="text" class="form-control" placeholder="Cari makanan" aria-label="Username"
              aria-describedby="basic-addon1"
              @keyup="searchFood"><!--keyup kita gunakan untuk menjalan kan method searchfood-->
            <span class="input-group-text" id="basic-addon1">
              <b-icon-search></b-icon-search>
            </span>
          </div>
        </div>
      </div>



      <div class="row mb-3">
        <div class="col-md-3 mt-4" v-for="product in product" :key="product.id">
          <Card :product="product" />
        </div>
      </div>
    </div>
  </div>
</template>

<script>
  // @ is an alias to /src
  import Navbar from '@/components/Navbar.vue'
  import Card from '@/components/Card.vue'
  import axios from "axios"

  export default {
    // eslint-disable-next-line vue/multi-word-component-names
    name: 'Foods',
    components: {
      Navbar,
      Card
    },

    data() {
      return {
        product: [],
        search: '' //kita tambahkan variable search dengan kondisi kosong
      }
    },
    methods: {
      setProducts(data) {
        this.product = data;
      },
      searchFood(){//pada method kita tambahkan method intuk mencari data yang diambil dari api json
        axios
        .get("http://localhost:3000/product?q="+this.search) //q=?digunakan untuk mengambil data sesuai denganinppurtan pada form pencarian
        .then((response) => this.setProducts(response.data))
        .catch((error) => console.log("Gagal", error))
      }
    },
    mounted() {
      axios
        .get("http://localhost:3000/product")
        .then((response) => this.setProducts(response.data))
        .catch((error) => console.log("Gagal", error))

    }
  }
</script>

<style>
h1{
  font-size: 60px;
}

</style>