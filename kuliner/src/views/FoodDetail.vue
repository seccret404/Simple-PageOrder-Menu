<template>
  <div class="food-detail">
    <Navbar />
    <!--navbar diatas-->
    <div class="container">
      <div class="row mt-3">
        <div class="col">
          <nav aria-label="breadcrumb">
            <ol class="breadcrumb">
              <li class="breadcrumb-item">
                <router-link to="/">Home</router-link>
              </li>
              <li class="breadcrumb-item">
                <router-link to="/food">Food</router-link>
              </li>
              <li class="breadcrumb-item active" aria-current="page">Food Deail</li>
            </ol>
          </nav>
        </div>
      </div>
      <!--breadcumd-end-->

      <div class="row">
        <div class="col-md-6">
          <img :src=" '../assets/image/' + product.gambar" class="card-img-top shadow mb-4 shadow" alt="...">

        </div>
        <div class="col-md-6">
          <h2>{{ product.nama }}</h2>
          <hr>
          <h5>Harga Rp.{{product.harga  }}</h5>
          <form action="" v-on:submit.prevent>
            <div class="form-group">
              <label for="jumlah_pemesanan">Jumlah Pesanan</label>
              <input type="number" class="form-control" min="1" placeholder="jumlah pesanan"
                v-model="pesan.jumlah_pemesanan">
            </div>
            <div class="form-group">
              <label for="keretangan">Keterangan</label>
              <textarea v-model="pesan.keterangan" class="form-control" placeholder="Keterangan: sesuai selera
                "></textarea>
            </div>

            <button type="submit" class="btn btn-success mb-2  " @click="pemesanan">
              <b-icon-cart></b-icon-cart>Pesan
            </button>

          </form>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
  import Navbar from '@/components/Navbar.vue'
  import axios from 'axios'
  export default {
    // eslint-disable-next-line vue/multi-word-component-names
    name: 'Detail',
    components: {
      Navbar
    },
    data() { //data digunakan untuk menampung data dengan kondisi kosong

      return {
        product: {},
        pesan: {}
      }
    },
    methods: { //method digunakan untuk menampung methods yang ada

      setProducts(data) {
        this.product = data
      },
      pemesanan() {
       if(this.pesan.jumlah_pemesanan){
         this.pesan.products = this.product;
        axios
          .post("http://localhost:3000/keranjang/", this.pesan)
          .then(() => {
            this.$router.push({path:"/keranjang"})//untuk mengarahkan ke halaman keranjang
            // eslint-disable-next-line no-undef
            this.$toast.success('Sukses masuk keranjang', {//dari vue toast notification 
              type: 'success',
              position: 'top-right',
              duration: 3000,
              dismissible: true
            })
          })
          .catch((error) => {
            console.log("gagal", error)
          })
       }else{
        this.$toast.error('Data harus diisi', {//dari vue toast notification 
              type: 'error',
              position: 'top-right',
              duration: 3000,
              dismissible: true
       })
      }
    },
  },
    mounted() {
      axios
        .get("http://localhost:3000/product/" + this.$route.params.id) //
        .then((response) => this.setProducts(response.data))
        .catch((error) => console.log("Gagal", error))

    }

  }
</script>

<style>

</style>