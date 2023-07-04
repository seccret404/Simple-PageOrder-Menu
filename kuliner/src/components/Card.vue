<template>
   <div class="card shadow">
  <img :src=" '../assets/image/' + product.gambar" class="card_img" alt="..." id="images" >
  <div class="card-body">
    <h5 class="card-title">{{ product.nama }}</h5>
    <p class="card-text">Rp.{{ product.harga }}</p>
    <router-link :to="'/food/'+product.id" class="btn btn-success"><b-icon-cart></b-icon-cart>Pesan</router-link>
  </div>
</div>
</template>

<script>
export default {
    // eslint-disable-next-line vue/multi-word-component-names
    name : 'Card',
    props : ['product']

}
</script>


<style>
.card_img{
    width:100%;
    height: 150px;
}

</style>